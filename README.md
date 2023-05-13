## **Plans**

### Summary

SeeV as a project will be an app for users to make their CVs easily, a data collection to use to market products, and a platform for companies to hire people based on their skills.

Users, will create an account, enter their personal data through a form, choose CV templates (for their data) then download or share it. Their data will be sent back to our servers. All this in a slick mobile app.

We, have a webapp accesses the data of all our users stored in the servers, and provides the ability to search and target groups, for marketing purposes (i.e. finding people likely to buy a course based on their skills). And we will have extensive data visualization and analysis. It will also list all company accounts, create and delete them, and let us update their permissions.

Companies, will have access to a the same web app, with less permissions, create an account, and get (permission based) access to CVs of the users to hire as employees. They can filter and search the data completely.

### Timeline

Start

- All - done setup
- Backend DB - connection and schema setup
- Backend Auth - working login/register/logout
- Backend Router - dummy data serving
- Backend Auth - integrated with router and allow based on user type
- Frontend Auth - connected to backend

May 4

- Mobile UI - 1/4 pages recreated
- Frontend Setup - most libraries needed installed
- Frontend UI - layouts recreated roughly
- Backend API - prototype cv generation ready

May 18

- Mobile UI - 3/4 pages recreated
- Frontend UI - all pages recreated (without data tables)
- Frontend Auth - router integrated with auth
- Backend API - all routes integrated with DB
- Backend API - file upload working
- Backend API - cv generation fully ready

June 1

- Frontend UI - menus recreated
- Frontend Data - data fetching from backend api
- Mobile UI - all pages recreated
- Mobile State - form state is saved
- Backend API - data validation added for routes with request data

June 15

- Frontend UI - data tables to display data
- Frontend Data/UI - all items editable for admin user
- Mobile Data - fetching from server and posting to server
- Mobile Logic - opening links / saving for cv
- Mobile Logic - compare user data to template

June 29

July 13


### Design Guidelines

1. [Web Design File](https://www.figma.com/file/R4vNqDJTtonLSxh9BRptIa/SeeV-Web?node-id=0%3A1&t=OmlKqHA49Mxzhxtf-1)
2. [Mobile Design File](https://www.figma.com/file/XRUjaHcrwJBJSu42xELiCT/SeeV-Mobile?node-id=0%3A1&t=mjbutj7zsYhJaOin-1)

Accents

![#primary](https://placehold.co/120x65/1C7FFC/black?text=Primary)
![#secondary](https://placehold.co/120x65/FC991C/black?text=Secondary)

=== `1C7FFC` ====== `FC991C` ===

![#bg](https://placehold.co/120x65/FAFAFA/black?text=Background)
![#bgAlt](https://placehold.co/120x65/EBEBEB/black?text=Boxes)
![#border](https://placehold.co/120x65/C3C3C3/black?text=Border)
![#fgAlt](https://placehold.co/120x65/676767/white?text=LightText)
![#fg](https://placehold.co/120x65/232022/white?text=Text)

=== `FAFAFA` ====== `EBEBEB` ====== `C3C3C3` ====== `676767` ====== `232022` ===

### Interfaces' flow

Mobile App **(Flutter)**:

- First time:
- Let user create account with oauth, getting a token.
- Send token back to server.
- Receive session cookie from server and login user.
- Get all user data using form.
- Send all user data to server.
- Let user choose template for generating cv from data.
- Send request to server for putting user data unto selected template.
- Let user see list of generated cv files (cvlist).
- Let user view file or download file.
- Second time:
- Let user login with oauth, getting a token.
- Send token back to server.
- Receive session cookie from server and login user.
- Let user see their data.
- Let user be able to update the data.
- Let user see list of generated cv files (cvlist).
- Let user manage account.

Web App **(React + Tailwind + React Query + Tanstack Table + React Icons + React Router)**:

- Let user login using oauth, getting a token.
- Send token back to server.
- Receive session cookie from server and login user.
- if admin:
- Receive all user acounts' data from the server.
- Display all the data, visualized.
- Let admin filter and sort through the data.
- Receive all company accounts' data.
- Let admin create company accounts.
- Let admin change company account permissions.
- Receive all templates.
- Let admin create templates.
- Let admin change templates.
- if company:
- Receive user accounts data according to company permissions.
- Let company filter and sort through the data.
- Let company download from cvlist of user.

Static Page **(Astro + Tailwind)**

- Show project info

### Services Configuration

- Auth: authentication provider - FirebaseAuth
- Backend: api and cv generation - Node on Railway
- Database: storing data - Mongo on Railway
- File Storage: storing templates, cv, and images - Firebase Storage

### API Endpoints

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
- GET /users: # admins, companies
  Get a list of all user accounts or only specific users if company.

- GET /templates: # users
  Get a list of available resume templates.
- PUT /templates/:id: # admins
  Update a template.
- DELETE /templates/:id: # admins
  Delete a template.
- POST /templates/:id: # users
  Generate a resume using the specified template and the user's profile information.
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

### Database Schema

The schema of the data stored in the database.

```typescript
interface account {
	username: string;
	auth: string;
	type: "admin" | "user" | "company";
	createdAt: date;
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
			date_start: string;
			date_end: string;
			subjects: string[];
			organizer: string;
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
	fields: {
		title: string;
		char_limit: number;
	}[];
	preview: string;
}
```
