# hireme-server

## Running

```bash
     $ mvn spring-boot:run
```

By default, it will run on port 5000. And use MySQL Database on `178.128.170.25:3306`.
You can change it in [application.properties](src/main/resources/application.properties) file

## API specification

### Authorization

`/api/auth`

| Method | Path           | Request                                                   | Response                   | Protected |
| :----: | :------------- | --------------------------------------------------------- | -------------------------- | :-------: |
|  POST  | `/auth/signin` | RequestBody: <br> `{usernameOrEmail, password}`           | `{accessToken, tokenType}` |     No    |
|  POST  | `/auth/signup` | RequestBody: <br> `{fullname, username, email, password}` | `{success, message}`       |     No    |

### User

`/api/user`, `/api/users`

| Method | Path                              | Request                        | Response               | Protected |
| :----: | :-------------------------------- | ------------------------------ | ---------------------- | :-------: |
|   GET  | `/user/me`                        | --                             | `{username, fullname}` |    Yes    |
|  POST  | `/user/me`                        | RequestBody: <br>_UserInfo_    | `{success, message}`   |    Yes    |
|   GET  | `/user/checkUsernameAvailability` | RequestParam: <br>`{username}` | `{isAvailable}`        |     No    |
|   GET  | `/user/checkEmailAvailability`    | RequestParam: <br>`{email}`    | `{isAvailable}`        |     No    |
|   GET  | `/users/{username}`               | PathVariable: <br>`{username}` | _UserInfo_             |     No    |

### Company

`/api/company`

| Method | Path              | Request                             | Response                 | Protected |
| :----: | :---------------- | ----------------------------------- | ------------------------ | :-------: |
|  POST  | `/company`        | RequestBody: <br>_CompanyInfo_      | `{success, message, id}` |    Yes    |
|   GET  | `/companies/{id}` | PathVariable: <br>`{id}`            | _CompanyInfo_            |     No    |
|   GET  | `/companies/find` | RequestBody: <br>`{name, location}` | _CompanyInfo_            |     No    |

```js
UserInfo = {
  username,             // Only in response
  fullname,
  location,
  employment: {         // Optional
    position,
    company
  },
  current_role,         // SE, designer, marketing, sales, management, other
  education: {          // Optional
    university,         // name,              'Nazarbayev University'
    graduation_year,    // graduation year    2020
    graduation_month,   // graduation month   'June'
    major,              //                    'Computer Science'
    degree,             // Bachelor, Master, PhD
  },
  hidden,               // Show in search     true
  job_type,             // Full-time/Part-time/Contractor/Intern
  job_field,            // [Frontend dev, backend dev, web dev, mobile]
  skills,               // [react, spring, kotlin, java, tensorflow]
  createdAt,            // Date when entry was created
}

CompanyInfo = {
  id,                   // Only in response
  name,                 // Google
  creator: {
    username,           // m_nny
    role                // Founder/HR/Team leader
  },
  logo_url,             // https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png
  location,             // Astana, Kazakhstan
  employee_number,      // 100+
  specialization,       // Search Engine
  description,           // Best search engine in the world
  createdAt,            // Date when entry was created
}
```
