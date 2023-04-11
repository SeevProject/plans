## **Plans**

### **Summary**

SeeV as a project will be an app for users to make their CVs easily, a data collection to use to market products, and a platform for companies to hire people based on their skills.

Users, will create an account, enter their personal data through a form, choose CV templates (for their data) then download or share it. Their data will be sent back to our servers. All this in a slick mobile app.

We, have a web dashboard that accesses the data of all our users stored in the servers, and provides the ability to search and target groups, for marketing purposes (i.e. finding people likely to buy a course based on their skills). And we will have extensive data visualization and analysis. It will also list all company accounts, create and delete them, and let us update their permissions.

Companies, will have access to a web app, create an account, and get (permission based) access to CVs of the users to hire as employees. They can filter and search the data completely.

### **Interfaces**

Mobile App **(Flutter)**:

- First time:
- Let user create account.
- Send account info to server.
- Receive auth status from server and login user.
- Get user data using form.
- Send user data to server.
- Let user choose template for generating cv from data.
- Send request to server for putting user data unto selected template.
- Let user see list of generated cv files (cvlist).
- Let user view file or download file.
- Second time:
- Let user login.
- Send login data to server.
- Receive auth status from server and login user.
- Let user see their data.
- Let user be able to update the data.
- Let user see list of generated cv files (cvlist).
- Let user manage account.

Web Admin Dashboard **(React + React Query + Component Library)**:

- Let admin auth.
- Receive all user acounts' data from the server.
- Display all the data, visualized.
- Let admin filter and sort through the data.
- Receive all company accounts' data.
- Let admin create company accounts.
- Let admin change company account permissions.

Web App Employee Finder **(React + React Query + Component Library)**:

- Let company auth.
- Receive user accounts data according to company permissions.
- Let company filter and sort through the data.
- Let company download from cvlist of user.

### **Services**

- Auth solution for all authentication needs. **(Backend, Pocketbase Auth, Auth0, JWT)**
- Backend API for responding to dashboard, employee finder, and mobile app. **(Pocketbase Backend, NodeTS on Railway)**
- Database for storing user data and cvlist. **(Railway PostgreSQL, Pocketbase DB, MongoDB, Planetscale)**
- Server process to merge user data and template (cv generation). **(docxtemplater library)**
- File hosting for CV templates and generated CVs, with links in database. **(S3, Pocketbase File Server)**

- Configuration Zero:
  - Backend Functions: Firebase Cloud Functions.
  - DB: Firebase Database.
  - Auth: Firebase Auth.
  - File: Firebase File Storage.
- Configuration One:
  - Backend Functions: NodeJS - Railway hosting.
  - DB: Planetscale/Mongo
  - Auth: Custom, integrated to DB.
  - File: ?
- Configuration Two:
  - Backend Functions: ?
  - DB: Pocketbase - Linode hosting.
  - Auth: Pocketbase - Linode hosting.
  - File: Pocketbase - Linode hosting.

### **Endpoints**

The server endpoints for the frontends to connnect to.

```yaml
# all accounts

- POST /auth/register: # user accounts only
user sends auth data, and server creates account with it, and creates a session.

- POST /auth/login:
user sends auth data, and server tries to find user with said data, and creates a session.

- POST /auth/logout:
user sends request for logout, and server deletes session.

# user account only

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

### **Database**

The schema of the data stored in the database.

```typescript
interface account {
  username: string;
  auth: string;
  type: "admin" | "user" | "company";
}

interface user extends account {
  data: {
    name: {
      first: string;
      middle: string;
      last: string;
    };
    phone: string;
    email: string;
    picture: string;
    status: {
      employed: boolean;
      student: boolean;
    };
    about: string;
    address: {
      country: string;
      city: string;
      street: string;
    };
    languages: {
      name: string;
      level: string;
    }[];
    education: {
      facility: string;
      location: string;
      degree_level: string;
      degree_field: string;
      date_start: string;
      date_end: string;
    }[];
    courses: {
      title: string;
      about: string;
      subjects: string[];
      location: string;
    }[];
    skills: {
      name: string;
      about: string;
      level: number;
    }[];
    hobbies: {
      name: string;
      about: string;
    }[];
  };

  cvlist: string[];
}

interface company extends account {
  permissions: {
    contact: boolean;
    status: {
      employed: boolean;
      student: boolean;
    };
    languages: {
      name: string;
    }[];
    skills: {
      name: string;
      level: number;
    }[];
    courses: {
      subjects: string[];
    };
    education: {
      facility: string;
      degree_level: string[];
      degree_field: string[];
    };
  }[];
}

interface template {
  link: string;
  fields: {}[];
  preview: string;
}
```
