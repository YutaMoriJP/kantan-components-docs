# Message

The `Message` component is useful to notify a user about a successful or an erroneous action. For example, if you have a login/logout feature for your project, then the `Message` component can be pretty handy to render a message like `Logged in!` or `Logged out!`. This [app](https://next-forum.netlify.app/) makes use of the `Message` component to send a `Logged in/out` message as well as let them become aware of invalid form actions.

## The Syntax

```jsx
const App = () => {
  const [open, setOpen] = useState(false);
  return (
    <>
      <button onClick={() => setOpen(true)}>open message</button>
      {open ? (
        <Message onClose={() => setOpen(false)} ms={2000}>
          SUCCESS!
        </Message>
      ) : null}
    </>
  );
};
```

### Props

| State              | Type                           | Explanation                                                                                                                                                                                                                   |
| ------------------ | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ` onClose`         | `Function `                    | A function that must unmount the `Message` component.                                                                                                                                                                         |
| ` ms`              | `Number `                      | The `ms` prop needs to be represented in milliseconds. It controls when the `Message` component will be unmounted. If you pass the prop `ms={2000}`, then the component will be unmounted after 2 seconds.                    |
| ` children`        | `String ` or `React.ReactNode` | The `children` prop is the content that you want `Message` to render. For example, if you use the `Message` component for notifying the user about a successful action, then write `<Message>SUCCESS!</Message>.              |
| optional ` bottom` | `Boolean `                     | If you pass the optional prop `bottom` to `Message`, then the message will be rendered at the bottom of the page.                                                                                                             |
| optional `below`   | `Boolean `                     | The optional `below` prop is used to render `Message` right below containing parent.                                                                                                                                          |
| optional `color`   | `String`                       | The `color` prop controls the background color of the `Message` component. Note that the `color` prop can only be used together with the `bottom/below` prop. The reason is to keep the component unoptionated about styling. |

### Example 1

For the demo, we will take advantage of the `useToggle` hook from the [`kantan-hooks`](https://kantan-hooks-docs.netlify.app/docs/intro/#installation) library. It will help us manage a boolean state with helpful functions. So, let's import the hook and the component from their respective libraries. We will also use another state called `message` to make the content dynamic, i.e. if a successful action happens, then `SUCCESS` is rendered, but if not then `ERROR` is rendered.

Note that you have the power to apply your own styling to the `Message` component. The example shows one approach you could take. Feel free to use `Sass`, `styled-components`, `Css Modules`, or whatever your preferrred way of styling is.

[CodeSandbox](https://f0524.csb.app/message)

```jsx title="src/App.js"
import { Message } from "kantan-components";
import { useToggle } from "kantan-hooks";
import { useState } from "react";

export default function App() {
  //used to mount/unomunt component
  const { open, onOpen, onClose } = useToggle(false);
  //dynamically render a message
  const [message, setMessage] = useState("");
  //function that you have to call when a successful action occurs
  const handleSuccess = () => {
    onOpen();
    setMessage("SUCCESS");
  };
  const handleError = () => {
    onOpen();
    setMessage("ERROR");
  };
  return (
    <>
      <button onClick={handleSuccess}>SUCCESS</button>
      <button onClick={handleError}>ERROR</button>
      {open ? (
        <Message onClose={onClose} ms={3000}>
          <div style={{ background: message === "SUCCESS" ? "green" : "red" }}>
            <p style={{ color: "#f8f9fa", textAlign: "center" }}>{message}</p>
          </div>
        </Message>
      ) : null}
    </>
  );
}
```

### Example 2

If you want to have some default styling, like rendering the `Message` component at the bottom of the page, then you can pass `bottom` prop as either `<Message bottom={true} />` or `<Message bottom />`. Also, passing `bottom` or `below`, allows you to pass the `color` prop that will control the background color for the `Message` component.

```jsx title="src/App.js"
import { Message } from "kantan-components";
import { useToggle } from "kantan-hooks";
import { useState } from "react";

export default function App() {
  //redacted for readibility - same as above
  return (
    <>
      <button onClick={handleSuccess}>SUCCESS</button>
      <button onClick={handleError}>ERROR</button>
      {open ? (
        <Message
          onClose={onClose}
          ms={3000}
          bottom
          color={message === "SUCCESS" ? "green" : "red"}
        >
          {message}
        </Message>
      ) : null}
    </>
  );
}
```