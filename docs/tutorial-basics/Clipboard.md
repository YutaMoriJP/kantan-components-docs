# Clipboard

The `Clipboard` component helps you to easily copy a value to the user's clipboard.

## The Syntax

```jsx
<Clipboard toBeCopied="Hello, World" message="COPIED!">
  <button>copy</button>
</Clipboard>
```

### Props

| State               | Type                         | Explanation                                                                                                                                |
| ------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `toBeCopied `       | `String`                     | The value that you want to copy to the user's clipboard.                                                                                   |
| `children `         | `React.ReactNode` or`String` | An element or string that invites the user to copy the `toBeCopied` value to their clipboard. An element like a `button` would make sense. |
| optional `message ` | `String`                     | The message that should be rendered after the copying operation was successful. The default message is `COPIED`.                           |

### Example

As the example illustrates, using the `Clipboard` component is easy. Simply pass a value to the `toBeCopied` prop and pass something like a `button` element as the `children` prop to invite the user to copy the value and you're done! The `message` prop is optional and it defaults to `COPIED`. If an error occurs, like a permission issue, the `Clipboard` component will make the user aware about what exactly went wrong.

[CodeSandbox](https://f0524.csb.app/clipboard)

```jsx title="src/App.js"
import { Clipboard } from "kantan-components";

export default function App() {
  return (
    <>
      <Clipboard toBeCopied="Hello World" message="copied!">
        <button>Copy 'Hello World'</button>
      </Clipboard>
    </>
  );
}
```
