## **Api Endpoints**

The server endpoints for the frontends to connnect to.

```yaml
# all accounts

- POST /auth/login:
user sends auth data, and server tries to find user with said data, and creates a session.

- POST /auth/logout:
user sends request for logout, and server deletes session.

# user account only

- POST /auth/register:
user sends auth data, and server creates account with it, and creates a session.

- POST /user:
user sends personal data to server, and server checks for session and saves the data with current user.

- PUT /user:
user sends data changes to server, and server checks for session and updates current user data.

- GET /user:
server checks user session and only sends back the data and cvlist of the current user.

- POST /user/generate/-template-id-:
user sends template id to server, and server puts user data unto the selected template. then it uploads to file server, and puts the link in user cvlist.

- GET /templates:
get a list of template previews to show user.

# company accounts only

- GET /company:
server returns the info of the company account.

- GET /company/users:
server checks company permissions and sends back the users that match it.

# admin accounts only

- GET /admin/accounts:
server returns all accounts data (users and companies) to admin.

- POST /admin/companies:
admin sends company data and permissions to create a new company account.

- PUT /admin/companies/-id-:
admin sends changed permissions to update company acccount.

- DELETE /admin/companies/-id-:
admin requests for company account deletion.
```
