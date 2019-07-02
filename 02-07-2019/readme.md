# Software development methodologies

- [Agile](#agile)
	- [Scrum](#scrum)
		- [Sprint](#sprint)
		- [Roles](#roles)
			- [product owner](#product-owner)
			- [scrum master](#scrum-master)
			- [team development](#team-development)
	- [Kanban](#kanban)
	- [Scrum vs Kanban](#scrum-vs-kanban)
	- [Minimum viable product](#mvp)

## Agile

- Type of project development which focus on flexibility, adaptive to changes. 
- Agile breaks the project into smaller
- Agile has 2 methodologies/frameworks :
	- [Scrum](#scrum)
	- [Kanban](#kanban)

![The-Ultimate-Guide-to-PM-Methodologies-flowchart](https://raw.githubusercontent.com/harryosmar/what-do-i-learn-today/master/02-07-2019/The-Ultimate-Guide-to-PM-Methodologies-flowchart.png)

### Scrum

- Has iterative [Sprint](#sprint) cycle
- There is 3 main [roles](#roles) :
	- [product owner](#product-owner)
	- [scrum master](#scrum-master)
	- [team development](#team-development)
- Should be there in no change on the current running [Sprint](#sprint), changes will wait until the next [Sprint](#sprint). This rule enforce by [scrum master](#scrum-master)
- Release in the end of sprint
- concerned on "more work done faster" to achieve [MVP/Minimum viable product](#mvp).
- Artifacts/Result :
	- Product Backlog
	- Sprint Backlog
	- Scrum Board (Todo, Dev, Test, Done)
	- Burndown Chart (Ideal task remaining vs actual task remaining) on the current `sprint board`

#### Sprint

The lifecycle of a sprint :
1. **BEFORE START** 
- `Sprint planning`
	- Estimate list of tasks/tickets on `product backlog` that need to be prioritized and added to `sprint backlog`.
	- Allocated time 1-4 hours.
minutes.
2. **STARTING/ON PROGRESS**
- `sprint backlog` converted to `sprint board`
- `Daily Scrum`
	- Discuss about current `sprint board`, the yesterday achievements and issues. It also called `Daily Standup`.
	- Allocated time 10-15 minutes.
3. **END** 
- `Sprint Review`.
	- Discuss what the result of the current `sprint`, what we can learn to be optimized on the next `sprint`.
	- Allocated time 0.5-2 hours.
- `Retrospective`
	- Discuss what went well & what did not on the current `sprint`
	- Allocated time 0.5-2 hours.


#### Roles

#### product owner

#### scrum master

- Enforce scrum roles, should be no compromise. eg : reject the changes on the running [sprint](#sprint).

#### team development

The development/engineer team, usually consist of : developer, designer User Interface/User eXperience, tester, devops/Server

### Kanban

- There is no [sprint](#sprint), Kanban is a continuous flow, which means any features or changes can come anytime.
- Suitable for `bug fix`, `support/maintenance` work on operational level (to keep the current system is running fine). And when changes are to fast.
- There is no meetings required
- Roles is flexible add as needed.
- concerned on "process improvements".
- Release anytime.
- Artifacts/Result :
	- Kanban Board (Todo, Dev, Test, Done).
	- Lead/Cycle time Diagram : Chart about the average amount of time is needed for a task to be processed from `start` to `finish` point.
	- Cumulative flow Diagram

## Scrum vs Kanban

|Scrum|kanban|
|-----|------|
|Has a sprint meetings & cycle 1-4 weeks|no meetings needed|
|Concerned on "more work done faster"|Concerned on "process improvements"|
|Changes can not be applied to the current running sprint|Changes always welcomed|
|Release in the end of sprint|Release anytime|
|Suitable for big project which need to be breakdown to a smaller parts to achieve MVP|Suitable for "operational level : bug fix/maintenance" when the change is too fast|
|There are 3 main roles: product owner, scrum master, team development|Roles is flexible add as needed|

![Scrum vs Kanban](https://raw.githubusercontent.com/harryosmar/what-do-i-learn-today/master/02-07-2019/scrum-vs-kanban.png)

## MVP

A minimum viable product (MVP) is a product with just enough features to satisfy early customers, and to provide feedback for future product development.

![MVP](https://raw.githubusercontent.com/harryosmar/what-do-i-learn-today/master/02-07-2019/mvp.png)


## Links
- https://www.lucidchart.com/blog/agile-vs-waterfall-vs-kanban-vs-scrum
- https://www.atlassian.com/agile/kanban/kanban-vs-scrum
