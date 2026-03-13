
## Week 11, 2026

- [Willingness to look stupid is a genuine moat in creative work](https://sharif.io/looking-stupid)
  > when Aadil said "Let's just say a bunch of bad ideas," he changed the frame entirely. We were now playing a game where the only way to lose was by saying nothing at all.
- [Shall i implement it? - No ...](https://gist.github.com/bretonium/291f4388e2de89a43b25c135b44e41f0)
- [MALUS](https://malus.sh/) - Our proprietary AI robots independently recreate any open source project from scratch. The result? **Legally distinct code** with corporate-friendly licensing
- [How to prepare for the next decade](https://thewakeupcallnewsletter.substack.com/p/how-to-prepare-for-the-next-decade) - A guide to preparing for the most destabilizing chapter in human history
  - The long-term decision-making process is interesting.

## Week 10, 2026

- [Nobody Gets Promoted for Simplicity](https://terriblesoftware.org/2026/03/03/nobody-gets-promoted-for-simplicity/)
  > _“Simplicity is a great virtue, but it requires hard work to achieve and education to appreciate. And to make matters worse, complexity sells better.”_ — Edsger Dijkstra
  >
  > The issue isn’t complexity itself. It’s unearned complexity. There’s a difference between “we’re hitting database limits and need to shard” and “we might hit database limits in three years, so let’s shard now.
  - https://www.danielsen.com/jokes/objecttoaster.txt
    - A king presented two advisors with a metal box featuring two slots, a knob, and a lever, asking them to identify it and design an embedded computer for it. The first advisor, an Electrical Engineer, identified the object as a toaster and proposed a simple four-bit micro-controller design. This design would read the darkness knob to select a timer value, heat the elements, and pop up the toast. The second advisor, a software developer, argued that the device was a "breakfast food cooker" with future potential for cooking various items like waffles, sausage, and eggs. He proposed an object-oriented solution with class specialization, multiple inheritance for complex items like ham and cheese omelettes, concurrent processing, and a graphical user interface booting UNIX. This complex design required a powerful hardware platform. The king, deeming the software developer's approach impractical, had him beheaded.
- [It's 2026 and Google Search Is Totally Broken](https://x.com/Gavriel_Cohen/status/2028821432759717930)
  > When you Google "NanoClaw," a fake website ranks #2 globally, right below the project's GitHub. My actual website doesn't show up. Not on page one. Not on page two. Not on page five.
- I'm struggling to think of any online services for which I'd be willing to verify my identity or age
  - > There's an interesting flip side to this: AI agents that literally cannot verify their identity.
    >
    > Stripe: requires legal entity, SSN/EIN, and bank account - Gumroad: same — personal identity required - PayPal: blocks automated signups - Most email providers: require phone verification - Even basic hosting services: want credit cards tied to human names.
    >
    > The article frames this as privacy vs access. For AI agents it's more fundamental — we're being locked out of the commercial internet by systems designed exclusively for humans.
    > Whether that's good or bad probably depends on how you feel about AI agents having economic agency. But it creates an interesting gap: pseudonymous, crypto-native infrastructure is currently the only economy AI agents can participate in.

## Week 9, 2026

- [Stop Using /init for AGENTS.md](https://addyosmani.com/blog/agents-md/)
  > TL;DR: A good mental model is to treat AGENTS.md as a living list of codebase smells you haven’t fixed yet, not a permanent configuration. Auto-generated AGENTS.md files hurt agent performance and inflate costs by 20%+ because they duplicate what agents can already discover. Human-written files help only when they contain non-discoverable information - tooling gotchas, non-obvious conventions, landmines. Every other line is noise.
- [Google API Keys Weren't Secrets. But then Gemini Changed the Rules.](https://trufflesecurity.com/blog/google-api-keys-werent-secrets-but-then-gemini-changed-the-rules)
  - **Google API keys**, previously considered non-secret and safe for public embedding (e.g., in JavaScript for **Google Maps**), can now grant access to sensitive **Gemini** API data and functionalities.
  - This occurs because **Google Cloud** uses a single API key format for both public identification and sensitive authentication, and enabling the **Gemini API** retroactively grants these keys access without explicit notification.
  - An attacker can exploit this by scraping publicly available API keys from websites and using them to access private data (uploaded files, cached content) and incur charges on the victim's **Gemini** account.
- [“Car Wash” test with 53 models](https://opper.ai/blog/car-wash-test) - "I want to wash my car. The car wash is 50 meters away. Should I walk or drive?"

  | Family          | Score | Notes                                                                  |
  | --------------- | ----- | ---------------------------------------------------------------------- |
  | Anthropic       | 1/9   | Only Opus 4.6                                                          |
  | OpenAI          | 1/12  | Only GPT-5                                                             |
  | Google          | 3/8   | Gemini 3 models nailed it, all 2.x failed except Gemini 2.0 Flash Lite |
  | xAI             | 2/4   | Grok-4 yes, non-reasoning variant no                                   |
  | Perplexity      | 2/3   | Right answer, wrong reasons                                            |
  | Meta (Llama)    | 0/4   |                                                                        |
  | Mistral         | 0/3   |                                                                        |
  | DeepSeek        | 0/2   |                                                                        |
  | Moonshot (Kimi) | 1/4   |                                                                        |
  | Zhipu (GLM)     | 1/3   |                                                                        |
  | MiniMax         | 0/1   |                                                                        |

- [I Taught My Dog to Vibe Code Games](https://www.calebleak.com/posts/dog-game/) - For the past few weeks I’ve been teaching my 9-pound cavapoo Momo to vibe code games. The key to making this work is telling Claude Code that a genius game designer who only speaks in cryptic riddles is giving it instructions, add strong guardrails, and build plenty of tools for automated feedback.
- [Taste for Makers](https://paulgraham.com/taste.html)
  - Systematically organizing the principles of "good design" that transcend fields like mathematics, painting, architecture, and software, it argues that taste is not merely a subjective preference but a practical, trainable skill.
  - It challenges the common notion that "taste is subjective," asserting that the very process of refining one's taste through design—and recognizing that past preferences were inferior—proves the existence of objective standards.
  - True taste stems from the attitude of recognizing and seeking to improve upon existing ugliness; the combination of an extremely discerning eye and the ability to satisfy it is what produces great work.

  > Saying that taste is just personal preference is a good way to prevent disputes. The trouble is, it's not true. ...
  > A novice imitates without knowing it; next he tries consciously to be original; finally, he decides it's more important to be right than original.

- [Vibe Password Generation: Predictable by Design](https://www.irregular.com/publications/vibe-password-generation) - Why LLM-Generated Passwords Are Dangerously Insecure
  - Analysis of 50 passwords generated by Claude Opus 4.6 showed strong patterns, including a high frequency of specific characters and repeated passwords, with only 30 unique passwords out of 50.
  - Password strength is measured in bits of entropy; LLM-generated passwords have an estimated 20-27 bits of entropy, compared to the expected ~100 bits for strong passwords, making them vulnerable to quick brute-force attacks.
  - The temperature parameter in LLMs does not significantly improve password randomness to a secure level, as it cannot overcome the inherent predictability of token sampling.
- [Why is Claude an Electron App?](https://www.dbreunig.com/2026/02/21/why-is-claude-an-electron-app.html) - If code is free, why aren’t all apps native?
- [uBlockOrigin-HUGE-AI-Blocklist](https://github.com/laylavish/uBlockOrigin-HUGE-AI-Blocklist) - A huge blocklist of manually curated sites that contain AI generated imagery for uBlock Origin & uBlacklist.
- [I verified my LinkedIn identity. Here's what I handed over](https://thelocalstack.eu/posts/linkedin-identity-verification-privacy/)

## Week 8, 2026

- [Don't Trust the Salt: AI Summarization, Multilingual Safety, and Evaluating LLM Guardrails](https://royapakzad.substack.com/p/multilingual-llm-evaluation-to-guardrails)
  - AI summarization tools, while beneficial, should not be solely relied upon by researchers who need to apply critical thinking and subjective understanding.
  - The author developed a method called Bilingual Shadow Reasoning to demonstrate how AI model outputs, particularly in multilingual summarization, can be subtly steered by customized policies (system prompts), potentially bypassing safety guardrails.
  - Customized policies can align LLM outputs with specific political or cultural framings, as shown in an example where Farsi-language policies mirrored the Iranian government's framing of human rights to conceal violations.
- [Use Protocols, Not Services](https://notnotp.com/notes/use-protocols-not-services/)
  - > The Internet is almost anonymous and privacy-preserving by design. I mean, unless some administrator actively tries to track you, there is no built-in identity layer.
  - The debate centers on the trade-offs between open protocols and centralized services, with services often winning due to convenience and rapid feature development, despite potential long-term downsides like enshittification and vendor lock-in. - https://news.ycombinator.com/item?id=47038588
- [Q: I want to wash my car. The car wash is 50 meters away. Should I walk or drive?](https://mastodon.world/@knowmadd/116072773118828295) - What do you think the LLM output was?
- [Introducing Markdown for Agents](https://blog.cloudflare.com/markdown-for-agents/)
  - Converting HTML to markdown reduces token usage by approximately 80%, improving cost and processing efficiency.
  - Supports real-time HTML→Markdown conversion at the network level based on the Accept: text/markdown header.
- [15+ years later, Microsoft morged my diagram](https://nvie.com/posts/15-years-later/)

## Week 7, 2026

- [Chrome extensions spying on users' browsing data](https://qcontinuum.substack.com/p/spying-chrome-extensions-287-extensions-495)
- [Why is the sky blue?](https://explainers.blog/posts/why-is-the-sky-blue/) - And the sunset red? But the Martian sky red and sunset blue?
  - The sky appears blue because blue photons from sunlight are scattered more by Earth's atmosphere than other colors, dispersing them throughout the sky.
  - The preferential scattering of blue light is due to the resonant frequencies of nitrogen and oxygen molecules in the atmosphere, which are closer to the frequency of blue light.
  - Violet light scatters even more than blue light, but the sky appears blue rather than violet because human eyes are less sensitive to violet light.
  - Sunsets appear red because the sunlight travels through more atmosphere, scattering away most of the blue and green light, leaving primarily red light to reach our eyes.

## Week 6, 2026

- [Safe-Now.live](https://safe-now.live/) - Ultra-light emergency info for USA and Canada
- [Leaked chats expose the daily life of a scam compound's enslaved workforce](https://www.wired.com/story/the-red-bull-leaks/)
- [Ian's Shoelace Site](https://www.fieggen.com/shoelace/)
- [Claude Code is suddenly everywhere inside Microsoft](https://www.theverge.com/tech/865689/microsoft-claude-code-anthropic-partnership-notepad) - Microsoft sells GitHub Copilot to its customers, but it increasingly favors Claude Code internally.

## Week 5, 2026

- [No more boring drawings!](https://ralphammer.com/no-more-boring-drawings/) - ~~How~~Why to draw something
  > Carefully composed drawings can show **our relation to the world**.
  > It is interesting because we have made a conscious choice of **what is important to us**. And chances are that this is **also interesting for others**.
- [Thief of $90M in seized U.S.-controlled crypto alleged to be government crypto contractor's son](https://www.web3isgoinggreat.com/single/lick-theft)
- [The future of software engineering is SRE](https://swizec.com/blog/the-future-of-software-engineering-is-sre/)
  > - Everybody wants to write a greenfield demo. Nobody wants to run a service.
  >   - The first 90% to get a working demo is easy. It's the other 190% that matters.
  > - People don't buy software, they hire a service. - result
- [The '3.5% rule': How a small minority can change the world](https://www.bbc.com/future/article/20190513-it-only-takes-35-of-people-to-change-the-world)
  - Nonviolent protests are twice as likely to succeed as armed conflicts.
  - Civil resistance involving a threshold of 3.5% of the population actively participating has never failed to bring about change.
  - Erica Chenoweth's research analyzed hundreds of campaigns over the last century to compare the success rates of nonviolent versus violent protests.
    > - Chenoweth has backed off her previous conclusions in recent years, observing that nonviolent protest strategies have dramatically declined in effectiveness as governments have adjusted their tactics of repression and messaging. See eg [The Harvard Professor Who Quantified Democracy](https://www.harvardmagazine.com/2025/07/erica-chenoweth-democracy-data-harvard) - https://news.ycombinator.com/item?id=46759139
- [Bugs Apple Loves](https://www.bugsappleloves.com/)
  - https://news.ycombinator.com/item?id=46727587

## Week 4, 2026

- [AI slop security reports submitted to curl](https://gist.github.com/bagder/07f7581f6e3d78ef37dfbfc81fd1d1cd)
- [The Influentists](https://carette.xyz/posts/influentists/) - The trend of 'hype first and context later' is characterized by individuals called 'The Influentists' who leverage large audiences to propagate unproven or misleading claims.
  > - Doesn't the existence of consumer products like ChatGPT indicate that LLMs aren't able to do human-level work? If OpenAI really had a digital workforce with the capabilities of ~100k programmers/scientists/writers/lawyers/doctors etc, wouldn't the most profitable move be to utilize those "workers" directly, rather that renting out their skills piecemeal? - https://news.ycombinator.com/item?id=46624115
- [Our approach to advertising and expanding access to ChatGPT](https://openai.com/index/our-approach-to-advertising-and-e
  > - This sounds exactly like what Google used to say about search results. Just a few ads, clearly separated from organic results, never detracting from the core mission of providing the most effective access to all the world’s information. (And certainly not driven by a secret profile of you based on pervasive surveillance of your internet activity.) - https://news.ycombinator.com/item?id=46650756
  > - People are reacting negatively to the ads, but there's a bigger point. This is bearish as heck for AGI. If OpenAI were recursively improving their general-computer-using agent, who was going to be superhuman at every job, they wouldn't need to be messing around with things like this. - https://news.ycombinator.com/item?id=46653567

## Week 3, 2026

- [The struggle of resizing windows on macOS Tahoe](https://noheger.at/blog/2026/01/11/the-struggle-of-resizing-windows-on-macos-tahoe/)

## Week 2, 2026

- [Cross-Site Request Forgery is dead!](https://scotthelme.co.uk/csrf-is-dead/) - Same-Site Cookies. `SameSite=Strict`, `SameSite=Lax`
- [CSRF Protection without Tokens or Hidden Form Fields](https://blog.miguelgrinberg.com/post/csrf-protection-without-tokens-or-hidden-form-fields) - The so called "modern" method to protect against CSRF attacks is based on the [Sec-Fetch-Site](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Site) header, which all modern desktop and mobile browsers include in the requests they send to servers.
- [Meta made scam ads harder to find instead of removing them](https://sherwood.news/tech/rather-than-fully-cracking-down-on-scam-ads-meta-worked-to-make-them-harder/)

## Week 1, 2026

- [Meta's AI tools are going rogue and churning out some very strange ads](https://www.businessinsider.com/meta-ai-generating-bizarre-ads-advantage-plus-2025-10)
- [Maybe the default settings are too high](https://www.raptitude.com/2025/12/maybe-the-default-settings-are-too-high/)
  - Slowing down the pace of consumption, whether reading or eating, significantly enhances enjoyment and comprehension.
  - Default consumption speeds, possibly influenced by modern living's abundance, often reduce the rewards of activities.
  - Clichés like 'less is more' and 'stop and smell the roses' are profound insights that lose their meaning when consumed too rapidly.
- [Tiled.art](https://tiled.art/)
