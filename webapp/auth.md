# Authentication

Authentication is handled via `firebase` right now.

It is plugged to the `@app/services/authentication/AuthenticationContext` which provides access to data/functions related to the authentication of users :

- login via credentials
- login via oauth (google)
- logout
- reset password
- confirm password reset
- current authenticated user
- current JWT token

# Authorization

Most of the application is only available to authenticated users. But the login page for example should only be available for non authenticated users (commonly called "guests").
To handle that logic, we created `AuthOnly` and `GuestOnly` components, that prevents access to their children unless the user is authenticated (or not). Here is an example on the `LoginPage` :

```typescript
export default function LoginPage() {
  return (
    <GuestOnly>
      // You won't see this unless you are a guest (not authenticated)
    </GuestOnly>
  );
}
```

> `GuestOnly` redirects to the index page (which is the dashboard page for now) if you are authenticated.

> `AuthOnly` redirects to the login page if you are not authenticated.

## Role based authorization

The same logic should be used for applying role based authorization.
It has not been implemented yet, but we could think of it as a `RoleOnly` component that would behave like this:

```typescript
export default function MyRestrictedPage() {
    return (
        <RoleOnly roles=["modaresa", "brand-admin", "brand-member"]>
        // here is the restricted page
        </RoleOnly>
    )
}
```
