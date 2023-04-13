## **Database Schema**

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
	fields: {
		title: string;
		char_limit: number;
	}[];
	preview: string;
}
```
