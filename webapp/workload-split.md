# How to split workload
Following detailed User Stories coming from our Product Manager (also designer !) with Figma mock-ups, we study the expected User Journey from end to end, we design each screen on a technical level (wireframe-like) using [Excalidraw](https://excalidraw.com/) allowing us to define if there are reused feature that would legitimate the use of generic components and define what we would need from back-end.


## First step at tech level : Using wireframe design
We begin by extracting the different layouts we're gonna have to use and define future or already existing components with 4 distinctions: 
- layouts (global or contextual),
- business components (containing all logic regarding a particular business need),
- pure components (ideally controled),
- hidden components being displayed after a particular interraction,
- placeholders (for non covering components),
- pure typescript functions (when a page needs to handle a specific load of data we try to handle it with pure typescript functions that have the advantage to be easily tested).
<img height="300" alt="Excalidraw legend" src="https://user-images.githubusercontent.com/20864211/226930585-3aaa02ce-c14f-4e4a-8896-2231d3c64399.png">

##
Each screen then contains:
- the page bringing together layouts and mostly business components also holds data queries;
- the business components containing and exporting all business logic and putting together pure components, for complex business components or complex pages we already define important props for components to have and revamp to their children according to which needs what;
- pure components, ideally all controlled by their business parents;
- we also link contextual components to their triggers and potential placeholders.
<img width="1072" alt="Full Pipe" src="https://user-images.githubusercontent.com/20864211/226928331-01588d34-f67e-4b0b-ac9a-40102d005651.png">

Globally, most of our component splitting takes testing into account (may it be from a technical point of view or for our PM to be able to test from a feature point of view if the delivery fits the User Story expectation), so we can have controle over either input or output (or both!).

To confirm what we got so far makes sense at a deeper level and what we need from back-end, we check the datas each page needs to load, define modals and what each component needs, reorganize what needs to be reorganized.

## 
From this point, it is safe to say that each element becomes a technical task tied to a parent User Story that would make sense for our Product Manager to test. Regarding granularity, we aim for each task to not be above 2 or 3 points (cf [Coding practices - Estimation](https://github.com/MRcalendar/how-do-we-work/blob/cbergon-patch-2/process.md#estimation)), so we can deliver features everyday.
We check each screen (having added all User Stories to each), create the technical tasks and define hom many points to assign each. Having an overview complete from end to end allow us to define when and where we need to implement non UI features and where to put the logic. Having testing in mind at this step is also crucial as it helps to define the scope of action and build simple small elements.

To be more specific, this process takes us 2 day to prepare an estimated 3 cycles User Journey (1 cycle = 1 week a the moment).
