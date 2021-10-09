<div style="text-align: center">
  <a href="https://github.com/github_username/repo_name">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h3 style="text-align: center">project_title</h3>

  <p style="text-align: center">
    project_description
    <br />
    <a href="https://github.com/github_username/repo_name"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/github_username/repo_name">View Demo</a>
    ·
    <a href="https://github.com/github_username/repo_name/issues">Report Bug</a>
    ·
    <a href="https://github.com/github_username/repo_name/issues">Request Feature</a>
  </p>
</div>
# react-loading-skeleton

Make beautiful, animated loading skeletons that automatically adapt to your app.

![Gif of skeleton in action](https://media.giphy.com/media/l0Iyk4bAAjac3AU2k/giphy.gif)

## Basic Usage

Install via one of:

```bash
yarn add react-loading-skeleton
npm install react-loading-skeleton
```

```js
import Skeleton from 'react-loading-skeleton'
import 'react-loading-skeleton/dist/skeleton.css'

<Skeleton/> // Simple, single-line loading skeleton
<Skeleton count={5}/> // Five-line loading skeleton
```

## Principles

### Adapts to the styles you have defined

The `Skeleton` component should be used directly in your components in place of
content that is loading. While other libraries require you to meticulously craft
a skeleton screen that matches the font size, line height, and margins of your
content, the `Skeleton` component is automatically sized to the correct
dimensions.

For example:

```tsx
function BlogPost(props) {
    return (
        <div>
            <h1>{props.title || <Skeleton />}</h1>
            {props.body || <Skeleton count={10} />}
        </div>
    )
}
```

...will produce the correctly-sized skeletons for the heading and body sections
without any further configuration.

This ensures the loading state remains up-to-date with any changes
to your layout or typography.

### Don't make dedicated skeleton screens

Instead, make components with _built-in_ skeleton states.

This approach is beneficial because:

1. It keeps styles in sync.
2. Components should represent all possible states — loading included.
3. It allows for more flexible loading patterns. In the blog post example above, it's possible to have the title load before the body, while having both pieces of content show loading skeletons at the right time.

## Theming

Customize individual skeletons with props, or render a `SkeletonTheme` to style all skeletons below it in the React hierarchy:

```tsx
import Skeleton, { SkeletonTheme } from 'react-loading-skeleton'

return (
    <SkeletonTheme baseColor="#202020" highlightColor="#444">
        <p>
            <Skeleton count={3} />
        </p>
    </SkeletonTheme>
)
```

## Props Reference

### `Skeleton` only

<table>
    <thead>
        <tr>
            <th>Prop</th>
            <th>Description</th>
            <th>Default</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>count?: number</code></td>
            <td>The number of lines of skeletons to render.</td>
            <td><code>1</code></td>
        </tr>
        <tr>
            <td><code>circle?: boolean</code></td>
            <td>
                Makes the skeleton circular by setting <code>border-radius</code> to
                <code>50%</code>.
            </td>
            <td><code>false</code></td>
        </tr>
        <tr>
            <td><code>className?: string</code></td>
            <td>
                A custom class name for the individual skeleton elements which is used
                alongside the default class, <code>react-loading-skeleton</code>.
            </td>
            <td></td>
        </tr>
        <tr>
            <td><code>containerClassName?: string</code></td>
            <td>
                A custom class name for the <code>&lt;span&gt;</code> that wraps the
                individual skeleton elements.
            </td>
            <td></td>
        </tr>
        <tr>
            <td><code>containerTestId?: string</code></td>
            <td>
                A string that is added to the container element as a
                <code>data-testid</code> attribute. Use it with
                <code>screen.getByTestId('...')</code> from React Testing Library.
            </td>
            <td></td>
        </tr>
        <tr>
            <td><code>style?: React.CSSProperties</code></td>
            <td>
                This is an escape hatch for advanced use cases and is not the preferred
                way to style the skeleton. Props (e.g. <code>width</code>,
                <code>borderRadius</code>) take priority over this style object.
            </td>
            <td></td>
        </tr>
        <tr>
            <td><code>wrapper?: React.FunctionComponent</code></td>
            <td>
                A custom wrapper component that goes around the individual skeleton
                elements.
            </td>
            <td></td>
        </tr>
    </tbody>
</table>

### `Skeleton` and `SkeletonTheme`

<table>
    <thead>
        <tr>
            <th>Prop</th>
            <th>Description</th>
            <th>Default</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>baseColor?: string</code></td>
            <td>The background color of the skeleton.</td>
            <td><code>#ebebeb</code></td>
        </tr>
        <tr>
            <td><code>highlightColor?: string</code></td>
            <td>The highlight color in the skeleton animation.</td>
            <td><code>#f5f5f5</code></td>
        </tr>
        <tr>
            <td><code>width?: number</code></td>
            <td>The width of the skeleton.</td>
            <td><code>100%</code></td>
        </tr>
        <tr>
            <td><code>height?: number</code></td>
            <td>The height of each skeleton line.</td>
            <td>The font size</td>
        </tr>
        <tr>
            <td><code>borderRadius?: number</code></td>
            <td>The border radius of the skeleton.</td>
            <td><code>0.25rem</code></td>
        </tr>
        <tr>
            <td><code>duration?: number</code></td>
            <td>The length of the animation in seconds.</td>
            <td><code>1.5</code></td>
        </tr>
        <tr>
            <td><code>direction?: 'ltr' | 'rtl'</code></td>
            <td>
                The direction of the animation, either left-to-right or right-to-left.
            </td>
            <td><code>'ltr'</code></td>
        </tr>
        <tr>
            <td><code>enableAnimation?: boolean</code></td>
            <td>
                Whether the animation should play. The skeleton will be a solid color when
                this is <code>false</code>. You could use this prop to stop the animation
                if an error is encountered.
            </td>
            <td><code>true</code></td>
        </tr>
    </tbody>
</table>

## Advanced

### Custom Wrappers

You can use the `wrapper` prop to wrap each line of the skeleton in a box:

```tsx
function Box({ children }: PropsWithChildren<unknown>) (
    <div
        style={{
            border: '1px solid #ccc',
            display: 'block',
            lineHeight: 2,
            padding: '1rem',
            marginBottom: '0.5rem',
            width: 100,
        }}
    >
        {children}
    </div>
)

// Method 1: use the wrapper prop
const wrapped1 = <Skeleton wrapper={Box} />

// Method 2: do it the normal way
const wrapped2 = <Box><Skeleton /></Box>
```

Prop for wrap the skeleton in a custom component.

### The height of my container is off by a few pixels!

## Acknowledgements

Our logo is based off an image from [Font Awesome](https://fontawesome.com/license/free). Thanks!
