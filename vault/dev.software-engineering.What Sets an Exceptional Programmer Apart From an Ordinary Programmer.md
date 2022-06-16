---
id: 97ha3zf4db021vg7p1jtby7
title: What Sets an Exceptional Programmer Apart From an Ordinary Programmer
desc: ""
updated: 1655427436942
created: 1655427370145
---

https://levelup.gitconnected.com/what-sets-an-exceptional-programmer-apart-from-an-ordinary-programmer-73d3fce24e21

Programming is a discipline which you can master with time.

The general rule is that the more time you _mentally_ spend with your code (not necessarily in front of your monitor), the better programmer you become.

That is the reason I personally do not like labels such as _exceptional_ and _ordinary_.

That said, this question always nags interviewers, because they are forced to make comparisons. Interview candidates also go through an intense amount of stress regarding how to demonstrate themselves better than others, as against being simply good — which is what is truly needed on the job.

What differentiates an exceptional programmer from an average one is the set of ideas, exhibited during the interview/interaction process. Those ideas have been described in detail in the greatest programming books.

Apart from those ideas, exceptional programmers also exhibit certain behavioural symptoms, gained via industry experience, or good collaboration practices. Those behavioural symptoms are visible through their habits, and interviewers expect to witness them during the interviews.

Here, we aim to go through the essence of being exceptional. Let’s begin.

## #1: Scope Refinement:

A wise person said once: Asking the right questions is 50% solution.

When presented with a code problem, good programmers start solving a problem. Exceptional programmers first try to define it.

This is because good programmers feel they have known enough. They can’t resist the temptation to show “_I know the kind of problem you are trying to solve. That’s why you should hire me._” I described this trait in my story [The Most Underrated Technique To Nail Senior Developer Interviews](https://betterprogramming.pub/the-most-underrated-technique-to-nail-senior-developer-interviews-f917025453b7)

Exceptional programmers, on the other hand, begin to show how it’s done.

They do it by starting to keep quiet, and listen. They try to ponder upon the overall context of the challenge that is presented. They already know how to code the solution. But even when they don’t, they know how to isolate that complex part, and make it seem minuscule compared to the overall solution.

They implicitly show that coding is the only (more often, the last) part of the solution.

> By refining scope, an exceptional programmer drives the interviewers towards his/her intended solution.

When an interviewer asks “_Given an array of a town’s citizens, how to calculate the average age of the voters?_”, a good programmer will quickly scribble the following solution:

function calculateAge(votersArray: \[Citizen\]) {  
 if (votersArray.count < 1) {  
 return 0  
 } sum = 0  
 for person in votersArray {  
 sum =+ voter.age  
 } average = sum / votersArray.count  
 return average  
}

On the other hand, an exceptional programmer will ask the following questions:

- What is the minimum voting age? (remember this is a **citizen** array, not the readymade list of voters!)
- Is there a data item to signal if a voter is a registered one with the electoral body?

At this point, most interviewers do not give concrete answers. They rather allow the candidate the freedom to implement it the best way they can. (Although they mentally assign some points for asking questions, and more points for asking the right ones)

The exceptional programmer will then code his/her solution like this (the solution does not adhere to any programming language):

class Citizen {  
 var age: Int  
 var isRegistered: Bool  
}function calculateAge(citizensArray: \[Citizen\], filterFunction: (Voter) -> Bool) {  
 if (citizensArray.count < 1) {  
 logMessage("Citizen list is empty!")  
 return 0  
 }var votersCount = 0 //tracks only the eligible voters  
for citizen in citizensArray {  
 if (citizen.age >= MINIMUM_VOTER_AGE && citizen.isRegistered == true)  
 sum =+ sum + citizen.age  
 votersCount += 1  
 }  
 } average = votersCount > 0 ? (sum / votersCount) : 0  
 return average  
}**// Usage:**citizen1 = Citizen(age: 38, isRegistered: true)  
citizen2 = Citizen(age: 30, isRegistered: true)  
citizen3 = Citizen(age: 28, isRegistered: false)citizens = \[citizen1, citizen2, citizen3\]//finds average age of voters - returns 34  
let average = calculateAge(citizensArray: citizens)

