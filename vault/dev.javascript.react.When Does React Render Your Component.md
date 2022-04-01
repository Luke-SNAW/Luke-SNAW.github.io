---
id: 94pcbxczg6umu6h5x0khd8r
title: When Does React Render Your Component?
desc: ""
updated: 1649034391768
created: 1648774140425
---

https://www.zhenghao.io/posts/react-rerender

# Tl;dr

- React (re)renders your component when:
  - there is a state update scheduled by your component
    - including updates scheduled by custom hooks your component consumes
  - the parent component got rendered and your component doesn’t meet the criteria for bailing out on re-rendering, where all these four conditions have to be satisfied at the same time:
    - Your component has been rendered before i.e. it already mounted
    - No props (referentially) changed
    - No any context value consumed by your component changed
    - Your component itself didn’t schedule an update
- You probably shouldn’t need to worry about seemingly unnecessary re-renders until it becomes a performance issue. Check out the flow chart I made for solutions you can adopt when a performance issue occurs.

> Disclaimer: I haven't used React's concurrent mode so some parts of this post might not be applicable in concurrent React.
