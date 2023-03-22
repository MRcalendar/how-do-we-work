# How to split workload
Following detailed User Stories coming from our Product Manager (also designer !) with Figma mock-ups, we study the expected User Journey from end to end, we design each screen on a technical level (wireframe-like) using excalidraw allowing us to define if there are reused feature that would legitimate the use of generic components and define what we would need from back-end.
- We begin by extracting the different layouts we're gonna have to use and define future or already existing components with 4 distinctions: layouts, business components, pure components and hidden components being displayed after a particular interraction.
- Each screen then contains:
    - the page bringing together layouts and mostly business components;
    - the business components containing and exporting all business logic and putting together pure components, for complex business components or complex pages we already define important props for components to have and revamp to their children according to which needs what;
    - pure components, ideally all controlled by their business parents;
    - we also link contextual components to their triggers.
- Alongside visual components when a page needs to handle a specific load of data we try to handle it with pure typescript functions that have the advantage to be easily tested. 
    -> Globally, most of our component splitting takes testing into account, so we can have controle over either input or output (or both!).
- To confirm what we got so far makes sense at a deeper level and what we need from back-end, we check the datas each page needs to load, what each component needs and reorganize what needs to be reorganized.
