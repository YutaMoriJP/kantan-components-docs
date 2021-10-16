# Tooltip

A Tooltip UI is an useful UI pattern that provides extra information. In modern web apps, icons are used to represent something; for example, a gear icon is often used to represent a setting. But not all icons are self explanatory. It would be helpful to use a tooltip to describe what exactly that icon is supposed to represent. The purpose of tooltips is not just for icons and you could use it for other purposes.

:::note

The `Tooltip` component is an `inline` element. If you want it to behave like a `block` level element, then wrap it with `div` or whatever fits your need.

:::

## The Syntax

```jsx
<Tooltip text="It might be a good idea to provide more information.">
  <strong>HOVER OVER ME</strong>
</Tooltip>
```

### Props

| Prop                | Type                          | Explanation                                                                                                                                                            |
| ------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `text`              | `String`                      | The extra information that appears when a user hovers over an element.                                                                                                 |
| `children`          | `String` or `React.ReactNode` | It could be a SVG icon, or a simple inline or block element, like `<strong>` or `<p>`. When the user hovers over `children`, the value of the `text` prop will appear. |
| optional - `bottom` | `Boolean`                     | `text` prop will be rendered below `children`.                                                                                                                         |
| optional - `top`    | `Boolean`                     | `text` prop will be rendered above `children`.                                                                                                                         |
| optional - `left`   | `Boolean`                     | `text` prop will be rendered left to `children`. It's a good idea to pass `left` when you know that there isn't any space on the right side.                           |
| optional - `right`  | `Boolean`                     | `text` prop will be rendered right to `children`. It's a good idea to pass `right` when there is no space on the left side.                                            |

### Example 1

Passing the positional props like `bottom`, `top`, `left` or `right` will position the tooltip at the desired place. However, if you don't use the position prop, then the default position will be `bottom`.

[CodeSandbox](https://f0524.csb.app/tooltip)

```jsx title/App.js
import { Tooltip } from "kantan-components";

const App = () => (
  <div>
    <Tooltip text="default position">
      <strong>default</strong>
    </Tooltip>
    <hr />
    <Tooltip text="top position" top>
      <strong>top</strong>
    </Tooltip>
    <hr />
    <Tooltip text="bottom position" bottom>
      <strong>bottom</strong>
    </Tooltip>
    <hr />
    <Tooltip text="right position" right>
      <strong>right</strong>
    </Tooltip>
    <hr />
    <Tooltip text="left position" left>
      <strong>left</strong>
    </Tooltip>
  </div>
);
```

### Example 2

Let's try another demo, using svg icons. We will use the `react-icons` library to import the icons. When the user hovers over the setting/info icon, then whatever you pass to the `text` prop will be rendered.

Install `react-icons` as below:

```shell
npm install react-icons
```

[CodeSandbox](https://f0524.csb.app/tooltip)

```jsx title/App.js
import { Tooltip } from "kantan-components";
import { AiFillSetting, AiFillInfoCircle } from "react-icons";

const App2 = () => (
  <div>
    <Tooltip text="Setting" right>
      <AiFillSetting />
    </Tooltip>
    <Tooltip text="Information" left>
      <AiFillInfoCircle />
    </Tooltip>
  </div>
);
```
