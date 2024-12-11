# Employee Insight Hub (EIH) Documentation

**Employee Insight Hub (EIH)** provides employees and organizations with tools for managing skills, projects, feedback, and organizational insights. It is modular, with each tab representing key functionalities.

## Core Tabs
- **Match Tab**: Employee-role alignment.
- **Skills Tab**: Skill tracking and certifications.
- **Projects Tab**: Overview of projects.
- **Organization Level Tab**: Company-wide insights.
- **Feedback Tab**: Performance feedback.
- **Resumes Tab**: Resume management.
- **Notes Tab**: Personal and professional note-taking.

## File Structure
- **constants**: Application constants.
- **controllers**: API route handlers.
- **middleware**: Authentication and feature eligibility checks.
- **processors**: Request-specific processing.
- **services**: Business logic and integrations.
- **utils**: Reusable helper functions.

## Middleware
1. **Auth Middleware**: Validates `x-api-key`.
2. **Eligibility Middleware**: Checks user and feature eligibility.

Details for each tab are provided in the following sections.

## Match Tab

The User Match Score Tab Service processes requests for fetching the match score details of a user profile against a job profile. The functionality involves:

* Fetching and comparing user skills, certifications, and specializations.
* Calculating match scores based on designation, experience, location, and allocation.
* Returning a detailed breakdown of match results.

### Controller

The controller handles incoming requests, interacts with the processor, and returns the response.

* Method: getUserMatchScoreDetails
  * Purpose: Fetches match score details for a user based on profile and job requirements.
  * Parameters:
    * req (Object): HTTP request containing userId and profileId.
    * res (Object): HTTP response object.
   
### Processor

The processor performs the core logic of fetching and calculating match scores.

* Retrieves user data, job profile data, and configurations.
* Processes multiple matching criteria such as skills, certifications, designations, and availability.
* Returns a structured response containing match scores.

### Utility

Provides helper functions for:

* Generating formatted responses.
* Calculating user experience.
* Validating and extracting expected fields.

### Request and Response Formats

#### API Endpoint
Request and Response Formats

#### Request
**Header**
```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer <your-jwt-token>"
}
```

**Body**
```json
{
  "userId": "12345",
  "profileId": "67890"
}
```

#### Response

**Succesful Response**
```json
{
  "status": true,
  "data": {
    "mandatorySkill": [...],
    "optionalSkill": [...],
    "designation": [...],
    "experience": [...],
    "certification": [...],
    "specialization": [...],
    "location": [...],
    "availabilityDate": [...],
    "allocationStatus": [...],
    "competencyPercent": 85,
    "availability": "High"
  }
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Invalid profileId"
}
```
## Skills Tab

The Skills Tab Service retrieves details about a user's skills, certifications, and specializations. Key functionalities include:

* Fetching user-specific skill data, including endorsements, ratings, and last used details.
* Retrieving active certifications and their associated skills.
* Sorting and structuring the data for optimized usage.

### Controller

* Method: getEihUserSkillsAndCertificationsAndSpecialization
 * Purpose: Fetch skills, certifications, and specialization data for a user.
 * Request Parameters:
  * userId (String): The user's unique identifier.
 * Response:
  * Returns structured data containing skills, certifications, and specializations.
    
### Processor

Method: getEihUserSkillsAndCertificationsAndSpecialization
* Fetches and processes data from multiple sources.
* Sorts skills based on rating, experience, and last usage.
* Filters and structures certifications and specializations.

### API Details

#### Endpoint
GET /:userId/getMySkills

