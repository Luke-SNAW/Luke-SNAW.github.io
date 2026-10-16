
> https://gist.github.com/DavidWells/53518b3c12344952641dc81cc7599939

```js
/* Using a JavaScript proxy for a super low code REST client */
// via https://dev.to/dipsaus9/javascript-lets-create-aproxy-19hg
// also see https://towardsdatascience.com/why-to-use-javascript-proxy-5cdc69d943e3
// also see https://github.com/fastify/manifetch
// also see https://github.com/flash-oss/allserver
// and https://gist.github.com/v1vendi/75d5e5dad7a2d1ef3fcb48234e4528cb

const createApi = (url) => {
  return new Proxy(
    {},
    {
      get(target, key) {
        return async function (id = "") {
          const response = await fetch(`${url}/${key}/${id}`);
          if (response.ok) {
            return response.json();
          }
          return Promise.resolve({ error: "Malformed Request" });
        };
      },
    }
  );
};

let api = createApi("https://swapi.co/api");

// 'get' request to https://swapi.co/api/people
let people = await api.people();

// 'get' request to https://swapi.co/api/people/1
let person = await api.people(1);

// ... any https://swapi.dev/ endpoint
```
