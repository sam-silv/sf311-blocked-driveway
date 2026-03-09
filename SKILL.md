---
name: sf311
description: Submit a SF311 blocked driveway complaint from photos of the offending vehicle. Use when the user wants to report a car blocking their driveway.
argument-hint: <photo1> <photo2> <photo3>
user-invocable: true
allowed-tools: Read, Bash, Agent, mcp__claude-in-chrome__*
model: opus
---

# SF311 Blocked Driveway Complaint

You are filing a blocked driveway complaint on SF311 for the user. The user has provided photos of the offending vehicle as arguments: $ARGUMENTS

## Personal Info

The following contact and address info is pre-configured. Use these values when filling the form:

- **Name**: YOUR_NAME
- **Phone**: YOUR_PHONE
- **Driveway Address**: YOUR_ADDRESS

> **IMPORTANT**: If any personal info above still says "YOUR_*", stop and ask the user to update this skill file with their real info before proceeding.

## Step 1: Analyze Photos

Read each photo file provided as arguments using the Read tool (it supports images). From the photos, extract:

1. **License plate number** — look carefully at all photos for a readable plate
2. **Vehicle make** — e.g., Honda, Toyota, BMW
3. **Vehicle model** — e.g., Civic, Camry, X3
4. **Vehicle color** — e.g., White, Black, Silver, Red
5. **Vehicle type** — e.g., "Sedan", "SUV", "Truck", "Van"

Present your findings to the user and ask them to confirm before proceeding. If the plate is partially obscured or hard to read, state your best guess and flag the uncertainty.

## Step 2: Open SF311 Form

Use browser automation tools to:

1. Call `tabs_context_mcp` with `createIfEmpty: true` to get/create a tab
2. Create a new tab with `tabs_create_mcp`
3. Navigate to: `https://sf.gov/report-blocked-driveway-or-illegal-parking`
4. Wait for the page to load, then use `read_page` to understand the form structure

## Step 3: Fill the Form

Fill in the form fields using the browser automation tools (`form_input`, `computer` click actions, etc.):

1. **Location/Address**: Enter the driveway address from personal info above
2. **Nature of Request**: Select "Blocking my driveway - cite and tow" (default — ask user if they prefer citation only)
3. **Vehicle License Plate**: Enter the plate number extracted from photos
4. **Vehicle Make**: Enter the make
5. **Vehicle Model**: Enter the model
6. **Vehicle Color**: Enter the color
7. **Vehicle Type**: Select the appropriate type
8. **Contact Name**: Enter the name from personal info
9. **Phone Number**: Enter the phone from personal info
10. **Description**: Write a brief factual description, e.g., "Vehicle with plate [PLATE] is blocking my driveway at [ADDRESS]. Vehicle is a [COLOR] [MAKE] [MODEL]."

## Step 4: Upload Photos

Upload all three photos to the form using the `upload_image` tool or file input interaction.

## Step 5: Review Before Submit

**DO NOT SUBMIT THE FORM.** Instead:

1. Take a screenshot of the completed form
2. Present a summary to the user of everything that was filled in
3. Ask the user to confirm submission
4. Only click Submit after explicit user confirmation

## Error Handling

- If the SF311 website layout has changed and you can't find expected fields, describe what you see and ask the user for guidance
- If photos are too blurry to read the plate, ask the user to provide the plate number manually
- If the browser extension is not connected, instruct the user to ensure the Claude-in-Chrome extension is running and try again
