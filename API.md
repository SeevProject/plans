## **API Endpoints**

The server endpoints for the frontends to connnect to.

```yaml
- POST /auth/login: # users, companies
  Authenticate a user and start a session.
- POST /auth/logout: # users, companies
  End a user's session and log them out.
- POST /auth/register: # users
  Create a new user account and start a session.

- GET /users/me: # users
  Get the current user's account and profile information.
- PUT /users/me: # users
  Update the current user's profile information.
- POST /users/me/generate/:id: # users
  Generate a resume using the specified template and the current user's profile information.
- GET /users: # admins, companies
  Get a list of all user accounts or only specific users if company.

- GET /templates: # users
  Get a list of available resume templates.
- PUT /templates/:id: # admins
  Update a template.
- DELETE /templates/:id: # admins
  Delete a template.
- POST /templates: # admins
  Create a new template.

- GET /companies/me: # companies
  Get the current company's account and profile information.
- GET /companies: # admins
  Get a list of all company accounts.
- POST /companies: # admins
  Create a new company account.
- PUT /companies/:companyId: # admins
  Update the permissions for the specified company account.
- DELETE /companies/:companyId: # admins
  Delete the specified company account.
```
