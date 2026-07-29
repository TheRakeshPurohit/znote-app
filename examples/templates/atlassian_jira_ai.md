# 🎫 Spin Up Jira Stories

This note shows **2 simple ways** to create Jira stories with AI:

- 📝 **Case 1**: create a story from a `txt` block inside your note
- 📄 **Case 2**: create one or multiple stories from a local file using `@file:///...`

---

## 🚀 Before you start

Make sure your Jira tools are available in this note.
👉 Install the **Atlassian plugin** 🧩

You can use AI to:

- read structured content from your note
- extract user stories
- create them directly in Jira
- return the created Jira keys

💡 **Attachments support**

User stories can include attachments (images or links) written in Markdown.

Example:

```md 
![Mockup](/path/to/mockup.png)
[Spec](./spec.pdf)
```

👉 When creating the Jira issue:

- extract attachment paths from the Markdown
- pass them as an array of file paths to the tool

Example:

```js 
["/path/to/mockup.png", "./spec.pdf"]
```

---

# 1️⃣ Create a Jira Story from a text block

## Example story

```txt blockName=us_demo;
#### Summary
Demo - Create a login page

#### Description
As a user, I want to access a login page so that I can authenticate on the platform.

##### Acceptance Criteria
- Display an email field
- Display a password field
- Display a "Sign in" button
- Display an error message if credentials are invalid

##### Attachments
![Login mockup](/path/to/login.png)
```

## AI prompt

```ai tools=searchJiraIssuesUsingJql,createJiraIssue;
Read the user story from block @us_demo and create it in Jira in project WEGRC as a Story.

Use:
- the content of "Summary" as the summary
- the content of "Description" as the description

If attachments are present:
- extract file paths from Markdown images or links
- pass them as an array of file paths to the "attachments" field

Return the created Jira key.
```

---

# 2️⃣ Create Jira Stories from a local file

> 💡 The file can contain **one story or multiple stories**.

## AI prompt

```ai tools=searchJiraIssuesUsingJql,createJiraIssue;
Read the content of file @file:///path/to/file.txt and create each user story found in Jira, project WEGRC, as a Story.

For each user story:
- use the title as the summary
- use the rest of the content as the description

If attachments are present in Markdown:
- extract file paths from images or links
- pass them as an array of file paths to the tool

At the end, return the list of created Jira tickets.
```

---

# ✅ Example file format

Here is an example of what `/path/to/file.txt` could look like:

```txt 
#### Summary
Demo - Reset password

#### Description
As a user, I want to reset my password so that I can regain access to my account.

##### Acceptance Criteria
- Enter email address
- Receive a reset link by email
- Set a new password

##### Attachments
![Flow](/path/to/reset.png)

---
#### Summary
Demo - View user profile

#### Description
As a logged-in user, I want to view my profile so that I can check my personal information.

##### Acceptance Criteria
- View first and last name
- View account email
- View saved preferences

##### Attachments
[Profile spec](./profile.pdf)
```

---

# 🧠 Tip

You can adapt the AI prompt to:

- create **Stories**, **Tasks**, or **Bugs**
- create tickets in another Jira project
- enrich descriptions before publishing
- validate or rewrite the content with AI before sending it to Jira

👉 This makes it easy to go from **draft note → structured Jira tickets with attachments**

---

# 🛠️ Available Jira Tools

| Tool                       | Parameters                                                  | Description                        | 
|----------------------------|-------------------------------------------------------------|------------------------------------| 
| `getJiraIssue`             | `issueIdOrKey`                                              | Fetch a single issue by key        | 
| `searchJiraIssuesUsingJql` | `jql`                                                       | Search issues with a JQL query     | 
| `getVisibleJiraProjects`   | `maxResults`                                                | List accessible projects           | 
| `createJiraIssue`          | `projectKey, summary, description, issueType, attachements` | Create a new issue                 | 
| `updateJiraIssue`          | `issueIdOrKey, fields, attachements`                        | Update fields on an existing issue | 
| `addCommentToJiraIssue`    | `issueIdOrKey, comment`                                     | Add a comment to an issue          | 
| `getJiraIssueTransitions`  | `issueIdOrKey`                                              | List available status transitions  | 
| `transitionJiraIssue`      | `issueIdOrKey, transitionId`                                | Move an issue to a new status      | 

---

# 📚 More Jira Examples

## Read from Jira

```ai tools=getJiraIssue,searchJiraIssuesUsingJql,getVisibleJiraProjects;
Show me the ticket PROJ-83
```

```ai tools=searchJiraIssuesUsingJql;
List all open issues in PROJ created this week
```

```ai tools=getVisibleJiraProjects;
What projects do I have access to?
```

---

## Write to Jira

```ai tools=createJiraIssue;
Create a bug in PROJ: login page crashes on mobile
```

```ai tools=updateJiraIssue;
Update the priority of PROJ-12 to High
```

```ai tools=addCommentToJiraIssue;
Add a comment on PROJ-42: Fixed in v2.1
```

---

## Move Jira tickets

```ai tools=getJiraIssueTransitions,transitionJiraIssue;
Move PROJ-42 to Done
```

---

# ✅ What’s next?

Try adapting this note to your own workflow:

- create stories from meeting notes
- generate tasks from specifications
- turn product ideas into Jira tickets

👉 **Your note can become your Jira assistant**
