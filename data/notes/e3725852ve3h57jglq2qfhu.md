
> https://medium.com/agileinsider/the-lessons-i-learned-during-my-first-big-prd-transfer-84a622ed61f8

## What to understand about tech

“Think from the perspective of a developer. If they look into your PRD requirement, would they know right away how to code it?” Wise words from Patrick.

Even for the most seemingly obvious thing, we need to be able to know where this data coming from. For example, a user ID is not just a user ID. How is it created from the back end? At what point does it appear in the front end? I probably could have written a much more detailed and clear PRD at the beginning, had I acquired more knowledge about how the back end works, and how data is stored and generated. This would not only help to better understand how your product is being built at its core, but also how to estimate the effort of development when talking to business stakeholders, specifically. This is super-helpful when requesters have fancy product requirements, while your team only has limited resources.

## What to understand when talking to business stakeholders

**The best product will be those allowing users to use without having to read or figure out too much on their own.** The product should be user friendly and instinctive, and it should minimize any complexity involved while in use. It is also crucial to keep looking for alternative use cases and brainstorm how the product can maximize the user experience.

PMs can be reluctant when asked to change their product design. But we are building it for our users, not ourselves.

While user experience is crucial, I find it very easy to fall into the trap of siding with users and forgetting you are also representing people on the development team. In my case, we were debating between the two ways to let reviewers update a user: whether to update a user on the spot using inline edit, or make them update batch users by uploading a CSV file. The former is, apparently, more user friendly and convenient, but in a business case when reviewers have to check thousands of users at a time, inline edit is not ideal. It would be best if we could do both features to optimize user experience, but again, the limited resources come into play, so we have to decide which option comes first.

While user experience is crucial, remember you are not only representing your users, but there are other stakeholders you should keep in mind, as well.

# Do research on edge cases

Another trap I fell into is I imagined the perfect route for the product without taking edge cases into much consideration. Edge cases here can include how your product handles empty state, errors or overload state. In each scenario, the logic behind the scene definitely changes and can be tricky. A great product manager (such as Patrick) is someone who can think of thousands of edge cases while communicating with business stakeholders and understand how the workflow will alter in between.

# No one has time for your detailed PRD

It’s a sad fact, but developers won’t have time to read a detailed PRD, regardless of how much effort you put into it. As a PM, it is important to do a detailed PRD, because developers will need to refer to small details during the development process. But how can we make developers have a grasp of what we are building, thereby allowing them to be able to estimate the effort as soon as possible?

I tried to put an overall mock-up flow at the beginning of my PRD, so developers can have an overview of how the whole thing works before writing detailed descriptions for each feature functionality. Visuals definitely do a better job than words.

For a product with more than one type of user (in this case, both reviewers and auditors are our clients), a PM needs to thoroughly understand how a change in the system can affect the other party. Developers will spend much of the time in the PRD review asking questions in order to save some time reading 10 pages, so a PM must make sure she/he understands all the logic behind the scene, any hidden problems that might arise, all use cases, and why (most important) the current product design is the most optimal — considering other factors, such as available resources, business requirements, user experience, etc.

# The ability to synthesize information

This is such an important skill that I can’t stress it enough; I’m still trying to improve it day by day. In some discussions, when a lot of information from different stakeholders is being thrown at you, you must make sure you have an idea of what they are talking about. Even if you don’t quite understand everything (such as in some technical discussions), it is important to, at least, have a sense of what they are trying to convey, then confirm with them by saying something such as: “Here is what I understand from what you are saying. Is this correct?”
