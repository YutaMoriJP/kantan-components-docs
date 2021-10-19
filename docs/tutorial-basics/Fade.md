# Fade

The `Fade` component allows you to render your component with a fade in animation. The API is simple and intuitive. Simply, wrap your component with `Fade` and pass a time value in milliseconds to the `ms` prop.

## The Syntax

```jsx
    <Fade ms={500}>
      <header>
        <h1>Welcome to Fade</h1>
      </header>
    </Fade>
    <Fade ms={1000}>
      <article>
        <h2>Introduce in a cool fading animation to your UI</h2>
        <p>
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. A minus illo
          iste voluptas. Voluptatibus quisquam optio accusantium odit fugit,
          reprehenderit sapiente ad ipsam quod itaque vero harum soluta numquam
          nulla?
        </p>
      </article>
    </Fade>
```

### Props

| Prop       | Type              | Explanation                                                                                                                                             |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ms`       | `Number`          | The `ms` prop controls when your component becomes visible to the user. If you pass `1000` to `ms`, then your component becomes visible after 1 second. |
| `children` | `React.ReactNode` | Wrap your component with `Fade`, like `<Fade ms={1000}><BlogPost /></Fade>`.                                                                            |

### Example 1

You do not need to be worried about side-effects or other challenges. Simply wrap your component with `Fade` and control the time interval when your components become visible with the `ms` prop. A difference of `500ms` makes sense.

[CodeSandbox](https://f0524.csb.app/fade)

```jsx title/App.js
import { Fade } from "kantan-components";

const App = () => {
  return (
    <>
      <Fade ms={150}>
        <header>
          <h1>FADE</h1>
        </header>
      </Fade>
      <Fade ms={500}>
        <h2>hi fade</h2>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut sint
          quidem eligendi necessitatibus expedita tenetur, sed optio ab officia
          nobis voluptatum iusto nisi corporis rem asperiores quia? Unde, odio
          alias!
        </p>
      </Fade>
      <Fade ms={1000}>
        <h3>hi fade</h3>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut sint
          quidem eligendi necessitatibus expedita tenetur, sed optio ab officia
          nobis voluptatum iusto nisi corporis rem asperiores quia? Unde, odio
          alias!
        </p>
      </Fade>
      <Fade ms={1500}>
        <h4>hi fade</h4>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut sint
          quidem eligendi necessitatibus expedita tenetur, sed optio ab officia
          nobis voluptatum iusto nisi corporis rem asperiores quia? Unde, odio
          alias!
        </p>
      </Fade>
      <Fade ms={2000}>
        <h5>hi fade</h5>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut sint
          quidem eligendi necessitatibus expedita tenetur, sed optio ab officia
          nobis voluptatum iusto nisi corporis rem asperiores quia? Unde, odio
          alias!
        </p>
      </Fade>
      <Fade ms={2500}>
        <h6>hi fade</h6>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut sint
          quidem eligendi necessitatibus expedita tenetur, sed optio ab officia
          nobis voluptatum iusto nisi corporis rem asperiores quia? Unde, odio
          alias!
        </p>
      </Fade>
    </>
  );
};
```