Notice the difference refining the scope makes? By doing it, the exceptional programmer-

- Shows his/her object design skills, where the abstraction and cohesiveness of data (citizen age, registration etc) are tested.
- Not only takes care of the boundary conditions, but is also instrumental in defining them (15000 registered voters vs 89000 citizens). By refining scope, he/she helps (and effectively drives) the interviewers towards his/her intended solution.
- Reports the errors. Here, empty citizens list is reported via logging, but exceptions can be another way to report them, too.
- Shows the benefit of his/her solution, by including the client call examples under the usage section.

Now, if you look at the good programmer’s solution in retrospect, you will observe that it is a correct solution to the problem narrated by the interviewers.

But it seems rooted in the online coding tests environment, where checking the boundary conditions is considered the end objective of perfect programming. That leads one to limit the area of the problem.

An exceptional programmer expands the problem area beyond mere coding, and in doing so, ends up creating more usable code that can be more readily deployed in production.

## #2: Clean Code:

Scope refinements leads one to solve 50% of the problem. Clean code accomplishes the rest.

Clean code is not a trait, but a state that is achieved with hours of working on the same piece of already well-functioning code. In other words, it is a result of countless hours of refactoring, done with clear knowledge of SOLID principles.

> Clean code is not a trait, but a state that is achieved with hours of refactoring

If you are the kind who copies solutions from StackOverflow and ship it without at least 3 iterations, you probably have much work to do in this area. I know, because I was one, and heavily paid for it throughout my career as a senior developer.

Let’s understand this with an example. In a typical coding assignment, interviewers ask about fetching data from an API, and display it in the UI.

This is typically done by converting API data (**_api/restaurants_**) into domain objects (**Restaurant** array), and write UI code that depends upon this domain objects.

A good programmer who has worked in areas ranging from IoT to media streaming is still likely to produce the code such as this:

var restaurantArray = Array<Restaurant>()  
if JSONDeSerializer().decode(httpResponse) != Error {  
 restaurantArray = JSONDeSerializer().decode(httpResponse)  
} else if XMLDeSerializer().decode(httpResponse) != Error {  
 restaurantArray = XMLDeSerializer().decode(httpResponse)  
}

The problem? Not only this code decodes the response twice (first in the check, then in the actual conversion), it is also soon likely to bubble into spaghetti. What if there are more deserialisation formats beyond XML and JSON?

> If-else is poor man’s polymorphism.

To reiterate, the problem isn’t the conversion itself, but the pattern. If you have a business logic that deals with checking 4 fields today, how likely it will accommodate 10 more, if you code it with **if-else approach** shown above?

Someone has rightly termed if-else as poor man’s polymorphism.

The exceptional programmer already realises this, and devises his/her solution something like this:

class APIDownloader {  
 APIDownloader(deserializer: Deserializer) {  
 this.deserializer = deserializer  
 } function downloadData() {  
 //downloading logic  
 deserializer.decode(httpResponse)  
 }  
}

What is **Deserialiser**? It is an interface/protocol that defines **decode(HttpResponse)** function. It must be implemented/conformed by **JSONDeSerializer** and **XMLDeSerializer** classes, which provide concrete implementations of the **decode**() function (mostly, open source)

Where is deserialiser coming from? From outside **APIDownloader**. It isn’t APIDownloader’s responsibility to decide what HTTP response format it is dealing with. Some other class creates an object of type **Deserializer** (which could be an instance of a class **JSONDeSerializer** or **XMLDeSerializer**), and hands it to the APIDownloader.

> The strategy is to push if/else outside the very class you are coding, eventually replacing it with switch/case

