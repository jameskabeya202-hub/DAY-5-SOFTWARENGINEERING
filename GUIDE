A) USER MANUAL PROCEDURES

You'll create a private, isolated space for a Python project (a "virtual environment"), switch it on, and install a package inside it. This keeps each project's tools separate, so installing something for one project can't break another.

Before you start
You'll need:

Python 3.8 or newer installed on your computer. If you're not sure, Step 2 will check.
A terminal. This is Command Prompt or PowerShell on Windows, or Terminal on macOS and Linux.
An internet connection, so you can download the package.
About 10 minutes and roughly 50 MB of free disk space.

Steps

1. Open your terminal.
On Windows, press the Windows key, type PowerShell, and press Enter. On macOS, press Cmd+Space, type Terminal, and press Enter.
Expected result: A window opens with a blinking cursor after a short line of text.

Screenshot 1: A terminal window just after opening. It should show an empty prompt with the cursor, and a callout arrow labelled "You'll type your commands here."

2. Check that Python is installed.
Type python --version and press Enter. (On macOS or Linux, use python3 --version.)
Expected result: The terminal prints a version, such as Python 3.12.4. Any version from 3.8 up is fine.

3. Create a folder for your project.
Type mkdir my_project and press Enter.
Expected result: Nothing is printed, and the prompt returns. That means it worked.

4. Move into the new folder.
Type cd my_project and press Enter.
Expected result: The prompt now ends with my_project, which shows you're inside the folder.

5. Create the virtual environment.
Type python -m venv venv and press Enter. (Use python3 on macOS or Linux.)
Expected result: After a few seconds, the prompt returns with no message. A new folder called venv now exists inside my_project.

6. Activate the environment.
Run the line that matches your system, then press Enter:

Windows (PowerShell): venv\Scripts\Activate.ps1
Windows (Command Prompt): venv\Scripts\activate.bat
macOS / Linux: source venv/bin/activate

Expected result: The prompt now starts with (venv).

Screenshot 2: The terminal after activation. The prompt should read (venv) C:\Users\you\my_project>, with a red box around the (venv) part and a caption: "This tells you the environment is switched on."

7. Install a package.
Type pip install requests and press Enter. We'll use requests as a friendly first example.
Expected result: Text scrolls past as it downloads, ending with Successfully installed requests-... and a few other package names.

8. Check that the install worked.
Type pip list and press Enter.
Expected result: A table appears with requests listed alongside a few other packages.

9. Switch the environment off when you're done.
Type deactivate and press Enter.
Expected result: The (venv) label disappears from the start of the prompt.

If something goes wrong

Problem: You see 'python' is not recognized as an internal or external command (Windows) or python: command not found (macOS/Linux).

Why it happens: Either Python isn't installed, or your computer doesn't know where to find it. This is the most common beginner stumble.

Fix:

On macOS or Linux, try python3 in place of python everywhere. On Windows, try py.
If that fails too, download Python from python.org and run the installer. On the first screen, tick the box that says "Add Python to PATH" before clicking Install.
Close your terminal, open a new one, and start again from Step 2.

B) API REFERENCE ENTRY
Creates a new task inside a project and returns the finished task, including the ID the system gave it. The task is added to the project's task list straight away. If you set an assignee, the system notifies them.
You must be signed in, and you must be a member of the project with permission to add tasks.

Path parameters
Name	Type	Required	Description
project_id	string	Yes	The ID of the project the task will belong to, e.g. prj_4821.
Query parameters

None.

Request headers
Header	Required	Description
Authorization	Yes	Your access token, in the form Bearer <token>.
Content-Type	Yes	Must be application/json.
Accept	No	Use application/json (the default).
Request body
Field	Type	Required	Description
title	string	Yes	A short name for the task. 1 to 150 characters.
description	string	No	More detail about what needs doing. Up to 2,000 characters. Leave it out if you don't need it.
assignee_id	string	Yes	The ID of the user responsible for the task, e.g. usr_1093. They must be a member of the project.
due_date	string	Yes	When the task is due, as a date in YYYY-MM-DD format. It can't be in the past.
priority	string	Yes	How urgent the task is. Must be exactly low, medium, or high (lowercase).
Example request
http
POST /api/v1/projects/prj_4821/tasks HTTP/1.1
Host: api.taskflow.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json
json
{
  "title": "Design onboarding email",
  "description": "Draft the welcome email new users receive after signing up. Include a link to the getting-started guide.",
  "assignee_id": "usr_1093",
  "due_date": "2026-10-30",
  "priority": "medium"
}
Response codes
Code	Name	When you'll see it
201	Created	The task was created successfully.
400	Bad Request	The request couldn't be read, usually because the JSON is malformed (a missing comma or quote, for instance).
401	Unauthorized	The token is missing, expired, or invalid.
403	Forbidden	Your token is valid, but you aren't allowed to add tasks to this project.
404	Not Found	The project doesn't exist, or the assignee_id doesn't match any user.
415	Unsupported Media Type	The Content-Type header isn't application/json.
422	Unprocessable Entity	The JSON is well-formed, but a value is wrong: a missing required field, a title that's too long, a past due date, an invalid priority, or an assignee who isn't a project member.
429	Too Many Requests	You've sent too many requests in a short time. Wait and try again.
500	Internal Server Error	Something went wrong on our end. Try again shortly, and contact support if it keeps happening.
Example successful response (201 Created)
json
{
  "id": "tsk_90317",
  "project_id": "prj_4821",
  "title": "Design onboarding email",
  "description": "Draft the welcome email new users receive after signing up. Include a link to the getting-started guide.",
  "assignee_id": "usr_1093",
  "due_date": "2026-10-30",
  "priority": "medium",
  "status": "open",
  "created_by": "usr_0457",
  "created_at": "2026-10-04T08:31:12Z"
}

New tasks always start with a status of open. The id, status, created_by, and created_at fields are set by the system, so you don't send them.

Example error response (422 Unprocessable Entity)
json
{
  "error": {
    "code": "validation_failed",
    "message": "priority must be one of: low, medium, high.",
    "field": "priority"
  }
}
