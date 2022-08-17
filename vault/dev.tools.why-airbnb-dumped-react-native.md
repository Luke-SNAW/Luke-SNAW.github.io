---
id: ph5gklgmlfqwdm75qelwakj
title: Why Airbnb Dumped React Native
desc: ""
updated: 1660691943876
created: 1660691194229
---

> https://www.theimmigrantprogrammers.com/p/why-airbnb-dumped-react-native  
> https://news.ycombinator.com/item?id=32485178  
> https://medium.com/airbnb-engineering/sunsetting-react-native-1868ba28e30a  
> https://instagram-engineering.com/react-native-at-instagram-dd828a9a90c7  
> https://news.ycombinator.com/item?id=32310392

### Why React Native became a Problem?

Now initially, it went well for them, however, as the company started to grow bigger they wanted to use native features of mobile applications, to be specific, they wanted to use the _native maps very precisely and very efficiently_, as for companies like Airbnb, detecting locations precisely is very crucial, for them, literally, everything depends on maps! They wanted things like _geolocation_, _internationalization_, and many other complex features, that are not often needed by other types of applications. This was the reason why React Native didn’t bode well for them anymore.

There are 2 big reasons why companies like Airbnb go for frameworks such as React Native, i) they don’t have a lot of dedicated developers to work on Android and IOS applications, however, they do have many full-stack/web developers, therefore it’s convenient for them to reuse their skill set to provide a native mobile application to their customers without having to add an extra cost on their business. Easy, right? At least, that’s what they think! ii) when companies do know that they won’t need many native functionalities, and even if they need some native functionalities, they won’t be very extensive and just a few bridges would make it work.

### How the Solution became the Problem?

Now, the above-mentioned reasons might seem justifiable in the initial phase of a company, but, as soon as you need more complex native features, it becomes stressful for the developers to maintain mobile apps as these frameworks don’t really provide all the features/conveniences provided by the native programming languages*(it isn’t a full switch).* As we saw before, some features need developers to write native code in C, Objective C, or Java/Kotlin. Now, when most of the firms hit this wall of limitations, they expect their web developers to start coding in native*(completely different)* programming languages which is clearly a big problem as most of them don’t know the first thing about these languages, there is a huge learning curve associated with it. However, even if the developers start doing that mid-way through their projects, the logic behind choosing popular frameworks has collapsed. As, now these frameworks rather have resulted in duplication of code, more work, more efforts, and more time; exactly the contrary to why they were chosen.

Airbnb faced the same challenges. They had to turn to developers from other teams*(who were well-versed with native programming languages)*, whenever they faced obstacles while adding more complex features to their React Native apps. As you can see, how this would lead to a huge wastage of their time. A developer working on a different project in a different team takes some time to adjust themself to what the React Native team was working on. Let’s take an instance, let’s say, Team A approaches a very experienced Android developer from Team B for help on a problem they are facing with a project. Team B’s manager allows this experienced developer to work with Team A for 10 days. Great! What happens next? Now, this Android developer spends the first 3–4 days understanding the problem, which could be anywhere*;* even in the part of the code of the _**web application**_ itself, and not specifically in the Android native code*.* If this happens to be the case, unfortunately, a senior developer ended up wasting a whole week for no good reason; and if not, then the developer who helps the other team doesn’t really get anything out of it, there are no incentives for them. This makes the environment of the company very political because now developers are expected to help other teams **anytime**_**(**problems can occur even a day before the release)._

Then there’s another problem that React team likes to call _land mines_; these are problematic areas, but no-one knows the origin of the problem. It’s hard to figure out if the problem was in their Javascript code, or in the reusable components that were created to work with React Native, or in the Android/IOS native code. As a result, it is really hard to debug these problems in so many different environments.

As if all those problems weren’t big enough, yet, the list doesn’t end here. Another issue with React Native is that it’s a _never-ending investment._ It’s just 2 years old and developing rapidly on an ongoing basis. It still has a lot of internal problems and Facebook is working really hard to make it better every day.

### Should you use React Native?

If you’ve reached this section of the article, and if you’ve thoroughly read everything that was mentioned above, I am sure you might be thinking, “Is React Native that bad?”, and the answer is NO, it’s not bad at all! The reason behind all the problems is that Airbnb had to use some native features that not all companies and not all applications need to use. So if you are thinking, if you could work with an alternative to React Native that might help you solve all these problems, I hate to break it to you, but _there’s no alternative_! It’s an either-or kind of a situation, where you have to choose between writing native code using native mobile-app development programming languages or a framework such as React Native, Flutter, etc.

Now, let’s address the most important question here, “After having learned what happened with Airbnb, should you or should you not choose React Native?” And the answer is, _it depends_ on your application. It depends on what kind of features and functionality your application should offer.
