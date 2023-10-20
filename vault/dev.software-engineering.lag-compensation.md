---
id: o2xgz8c6d9xn3at1rjymbnw
title: "Fast-Paced Multiplayer (Part IV): Lag Compensation"
desc: ""
updated: 1697781940369
created: 1697781915128
---

> https://www.gabrielgambetta.com/lag-compensation.html

## [Introduction](https://www.gabrielgambetta.com/lag-compensation.html#introduction)

The previous three articles explained a client-server game architecture which can be summarized as follows:

- Server gets inputs from all the clients, with timestamps
- Server processes inputs and updates world status
- Server sends regular world snapshots to all clients
- Client sends input and simulates their effects locally
- Client get world updates and
  - Syncs predicted state to authoritative state
  - Interpolates known past states for other entities

From a player’s point of view, this has two important consequences:

- Player sees **himself** in the **present**
- Player sees **other entities** in the **past**

This situation is generally fine, but it’s quite problematic for very time- and space-sensitive events; for example, shooting your enemy in the head!

## [Lag Compensation](https://www.gabrielgambetta.com/lag-compensation.html#lag-compensation)

So you’re aiming perfectly at the target’s head with your sniper rifle. You shoot - it’s a shot you can’t miss.

But you miss.

Why does this happen?

Because of the client-server architecture explained before, you were aiming at where the enemy’s head was 100ms _before_ you shot - _not_ when you shot!

In a way, it’s like playing in an universe where the speed of light is really, really slow; you’re aiming at the past position of your enemy, but they’re long gone by the time you squeeze the trigger.

Fortunately, there’s a relatively simple solution for this, which is also pleasant for _most_ players _most_ of the time (with the one exception discussed below).

Here’s how it works:

- When you shoot, client sends this event to the server with full information: the exact timestamp of your shot, and the exact aim of the weapon.
- **Here’s the crucial step**. Since the server gets all the input with timestamps, it can authoritatively reconstruct the world at any instant in the past. In particular, it can reconstruct the world exactly as it looked like to any client at any point in time.
- This means the server can know exactly what was on your weapon’s sights the instant you shot. It was the _past_ position of your enemy’s head, but the server knows it was the position of their head in _your_ present.
- The server processes the shot _at that point in time_, and updates the clients.

And everyone is happy!

The server is happy because it’s the server. It’s always happy.

You’re happy because you were aiming at your enemy’s head, shot, and got a rewarding headshot!

The enemy may be the only one not entirely happy. If they were standing still when he got shot, it’s their fault, right? If they were moving… wow, you’re a really awesome sniper.

But what if they were in an open position, got behind a wall, and _then_ got shot, a fraction of a second later, when they thought they were safe?

Well, that can happen. That’s the tradeoff you make. Because you shoot at him in the past, they may still be shot up to a few milliseconds after they took cover.

It is somewhat unfair, but it’s the most agreeable solution for everyone involved. It would be much worse to miss an unmissable shot!

## [Conclusion](https://www.gabrielgambetta.com/lag-compensation.html#conclusion)

This ends my series on Fast-paced Multiplayer. This kind of thing is clearly tricky to get right, but with a clear conceptual understanding about what’s going on, it’s not exceedingly difficult.

Although the audience of these articles were game developers, it found another group of interested readers: gamers! From a gamer point of view it’s also interesting to understand why some things happen the way they happen.

### [Further Reading](https://www.gabrielgambetta.com/lag-compensation.html#further-reading)

As clever as these techniques are, I can’t claim any credit for them; these articles are just an easy to understand guide to some concepts I’ve learned from other sources, including articles and source code, and some experimentation.

The most relevant articles about this topic are [What Every Programmer Needs to Know About Game Networking](http://gafferongames.com/networking-for-game-programmers/what-every-programmer-needs-to-know-about-game-networking/) and [Latency Compensating Methods in Client/Server In-game Protocol Design and Optimization](https://developer.valvesoftware.com/wiki/Latency_Compensating_Methods_in_Client/Server_In-game_Protocol_Design_and_Optimization).

[<< Part III: Entity Interpolation](https://www.gabrielgambetta.com/entity-interpolation.html) · [**Live Demo >>**](https://www.gabrielgambetta.com/client-side-prediction-live-demo.html)
