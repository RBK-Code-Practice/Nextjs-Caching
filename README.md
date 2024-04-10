
**Next.js Caching** 


1. Request memoization 
1. Data cache 
1. Full Router cache
1. Router cache


**Full Router Cache** 

Next.js automatically renders and caches routes at build time. This is an optimization that allows you to serve the cached route instead of rendering on the server for every request, resulting in faster page loads.


**Static and Dynamic Rendering** 

Whether a route is cached or not at build time depends on whether it's statically or dynamically rendered. Static routes are cached by default, whereas dynamic routes are rendered at request time, and not cached.

- Next.js considers particular route as dynamic if it contains any of the following




**Subsequent Navigations:**

- **D**uring subsequent navigations or prefetching:
- Next.js checks if the React Server Components Payload is already stored in the Router Cache.
- If found, it avoids sending a new request to the server.
- If the route segments aren’t cached, Next.js fetches the Payload from the server and populates the Router Cache on the client.

**Duration** 

By default, the Full Route Cache is persistent. This means that the render output is cached across user requests**.**

**Revalidation**

We can revalidate the Router Cache on demand similar to how we did it for the Data Cache. This means that revalidating Data Cache using revalidatePath or revalidateTag also revalidates the Router Cache.

**revalidateTag()**

**revalidatePath()**

**Opting out** 

1. Using Route segment config options 
- const dynamic = 'force-dynamic'
- const revalidate = 0


**Caching Dynamic Route**

1. generateStaticParams()

- For dynamic paths, paths provided by generateStaticParams are cached in the Full Route Cache at build time. At request time, Next.js will also cache paths that weren't known at build time the first time they're visited.
- generateStaticParams replaces the [getStaticPaths](https://nextjs.org/docs/pages/api-reference/functions/get-static-paths) function in the Pages Router.

**DynamicParams** 
**
Control what happens when a dynamic segment is visited that was not generated with [generateStaticParams](https://nextjs.org/docs/app/api-reference/functions/generate-static-params).

export const  dynamicParams=true

True- Dynamic segments not included in generateStaticParams are generated on demand.

False - Dynamic segments not included in generateStaticParams will return 404.


