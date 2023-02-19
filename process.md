# Our process

## Tools

- Communication
    - Slack
    - Google Workspaces
    - Notion
    - Gather app
- Project and code management
    - Github Enterprise
    - Linear app
- Hosting
    - AWS
    - CleverCloud
    - Cloudflare Pages
- Security
    - Bitwarden

## Rituals

🤚 Always come prepared !

### Daily

🕘 Meeting at 9:00 ~ 10 min **Tuesday**, **Thursday** and **Friday** morning

- **What to say ?**
    - (the most important) What do I need help with, and by what time do I need it?
    - What did I achieve yesterday?
    - What am I achieving today?

### Cycle

📅 one week sprint, from starting on Thursday

🕘 **Product team** Tuesday morning, meeting at 10:30 - 11:30
Product team prepare US/Tasks based on the quarter projects/epics
- Adjust tasks if bugs/urgent improvements
- Any urgent problems to retrieve from the Problem Sheet from the past 7 days?

🕘 **Tech team** Tuesday afternoon, meeting at 17:00 - 18:00
Tech team 
1. review the current cycle
    - Did we complete them all? If not, why?
    - Did we have a task blocked in “In progress” for too long? If so ask the 5 WHYs to figure out the true root cause
        - What US/task are blocked?
        - Did we pull the andon ? 
        - Should we take some action to resolve them in the next sprint filling [Technical Obstacles](https://docs.google.com/spreadsheets/d/1JNJU-pOwqTwDnI49YVC6DhZps8tVyQGCMlenqe4HG84/edit?usp=drivesdk)
2. take a look at the next User Stories prepared by the product team.
    - Blink estimation in fibonacci points.
    - Do we understand the need ? Do we have questions for the product team ?
    - Assignation of US to devs or binome if pair programming
    - Splitting in technical sub task done asynchronously by assignee on Wednesday.


🕘 Wednesday morning, meeting at 10:30 - 11:30
1. Demo of the work done.
2. If any, presentation of the tech obstacle and countermeasures 
3. Discussion with the product team about the next user stories.
  - Be sure we have a shared understanding between Product & Tech. Ask many questions. Think about edge cases.)
  - Plan an example mapping workshop if US has complex business

### Estimation
        
1 - easy / fast. (typo, small design fix, simple new business rules to add with unit tests.. )

2 - more code, still fast and easy.

3 - we need to change a more stuff, should take 1  day or max 2 days.

5 - half sprint maybe, more complex, more code.

