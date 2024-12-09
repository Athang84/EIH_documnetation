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
