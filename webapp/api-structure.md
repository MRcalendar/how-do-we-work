# API Structure

The API gives us a swagger that we can use to create interfaces and hooks on the frontend in the same manner.

Everything will go in the `src/services/api` folder.

It is supposed to be replicating the API swagger.

- If an endpoint is in Swagger but not in the folder => **create it**
- If an endpoint is not in Swagger, but you need it for your current task => **notify the backend team and agree on the interface, then create it**
- If an endpoint is in Swagger and the folder, but isn't up-to-date => **update it**
- If an endpoint is in Swagger, but the doc is not enought to create it => **notify the backend / try sending some requests and see what are the types returned**

A file in that folder is supposed to represent a URL & method (GET, POST, etc...) from swagger.

# Creating a new endpoint

> **We use kebab-case for file names**

An endpoint will be defined in two files :
- the first one for using that endpoint. we'll call it the **main file**
- the second one for mocking that endpoint. we'll call it the **mock file**

The **main file** will be placed in a subfolder of  `src/services/api`, according to the swagger.
The name will be of the form : {method}-{intent}.ts
Ex:
- `POST /api/brands/{brandId}/collections` in swagger =>  `src/services/api/collections/post-create-collection.ts`
- `GET /api/brands/{brandId}/collections` in swagger =>  `src/services/api/collections/get-brand-collection.ts`
- `PUT /api/brands/{brandId}/collections/{collectionId}` in swagger =>  `src/services/api/collections/put-update-collection.ts`
- `PUT /api/brands/{brandId}/collections/{collectionId}/archive` in swagger =>  `src/services/api/collections/put-archive-collection.ts`

The **mock file** will use the same name but :
- will have a `.mock` suffix added
- will be placed in the `__tests__` folder in the same subfolder as the **main file**
Ex:
- `src/services/api/collections/post-create-collection.ts` => `src/services/api/collections/__tests__/post-create-collection.mock.ts`
- `src/services/api/collections/get-brand-collection.ts` => `src/services/api/collections/__tests__/get-brand-collection.mock.ts`
- `src/services/api/collections/put-update-collection.ts` => `src/services/api/collections/__tests__/put-update-collection.mock.ts`
- `src/services/api/collections/put-archive-collection.ts` => `src/services/api/collections/__tests__/put-archive-collection.mock.ts`

## Main file

The main file will be named after the endpoint intent.
We are going to reuse that intent for naming inside that file, but using TitleCase instead of kebab-case
Ex: `post-create-collection.ts` => endpoint's intent is `CreateCollection`

The **main file** content include :
- a `path` function
  - responsible for building the path
- a `fetch` function 
  - responsible for sending the request (using **axios**)
- a `useCreateCollection` function
  - responsible for using **tanstack-query** hooks
  - mutations should invalidate queries here
- a `CreateCollectionParams` interface (using the same name as the file) for parameters
  - **use only one parameter with named properties, instead of 2-3 parameters**
- a `CreateCollectionResponse` interface for the API output (**USE ONLY SCALAR VALUES. NO DATE OR ANY OBJECT**)
  - responsible for describing what the API will return
- *(Optional)* a `serialize`/`deserialize` function
  - Remember: **the API output is ALWAYS serialized**
  - responsible for mapping scalar values to objects (usually Date objects, but could be anything not scalar)

Example of a main file :

```
// @todo
```

## Mock file

Using the same naming convention, the **mock file** contents include :
- a `getCreateCollectionHandler` function
  - responsible for returning a handler
  - *There could be multiple in case we have to mock errors*, in that case handlers should be named accordingly (see example)
- a `mockCreateCollection` function
  - responsible for returning a mocked response (satisfying the API output interface)

Example of a mock file :

```
// @todo
```