8 - entire week, probably a new feature and need to think how to implement (surely too much, we need to push on splitting this in smaller US
            
### Defintion

✍️ **Epic** : A large story that cannot be simply achieved in a single sprint. In Linear, it’s called “Projects”.

Example : 
- A brand must be able to access one calendar grouping all their appointments.
- A buyer must be able to easily make an appointment with a brand.  

✍️ **User story (US)** : An item that needs to be done within a project/epic. A user story is a very high-level definition of the project requirements. Ideally, it should not be longer than a sprint to complete. It’s called “Issues” in Linear and we put it in the “user story” column in a cycle.

A US should be completed within a sprint/cycle, if not, it's too big and should be split into smaller stories. A good habit is to ask for help if you've been blocked beyond 2 hours on a subject. 

Example : 
- As a brand, I want to see at a glance the useful information about an appointment.
- As a buyer, I want to book a virtual appointment with the brand.

✍️ **Task** : Detailed pieces of work that are necessary to complete a story. A user story is not considered complete until all tasks associated to it are done. Tasks are placed on a Scrum Board for easy tracking. On Linear, it’s called “sub-issues” and it’s placed on the “to do” column. We can also have “issues” purely technical that goes in the “to do” column as not necessary related to an US.

Example : 
- Display the status (prospect/active) of the account on each appointment card.
- Ask the buyer to choose between virtual or face-to-face appointment.

### Kanban standards

| Column title | User-stories | To Do | In Progress | To Review | To Test | ⌛️ Ready for prod | Done | Blocking |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Description | Keep an overview of the actual user stories that are going out this sprint. | The subtasks of each user-story + tasks outside US that will be done for the ongoing sprint. | Tasks + Subtasks started. Each team member should have only one task at the same time.  | Tag the person that should review it in comments. | Once your task has been code reviewed, deploy to Staging and tags @Louise in comment for testing. | Every evening tech team checks this column and deploys if necessary. | Task deployed on prod.

Louise checks every days this column, to do a final test in prod. | If you are blocked, write your reasons of blockers in comment and tag a team member that can help you, and move it to this column. This enables you to always have one task in “In progress” at all times. |

### Share and Learn

📅 Last **Friday** of the month
🕘 16:30 - 18:00

- **What topics should we discuss**
    - Kaizen. What were the problems we faced ? Why ? [Review the Technical Obstacles sheet.](https://docs.google.com/spreadsheets/d/1JNJU-pOwqTwDnI49YVC6DhZps8tVyQGCMlenqe4HG84/edit#gid=0)
    - Someone on the team shares a learning (through presentation)
        - Ex: a better lib, a better way to code, a better way to test
    - Share a video or article —> can be done in random progressively
        - Ex: share article, video, conf about the tools we use (Typescript, React, NestJS ...)
    - Share some code you have done or problem you have faced and want a deeper discussion

## Coding practices

We will build our practices around [Lean](https://kanbanize.com/lean-management/implementing-lean), [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming), [continuous integration](https://martinfowler.com/articles/continuousIntegration.html) and [continuous delivery](https://continuousdelivery.com/principles/).

Lean and Extreme Programming means:

- Think about the customer and the domain first
- Tests are fundamentals
    - **If the user stored is not 100% tested, it’s not complete**
    - Always try to start with a failing test first
    - Think about dependency injection, function composition to make tests easy, single responsibility principles
- Face every problems and find little steps to solve them
- Continuous learning
    - **Do design document in the form of [Architecture Decision Records](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)**. Ask for review.
- Improve the flow : **split each US in tasks which takes no more than 1 day**. Each task will lead to a commit with the associated [description](https://www.conventionalcommits.org/en/v1.0.0/).
- Have courage to refactor and improve the code a bit every time. Think about the [boy scout rule](https://matheus.ro/2017/12/11/clean-code-boy-scout-rule/).
- Don’t hesitate to do pair programming.

Continuous Integration means:

- Avoid all tunnel effect
    - Ask for help
    - Split your commits
    - Delivery little increments
- Short Lived Branch and Pull Request
    - **A PR should not be open more than 3 days.**
    - Open PR when you start a task.
    - **A PR need at least 1 approve.**
    - Pair programming is even better 🙂

Continuous Delivery means

- The main branch should always be working and capable to go into production. See Trunk Based Development [https://trunkbaseddevelopment.com/](https://trunkbaseddevelopment.com/)
- **Main branch is automatically deployed on staging envs**
- No breaking API changes if possible. If not, non breaking migration by multiple steps.
- Use feature toggles to deliver codes we don’t want the customer to access

### How to write tests

We are using `testing-library/react` for testing our react components.

### React design system components

Design system components are the building blocks of the app. Their behavior absolutely needs to be tested.

Good practices include :

- use `getByRole` as much as possible, as it will only find visible elements following the accessibility standards
- write helper functions to access/interact with a component
    - each component knows its implementation, therefore it should dictate how it is accessible, or how to interact with it (see the `Checkbox` component for an example)

### Business components

Business components are more complex components, often reusing multiple design system components and specific hooks to achieve a particular scenario.

Good practices include :

- When accessing/interacting with a design system component in that business component, reuse/create helper functions
- avoid testing a design system component’s behavior. Here’s an example of do/don’t :
    - ❌ don’t test that an unchecked checkbox gets checked when you click on it
    - 🆗 do test that a checkbox is checked/unchecked by default/after another component’s interaction
    - 🆗 do test that checking/unchecking a checkbox impacts another component’s behavior
