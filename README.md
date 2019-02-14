This simple project was built to showcase usage of CSS modules.

## Running

```
yarn install
yarn start
```

## Advantages of such approach and gotchas

- Available out-of-the-box with CRA2 and `react-scripts` with almost zero-configuration 😍
- CSS modules take care of scoping
  - developers create CSS stylesheet in scope of a component only
  - they **don't have to bother about global naming and possible clashes**
- It's possible to attach multiple classes to one container using `classnames`
- Creating a CSS Module is no different then creating any other CSS file
- The CSS syntax is unchanged - reusability
- It kinda automates BEM. Outcome is the same, but it's not on a developer to care about proper and unique naming.
- We're avoiding maintaining long class names, e.g. `MyShadowContainer__spinner--running` - no more complicated BEM names
- Scalable

## What happens after running the application

`css-loader` translates a CSS sheet into a key-values object, replacing the class name and making it unique, e.g. this CSS sheet:

```
.app {
  text-align: center;
}

.app .logo {
  pointer-events: none;
}
```

is converted into the following JSON:

```
{
  app: "App_app__3-MCU",
  logo: "App_logo__2ICcM
}
```

Note that class names generated are very similar to the BEM concept, where you have the Block, then Element, but instead Modifier there's a unique suffix, that makes this particular class unique within the scope of entire application. Even if in 10 sheets you'd have class `.logo`.

The way the class name is being build is fully customizable though.

So now that said, doing

```
import styles from './App.module.css'

...

<div className={styles.app}>Test</div>
```

will result in rendering

```
<div class="App_app__3-MCU">Test</div>
```

Slick as that.

## We could use SASS as well

I'm not like the biggest fan, and not saying we should use it for everything, but using SASS we could simplify:

```
.app {
  text-align: center;
}

.app .logo {
  pointer-events: none;
}
```
into
```
.app {
  text-align: center;
  .logo {
    pointer-events: none;
  }
}
```
which might seem as not such a big win, but I find it pretty useful, when there's more nesting, we're avoiding doing stylesheet like:
```
.container .header .leftPane .icon .image {...}
.container .header .leftPane .icon .text {...}
```
