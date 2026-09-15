
https://news.ycombinator.com/item?id=31272681

With JavaScript, these kinds of optimizations in an engine make sense due to the web being limited by it and thus speed is a huge factor. With Python, however, if a Python web framework is “too” slow, I would honestly say the problem is using Python at all for a web server. Python shines beautifully as a (somewhat) cross platform scripting language: file reading and writing, environment variables, simple implementations of basic utilities: sort, length, max, etc that would be cumbersome in C. The move of Python out of this and into practically everything is the issue and then we get led into rabbit holes such as this where since we are using Python, a dynamic scripting language, for things a second year computer science student should know are not “the right jobs for the tool.”
Instead of performance, I’d like to see more effort in portability, package management, and stability for Python because, essentially since it is often enterprise managed, juggling fifteen versions of Python where 3.8.x supports native collection typing annotations but we use 3.7.x, etc. is my biggest complaint. Also up there is pip and just the general mess of dependencies and lack of a lock file. Performance doesn’t even make the list.

This is not to discredit anyone’s work. There is a lot of excellent technical work and research done as discussed in the article. I just think honestly a lot of this effort is wasted on things low on the priority tree of Python.

---

I want a common language I can work with. Right now, Python is the only tool which fits the bill.
A critical thing is Python does numerics very, very well. With machine learning data science, and analytics being what they are, there aren't many alternatives. R, Matlab, and Stata won't do web servers. That's not to mention wonderful integrations with OpenCV, torch, etc.

Python is also competent at dev-ops, with tools like ansible, fabric, and similar.

It does lots of niches well. For example, it talks to hardware. If you've got a quadcopter or some embedded thing, Python is often a go-to.

All of these things need to integrate. A system with Ruby+R+Java will be much worse than one which just uses Python. From there, it's network effects. Python isn't the ideal server language, but it beats a language which _just_ does servers.

As a footnote, Python does package management much better than alternatives.

pip+virtualenv >> npm + (some subset of require.js / rollup.js / ES2015 modules / AMD / CommonJS / etc.)

JavaScript has finally gone from a horrible, no-good, bad language to a somewhat competent one with ES2015, but it has at least another 5-10 years before it can start to compete with Python for numerics or hardware. It's a sane choice if you're front-end heavy, or mobile-heavy. If you're back-end heavy (e.g. an ML system) or hardware-heavy (e.g. something which talks to a dozen cameras), Python often is the only sane choice.
