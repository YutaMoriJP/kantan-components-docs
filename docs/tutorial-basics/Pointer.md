# Pointer

The `disabled` attribute in HTML prevents elements from being `focusable`, and makes the element impossible to interact with. However, the `disabled` attribute is only supported by elements like `button`, `input`, `textarea` etc.

Most of the time that is totally fine. However, there might be moments where you wished you could achieve the same thing with other elements like with an `anchor` tag. You could achieve it with the CSS `pointer-events` property. Or simply use the `Pointer` component from `kantan-components`.

Pass a boolean value to the `disabled` prop, and the optional `cursor` prop allows you to control what the cursor should be while the element cannot be interacted with. If you want your `<a>` element to listen to a `click` event, then pass your event handler to the `Pointer` component's `onClick` prop.

The `Download` component uses the `Pointer` component under the hood as well. While the content is being downloaded, users cannot interact with the element. If you want the same behavior, then the `Pointer` component will come in handy. Just make sure that you correctly manage your `disabled` boolean state.

## The Syntax

```jsx
//the disabled boolean state gives you control when your element should be focusable again. Like after a network request has completed.
const [disabled, setDisabled] = useState(true)
<Pointer disabled={disabled} cursor="not-allowed" onClick={handleClick}>
  <a href="#">Don't click</a>
</Pointer>
```

### Props

| Prop       | Type              | Explanation                                                                                                                                                                                                                       |
| ---------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `disabled` | `Boolean`         | If `true`, the element cannot be focused and interacted with.                                                                                                                                                                     |
| `children` | `React.ReactNode` | Wrap your JSX element like an anchor tag with `Pointer`. But make sure that it's only for elements that don't support the native `disabled` attribute. Wrapping a `button` or `input` element with `Pointer` does not make sense. |

| optional - `cursor` | `help` or `wait` or `crosshair` or `not-allowed` or `zoom-in` or `grab` | Controls how the cursor should look like. Defaults to `not-allowed`. |

:::note
Make sure that event handlers are passed to `Pointer`. The `Syntax` example shows how you could approach it.
:::

### Example 1

While the `Pointer` component will manage the appearance of the cursor, you have to manage the color of your element while the element is `disabled`. If you use an anchor tag, then it's a good idea to apply a `grey` color to it while it's disabled.

[CodeSandbox](https://f0524.csb.app/pointer)

```jsx title/App.js
import { Pointer } from "kantan-components";
import { useState } from "react";

const App = () => {
  const [disabled, setDisabled] = useState(true);
  const buttonText = disabled ? "allow pointer" : "disallow pointer";
  const handleClick = () => alert("anchor tag can be clicked again🎉");
  const toggleDisable = () => setDisabled(prevDisabled => !prevDisabled);
  return (
    <>
      <div>
        <Pointer disabled={disabled} onClick={handleClick}>
          <a href="#hi" style={{ color: disabled ? "grey" : "blue" }}>
            Say hi
          </a>
        </Pointer>
        <hr />
        <button onClick={toggleDisable}>{buttonText}</button>
      </div>
      <article id="hi">
        <h2>Hi there!</h2>
      </article>
    </>
  );
};
```
