# Rituals

🤚 Always come prepared !

## Daily ritual

🕘 Meeting at 9:00 ~ 10 min **Tuesday**, **Thursday** and **Friday** morning

**What to say ?**

- (the most important) What do I need help with, and by what time do I need it?
- What did I achieve yesterday?
- What am I achieving today?

## Cycle rituals

📅 one week cycle, from starting on Thursday

### Grooming - Product team

🕘 Tuesday morning, meeting at 10:30 - 11:30

Product team prepare US/Tasks based on the quarter projects/epics

- Adjust tasks if bugs/urgent improvements
- Any urgent problems to retrieve from the Problem Sheet from the past 7 days?

### Grooming - Tech team

🕘 Tuesday afternoon, meeting at 15:00 - 16:00

Tech team:

1. review the current cycle
   - Did we complete it? If not, why?
   - Did we have a task blocked in “In progress” for too long?
   - Did we meet any [Technical Obstacles](https://docs.google.com/spreadsheets/d/1JNJU-pOwqTwDnI49YVC6DhZps8tVyQGCMlenqe4HG84/edit?usp=drivesdk) ?
     - Ask the 5 WHYs to figure out the true root cause
     - What countermeasure can we put in place and improve our standards ?
2. Prepare the demo
3. take a look at the next User Stories prepared by the product team.
   - Blink estimation in fibonacci points.
   - Do we understand the need ? Do we have questions for the product team ?
   - Plan an example mapping workshop if US has complex business rules
   - Assignation of User Stories to devs or binome if pair programming
   - Aach assignee asynchronously split in technical sub task done asynchronously after. At this moment the estimation can be moved from the US to the tech subtasks.
   - (optional) adding acceptance criteria for each subtask

a new epic (aka project) needs to be correctly understood and splitted before starting development. It needs more time than this time constrained ritual.
In this case, we do a workload split described in details in this [page](https://github.com/MRcalendar/how-do-we-work/blob/main/webapp/workload-split.md)

### Cycle review - full team

🕘 Wednesday morning, meeting at 10:30 - 11:30

1. Demo of the features delivered.
2. If any, presentation of the tech obstacles and countermeasures
3. Discussion with the product team about the next user stories.

- Be sure we have a shared understanding between Product & Tech. Ask many questions. Think about edge cases.

## Estimation

1 - easy / fast. (typo, small design fix, simple new business rules to add with unit tests.. )

2 - more code, still fast and easy.

3 - we need to change a more stuff, should take 1 day or max 2 days.

5 - half sprint maybe, more complex, more code.

8 - entire week, probably a new feature and need to think how to implement (surely too much, we need to push on splitting this in smaller US

## Definition

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

## Kanban standards

| Column title | User-stories                                                                | To Do                                                                                        | In Progress                                                                            | To Review                                         | To Test                                                                                           | ⌛️ Ready for prod                                                   | Done                   | Blocking |
| ------------ | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ---------------------- | -------- |
| Description  | Keep an overview of the actual user stories that are going out this sprint. | The subtasks of each user-story + tasks outside US that will be done for the ongoing sprint. | Tasks + Subtasks started. Each team member should have only one task at the same time. | Tag the person that should review it in comments. | Once your task has been code reviewed, deploy to Staging and tags @Louise in comment for testing. | Every evening tech team checks this column and deploys if necessary. | Task deployed on prod. |

Louise checks every days this column, to do a final test in prod. | If you are blocked, write your reasons of blockers in comment and tag a team member that can help you, and move it to this column. This enables you to always have one task in “In progress” at all times. |

## Share and Learn

📅 Last **Friday** of the month
🕘 16:30 - 18:00

- **What topics should we discuss**
  - Kaizen. What were the problems we faced ? Why ? [Review the Technical Obstacles sheet.](https://docs.google.com/spreadsheets/d/1JNJU-pOwqTwDnI49YVC6DhZps8tVyQGCMlenqe4HG84/edit#gid=0)
  - Someone on the team shares a learning (through presentation)
    - Ex: a better lib, a better way to code, a better way to test
  - Share a video or article —> can be done in random progressively
    - Ex: share article, video, conf about the tools we use (Typescript, React, NestJS ...)
  - Share some code you have done or problem you have faced and want a deeper discussion
