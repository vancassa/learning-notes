# React Global Online Summit 2022 - Junior track

## [Dexie.js For Offline Data Storage In React Apps - by Ebenezer Don](https://www.youtube.com/watch?v=u4QTr56t7iM&t=3341s)

Topic: IndexedDB, localStorage, web worker

Dexie.js is a minimal wrapper for IndexedDB. IndexedDB is an alternative to localStorage to store offline data.

IndexedDB Pros:

IndexedDB Cons:

### Q&A:

**Local storage is vulnerable to XSS. How does IndexedDB mitigate that? How's the security like around IndexedDB?**

**Does Dexie provide fallback when browser doesn't support IndexedDB**?

No, you have to do your own check whether the browser supports it or not, e.g.

```js
var db = new Dexie ('appDB');
db.version (...).stores (...)
db.open()
    .catch ('MissingApiError', function (e) {
        // Show message to user that indexedDB is missing
    }).catch (function (e) {
        // Show e.message to user
    });
```

**When do you use local storage instead of IndexedDB?**

**Syncing IndexedDB to the backend?**

**Intermediary computation result (performance)**

**Does web worker has access to IndexedDB?**

## [AG Grid's new React Rendering Engine - by Niall Crosby](https://www.youtube.com/watch?v=u4QTr56t7iM&t=8890s)

Topic: grid, table, reusable component

**AG Grid's challenge:** how to develop a reusable component that can be used in multiple frameworks?

**Two common solutions:**

1. Write in pure JS and wrap the component (poor dev experience)
2. Write the component many times for each framework (expensive)

**AG Grid's previous solution:** option 1 + allow custom component

This has some problems, e.g. for React, in React DevTools, you will only see the React custom component but not the others (because they're written in pure JS). Since they need to use Portal to allow custom React component to be rendered, it may cause performance issues, e.g. flickers.

**AG Grid's current solution:** Separate the computation from the rendering. Write the computation logic in pure JS, but render it using the framework. For example, calculate the new column width in JS, but render the column using React. This means the code for rendering has to be as simple as possible.

As a result, in React DevTools, you will see all the components (cells, columns, etc) as React components.

### Q&A:

**Is the same concept adapted to the other frameworks?**

No. Other frameworks (Vue, Angular) don't have the performance issue that React had with the previous AG Grid. Due to React's virtual DOM and lifecycle that is quite bespoke to React, when you try to use React with pure JS libraries, it causes more friction that you don't see in other frameworks.

**React-table vs AG Grid**

React Table is just a utility function to allow you to generate your own grid. AG Grid comes with a UI, but React Table does not. So you need more code to generate a grid when using React Table. AG Grid also has many built-in features.

**Would you consider using WebComponent for AG Grid?**

WebComponent doesn't do well with binding of the data. You need a framework to bind the data for you. WebComponents can't stand alone. AG Grid used to support Web Components, but there wasn't enough demand for it.

**What is the chart performance in AG Grid?**

AG Grid uses canvas for chart. If the chart uses SVG, it will add <image> to DOM and you will hit performance limit. But using <canvas>, it has higher performance limit.
