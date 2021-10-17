# 🚧 Download

The `Download` component helps you to generate a download link by either fetching the content across the network, like from an `API` endpoint, or a `Blob`object like in example 4.

:::note

To make sense of which text is displayed at which stage, the following process might be useful. The process of how a download link is generated is managed by the internal `status` state, which follow these steps `idle` -> `pending` -> `resolved(children)/rejected`. So passing `Generate link` to `idle`, `Loading...` to `pending`, and `Download now` to `children`, you would have a logical description that the user can follow.
:::

## The Syntax

```jsx
<Download
  url={resourceLocation}
  fileName={fileName}
  wait={true}
  idle="Generate download link"
  pending="Loading..."
>
  Download now
</Download>
```

### Props

| State                  | Type                | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ` url`                 | ` String` or `Blob` | The `url` can be the endpoint of an API or a `Blob` object instance. See the examples to make sense of it.                                                                                                                                                                                                                                                                                                                                        |
| ` fileName`            | ` String`           | Controls the file name, like `file.txt`. Note that the `extension` controls what kind of file it is. If the download content is an image, then using the `txt` extension will not work.                                                                                                                                                                                                                                                           |
| optional - ` wait`     | ` Boolean`          | The `wait` prop controls whether you want the download link to be generated right after the component is mounted or not. Note that if it's not a `Blob` object, and the content is served across the network, then a HTTP request is sent. So it's up to you to wait for the request to be sent, which happens after a click event. If `wait` is true, then the download link is generated after a click event is fired. Default value is `true`. |
| optional - ` pending`  | ` String`           | The `pending` state controls what will be displayed while the network is happening. The default is `Loading...`.                                                                                                                                                                                                                                                                                                                                  |
| optional - ` children` | ` String`           | The `children` prop controls what will be displayed after the download link is ready. The default is `Download ${fileName}`.                                                                                                                                                                                                                                                                                                                      |
| optional - ` idle`     | ` String`           | If you pass the boolean value `true` to the `wait` prop, then the `idle` prop can be used to pass a default text value while status is `idle`. Something like `Generate download link` would make sense. The default is `Generate ${fileName} download link`.                                                                                                                                                                                     |
| optional - ` options`  | ` Object`           | If the request can only be send by authroized users, like with the `Authorization` header or `app-id` header, then you can pass an option object, which will be passed as the second argument to the `fetch` API, like `fetch(url, option)`. So, your `options` object should look like `{method: "GET", headers: { Authorization: "Bearer ${API_KEY}" }}`.                                                                                       |

:::note

Even if you hide your `API KEY` in an enviornment variable like `env.process.API_KEY`, as long as the request is sent from the client side, it will always be exposed. To really hide your `API KEY`, you should send it from your backend, and then send it back to your client side app.

:::

### Example 1

[CodeSandbox](https://f0524.csb.app/download)

This example generates a download link after the component mounts. If the download URL is created from a `blob` object, then this might make sense since no network request is sent.

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  return (
    <>
      <div>
        <h2>Download link is generated when components mount:</h2>
        <button>
          <Download
            url="https://jsonplaceholder.typicode.com/comments/1"
            fileName="comments.txt"
            wait={false}
            pending="Generating download link..."
          >
            Download now
          </Download>
        </button>
      </div>
    </>
  );
}
```

### Example 2

Here, `wait` is `true`, so the download content is generated after a click event is fired.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  return (
    <>
      <div>
        <h2>Download link is generated AFTER "click" even is fired:</h2>
        <button>
          <Download
            url="https://jsonplaceholder.typicode.com/comments/1"
            fileName="comments.txt"
            wait={true}
            idle="Generate Download Link"
            pending="Generating download link..."
          >
            Download now
          </Download>
        </button>
      </div>
    </>
  );
}
```

### Example 3

In this example, we pass an image url to allow the user to download the imported image.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";
import image from "./Image/profilePic.png";

export default function App() {
  return (
    <>
      <div>
        <h2>Download image:</h2>
        <button>
          <Download
            url={image}
            fileName="profile.png"
            wait={true}
            idle="Generate download link"
            pending="Generating download link..."
          >
            Download image
          </Download>
        </button>
      </div>
    </>
  );
}
```

### Example 4

Unlike the other examples, this example does **not** fetch the resource, but instead turns the `Blob` object to an `URL object` and allows the user to download the `Blob` content.

[CodeSandbox](https://f0524.csb.app/download)

```jsx title="src/App.js"
import { Download } from "kantan-components";

export default function App() {
  return (
    <>
      <div>
        <h2>Download image:</h2>
        <button>
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
          >
            Download blob object
          </Download>
        </button>
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
  return (
    <>
      <div>
        <h2>Download image:</h2>
        <button>
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
            idle="Get content"
            pending="Loading..."
          >
            Download blob object
          </Download>
        </button>
      </div>
    </>
  );
}
```
