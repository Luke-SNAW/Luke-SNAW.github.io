---
id: 6a4pspgy5vpdeqr0t75ja88
title: Links vs Buttons in Modern Web Applications
desc: ""
updated: 1669098305522
created: 1647936095746
---

https://marcysutton.com/links-vs-buttons-in-modern-web-applications

## Buttons

Somehow people become web developers without learning about the HTML `<button>`element. (I'll admit it took me a few years before I knew what h1-h6 headings were for, so it happens.) The mighty button is actually really cool. It can do all these things:

- Receive keyboard focus by default
- "Click" with the Space key
- Submit form data to a server
- Reset a form
- Be disabled with the disabledattribute
- Instruct a screen reader with the implicit buttonrole
- Show :focus, :hover, :active, :disabled

With a little scripting, a button is the perfect element for:

- Opening a modal window
- Triggering a popup menu
- Toggling an interface
- Playing media content
- Inserting with JS if they only work with JS

## Links

Here are a few of the basic features of links, a.k.a. anchors, a.k.a. the foundation of the Web:

- Create hypertext, a network of online resources
- Navigate the user to a new page or view
- Change the URL
- Cause a browser redraw/refresh
- Support page jumps with internal hrefattributes
- Deep-link client-rendered applications
- Are focusable by default with the hrefattribute
- Register a click with the Enter key
- Have the implicit linkrole
- Can't be disabled like buttons but can be made inert with tabindex="-1"and aria-hidden="true"
- Allow opening in new windows (and back in the day, framesets)
- Show :link, :visited, :focus, :hover, :active

The starkest difference between a link and a button to me is that a link navigates the user to a new resource, taking them away from the current context (internal links are the only wrinkle here). A button toggles something in the interface, like a video player; or triggers new content in that same context, like a popup menu using **aria-haspopup**.

### What is navigation? What is routing?

### Where does the confusion come from?

## The Role of UX in Accessible Development
