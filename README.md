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


