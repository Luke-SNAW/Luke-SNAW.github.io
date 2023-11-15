---
id: ntv9jsdm9vei4te6wd9dvls
title: Reasons to prefer blake3 over sha256
desc: ""
updated: 1699933517066
created: 1699933385937
---

> https://peergos.org/posts/blake3
>
> https://github.com/BLAKE3-team/BLAKE3

SHA256 was designed by the NSA. BLAKE (the original) and BLAKE3 were designed by Jean-Philippe Aumasson and others (including me, but Jean-Philippe and the other contributors did a lot more of the cryptographic heavy lifting than I did).

SHA256 was based on SHA1 (which is weak). BLAKE was based on ChaCha20, which was based on Salsa20 (which are both strong).

NIST/NSA have repeatedly signaled lack of confidence in SHA256: first by hastily organising the SHA3 contest in the aftermath of Wang's break of SHA1, then by making "Don't be like SHA256" a goal for the algorithms of that contest, and then by banning SHA256 from new designs to be used by the USA government (except for in one specific cryptosystem that protects from weaknesses in the hash function [https://media.defense.gov/2022/Sep/07/2003071836/-1/-1/0/CSI_CNSA_2.0_FAQ\_.PDF](https://media.defense.gov/2022/Sep/07/2003071836/-1/-1/0/CSI_CNSA_2.0_FAQ_.PDF)).

BLAKE (the original) was very well-studied during the SHA3 competition. In NIST's final report on the SHA3 process, they stated that the depth of scientific analysis applied to BLAKE exceeded even that applied to Keccak (the final SHA3 winner).

[blake3 analysis](https://peergos.org//theme/img/blog/blake3-analysis.jpeg)

Known, feasible attacks can break 31 out of 64 rounds of SHA256 (48% of the rounds). Known, feasible attacks can break only 2 out of 7 rounds of BLAKE3 (29% of the rounds).

BLAKE3 comes “out of the box” with security features that can protect users in common use cases, such as protection against length-extension attack, a standard method of keying, "personalization tags" to guarantee domain separation, etc.

BLAKE3 is _much_ more efficient (in time and energy) than SHA256, like 14 _times_ as efficient in typical use cases on typical platforms.

[blake3 performance](https://peergos.org/theme/img/blog/blake3-performance.jpeg)

BLAKE3 also offers performance that is competitive against SHA256 in a lot of different use cases and platforms, including some that might surprise you, such as sometimes being more efficient than SHA256 _even_ when your CPU comes with SHA256 acceleration circuits built into it!

BLAKE3 is highly parallelizable. This provides two performance advantages, only the first of which most people think about.

- The first is big data + big multicore: if the size of your data inputs scale up 100X but the number of CPU cores in your platform also scale up 100X, BLAKE3 takes only a little longer, but SHA256 takes approximately 100X times as long.
- The other advantage, less widely understood, is that inside a single compute device, new tech improvements provide more and more parallel power. This is true in FPGAs and GPUs, and it is true in CPUs because of vectorization upgrades.

AVX in Intel/AMD, Neon and Scalable Vector Extensions in Arm, and RISC-V Vector computing in RISC-V. BLAKE3 can take advantage of all of it.

When you upgrade to a newer CPU/platform/device, BLAKE3 typically _further extends_ its performance advantage over SHA256 compared to the performance advantage it already had on the previous platform!

Finally, BLAKE3 was designed and implemented by both cryptographers _and_ software engineers. The reference implementations are super efficient and well-engineered for security, thanks to Jack O'Connor, Samuel Neves, and Jean-Philippe Aumasson: [https://github.com/BLAKE3-team/BLAKE3](https://github.com/BLAKE3-team/BLAKE3)
