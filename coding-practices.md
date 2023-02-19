# Coding Pratices

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
