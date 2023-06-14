## File Structure
Specification for the file structure of the `webapp` project

### Folders

- `/components` : contains all the design system elements
- `/layouts` : contains all the different layouts used by pages
- `/modules` : contains all the business related modules
    - A module is made of `components`/`helpers`/`hooks` specific to a certain part of the business (ex: onboarding, sales-campaign-setup, calendars, reporting, etc…)
    - a `shared` module will contain the components/helpers/hooks shared by different modules.
- `/models` : all the typescript definitions (interfaces, types, enums, …)
- `/services` : contains functions that are impure and not related to a specific module
    - `/services/api` : will contain all the API related stuff
    - `/services/auth` : for authentication
    - `/services/i18n` :  for internationalization,
    - etc…
- `/pages` : the structure here will follow the routes structure of the website.
    - Each `.tsx` file will export a component and a `route` constant, defining its own route(s)
    - The route constant will be used to build the routes tree in the router.

### File naming conventions

- kebab-case for long names (onboarding-form.tsx)
- keep file names simple (representing the component in its folder, not over the whole codebase)
