---
id: t2mnbwz72sq8t4csp7wlpf0
title: Software Component Names Should Be Whimsical and Cryptic
desc: ""
updated: 1765847451632
created: 1765847432206
---

> https://medium.com/better-programming/software-component-names-should-be-whimsical-and-cryptic-ca260b013de0

- Descriptive names for software components can be misleading as the scope and purpose of a component can change over time, rendering the original name inaccurate.
- Descriptive names create an illusion of transparency rather than true clarity, leading to incorrect assumptions about a component's functionality.
- For variables within code that are frequently changed, descriptive names like numCols and numRows are preferable to generic ones like i and j.
- When a name serves as an identifier for a complex, long-lived entity, it should be an opaque and immutable identifier, similar to using numerical IDs instead of email addresses as foreign keys in databases.

---

I often see this call to action: “Please, engineers, name your services/repos/libraries more descriptively!
No. Unironically, no. This is a bad idea.
I’m probably being overdramatic there, but I hope my point is clear. “Descriptive” names don’t create transparency, they create the [illusion of transparency.](https://en.wikipedia.org/wiki/Illusion_of_transparency) If you see that something has the name OrderStatusService, you will instinctively assume you know what it is and does, and you will probably be wrong.

- `[django-htmlmin](https://github.com/cobrateam/django-htmlmin)`: HTML minifier for Python frameworks (not only Django, despite the name).
- `[plugin-update-checker](https://github.com/YahnisElsts/plugin-update-checker)`: Despite the name, it also works with themes.
- `[svox2](https://github.com/sxyu/svox2/blob/master/README.md)`: Despite the name, it’s not strictly intended to be a successor of svox.
- `[CO_Cron](https://github.com/ColoradoDemography/CO_Cron)`: Despite the name, uses node-schedule rather than cron.
- `[TensorFlow Infra Validator](https://github.com/tensorflow/tfx/blob/master/docs/guide/infra_validator.md)`: Despite the name, does not validate the infrastructure being used to run TensorFlow.

(Even worse are those ubiquitous diagrams everybody uses to communicate about software, where there’s a box labeled OrdersService with an arrow connecting it to a box labeled OrderStatusService. I don’t understand why anybody draws those. You can just say “The Orders Service asynchronously pushes order ids, ETAs, and statuses to the Order Status Service.” If you draw a diagram instead, anybody who wants to believe that the data flows in the other direction, or is synchronous, or is different data, will look at the diagram and see confirmation.)

Now, if a name is going to be easily changeable forever, please do make it descriptive. I’d much rather maintain code where the variables look like numCols and numRows than i and j. (Just, for the love of God, if you change the meaning, also change the name). But if a name is going to serve as, in any sense, an identifier, something that will point at a big complicated thing from many places far away, make it an opaque identifier. You get similar advice in database schema design — if your user’s email address can change, don’t use their email address as a foreign key in your database. Use a number or a random string instead. Something immutable.