#### Request 
**parameters**
userId (String)

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": {
    "skillCategories": [...],
    "skillItems": [...],
    "certifications": [...],
    "specializations": [...],
    "lastSkillUpdatedOn": "2024-12-01T10:00:00Z"
  }
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Error fetching skills data."
}
```

## Projects Tab

### Controller
Function: getUsersProjects
Description:
Handles requests to fetch a user's project data.

* Calls the processor function getUserProject to fetch and process project details.

### Processor
* Method: getUserProjects
 * Fetches and processes:
  * User's basic allocation details (bench ageing, availability, pool code).
  * Project allocations grouped into past, current, and future.
  * Skills used in each project

### API Detials

#### Endpoint
GET /:userId/getUserProjects

#### Request
**parameters**
userId (String)

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": {
    "basicEmpDetails": {
      "benchAgeing": 30,
      "availableFrom": "2024-12-15",
      "candidateAllocationPoolCode": "ACTIVE",
      "candidateAllocationName": "Engineering",
      "candidateMultiAllocationStatus": "Single",
      "candidateIsSearchableAllocationPool": "Yes"
    },
    "allocations": {
      "past": [
        {
          "candidateAllocationStartDate": "2023-01-01",
          "candidateAllocationEndDate": "2023-12-01",
          "candidateProjectName": "Project A",
          "candidateProjectId": "P123",
          "candidateCustomerId": "C001",
          "candidateCustomerName": "Customer X",
          "candidateAllocationPercentage": 100,
          "skillsUsed": ["Java", "Spring Boot"]
        }
      ],
      "current": [
        {
          "candidateAllocationStartDate": "2023-12-02",
          "candidateAllocationEndDate": "2024-12-01",
          "candidateProjectName": "Project B",
          "candidateProjectId": "P124",
          "candidateCustomerId": "C002",
          "candidateCustomerName": "Customer Y",
          "candidateAllocationPercentage": 50,
          "skillsUsed": ["Python", "Django"]
        }
      ],
      "future": [
        {
          "candidateAllocationStartDate": "2025-01-01",
          "candidateAllocationEndDate": "2025-12-01",
          "candidateProjectName": "Project C",
          "candidateProjectId": "P125",
          "candidateCustomerId": "C003",
          "candidateCustomerName": "Customer Z",
          "candidateAllocationPercentage": 75,
          "skillsUsed": ["React", "Node.js"]
        }
      ]
    }
  }
}

```

**Error Response**
```json
{
  "status": false,
  "message": "Error fetching project data."
}
```


## Organization Level Tab

The Organization Level Tab Service provides hierarchical organization details for a user, including their reporting structure and reportees. It also includes configurable organizational overview information based on user data.

### Controller: orgLevelTabController.js
* Method: getOrgLevelDetails
 * Purpose: Handles incoming requests to retrieve organization-level details for the user.
 * Error Handling: Logs errors and returns appropriate HTTP status codes and messages.

### Processor: orgLevelTabProcessor.js
* Method: getOrgLevelDetails
 * Retrieves:
  * Organizational overview information for the user based on configurable fields.
  * Hierarchical structure, including reporting managers and reportees.

### API Details

#### Endpoint
GET /:userId/getOrgLevelDetails

#### Request
**parameters**
userId (String)

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": {
    "orgOverviewInfo": {
      "department": "Engineering",
      "position": "Senior Developer",
      "location": "New York",
      "joiningDate": "2020-01-15"
    },
    "orgChart": {
      "reportingToList": [
        {
          "name": "John Doe",
          "src": "https://example.com/profiles/john.jpg",
          "designation": "Manager",
          "empId": "E12345"
        }
      ],
      "currentUserInfo": {
        "name": "Jane Smith",
        "src": "https://example.com/profiles/jane.jpg",
        "designation": "Senior Developer",
        "empId": "E54321"
      },
      "reporteesList": [
        {
          "name": "Alice Brown",
          "src": "https://example.com/profiles/alice.jpg",
          "designation": "Junior Developer",
          "empId": "E67890"
        }
      ]
    }
  }
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Error fetching organization-level details."
}
```

## Feedback Tab

### Controller: userFeedbackController.js
* Method: getUserFeedbacks
 * Purpose: Handles incoming requests to retrieve feedback data for the user.
 * Error Handling: Logs errors and returns appropriate HTTP status codes and messages.

### Processor: userFeedbackProcessor.js
* Method: getUserFeedbacks
 * Fetches:
  * Feedback for selected and rejected candidates from the database.
  * Candidate status and historical data to generate detailed feedback.
    
### API Details

#### Endpoint
GET /:userId/getUserFeedbacks

#### Request
**parameters**
userId (String)

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": [
    {
      "name": "Feedback for Job Profile A",
      "type": "Selection",
      "date": "2024-01-15T12:30:00Z",
      "candidateOverallRating": 4.5,
      "reason": "Excellent performance in technical skills",
      "internalFeedback": "Candidate showed great potential.",
      "clientFeedback": "Highly recommended.",
      "candidateImprovementSectors": ["Communication Skills"],
      "additionalFeedback": "Needs improvement in time management.",
      "evaluationDoneBy": "John Doe",
      "skillsEvaluatedOn": ["Java (4/5)", "SQL (5/5)"]
    }
  ]
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Error fetching feedback details."
}
```

