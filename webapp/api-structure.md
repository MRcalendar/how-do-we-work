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

> There are 2 helpers that should be used when building endpoint files
> - the `ApiResponse<T>` interface, used when the response is wrapped in a "data" property
> - the `getAPIQueryKey(path)` function, used to consistently get the value for the `queryKey` parameter of any given path

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
For the sake of the example, let's pretend we're doing a real endpoint.

We see in Swagger a new endpoint `GET /brand/{brandId}/collections`.
The main file will be named `get-brand-collections.ts` and the base for its content will be `GetBrandCollections`

The **main file** will include :
- a `GetBrandCollectionsParams` interface (using the same name as the file)
  - responsible for describing parameters needed to complete the request
  - **when the endpoint has only one parameter, we should still wrap it in an object, it gives better context on what is needed to complete the request**
- a `GetBrandCollectionsResponse` interface for the API output (**USE ONLY SCALAR VALUES. NO DATE OR ANY OBJECT**)
  - responsible for describing what the API will return
- a `getBrandCollectionsEndpoint` object with :
  - a `path` method, responsible for building the path
  - a `fetch` method, responsible for sending the request (using **axios**)
  - *(Optional)* a `serialize`/`deserialize` function
    - responsible for mapping scalar values to objects (usually Date objects, but could be anything not scalar)
    - Remember: **the API output is ALWAYS serialized**
- a `useGetBrandCollections` function
  - responsible for using **tanstack-query** hooks
  - mutations should invalidate queries here

### How to type outputs ?

Because we will have multiple files with almost the same types everywhere, it can be bothering to repeat the same.
To avoid that, since we are going to type scalar values only for the API response, we can have interfaces for each entity that can be returned, without its related entities.
Then in each endpoint, we compose a response type using those interfaces and some Typescript magic (Pick, Omit, &, extends, etc...)

Ex: Assume we have a Portfolio & a Seller interface, with only scalar data in each. An endpoint returning the portfolios with sellers might be typed as :
```ts
type GetPortfoliosWithSellersResponse = (Portfolio & { sellers: Seller })[]
```

### Example of a main file

```ts
export interface GetCollectionsParams {
  brandId: Brand["id"];
}

export type GetCollectionsResponse = Collection[];

export const getCollectionsEndpoint = {
  path: ({ brandId }: GetCollectionsParams) => `/brands/${brandId}/collections`,
  fetch: ({ brandId }): GetCollectionsParams) =>
      axiosInstance
        .get<any, ApiResponse<GetCollectionsResponse>>(
          getCollectionsEndpoint.path({ brandId }),
        )
        .then((res) => res.data)
};

export const useGetCollections = (params: GetCollectionsParams, useQueryOptions: UseQueryOptions<GetCollectionsResponse>) =>
  useQuery<GetCollectionsResponse>({
    queryKey: getAPIQueryKey(getCollectionsEndpoint.path(params)),
    queryFn: () => getCollectionsEndpoint.fetch(params),
  });

```

## Mock file

Using the same naming convention, the **mock file** contents include :
- a `getCreateCollectionHandler` function
  - responsible for returning a handler
  - *There could be multiple in case we have to mock errors*, in that case handlers should be named accordingly (see example)
- a `mockCreateCollection` function
  - responsible for returning a mocked response (satisfying the API output interface)

### Example of a mock file

```ts

export function getGetCollectionsHandlerOk(params: GetCollectionsParams, mockedCollections: GetCollectionsResponse) {
  return rest.get(getCollectionsEndpoint.path(params), (req, res, ctx) => res(ctx.status(200), ctx.json({ data: mockedCollections }));
}
```

