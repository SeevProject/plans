## **API Endpoints**

The server endpoints for the frontends to connnect to.

```yaml
# Authentication Endpoints
- POST /auth/login:
  Description: Authenticate a user and start a session.
- POST /auth/logout:
  Description: End a user's session and log them out.
- POST /auth/register:
  Description: Create a new user account and start a session.

# User Endpoints
- GET /users/me:
  Description: Get the current user's account and profile information.
- PUT /users/me:
  Description: Update the current user's profile information.
- POST /users/me/templates/:templateId:
  Description: Generate a resume using the specified template and the current user's profile information.
- GET /templates:
  Description: Get a list of available resume templates.

# Company Endpoints
- GET /companies/me:
  Description: Get the current company's account and profile information.
- GET /companies/me/users:
  Description: Get a list of users associated with the specified company.

# Admin Endpoints
- GET /users:
  Description: Get a list of all user accounts.
- GET /companies:
  Description: Get a list of all company accounts.
- POST /companies:
  Description: Create a new company account.
- PUT /companies/:companyId:
  Description: Update the permissions for the specified company account.
- DELETE /companies/:companyId:
  Description: Delete the specified company account.
- POST /templates:
  Description: Create a new template.
- PUT /templates/:id:
  Description: Update a template.
- DELETE /templates/:id:
  Description: Delete a template.
```
