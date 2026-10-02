
> https://django-htmx-alpine.nicholasmoen.com/

## Why Alpine.JS?

Alpine.js is designed to act as a lighter version of Vue.JS. It allows you to easily add the power of reactivity, but allows the functionality to be sprinkled into your code as desired. It works with the paradigm of a predominantly server-driven experience, not against it.

## Why HTMX?

HTMX is a interesting library that adds client-server interactivity to plain HTML tags. It is a tool that makes it easy to add REST-style interactions to your page, but with one difference from other such tools: It works with entire DOM elements (HTML tags), not just JSON.

This means you don't have to process the data on the client-side; you can simply return page fragments from your server. As with Alpine.JS, this gives the power back to the server-based frameworks. For example, your Django server can render all the elements with the proper data, and you simply receive the data and pop it right where it needs to go, with no Javascript-based messing around with Fetch calls.

Simply adding a couple attributes to the HTML completely changes the dynamic of the form.

The `hx-post` attribute tells HTMX to send a [POST request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) to the location specified in the attribute's value (e.g. `/get_weather/)`. The POST request will contain the values of every element contained in the form, and the Django server will process them as a dictionary (key-value pair) with the form element's `name` as the key, and the element's `value` as the value.

The `hx-target` attribute specifies which HTML element to replace when the server sends a response (e.g. the HTML element on this page that contains `id="demo-htmx-target"`).

In summary, when the link is clicked, here's what happens:

- The browser sends the data from the form to the URL specified in the `hx-post` tag, which points to a endpoint on our server that handles the request,
- Our server receives and processes the response,
- Our server sends a request containing the processed data to a weather API server,
- Our server receives and processes the response from the weather API server,
- Our server builds and sends an HTTP response (rendered as plain old HTML, not JSON) back to the browser, containing (among other things):
  - The [HTTP status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) of the response (NOTE: The server always returns a successful `200` code because HTMX may not swap out the content for certain response codes. The error code that is displayed is just a simulation of what the actual error code should be.)
  - The message created on the Django server, which is made using the data from the weather API server's response.
- The browser receives the response from our server and swaps out the element specified in the `hx-target` element with the content received from the server.

Now, instead of completely refreshing the page, the client can replace fragments of the page. The server will send back the proper fragment, and it will be put in the desired location. This gives a more integrated, app-like feel, instead of refreshing the whole page and breaking the user experience.

In short, using HTMX allows us to easily extend HTML to provide a modern web experience without getting bogged down in Javascript boilerplate. It can also help us to move our business logic onto the server, which can be useful for preventing sensitive data from being exposed (such as the API key used to access the weather service, or even the name of the weather service).

## Where's the Alpine?

Pretty much any fancy client-side stuff in this project was made with Alpine:

- The Alpine.JS demo above (duh)
- Toggling modals (including fade effects)
- Updating DOM elements in the task list when client-side-rendering is enabled.
- Status message popups (I had a lot of fun with these. Clicking them can dispatch events and toggle actions, and HTMX calls can cause status messages to appear with relevant messages from the Django server. Try creating a task when you aren't logged in, then click on the status message.)

A lot of the logic in the Alpine components could have just as easily been implemented in Vanilla JS, but I find it's just easier to use an Alpine component so Alpine's magic is available when you need it.

**Note:** By default, the list of tasks is rendered server-side. This means that Django will retrieve the whole queryset and return it for each create/update/edit/update/destroy action, ie. complete server-side re-rendering (which is very inefficient). _However_, However, if you add a GET parameter (`is_csr=1`) to the URL while viewing your tasks (e.g. `/tasks/?is_csr=1`), this will enable a more efficient mode that utilizes client-side rendering. Django will only return as much data as necessary, and Alpine will iterate over the data to create your task list.

## Where's the HTMX?

Anything that requires a network call without completely reloading the page uses HTMX (Basically anything other than clicking on links). This includes:

- The HTMX demo above (also duh)
- Fetching CAPTCHAs when the modals are opened, or when the CAPTCHA refresh button is clicked.
- Sending authentication credentials to the server and providing a relevant response.
- Posting data to the server when tasks are created, updated, and destroyed.
