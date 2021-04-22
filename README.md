# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Session timeouts, if any, for the server containing telemetrics in a csv file
3. Threshold for the count of breaches in a month
4. PDF reporting details - day of the week when this report needs to be stored
5. Notification details - receiver details (email or text messages)
6. Maximum storage capacity of the server for storing the PDF reports

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This plugin is used to convert csv to pdf
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is a major part of the software being developed
Notification utility        | Yes           | This is a major part of the software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data

3. Write "Access denied" to the PDF when the there is no access to the server containing the file
4. Write "Session ended" when the session to the server ended intermittently
5. Write "File Not Found" to the PDF when the csv file is not available in the server
6. Calculate "Count of breaches" when the threshold limit is exceeded
7. Write "Count of breaches" to the PDF when the threshold limit is exceeded
8. Write "Date and time" along with the "breach detected" message to the PDF when the reading was continuously increasing for 30 mins
9. Print "Notified trend" when the notification is sent
10. Print "Notification details not found" when the email and mobile number details are not found
11. Print "Notify Failed" when there is a failure in sending notification
10. Print "Storage Full" when the storage memory of the server reaches 95%


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input            | Output                      | Faked/mocked part
|--------------------------|------------------|-----------------------------|-----------------------------
Read input from server     | csv file         | internal data-structure     | Fake the server store
Validate input             | csv data         | valid / invalid             | None - it's a pure function
Notify report availability | PDF file         | Email sent for notification | Fake email notification
Report inaccessible server | Access to server | PDF with Access Denied msg  | Fake PDF generation
Find minimum and maximum   | csv file         | minimum / maximum           | None - it's a pure function
Detect trend               | PDF file         | Trend info with date & time | None - it's a pure function
Write to PDF               | csv file         | PDF File                    | Mock PDF file generation
