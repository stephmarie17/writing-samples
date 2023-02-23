# Technical Writing Samples

## Netlify Email Integration
**This is a sample from documentation that I wrote for the [Netlify Email Integration](https://docs.netlify.com/integrations/email-integration/). This section describes how to use the add attachment feature of the Integration.**

### Add attachments to your email
When sending messages, you can also specify any files you’d like to attach. Using the snippet generated during the [email preview](https://docs.netlify.com/integrations/email-integration/#preview-email-templates), add the `attachments` property to the request `body`. The `attachments` property is an array that may contain three properties to attach your file: `content`, `filename`, and `type`.

| Property Name | Type     | Description                                         | Required |
| ------------- | -------- | --------------------------------------------------- | -------- |
| `content`     | `string` | Base64 encoded string of the file                   | Yes      |
| `filename`    | `string` | The name of the file as it will appear in the email | Yes      |
| `type`        | `string` | the MIME type of content you’re attaching           | Yes      |

For example, the following handler function parses a `.pdf` file saved in an assets folder in the project. Nested in the body object is an `attachments` array that lists the `content`, `filename`, and `type` properties for that file.

```tsx
import { Handler } from "@netlify/functions";
import fetch from “node-fetch”;
import fs from “fs”;

const handler: Handler = async () => {
  const file = fs.readFileSync(“./assets/example.pdf”).toString(“base64”);
  const response = await fetch(
    `${process.env.URL}/.netlify/functions/emails/forgotten-password`,
    {
      headers: {
        “netlify-emails-secret”: process.env.NETLIFY_EMAILS_SECRET, 
      },
      method: “POST”,
      body: JSON.stringify({
        from: “sender@myemailsender.com”,
        cc: “recipient@youremail.com”,
        to: “recipient@youremail.com”,
        subject: “Password Reset”,
        attachments: [
	        {
            content: file,
            filename: “example.pdf”,
            type: “pdf”,
          }
        ],
        parameters: {
          name: "Test",
        } 
      })
    }
  );

  const responseBody = await response.json();

  return (
    statusCode: response.status,
    body: JSON.stringify(responseBody)
  );
};

export { handler };

```
Refer to your email provider's documentation to verify which types of content are valid. 

## Twilio Platform Advanced
**A hands-on course with a demo application developed for the Twilio Build Partner Community to teach advanced Voice and Messaging API features.**

### Intro
This project was created in collaboration with one of my team members at Twilio’s Center of Excellence. On this team, I crafted technical training courses for Partner Enablement. Twilio Platform Certification was a requirement for Twilio Partners to complete; this course was the next step in their learning journey to implement advanced API features. To create this course, I learned the usage of Twilo’s Voice and Messaging APIs, with a focus on Messaging to create a sample voicemail system that triggered automatic SMS alerts to the voicemail owner whenever a new one was received. 

The key features this app highlighted were:
- Recording messages and deleting recordings
- Creating transcriptions of voicemail recordings and deleting transcriptions
- Sending automated SMS alerts
- Scheduling SMS alerts
- Utilizing Messaging Insights via the Twilio Console

### Course preview
Here, the learner is provided the starter code for a voicemail application to review the project structure. From here, the learner is introduced to incorporating SMS functionality into the app, by sending an SMS alert when a new voicemail is received in the mailbox.
![Sending SMS alerts](/assets/sms_app_example_edit.png)


In this example from the course, I've included two code snippets that I wrote to demonstrate how to include the necessary parameters for the SMS API. In addition to writing these snippets, I styled them in order to be embedded into the Rise course with proper colors and indentations for readability. 
![Code snippets](/assets/sms_app_example2_edit.png)

### Resources
To view the starter code that learners utilized for this course, access the GitHub repository [here](https://github.com/TwilioTraining/platform-advanced-voice). Note: only the starter code is available for me to share; the detailed course with additional code snippets are proprietary to the Twilio Build Community.

## Twilio Console Overview
**Technical training course developed for [twiliotraining.com](https://www.twiliotraining.com/store).**

### Intro
I developed this course using Articulate360 - Rise as an update to an existing version created by another team member. The Twilio Console is the web-based interface for utilizing Twilio products and APIs; the 2.0 version launched to the public in 2021. This course update was designed in order to incorporate the latest changes to the Console. The intended audience for the course are developers, administrators, and support teams. The process for this update included: meeting with the product SME, auditing the existing course and identifying and correcting errors, creating new content for additional course modules, editing the course, and deploying to the appropriate learning management systems.

Below, explore an outline of this course.

### Learning objectives
I developed the learning objectives for this course based upon instructional design best practices.
![Learning objectives](/assets/console_01_edit.png)

### Navigation and site tour
This section breaks down the key sections of the updated Console interface, and includes an interactive heatmap for a  self-guided tour of the application.
![Navigation and site tour](/assets/console_02_edit.png)

### Account quickstart
In this module, I created a step-by-step quickstart guide for upgrading Trial Console accounts to Paid Console accounts. 
![Quickstart](/assets/console_03_edit.png)

### Video tour
In this section, I collaborated with another technical writer on the team to write a script for a video tour (developed in Storyline) of the Console including:
- Locating Account SIDs and Auth Tokens
- Monitoring API insights
- Setting up billing accounts
- Customizing the developer toolbar
- Accessing and submitting support requests

![Video tour](/assets/console_04_edit.png)







