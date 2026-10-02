
## Collections

- [Django, HTMX and Alpine.js: Modern websites, JavaScript optional](https://www.saaspegasus.com/guides/modern-javascript-for-django-developers/htmx-alpine/)
  - Alpine focuses on client-side state and operations, HTMX focuses on interaction with your server.
  - The core workflow of HTMX is: _make a request to the server and swap the response into the page_. At first this sounds a lot like every other AJAX workflow, but there’s a key difference: **the response is returned (and rendered) as HTML.**
- [recursivedoubts](https://news.ycombinator.com/item?id=29966898)
  - htmx is a relatively low level extension to HTML, by design. Unpoly offers a lot more structure, such as layers, which you would need to implement on your own or using another library (e.g. tailwinds or bootstrap) if you are using htmx.
  - This is reflected in their overall sizes: 11k for htmx, 41k for unpoly.
  - I don't view either as better in general: they are two different approaches to building hypermedia-oriented applications, one more structured and one less. Which one is better for your particular application depends on your own engineering needs and tastes.
