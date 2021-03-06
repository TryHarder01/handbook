# Programming

A programmer should know [lots](http://programmer.97things.oreilly.com/wiki/index.php/Contributions_Appearing_in_the_Book) [of](http://www.artima.com/weblogs/viewpost.jsp?thread=331531) [concepts](http://programmer.97things.oreilly.com/wiki/index.php/Other_Edited_Contributions). Try to keep in mind the following principles:

* **Small is beautiful**.
  Small things have tremendous advantages over their larger counterparts.
  Among these is the ability to combine with other small things in unique and useful ways.

* **Design for simplicity**.
  Do the [simplest thing](https://landing.google.com/sre/book/chapters/simplicity.html) that could possibly work.
  Benefits of simplicity: ease of understanding, ease of change, ease of debugging, flexibility.
  We can't change our brain to grasp something complex. We need to simplify complexity so we can handle it.

* **Do one thing and do it well**.
  By focusing on a single task, a program or function can eliminate much extraneous code that often results in excess overhead, unnecessary complexity, and a lack of flexibility.

* **Make it work, make it right, make it fast**.
  Build a prototype as soon as possible to get a sense of the entire process.
  Once you have a working prototype, apply guidelines and previous learnings. Then, focus on performance.
  Apply small improvements at each iteration.

* **Choose portability over efficiency**.
  If today's hardware just about runs a program with just about adequate efficiency, tomorrow's will run it with power to spare.
  The developer task is to make sure his program will run on that new hardware with minimal effort.

* **Data is only useful as long as it's being used**.
  Flat files help ensure that data is usable for the longest possible time.
  For complex data structures where plain text really isn't appropriate, use a structured text format instead.

* **A programmer who can't re-use other programs is condemned to re-write them**.
  Use software leverage to your advantage.
  Many programmers have only a superficial understanding of the importance of re-usable code modules.

* **Silence is golden**.
  A silent command is often more usable, providing the function asked for and nothing more.

* **Think parallel**.
  Most tasks are composed of sub-tasks which may be attacked in parallel.
  This also applies to user interactions.
  Parallelism can save a great deal of time and frustration.

* **The sum of the parts is greater than the whole**.
  A large application built from a collection of smaller programs is more flexible and hence more useful than a single large program.
  The same functional capability may exist in both solutions, but the collection-of-small-programs approach is the more forward-looking of the two.

* **Look for the 80% solution**.
  Doing 100% of anything is difficult.
  Focusing in the 80% is far more efficient and cost-effective.
  Handle the 80% and let the 20% fend for themselves.

* **Treat all the data as an event log**.
  Use a central log where consumers can subscribe to the relevant events.
  Having a central place \([the log](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)\) for continuous events make easy to create a stream of data to process and sets a source of truth.

* **There is no silver bullet**.
  Accept that many programming decisions are opinions.
  Discuss [tradeoffs](https://twitter.com/kelseyhightower/status/774076482637312001), which you prefer, and reach a resolution.

* **Keep the iteration loop short**.
  Invest in tools to automate and improve the development cycle \(CI, CD\). Decreasing build times a few seconds actually saves a lot of time over time. Deploy often to make the loop end to end. If you need to sinetgubg manually more than twice, then write a tool for the third time.

Like any other field, the world of Software Development has some interesting and famous "laws". These are some of them I've found interesting, funny or worth knowing:

* [Laws of Software Development](http://www.globalnerdy.com/2007/07/18/laws-of-software-development/)
* [Famous Laws Of Software Development](https://www.timsommer.be/famous-laws-of-software-development/)
* [Laws of Computing](https://gist.github.com/sorahn/905f67acf00d6f2aa69e74a39de65941)

## Data Pipelines

Data Pipelines are a set of actions that extract data, transform it, and then load the final data somewhere. As any [distributed system](https://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/), they're tricky to work with. These are some great principles to keep in mind.

### Basic Principles

* Simplicity: Each steps is easy to understand and modify.
* Reliability: Errors in the pipelines can be recovered. Pipelines are monitored and tested. Data is saved in each step (storage is cheap) so it can be used later if needed. For example, adding a new column to a table can be done extracting the column from the intermediary data without having to query the data source.
* Modularity: Steps are independent.
* Consistency: Same conventions and design patterns across pipelines.
* Efficiency: Low event latency when needed. Easy to scale up and down.
* Flexibility: Steps change to confort data points. Changes don't stop the pipeline or losses data.

### Data Flow

* In each step of the pipeline there are producers of data and consumers. Consumers can be also producers, e.g `B` in `A | B | C`.
  * Decouple producers and consumers adding a layer in between. That can be something as simple as a text file or complex as a database.
* Schemas changes. Most of the time you won't be there at the exact time of the change so try to save everything.
  * Ideally, the schema will evolve in a backward compatible way:
    * Data types don't change in the same column
    * Columns are either deleted or added but never renamed
* Create a few extra columns like `processed_at` or `schema_version`


## Data Science Projects

1. Frame the problem. Define a clear and concise objective.
1. Get the data.
1. Explore the data.
1. Define metrics.
1. Make the data tidy.
1. Model the data. [Start with the simplest model!](https://developers.google.com/machine-learning/guides/rules-of-ml/)
1. Make sure everything works end to end. Deploy the model.
1. Make results reproducible (code, environment and data).
1. Iterate. Go back to the first point and change one thing at a time. It’s really hard to tell in advance what’s hard and what’s easy. [Engineering projects generally move forward, but machine learning projects can completely stall. It’s possible, even common, for a week spent on modeling data to result in no improvement whatsoever.](https://medium.com/@l2k/why-are-machine-learning-projects-so-hard-to-manage-8e9b9cf49641)
