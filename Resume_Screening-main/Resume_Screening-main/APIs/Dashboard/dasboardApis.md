## 1. Get User Dashboard (GET)

Retrieves the authenticated user's dashboard statistics.

Endpoint: /auth/dashboard

Method: GET

Auth Required: Yes (JWT)

Request Headers

| Field         | Type   | Required | Description                                      |
| :------------ | :----- | :------- | :----------------------------------------------- |
| Authorization | String | Yes      |<your_jwt_token>` |


### Response

**Success (200 OK):**

```json
{
  "status": "success",
  "message": "Dashboard data retrieved successfully",
  "data": {
    "user": {
      "userId": "usr_987654321",
      "fullName": "Jane Doe",
      "email": "jane.doe@example.com"
    }
  }
}
```

**Error (401 Unauthorized):**  
*Occurs when the token is missing or incorrectly formatted.*

```json
{
  "status": "error",
  "message": "Unauthorized access. Please provide a valid token."
}
```

**Error (403 Forbidden):**  
*Occurs when the token is expired or invalid.*

```json
{
  "status": "error",
  "message": "Token has expired. Please login again."
}
```

---
## 2. Fetch Posted Jobs (GET)
Retrieves a list of available jobs. 

*   **Endpoint:** `/postedJobs`
*   **Method:** `GET`
*   **Auth Required:** Yes (JWT)

#### Request Headers
| Field | Value | Description |
| :--- | :--- | :--- |
| **Authorization** | `JWT` | The token received from the Login API. |
||


#### Response
**Success (200 OK):**
```json
{
  "status": "success",
  "message": "Jobs retrieved successfully",
  "data": [
    {
      "jobId": "job_001",
      "title": "Software Engineer",
      "Must have skill": "Java, springBoot",
      "applicants": "214",
      "shortlisted": "24",
      "postedDate": "2023-10-25"
    },
    {
      "jobId": "job_002",
      "title": "Product Designer",
      "Must have skill": "Java, springBoot",
      "applicants": "214",
      "shortlisted": "24",
      "postedDate": "2023-10-24"
    }
    .
    .
    .
    .
    .
    .
    .
    .
    .
    .
  ]
}
```

**Error (401 Unauthorized):**
*Occurs if the token is missing, expired, or invalid.*
```json
{
  "status": "error",
  "message": "Unauthorized access. Please login again."
}
```
---
## 3. Fetch Posted Jobs with Filter (GET)

Retrieves a list of available jobs. When a user selects a department from the dropdown menu.

*   **Endpoint:** `/postedJobs/:department`
*   **Method:** `GET`
*   **Auth Required:** Yes (JWT)

#### **Query Parameters**
| Field | Type | Description |
| :--- | :--- | :--- |
| `department` | `string` | **(Optional)** When a user selects a department from the dropdown, it is passed as a parameter (e.g., Engineering, Design, HR). If no department is selected, all jobs are returned. |

#### **Request Headers**
| Field | Value | Description |
| :--- | :--- | :--- |
| `Authorization` | `Bearer <JWT_TOKEN>` | The token received from the Login API. |
| `Content-Type` | `application/json` | Standard JSON header. |

#### **Example Request URL**
`GET /jobs?department=Engineering`

---

#### **Response**

**Success (200 OK):**
```json
{
  "status": "success",
  "message": "Jobs retrieved successfully",
  "departmentSelected": "Engineering",
  "data": [
    {
      "jobId": "job_001",
      "title": "Backend Developer",
      "department": "Engineering",
      "applicants": "150",
      "shortlisted": "15",
      "postedDate": "2023-11-01"
    },
    {
      "jobId": "job_005",
      "title": "Frontend Engineer",
      "department": "Engineering",
      "applicants": "98",
      "shortlisted": "10",
      "postedDate": "2023-11-05"
    }
  ]
}
```

**Error (401 Unauthorized):**
Occurs if the token is missing, expired, or invalid.
```json
{
  "status": "error",
  "message": "Unauthorized access. Please login again."
}
```

**Error (404 Not Found):**
Occurs if no jobs exist for the selected department.
```json
{
  "status": "error",
  "message": "No jobs found for the selected department."
}
```
---

Got it! Here is the clean, professional English documentation and implementation for the **Job Post Access API**.

---

## 4. Job Post (GET)

This API verifies if the user and redirect  to the "Job Post" page.

*   **Endpoint:** `/jobPost`
*   **Method:** `GET`
*   **Auth Required:** Yes (JWT)

### Request Headers

| Field         | Type   | Required | Description                                      |
| :------------ | :----- | :------- | :----------------------------------------------- |
| Authorization | String | Yes      | ` <your_jwt_token>`                        |

---

### Response

**Success (200 OK):**  
*The token is valid. The frontend can now redirect the user to the "Job Post" page.*

```json
{
  "status": "success",
  "message": "TAccessing Job Post page...",
  "access": true
}
```

**Error (401 Unauthorized):**  
*The token is invalid or has expired. Redirect the user to the login page.*

```json
{
  "status": "error",
  "message": "Unauthorized access.",
  "access": false
}
```

---