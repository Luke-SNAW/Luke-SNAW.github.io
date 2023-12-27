---
id: r0ap6jxla9lz2ytw97o5jbk
title: "Micro Frontend Synergy: Techniques for Effective Communication"
desc: ""
updated: 1703661786803
created: 1703661665555
---

> https://medium.com/@rk-tech/micro-frontend-synergy-techniques-for-effective-communication-97df104931ed

In the evolving landscape of web development, the adoption of micro frontends has emerged as a game-changer, offering unparalleled flexibility and scalability. However, this modularity introduces a significant challenge to seamless communication between these disparate parts.

The core problem lies in the inherent isolation of micro frontends. While each unit operates independently, they often need to share data and state or trigger actions in one another. Consider a travel booking website with separate micro frontends for flight search, hotel booking, and user profiles. Efficient communication between these components is crucial for a seamless user experience.

Let’s embark on this journey to unlock the full potential of micro frontends through effective and efficient communication.

## Through Props

In this method, the main application (container) manages the state and passes it down to micro frontends. Imagine a dashboard application where the main container holds user preferences and propagates them to various micro frontends like settings panel, display panel, etc.

```js
// In the main container
class Dashboard extends React.Component {
  state = { theme: 'dark' };

  setTheme = (theme) => {
    this.setState({ theme });
  };

  render() {
    return (
      <div>
        <SettingsPanel setTheme={this.setTheme} />
        <DisplayPanel theme={this.state.theme} />
      </div>
    );
  }
}

// In SettingsPanel
const SettingsPanel = ({ setTheme }) => (
  <button onClick={() => setTheme('light')}>Light Theme</button>
);

// In DisplayPanel
const DisplayPanel = ({ theme }) => (
  <div className={\`theme-${theme}\`}>Display Content</div>
);
```

**Pros:**

- **Supported by Many Frameworks:** Most modern front-end frameworks, like React, Vue, and Angular, have built-in support for props (or similar concepts).
- **Easy to Understand and Implement:** Props represent a straightforward way to pass data from parent to child components, making the flow of data easy to trace and understand.

**Cons:**

- **Creates Tight Coupling:** Using props for communication implies a direct dependency between the micro frontends. Changes in one component can necessitate changes in others, leading to a ripple effect.
- **Unnecessary Re-Renders**: In some frameworks, passing props down a component tree can cause components to re-render unnecessarily, even if the data they consume hasn’t changed.
- **Framework dependent:** In a micro frontend architecture, different teams might use different frameworks for each frontend. Props are framework-specific and can’t be used for inter-framework communication.

## Custom Events

This approach uses the browser’s custom event APIs. Consider a stock market dashboard where one micro frontend publishes stock updates, and another micro frontend listens to these updates to display real-time charts.

```js
// In StockUpdate Micro Frontend
function publishStockUpdate(stockData) {
  const event = new CustomEvent("stockUpdate", { detail: stockData })
  window.dispatchEvent(event)
}

// In StockDisplay Micro Frontend
window.addEventListener("stockUpdate", (e) => {
  displayStockData(e.detail)
})
```

### **Pros:**

- **Decoupling of Components:** Custom Events allow micro frontends to communicate without needing direct references to each other. This decoupling facilitates a more modular and maintainable codebase, where individual components can be developed, tested, and deployed independently.
- **Native Browser Support:** Custom Events are supported natively by modern web browsers, eliminating the need for additional libraries or dependencies for event handling in web-based micro frontends.

### **Cons:**

- **Browser Dependency**: Custom Events are primarily a web browser feature. This reliance on browser capabilities can limit their use in environments outside of traditional web browsers, such as native mobile apps or server-side rendering scenarios
- **Potential for Memory Leaks**: If not managed properly, custom event listeners can lead to memory leaks.
- **Global Scope Pollution**: Custom Events typically operate at a global level (like the window object in a browser). This global scope can lead to naming conflicts and inadvertent triggering of events across unrelated parts of the application.

## Using Browser Storage APIs

This technique involves using browser storage (like sessionStorage) for communication. For example, a news portal could use this to store and share user preferences (like language or region) between its article listing and article detail micro frontends.

```js
// In ArticleListing
function selectCategory(category) {
  sessionStorage.setItem("selectedCategory", category)
}

// In ArticleDetail
function getSelectedCategory() {
  return sessionStorage.getItem("selectedCategory")
}
```

**Pros:**

- **Simplicity and Ease of Use**: Requiring minimal code to store and retrieve data
- **No Server Interaction:** Since the data is stored locally in the user’s browser, it doesn’t require server calls to fetch or save, which can improve performance and reduce server load.

**Cons:**

- **Limited scalability:** Browser Storage APIs have a limited capacity (usually about 5MB), which is not suitable for storing large amounts of data.
- **Lack of Real-Time Sync:** There’s no built-in mechanism to notify micro frontends of changes in stored data, making real-time synchronization challenging.
- **Not Suitable for Complex Data:** These APIs are designed for key-value pairs and are not ideal for storing complex or hierarchical data.

## Custom Message Bus

Similar to custom events, but with a self-built pub-sub system. In a social media application, different micro frontends could use a message bus to update and display new messages or notifications.

```js
// MessageBus implementation
const MessageBus = {
 events: {},
 subscribe: function (eventName, fn) {
 this.events\[eventName\] = this.events\[eventName\] || \[\];
 this.events\[eventName\].push(fn);
 },
 publish: function (eventName, data) {
 if (this.events\[eventName\]) {
 this.events\[eventName\].forEach(fn => fn(data));
 }
 }
};

// In MessageSender Micro Frontend
MessageBus.publish('newMessage', { content: 'Hello!' });

// In MessageReceiver Micro Frontend
MessageBus.subscribe('newMessage', (data) => {
 displayNewMessage(data);
});
```

**Pros:**

- **Flexibility and Scalability:** A custom message bus allows for tailored, scalable inter-component communication, fitting diverse application needs.
- **Framework Independence:** It provides a framework-agnostic approach, enabling integration across different technologies within micro frontends.

**Cons:**

- **Complexity in Implementation:** Setting up a custom message bus can be complex, requiring careful design and maintenance.
- **Consistency Challenges:** Ensuring consistent use and understanding across different teams and micro frontends can be challenging.

In conclusion, The key takeaway is the importance of carefully evaluating the communication needs of your micro frontend architecture. Factors such as framework compatibility, the need for scalability, performance considerations, and the level of coupling between components should guide the decision-making process. Embracing the right communication strategy not only enhances the functionality and user experience of the application but also ensures a maintainable and scalable codebase.

Ultimately, effective communication in micro frontends is about striking the right balance between independence and integration, ensuring that each component functions seamlessly as part of a greater whole, without losing its standalone capabilities. As the field of web development continues to evolve, so too will the strategies for micro frontend communication, promising more innovative and efficient ways to tackle this complex yet crucial aspect of modern web architecture.
