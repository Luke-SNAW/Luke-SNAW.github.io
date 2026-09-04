
# [React Components render twice - any way to fix this?](https://www.heissenberger.at/en/blog/react-components-reder-twice/)

> The reason why this happens is an intentional feature of the React.StrictMode. It** only happens in development mode** and should help to find accidental side effects in the render phase.

## What is happening behind the scenes?

The main reason is `React.StrictMode` which was introduced in version 16.3.0. Back then it only could be used for class components. With the release of 16.8.0 it is also applied for hooks.

## Why should I use React.StrictMode?

React will soon provide a new [**Concurrent Mode**](https://reactjs.org/docs/concurrent-mode-intro.html) which will break render work into multiple parts. Pausing and resuming the work between this parts should avoid the blocking of the browsers main thread.

> This means that the render phase could be invoked multiple times and should be a Pure Function without any side effects!
