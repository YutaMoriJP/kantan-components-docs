# Download

The `Download` component helps you to generate a download link by either fetching the content across the network, like from an `API` endpoint, or a `Blob`object like in example 4. The `Download` component will do all the heavy lifting for you, but you still have to manage a `textContent` React State, which is passed to your JSX, like `<button>{textContent}</button>`. This allows `Download` to keep the text content in sync with the 3 different stages it will go through. See the note below.

:::note

To make sense of which text is displayed at which stage, the following process might be useful. The process of how a download link is generated is managed by the internal `status` state, which follow these steps `idle` -> `pending` -> `resolved/rejected`. So if your initial `textContent` state is `Generate link` then it will be in sync with the `idle` status, and if you pass `Loading...` to `pending`, and `Download now` to `resolved`, you would have a logical description that the user can follow.
:::

## The Syntax

```jsx
const [textContent, setTextcontent] = useState("Start Downloading");
<Download
  url={resourceLocation}
  fileName={fileName}
  wait={true}
  pending="Loading..."
  resolved="Download now"
  setTextcontent={setTextcontent}
>
  {textContent}
</Download>;
```

### Props

| State                        | Type                | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ` url`                       | ` String` or `Blob` | The `url` can be the endpoint of an API or a `Blob` object instance. See the examples to make sense of it.                                                                                                                                                                                                                                                                                                                                        |
| ` fileName`                  | ` String`           | Controls the file name, like `file.txt`. Note that the `extension` controls what kind of file it is. If the download content is an image, then using the `txt` extension will not work.                                                                                                                                                                                                                                                           |
| optional - ` wait`           | ` Boolean`          | The `wait` prop controls whether you want the download link to be generated right after the component is mounted or not. Note that if it's not a `Blob` object, and the content is served across the network, then a HTTP request is sent. So it's up to you to wait for the request to be sent, which happens after a click event. If `wait` is true, then the download link is generated after a click event is fired. Default value is `true`. |
| optional - ` pending`        | ` String`           | The `pending` state controls what will be displayed while the network is happening. The default is `Loading...`.                                                                                                                                                                                                                                                                                                                                  |
| optional - ` resolved`       | ` String`           | The `resolved` state controls what will be displayed when the download content is ready. It defaults to `Download: ${fileName}`.                                                                                                                                                                                                                                                                                                                  |
| optional - ` children`       | ` React.ReactNode`  | It can be a JSX like a button element, e.g. `<button>{textContent}</button>` You must ensure that the text content of `children` renders your internal `textContent` state. This allows `Download` to update the text content depending on the current stage, like `resolved/rejected`.                                                                                                                                                           |
| optional - ` setTextcontent` | ` Function`         | State setter function that updates the `textContent` state. As the `Download` component goes through the different stages, the function receives your `pending`, and `resolved` arguments.                                                                                                                                                                                                                                                        |
| optional - ` options`        | ` Object`           | If the request can only be send by authroized users, like with the `Authorization` header or `app-id` header, then you can pass an option object, which will be passed as the second argument to the `fetch` API, like `fetch(url, option)`. So, your `options` object should look like `{method: "GET", headers: { Authorization: "Bearer ${API_KEY}" }}`.                                                                                       |

:::note

Even if you hide your `API KEY` in an enviornment variable like `env.process.API_KEY`, as long as the request is sent from the client side, it will always be exposed. To really hide your `API KEY`, you should send it from your backend, and then send it back to your client side app.

:::

### Example 1

[CodeSandbox](https://f0524.csb.app/download)

This example generates a download link after the click event is fired. First, the text content will be the initial value of the `textContent` state, which is `Start Downloading`. And once the user clicks on the button, `textContent` updates to `Generating download link...`. Once the download link is ready, the `textContent` updates to `Download now`. There is also a possibility that the operation fails. The `Download` component manages the `Error` message for you.

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  const [textContent, setTextcontent] = useState("Start Downloading");
  return (
    <>
      <div>
        <h2>Download link is generated when components mount:</h2>
        <Download
          url="https://jsonplaceholder.typicode.com/comments/1"
          fileName="comments.txt"
          wait={true}
          pending="Generating download link..."
          resolved="Download Now."
          setTextcontent={setTextcontent}
        >
          <button>{textContent}</button>
        </Download>
      </div>
    </>
  );
}
```

### Example 2

Here, `wait` is `false`, so the download content is generated right after the component mounts.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  const [textContent, setTextcontent] = useState("Generate Download Link");
  return (
    <>
      <div>
        <h2>Download link is generated AFTER "click" even is fired:</h2>
        <Download
          url="https://jsonplaceholder.typicode.com/comments/1"
          fileName="comments.txt"
          wait={false}
          pending="Generating download link..."
          resolved="Download now"
          setTextcontent={setTextcontent}
        >
          <button>{textContent}</button>
        </Download>
      </div>
    </>
  );
}
```

### Example 3

In this example, we pass an the imported image to `url` to allow the user to download the image.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";
import image from "./Image/profilePic.png";

export default function App() {
  const [textContent, setTextcontent] = useState("Generate Download Link");

  return (
    <>
      <div>
        <h2>Download image:</h2>
        <Download
          url={image}
          fileName="profile.png"
          wait={true}
          pending="Generating download link..."
          resolved="Download image"
          setTextcontent={setTextcontent}
        >
          <button> {textContent}</button>
        </Download>
      </div>
    </>
  );
}
```

### Example 4

Unlike the other examples, this example does **not** fetch the resource, but instead turns the `Blob` object to an `URL object` and allows the user to download the `Blob` content. For usage like this, it makes sense to set `wait` to `false` since it does not make a request to an external server, and content should be ready to be download immediately.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  const [textContent, setTextcontent] = useState("Generate Download Link");

  return (
    <>
      <div>
        <h2>Download image:</h2>
        <Download
          url={
            new Blob(
              [JSON.stringify({ name: "yuta", lastName: "mori" }, null, 2)],
              {
                type: "text/plain",
              }
            )
          }
          fileName="name.txt"
          wait={false}
          pending="Loading..."
          resolved="Download blob content"
          setTextcontent={setTextcontent}
        >
          <button> {textContent}</button>
        </Download>
      </div>
    </>
  );
}
```

### Example 5

This example illustrates how you can use the `options` prop to make a request to an API endpoint that requires an `API KEY`. But **note** that any request made from the client side will always be exposed. See the note at the top.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  const [textContent, setTextcontent] = useState("Generate Download Link");

  return (
    <>
      <div>
        <h2>Download image:</h2>
        <Download
          url={apiEndpoint}
          fileName="api content.txt"
          options={{
            method: "GET",
            headers: {
              "Content-Type": "application/json",
              Authorization: `Bearer ${process.env.API_KEY}`,
            },
          }}
          wait={true}
          pending="Loading..."
          resolved="Download Now"
          setTextcontent={setTextcontent}
        >
          <button>{textContent}</button>
        </Download>
      </div>
    </>
  );
}
```