## Resumes Tab

The Resumes Tab Service allows users to view and manage their resumes, including those uploaded manually and generated from their profiles. It fetches resume details, sorts them by the latest update date, and provides pre-signed URLs for secure access to resume files.

### Controller: userResumesController.js
Method: getUserResume
* Purpose: Handles incoming requests to retrieve resume details for a user.
* Error Handling: Logs errors and returns appropriate HTTP status codes and messages.

### Processor: userResumeProcessor.js
Method: getUserResume
* Fetches:
`* Resumes uploaded by the user.
 * Resumes generated from user profiles.

### API Details

#### Endpoint
GET /:userId/getUserResume

#### Request
**parameters**
userId (String)

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": [
    {
      "name": "John_Doe_Resume.pdf",
      "loc": "https://example-bucket.s3.amazonaws.com/John_Doe_Resume.pdf?AWSAccessKeyId=...&Expires=...",
      "source": "Uploaded by User",
      "dt": "2024-01-15T12:30:00Z"
    },
    {
      "name": "Generated_Resume_Profile_A.pdf",
      "loc": "https://example-bucket.s3.amazonaws.com/Generated_Resume_Profile_A.pdf?AWSAccessKeyId=...&Expires=...",
      "source": "Built from Profile",
      "dt": "2024-01-10T09:15:00Z"
    }
  ]
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Error fetching resume details."
}
```

## Notes Tab

The Notes Tab Service manages candidate-related notes, including creation, retrieval, deletion, restoration, and attachments. It ensures secure handling of notes and adheres to user roles and permissions.

### Controller: userNotesController.js
Methods:
* createUserNotes
 * Handles the creation of new notes.
* getUserNotes
 * Retrieves notes based on the candidate and publishing type.
* deleteUserNotes
 * Deletes a note by its ID.
* undoUserNotes
 * Restores a deleted note.
* addAttachmentToUserNotes
 * Adds attachments to an existing note.

### Processor: userNotesProcessor.js
Methods:
* createUserNotes
 * Saves a note using the saveNote service.
 * Validates role and permissions before saving.
* getUserNotes
 * Fetches notes for a candidate.
 * Includes details like deletion status and modifier info.
* deleteUserNotes
 * Deletes a note by calling the removeNote service.
* undoUserNotes
 * Restores a deleted note using the reviveNote service.
* addAttachmentToUserNotes
 * Attaches files to a note.

   
### API Details

#### Endpoint
POST /notes/:noteId/addAttachment

#### Request
**parameters**
userId (String)

**Request Body**
```json
{
  "title": "Follow-up Meeting",
  "content": "Discuss progress with the candidate.",
  "publishType": "Private",
  "attachments": ["file1.pdf", "file2.png"]
}
```

#### Response
**Succesful Response**
```json
{
  "status": true,
  "data": {
    "noteId": "12345",
    "title": "Follow-up Meeting",
    "content": "Discuss progress with the candidate.",
    "publishType": "Private",
    "createdBy": "John Doe",
    "createdDate": "2024-12-10T14:00:00Z"
  }
}
```

**Error Response**
```json
{
  "status": false,
  "message": "Error occurred while processing the request."
}
```