That _some other class_ could be an **APIClient** class, who, before even making an HTTP request, knows which format the HTTP response is going to be. Or, it could be a unit test for the **APIDownloader,** which makes the task for APIDownloader quite well-defined: Just download the data, and return to me the XML/JSON domain objects.

If you think it one more time, this whole exercise is aimed at pushing if-else outside the scope of the very class you are coding. APIDownloader delegates if-else to **APIClient**/unit test, and so on**.** When it becomes absolutely necessary to use it, one can replace it with **switch case**, which makes the job of compiler fairly easy (of course, depending upon the programming language)

In programming parlance, this technique is called dependency injection, and it is one of the founding cornerstones of clean code.

It is so, because it automatically enforces the fundamental principles of clean code:

- Class design and separation of concerns (aka the S in the SOLID)
- Single layer of abstraction (APIDownloader deals with only downloading, not conversion**)**
- Polymorphism (**Deserialiser** abstract interface**)**
- Test driven development

If you only know how to use the dependency injection technique, you will start self-correcting and refactoring your code more often. It has its limitations, yes — especially when you end up injecting N arguments into your class, at which point you should simply lay out a separate class by coalescing them.

But in general, when you start using DI, it will become a habit quite easily. You will turn into an exceptional version of yourself before you even realise.

## #3: Build capabilities, not features:

If you revisit the example we saw in #1, you will realise one glaring shortcoming in the exceptional programmer’s approach. In demonstrating the scope refining capabilities, he/she ends up adding two more fields (**isRegistered** and **age**) to the **Citizen** class.

While these are the crucial details, they make the solution laden with an extra set of _if_ conditions (**citizen.age >= MINIMUM_VOTER_AGE && citizen.isRegistered == true).**

There can be an endless list of attributes that can be added to the **Citizen** class. But for the time it takes to code/present the solution, will it demonstrate more capabilities of the candidate? Not at all.

Interviewers will invariably spot this too, although when they reject such a candidate, all they will say is “_Candidate ended up doing things outside the scope._”

What they might omit to report (although it was a fact) was this statement:

> With no other capability demonstrated.

Good programmers can implement features without bugs, exactly as presented in the requirements. When they go an extra mile, their **complexity vs outcome** graph is linear. In achieving more, they end up making the code much more complex.

Exceptional programmers will implement features with or without bugs. But in doing so, they will leave the code to their successors with extra capabilities. These capabilities ensure that any amount of increase in attributes or functions can be handled with minimal extra altercations.

Exceptional programmers’ **complexity vs outcome** graph would be better than linear — probably an exponential one. In other words, they will achieve much better outcomes with less amount of added complexity.

During scope refinement, an exceptional programmer might additionally ask:

> Are we interested in just the overall age average, or also the average age of a certain group of voters (e.g. right-wing voters, female voters, educated voters etc.)

Once again, the interviewers won’t offer anything concrete, but they will observe the keenness to go an extra mile. More importantly, though, they will be interested in seeing how the candidate pulls **_it_** off.

The bold+italicised **_it_** part in the above sentence stands for capabilities to verify/evaluate any number of extra Citizen attributes, without bloating the code with unnecessary if/else conditions, adhering to the #2 above.

