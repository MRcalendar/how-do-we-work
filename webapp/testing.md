# How to write tests
## https://github.com/MRcalendar/how-do-we-work/edit/main/webapp/testing.md#generic-guidelines
## https://github.com/MRcalendar/how-do-we-work/edit/main/webapp/testing.md#coding-guidelines

Testing in the webapp is done primarily with `@testing-library/react`, ideally using TDD.

Tests cover different kind of scopes :
- a pure function: typically helper functions, for business oriented logic manipulating data
- a reusable component: UI components typically, or could be more complex and business oriented, like forms.
- a page component: or user story, since one usually fits in one page component

> Testing pure functions is easy, so we are not going to cover that here.

## Generic guidelines

When testing in a frontend environment, you will almost always be testing behavior rather than implementation.

When writing tests, there are a few things to keep in mind :
- what is being tested exactly ?
- how is it going to be tested ?
- what mocks are needed to test it ?

It’s important to separate what is a component's responsibility, and what isn’t, but it can be tricky.
As a rule of thumb :

> A test on a component should never only involve one of its imported sub-component.

We distinguished 4 kinds of tests for react components :
- props testing : mostly applicable to low-level components, 
- events testing : usually used for low to mid-level components, components made to be reusable usually have event props to be tested
- state testing : suited for any component with a local state,
- scenario testing : a business oriented test, which covers how the component is going to be interacted with by a user.

### Prop testing / Event Testing / State testing
#### Prop testing
- render with default props ⇒ expect default values to appear
- render with custom props ⇒ expect custom values to appear

**Examples**
- render button with just a label
- render button with icon
- render button with label + icon

#### Event testing
- mock handler + interact with component => expect handler was called

**Examples**
- render button with onClick handler + click button => expect handler to be called
- render form with onSubmit handler + fill the form + submit it => expect handler to be called with the filled data

#### State testing
- render page component with drawer + click button to display it => expect drawer to be displayed

### Scenario testing

Scenario testing is the most complex test we have right now. It usually consists of :
- rendering a page component
- interacting with it describing the behavior of a user
- expecting the correct behavior

## Coding guidelines

Tests should NEVER be in the `/src/pages` folder

Here are the common things we do when writing tests, and how to do it
- mock API calls
- mock imports

### mock API calls

API mocks are done using `msw`, and it is **NOT** defined globally, so you always have to call `setupServer(...someHandlers)` before your tests.

There are some handlers prepared already, which should convey a coherent set of data in `@app/__mocks__/presets`
If you need to change some values to test a specific behavior, you can also do that without creating a whole new preset.
Just import whatever entity you want to change, and call `server.use()` **inside your test**

Here is an example of how it is done for the seller-setup page component :
```typescript
import { setupServer } from "msw/node";

import brandBasedOnCollectionHandlers, {
  basicShowroom,
  basicSalesCampaign,
} from "@app/__mocks__/presets/brand-based-on-collections";

const server = setupServer(...brandBasedOnCollectionHandlers);

describe("...", () => {
  beforeAll(() => {
    server.listen();
  });

  afterAll(() => {
    server.close();
  });
  
  vi.test("...", () => {
    // In this specific test, we want to make sure :
    // - an error is shown when an appointment type has no seller associated
    // - an error is shown when a seller has no appointment type
    // - a warning is displayed when VIRTUAL is allowed but a seller has no virtual tool setup
    const showroomWithMisConfiguration: Showroom = {
      ...basicShowroom,
      appointmentFormats: ["IN_PERSON", "VIRTUAL"],
      sellers: basicShowroom.sellers.map(
        (basicSeller, index) =>
          index === 0
            ? { ...basicSeller, appointmentTypes: [] } // first seller has no appointment type
            : { ...basicSeller, appointmentTypes: ["WALKTHROUGH"] }, // other sellers only cover the walkthrough
      ),
    };
    server.use(
      rest.get(
        `/api${SalesCampaignAPIPaths.getShowrooms(
          basicSalesCampaign.id,
        )}`,
        (req, res, ctx) =>
          res(ctx.status(200), ctx.json([showroomWithMisConfiguration])),
      ),
    );
    // the rest of the test
  });
});
```

### Mocking imports
#### Mocking a whole import
very easily done with `vi.mock("", () => ({...the returned module...}))`
#### Mocking parts of an import
We have two ways of doing it, depending on if we need to change the mock between each test or not.
If you don't need to change the mock on each test :

```typescript
// you can put this above the "describe" block
vi.mock("my-node-module", async () => {
  const original = await vi.importActual("my-node-module");
  return {
    ...(original as Object),
    theFunctionIwantToMock: () => {...whatever we need here...}
  }
});
```

If you need to change the mock between each test (here using `mockReturnValue` but we could also use `mockImplementation` :

```typescript
import { theFunctionIwantToMock } from "my-node-module";

vi.mock("my-node-module");

describe("...", () => {
  vi.test("...", () => {
     vi.mocked(theFunctionIwantToMock).mockReturnValue(...whatever we need here...);
  });
  vi.test("...", () => {
     vi.mocked(theFunctionIwantToMock).mockReturnValue(...whatever we need here...);
  });
});
```
