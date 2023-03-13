# Troubleshooting

This page will help us maintain a knowledge base of all the problems encountered yet, and how we fixed them.

If you find yourself having an issue 

## The build fails
### Possible cause : test files are present in the `/src/pages` folder

When test files are present in the `/src/pages` folder, the package `generouted` will import them during the build process, which will then try to include the `vitest` package, which is not supported in production environment, causing an error like this one :

```
[...] "fileURLToPath" is not exported by "__vite-browser-external", imported by "node_modules/local-pkg/dist/shared.mjs".
```

To fix this, we checked the dependency tree of the package involved (`local-pkg`), and it turned out to be related to `vitest`.

- Then we checked where `vitest` is imported, and it was only imported in test files
- Then we checked out the previous commit on the main branch, to see if the error was reproduced, and it wasn't.
- Then we cherry-picked the commit where the issue was spotted, but removing the new test files, and it worked.
- Then we reintroduced the new test files, but not where they were included in the commit, but next to other test files, and it was working.
