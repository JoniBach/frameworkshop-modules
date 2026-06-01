# Login Lesson

This lesson helps you build a login page in the React workshop app by following the same patterns as the existing register page.

The goal is to practise:

- Reading an existing implementation before writing new code
- Reusing shared components
- Creating a form with validation
- Calling a backend API with `fetch`
- Handling success and error states
- Adding a route so the page can be visited in the browser

## Starting point

You should already have:

- A React app in `frameworkshop-react`
- A Deno backend running on `http://localhost:3000`
- A register page at `src/pages/Register.tsx`
- A shared text input component at `src/components/TextInput.tsx`

The login page should be created at:

```text
frameworkshop-react/src/pages/Login.tsx
```

## Backend contract

The login page should send a request to:

```text
POST http://localhost:3000/auth/login
```

The request body should be JSON:

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

A successful response looks like this:

```json
{
  "status": "ok",
  "user": {
    "id": "string",
    "email": "user@example.com",
    "createdAt": "2026-06-01T11:00:00.000Z"
  }
}
```

An error response looks like this:

```json
{
  "error": "Unauthorized: invalid email or password"
}
```

## Exercise steps

## 1. Read the register page first

Open:

```text
frameworkshop-react/src/pages/Register.tsx
```

Look for these things:

- How `useForm` is configured
- How `Controller` connects form fields to `TextInput`
- How validation errors are displayed
- How `fetch` sends data to the backend
- How success and error state are stored with `useState`

The login page should feel very similar, but it only needs two fields:

- Email
- Password

## 2. Create the login page file

Create:

```text
frameworkshop-react/src/pages/Login.tsx
```

The page should import:

- `useState` from React
- `Controller` and `useForm` from `react-hook-form`
- `TextInput` from `../components/TextInput`
- The shared CSS file used by the register page

## 3. Define the form values

The login form needs a type with two fields:

```ts
email: string
password: string
```

This keeps the form strongly typed and helps TypeScript catch mistakes.

## 4. Add local state

The login page needs state for:

- The logged-in user
- Any error message

Later, you can also add state for:

- Delete-user status
- Loading state while deleting a user

## 5. Set up `useForm`

Use default values for the fields:

```ts
email: ''
password: ''
```

Use `mode: 'onTouched'` so validation appears after a field has been touched.

## 6. Add the submit handler

When the form is submitted, send a `POST` request to:

```text
http://localhost:3000/auth/login
```

The request should include:

- `method: 'POST'`
- `Content-Type: application/json`
- A JSON body containing `email` and `password`

If the response is successful:

- Store the returned user in state
- Clear any previous error
- Reset the password field

If the response fails:

- Show the error message from the backend
- Clear the logged-in user
- Reset the password field

## 7. Build the form UI

The page should include:

- A heading saying `Login`
- A short paragraph explaining what the page does
- An email field
- A password field
- Validation messages
- A submit button

Email validation should check:

- The field is required
- The value looks like an email address

Password validation should check:

- The field is required

## 8. Show the logged-in user

After a successful login, show:

- A heading such as `Logged in user`
- The user email
- The user creation time

Do not show the password or password hash. The backend should never return those values.

## 9. Add a signout button

When a user is logged in, show a `Sign out` button.

Clicking the button should:

- Clear the logged-in user
- Clear any error message
- Reset the form

This is frontend-only signout because the current backend does not create a session or token.

## 10. Add a delete-user button

When a user is logged in, show a `Delete user` button.

The button should send:

```text
DELETE http://localhost:3000/auth/user
```

With this JSON body:

```json
{
  "email": "user@example.com"
}
```

On success:

- Show a message confirming the user was deleted
- Clear the logged-in user
- Reset the form

On failure:

- Show the backend error message

## 11. Add the route

Creating the page file is not enough. You must also add the route.

Open:

```text
frameworkshop-react/src/main.tsx
```

Import the login page:

```ts
import Login from './pages/Login'
```

Add a route:

```tsx
<Route path="/auth/login" element={<Login />} />
```

The route should be inside the same parent route as the existing pages.

## 12. Add the navigation link

Open:

```text
frameworkshop-react/src/App.tsx
```

Add a link to the navigation:

```tsx
<Link to="/auth/login">Login</Link>
```

Now the page can be reached from the app navigation.

## 13. Test it in the browser

Start the Deno backend and React app.

Visit:

```text
http://localhost:3002/auth/login
```

Try these checks:

- Submitting an empty form shows validation errors
- Logging in with a missing user shows an error
- Registering a user and then logging in works
- Signing out clears the logged-in user
- Deleting a user removes the user and clears the logged-in state

## Common mistakes

- Forgetting to add the route in `main.tsx`
- Forgetting to add the navigation link in `App.tsx`
- Sending the request to the React app port instead of the Deno backend port
- Missing the `Content-Type: application/json` header
- Forgetting to call `JSON.stringify` on the request body
- Trying to display `password` or `passwordHash`, which should not exist in the response
- Not handling non-OK responses from `fetch`

## Stretch goals

If you finish early, try one of these:

- Hide the login form while a user is logged in
- Add a loading state to the login button
- Add a confirmation step before deleting a user
- Move the backend base URL into a shared constant
- Create a reusable `UserSummary` component

## Success criteria

You are finished when:

- `/auth/login` displays the login page
- The form validates email and password
- The page can log in a registered user
- The page shows backend errors clearly
- A logged-in user can sign out
- A logged-in user can delete their account
- The app builds without TypeScript errors
