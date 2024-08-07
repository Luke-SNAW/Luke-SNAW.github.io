
> https://thenewstack.io/the-origin-story-of-sqlite-the-worlds-most-widely-used-database-software/

Two decades ago, while building software for a Navy destroyer, he led the creation of a new open source database to overcome the glitches he encountered. Then Google came calling.

Jul 11th, 2021 6:00am by [David Cassel](https://thenewstack.io/author/destiny/)

---

Last week [Adam Gordon Bell](https://www.linkedin.com/in/adamgordonbell/?originalSubdomain=ca) [brought a special guest onto his podcast Corecursive](https://corecursive.com/066-sqlite-with-richard-hipp/): [Richard Hipp](https://twitter.com/drichardhipp?lang=en), the main author of SQLite.

In a little more than two decades, it’s become the most widely deployed database in the world, according to the [official webpage at SQLite.org](https://sqlite.org/about.html) — partly due to its simplicity. Because it’s contained in a library of C code, SQLite can be easily embedded into other software, and it’s fully self-contained. “Unlike most other SQL databases, SQLite does not have a separate server process,” its official page explains. “SQLite reads and writes directly to ordinary disk files.”

But crucially, it’s also open source, which leads Bell’s podcast to an intriguing question: What happens if your fun side project ends up powering the world? And the host promises that, along the way, the interview will explore the dilemma which still haunts the open source movement today: How to survive becoming core infrastructure for the world.

Bell points out that SQLite is now installed in everything from web browsers to commercial airplanes, as well as popular software like iMessage and WhatsApp.

But the software was born out of Hipp’s frustration with a database that was installed on a battleship.

## ‘Can’t Connect to Server’

The story begins in a shipyard in Bath, Maine (population: 8,329). Back in the year 2000, Hipp was working for [Bath Iron Works](https://www.gd.com/our-businesses/marine-systems/bath-iron-works), a shipbuilding subsidiary of defense contractor [General Dynamics](https://www.gd.com/), and was building software for a Navy destroyer (the USS Oscar Austin). The software would operate on crucial data about the ship’s valves (for routing around pipe ruptures), and their stack had included [Informix](https://www.ibm.com/products/informix), which unfortunately stopped working whenever the server went down.

“That was embarrassing,” Hipp recalled to Bell. “A dialog box would pop up, they’d double click on the thing, and a dialog box would pop up that says, ‘Can’t connect to database server.’ It wasn’t our fault — we didn’t have any control over the database server. But what do you do if you can’t connect to the server? So we got the blame all the same, because we were painting the dialog box.”

And, as Hipp noted, “it’s a warship.” So besides the ship being continually in use, “the idea is it’s supposed to be able to work if you take battle damage! So it’s more than one pipe breaking. There’s going to be a lot of stuff broken, and people are going to be crazy, and there’s going to be smoke and blood and chaos — and in a situation like that they don’t want a dialog box that says, ‘Cannot connect to database server.'”

Hipp wondered if there was a way his team could pull its data straight from the database without an external dependency. “I looked around and there were no SQL database engines that would do that, and one of the guys I was working with says, ‘Richard, why don’t you just write one?'” During a temporary shutdown of government contracts (which had lasted a few months), “I was out of work for a few months, and I thought, ‘Well, I’ll just write that database engine now.'”

Back in 2006, Hipp tried to explain SQLite’s appeal [to an audience at Google](https://youtu.be/giAMt8Tj-84). “Most people hear SQL database engine, and they’re thinking [Oracle](https://www.oracle.com/index.html) — something big that you run your whole enterprise on. SQLite is sort of the opposite of that — it tries to be very small, so it’s very compact.” In fact, fully configured, at the time it was less than 250 kilobytes. And it was also serverless — and designed to be embedded within larger applications.

But the story of SQLite also shows how initiative and dedication can pay off — and how nothing can stop a determined developer. Later in his interview at Corecursive.com, Hipp recalled looking for a reference on how to write an SQL database engine — and not finding one.

“So I just had to kind of invent it myself,” he said. “It was a completely independent invention.”

For instance, Hipp remembers referring to [Donald Knuth](https://www-cs-faculty.stanford.edu/~knuth/)’s [The Art of Computer Programming](https://www-cs-faculty.stanford.edu/~knuth/taocp.html) for an implementation of a search algorithm. While theoretical underpinnings might’ve been taught at [MIT](https://web.mit.edu/), [Harvard](https://www.harvard.edu/), or the [University of California-Berkeley](https://www.berkeley.edu/), “if you didn’t go to one of those three schools, you didn’t even know this body of theory existed, and there wasn’t a real good way to find it.”

Years later he learned that nonetheless, both SQLite and Postgres had converged on the same ideas.

Ironically, back at the shipyard, Hipp’s higher-ups still insisted on using  Informix, Hipp tells Bell (although his team did use SQLite for their testing). But in addition, “I put it out there on the internet and other people started picking it up.” Soon Hipp was surprised by the uptake — including one user who’d bragged they now had an SQL database engine running on their Palm Pilot. “It really attracted a lot of attention, and that encouraged me to work on it.”

## Ringing Phones

Hipp’s [website](http://www.hwaci.com/drh/) still proudly points out that SQLite won a 2005 Google O’Reilly Open Source Award. But that was the only acclaim that SQLite received. Back in 2006, Hipp told his audience at Google that “it’s public domain, so lots of people are using it that I don’t know about” — but confirmed users included [Apple](https://www.apple.com/) and [PHP](https://www.php.net/). (At one point both [General Electric](https://www.ge.com/) and [Toshiba](https://www.toshiba.com/tai/) had contacted him requesting the U.S. export control number for SQLite — though he never found out why.)

But soon Hipp confronted another theme that haunts most open source developers: monetization. Hipp told the Corecurisve podcast that very early on, he’d received a phone call from [Motorola](https://www.motorola.com/us/), who’d wanted to include SQLite in its operating system for cellphones. “Of course, inside, I was like, ‘What? You can make money with open source software? How does this work? How do I price this?” Hipp said. “I have no idea how to do this.'”

But fortuitously, he’d brought in three people who’d worked on the original SQLite, “and that was sort of the beginning.”

The next call he fielded was from [America Online](https://www.aol.com/), which wanted to use an SQLite database on the free-trial CDs it was sending in the mail to prospective users. And soon there was a call from Symbian (which made the operating system on [Nokia](https://www.nokia.com/) phones). The company had tested 10 different database systems — two open source, and seven more proprietary. But even after giving the other vendors a chance to fine-tune their systems, SQLite still won the competition. Hipp recalled, “We cut a contract to do some development work for them.”

This led to an important development, when Symbian asked them to increase their “[bus factor](https://en.wikipedia.org/wiki/Bus_factor),” which Hipp describes as “the number of people who have to be hit by a bus in order to stop all development work… They felt like the bus factor at SQLite was too low.” Symbian’s solution? It helped fund the [SQLite Consortium](https://www.sqlite.org/consortium.html), which Hipp said is “a way of funding the project and getting more people involved to guarantee that it was going to be available long term.”

But he also gives a lot of credit to [Mitchell Baker](https://twitter.com/mitchellbaker?lang=en) (pictured), who was then the CEO of the Mozilla Foundation (and a lawyer by training). She’d reached out, and as he remembers it, insisted that “the developers have to be in control. Their decision is final… The companies that are using, they get the honor of contributing money, but you make all the decisions. She was very adamant about this and she laid out everything.”

In the end, Mozilla and [Adobe](https://www.adobe.com/) joined Symbian in funding the group, and to this day Hipp expresses gratitude for all the early support. “it’s been such an amazing journey… we would not be in this situation were it not for these circumstances.

## When Google Calls

Soon all major smartphones were using SQLite, Adam explains — and soon Richard fielded a phone call from [Google](https://about.google/), “before Android was a thing. This was before iPhone.”

This led the project to another key open source lesson about the value of testing. “It’s amazing how many bugs will crop up when your software suddenly gets shipped on millions of devices,” Hipp told Bell.

He spent a whole year generating tests to cover every single branch operation in the resulting binary code, he said. He’d had hopes of selling the test suite to avionics manufacturers — but while they never landed any customers, when it came to reports of bugs in Android, “it made a huge, huge difference. We just didn’t really have any bugs for the next eight or nine years.”

As a result, he said, “It did work out really well for us in that it keeps our product really solid and it enables us to turn around new features and new bug fixes very fast.”

The details are pretty impressive. “We’ll have a test case but it’ll be parameterized, so that one test case might run 100, 1,000, 100,000 tests, just by looping, by changing one of the parameters.” For a typical release, Hipp estimated that there’s on the order of 100,000 distinct test cases — and billions of tests. “We have a checklist and we will run tests for at least three days prior to a release.”

Corecursive’s interview closed with Hipp’s own inspiring advice to others who want to create impactful open source software. “I had this crazy idea that I’m going to build a database engine that does not have a server, that talks directly to disk, and ignores the data types,” he said. “And if you asked any of the experts of the day, they would’ve said, ‘That’s impossible. That will never work. That’s a stupid idea.’

Fortunately, I didn’t know any experts — and so I did it anyway.”