**type CitizenEvaluator =** **(Citizen) -> Bool**function calculateAge(citizensArray: \[Citizen\], **filterFunction**: **CitizenEvaluator**) {  
 if (citizensArray.count < 1) {  
 logMessage("Citizen list is empty!")  
 return 0  
 } var eligibleVotersCount = 0 //tracks only the eligible voters  
 for citizen in citizensArray {  
 if (fliterFunction(citizen) == true)  
 sum =+ sum + citizen.age  
 eligibleVotersCount += 1  
 }  
 } average = eligibleVotersCount > 0 ? (sum / eligibleVotersCount) : 0  
 return average  
}**// Usage:  
**ageEligibleFilterFunction = function(citizen) {  
 return citizen.age >= MINIMUM_VOTER_AGE  
}registrationFilterFunction = function(citizen) {  
 return citizen.isRegistered == true  
}function maleVoterFilterFunction = function(citizen) {  
 return ageEligibleFilterFunction(citizen) && registrationFilterFunction(citizen) && citizen.gender == MALE  
}femaleVoterGraduateFilterFunction = function(citizen) {  
 return ageEligibleFilterFunction(citizen) && registrationFilterFunction(citizen) && (citizen.gender == FEMALE && citizen.education > GRADUATE)  
}citizen1 = Citizen(age: 34, isRegistered: true, gender: MALE, education: GRADUATE)  
citizen2 = Citizen(age: 23, isRegistered: true, gender: FEMALE, education: POSTGRADUATE)  
citizen3 = Citizen(age: 9, isRegistered: false, gender: FEMALE, education: STUDY)  
citizen4 = Citizen(age: 28, isRegistered: false, gender: FEMALE, education: GRADUATE)citizens = \[citizen1, citizen2, citizen3, citizen4\]//finds the average age of male voters  
let maleAverage = calculateAge(citizensArray: citizens, filterFunction: **maleFilterFunction**)//finds the average age of female, post-graduate voters  
let femalePGAverage = calculateAge(citizensArray: citizens, filterFunction: **femaleGraduateFilterFunction**)

Notice the **CitizenEvaluator type,** which is a type alias to a function that accepts a Citizen argument, and returns a boolean based on various attributes of the Citizen object. It is added as an argument to the **calculateAge()** function, thus enforcing all its clients to supply their suitable if conditions themselves, thus ridding the **calculateAge()** off any of the **if-else** madness.

Both **ageEligibleFilterFunction** and **registrationFilterFunction are of** CitizenEvaluator type**.** The **maleVoterFilterFunction** and **femaleVoterFilterFunction** are also of the CitizenEvaluator type**,** but they additionally rely on ageEligibleFilterFunction and registrationFilterFunction — not unlike object composition design pattern, where an object can contain other nested objects.

As you can see, a highly customised and powerful chain of capabilities can be built on top of each other, using function block approach shown above.

Using this approach, an exceptional developer can demonstrate several traits:

- **Abstraction in communication:** While asking questions, the exceptional programmer does not discuss about the technical aspects of the intended solution (e.g. things such as _should I use functional programming?_). He/she just asks using terms surrounding the functionality. Talking at the code level would be necessary only if he/she would be discussing about the code problems/quality. This ability is known as working at the right level of abstractions, and it is intensely necessary in real programmers’ lives.
- **Functionality understanding**: The solution not only shows how much can be achieved with minimal lines, but also how much details a simple statistical average can reveal about a collection of data (voter education, voter gender etc.).
- **Simplicity:** Details can be added in a linear fashion by average programmers, but they do not add to the complexity of the function developed by the exceptional programmer. In a way, the exceptional programmer enables infinite number of features to be added to the product, and they do not need to be added by himself/herself. Even average programmers can use this code to build a product with incremental feature set.
- **Conciseness:** The Citizen attribute list can be endless, but the two items (gender and education) are enough to demonstrate he/she can put the problem in the right context, before even trying to solve it.

When interviewers meet such an exceptional candidate, they are much less likely to even consider other candidates, unless they are fearful of their own obliteration by a much better replacement.

## Conclusion:

Achieving the functionality is the #1 requirement in the interviews. This conclusion is heavily inspired by coding interview schools, which trains candidates to better their presentation by separating and sorting things they should address to comfort the interviewers.

While this is an acceptable version of the truth, it is not the complete truth. In hiring for technically advanced roles, interviewers are looking for things beyond their line of questioning. They want someone who can supplement their thoughts, thus guiding the solution process.

That someone can be a living monument of the Leonardo Da Vinci’s timeless quote that says:

> Simplicity is the ultimate sophistication.

Mastering these 3 powerful attributes makes one an exceptional programmer, not just an exceptional candidate. Success in the interviews, then, becomes a by-product rather than the goal of life.
