---
id: 8ul8ufv7zsvlzl3mibuuwlz
title: A Completely Non-Technical Explanation of AI and Deep Learning
desc: ""
updated: 1682466602751
created: 1682466544483
---

> https://www.parand.com/a-completely-non-technical-explanation-of-ai.html

## Overview

This document will explain what neural networks are and how they work, which will help you understand how AI and machine learning work. In the scenario below you'll play the part of the neural network.

## Day One

First day of your new job as a "classifier" your boss walks in and drops a big spreadsheet of numbers on your desk.

"Is this a cat?" she asks.

Confused you ask "What?"

"Is this a cat?"

Even more confused, you respond "I don't know".

"Wrong!" she says, and slaps you across the face.

Before you've had a chance to be shocked she drops another large spreadsheet on your desk. "Is this a cat?"

"I don't understand" you respond.

"Wrong!" she says, and slaps you again.

Another spreadsheet. "Is this a cat?"

Not wanting another slap, you meekly respond "Yes?"

"Correct! Good job!" she says, and gives you a wonderful reward. Almost makes up for the slaps.

Another spreadsheet. Cat?

Slightly more confident and wanting another reward you respond "Yes"

"Wrong!". Another slap.

You are very confused. "I don't understand what's going on. You haven't told me the rules, you haven't told me how to figure out something is a cat, you haven't given me the logic to figure this out. You haven't trained me."

"Correct" says the boss. "This is training. Trust me, you're going to get very good at recognizing cats"

Another spreadsheet. This time you focus on the sheet. It's 256 columns and 256 rows, filled with numbers. Is it a cat? You don't know, so you guess.

Another and another. Right, wrong, wrong, right again, it keeps going. Slaps and rewards.

You're starting to notice some patterns - if the sheet is almost all zeros then it's not a cat. You look at the center of the sheet - that part should have larger numbers.

It's getting slightly better - you're getting more rewards than slaps, guessing correctly more often than not. It's all about the patterns of the numbers.

## Day Two

This is the strangest job you've ever had. The slaps are terrible, but the rewards are so great you don't want to quit. How do you get better at this? It's not really possible for one person. If you had more people they could focus on different aspects of the sheet, look for different patterns, and you could use their findings to make better guesses.

You hire 10 people and bring them to work the next day. When you get a spreadsheet you show it to those 10 people and ask them "Is this a cat?"

They are as confused as you were. You force them to guess. The first guy looks like an idiot, so you decide to go with the opposite of what he says. The third lady looks really thoughtful so you put a lot of weight on what she says. In your mind you assign a weight to each of their guesses to come up with your final answer.

Each time you get a reward or punishment you share it with the 10 people you've hired: you reward or slap them based on how much weight you put on their input and how much they contributed to you getting the answer right or wrong. You learn the patterns: if the first guy says a strong no and the third lady a strong yes then it's very likely a cat. You learn many more patterns like this.

The 10 people are learning to hone their opinions based on the rewards and punishments they get. They can focus on different aspects of the sheet, and their opinions together can tell you a lot about the sheet.

After what feels like an epoch and a lot of spreadsheets, eventually you get better. You're getting more rewards. This is working. Your boss says you're very perceptive, and starts calling you Perceptron.

## Day Ten

What if you get more people involved? You could make it 50 people reporting to you, but that'd be hard to manage. How about we add another layer of people before your 10?

You hire 50 more people, have them give their guesses to the 10 people that report to you. You're now very removed from looking at the spreadsheets - instead you rely on the patterns found by the first layer of the people, who give their opinions to the second layer of the people, who then inform you. Everybody passes the slaps and rewards down the line based on how much each earlier person's guess contributed to their guess.

It takes even longer, but eventually the system starts working. You're much more accurate in identifying when it's a cat.

Interestingly you were never taught the rules or logic, and you didn't teach your people the logic or rules. You just propagated the rewards and punishments back through each layer: the more each person's opinion contributes to the answer, the more rewards or punishment you shared with them, and they in turn with the people in the layer behind them. Each person uses the same method to propogate their rewards and punishment back to the people in the layer below them.

## Neural Networks

This is how neural networks work: they see many examples and get rewarded or punished based on whether their guesses are correct. They use multiple layers of workers and eventually learn patterns. Importantly no one is teaching them what patterns they should be looking for or telling them the logic or the rules - the networks eventually figure out the patterns and logic based on very many rounds of example, reward, and punishment. This is called **machine learning**, because the machine is learning the rules by itself.

Neural networks work well when you have many examples of something (eg. pictures of cats), but it's hard to write the logic and rules to describe how to recognize that thing. Try it - write down some rules for how to recognize a cat (eg. "has 4 legs"), then look at pictures of cats and see where the rules fail (eg. a picture of a cat's head). In these cases you use machine learning so the machine learns the rules by itself.

Also note that computers see things as multi-dimensional tables of data. They don't look at a "picture" - they see 3 spreadsheets of numbers representing the RGB values of the picture.

## Day Forty

Identifying cats is a lucrative business and you're pretty good at it. But not good enough. How can we get even better? More people, more layers!

Unfortunately it takes a long time for people to do their calculations, so you've been stuck with just a few layers of people for a while. Having a lot more people would make the process take too long.

One day you run into a group of people who call themselves Gaming People United (GPU). These people play a game that has taught them to be very good at looking at spreadsheets and calculating numbers - in fact they can do a lot of calculations in parallel, very quickly.

Excited, you hire a bunch of them and put them to work recognizing cats. Now instead of two layers of people you can have 10! Each layer can focus on higher and higher concepts - the first layer can look for small details (eg. do I see a pattern that looks like a small circle? Do I see a pattern that looks like a sharp edge?), the second layer can look for patterns from the results of the first layer (eg. are there two circles close to each other), the third layer can build on that (eg. are there two circle close to each other, and a triangle below them), and so forth. By the time the results of the layers get to you you have some fairly sophisticated concepts - we see a pattern that looks like a face, we also see patterns that could be legs, and a sharp thing that might be a beak. Now your guess is more informed than ever.

You train the layers sending slaps and rewards down through each layer, and after many epochs you get really good at recognizing cats.

## Deep Learning

One of the major break-throughs in machine learning was the advent of _Deep Learning_, which is basically what we describe above - GPUs (Graphics Processing Units) got popular because they enable fast 3D graphics for games. They also happen to be very good at quickly doing the types of calculations neural networks need. Machine learning people started using GPUs for training neural networks, and with this extra speed they could have many more layers - from 3 or 4 layers to 10 or 11, and then hundreds.

This addition of layers led to significant advances in neural network performance - very quickly neural networks became the best solution for voice recognition, for image recognition, image creation, and sophisticated language models. This is called **Deep Learning** because there are so many layers, not because it's profound.
