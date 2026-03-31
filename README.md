---
layout: page
title: User Guide
---

**HireME** is a **desktop app for managing internship applications, optimized for use via a Command Line Interface** (CLI) while still having the benefits of a Graphical User Interface (GUI). If you can type fast, HireME lets you manage your internship hunt more efficiently than fiddling around with spreadsheets or Notion boards.

<img width="946" height="790" alt="image" src="https://github.com/user-attachments/assets/9a120773-6daa-4bcc-8be6-3c8f2783e96b" />

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.<br>
   **Mac users:** Ensure you have the precise JDK version prescribed [here](https://se-education.org/guides/tutorials/javaInstallationMac.html).

1. Download the latest `.jar` file from [here](https://github.com/AY2526S2-CS2103T-W11-3/tp/releases).

1. Copy the file to the folder you want to use as the _home folder_ for HireME.

1. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar HireMe.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * `list` : Lists all applications.

   * `add n/Google r/Software Engineer w/https://careers.google.com a/70 Pasir Panjang Rd d/15-03-2026 s/Pending` : Adds an application to Google for the Software Engineer role.

   * `delete 3` : Deletes the 3rd application shown in the current list.

   * `clear` : Deletes all applications.

   * `exit` : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

> **Notes about the command format:**
>
> * Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
>   e.g. in `add n/COMPANY_NAME`, `COMPANY_NAME` is a parameter which can be used as `add n/Google`.
>
> * Items in square brackets are optional.<br>
>   e.g. `n/COMPANY_NAME [e/EMAIL]` can be used as `n/Google e/hr@google.com` or as `n/Google`.
>
> * Items with `…`​ after them can be used multiple times including zero times.<br>
>   e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/tech`, `t/tech t/remote` etc.
>
> * Parameters can be in any order.<br>
>   e.g. if the command specifies `n/COMPANY_NAME r/ROLE`, `r/ROLE n/COMPANY_NAME` is also acceptable.
>
> * Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
>   e.g. if the command specifies `help 123`, it will be interpreted as `help`.
>
> * Each parameter (except tags) should only appear once in a command. If you accidentally provide duplicates (e.g. `n/Google n/Meta`), the app will flag an error.
>
> * If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.

### Viewing help : `help`

<img width="622" height="452" alt="image" src="https://github.com/user-attachments/assets/415a3b68-2d8c-46dc-95a1-ad3e44bc7079" />

Don't remember a command? No worries — `help` opens a window with a quick reference of all available commands and their formats.

Format: `help`


### Adding an application: `add`

Adds an internship application to HireME.

Format: `add n/COMPANY_NAME r/ROLE [e/EMAIL] w/WEBSITE a/ADDRESS d/DATE s/STATUS [t/TAG]…​`

**Parameter details:**

| Parameter | Prefix | Required | Constraints |
|-----------|--------|----------|-------------|
| Company Name | `n/` | Yes | Alphanumeric characters and spaces only |
| Role | `r/` | Yes | Alphanumeric characters and spaces only |
| Email | `e/` | No | Must follow `local-part@domain` format |
| Website | `w/` | Yes | Must be a valid website |
| Address | `a/` | Yes | Must not be blank |
| Date | `d/` | Yes | Must be in `DD-MM-YYYY` format |
| Status | `s/` | Yes | Must be `Offered`, `Pending`, or `Rejected` (case-insensitive) |
| Tag | `t/` | No | Alphanumeric only, no spaces. Can have multiple tags |

> [!TIP]
> An application can have any number of tags (including 0). Tags are handy for labelling things like `remote`, `onsite`, `highPriority`, etc.

> [!NOTE]
> Two applications are considered duplicates if they have the same **company name** and **role**. HireME will not allow you to add a duplicate.

Examples:
* `add n/Google r/Software Engineer w/https://careers.google.com a/70 Pasir Panjang Rd d/15-03-2026 s/Pending`
* `add n/Grab r/Backend Developer Intern e/careers@grab.com w/https://grab.com/careers a/3 Media Close d/01-03-2026 s/Pending t/tech t/startup`

### Listing all applications : `list`

<img width="945" height="787" alt="image" src="https://github.com/user-attachments/assets/4cb72b61-ee19-4402-bf2e-3aea9e25d1dd" />

Shows a list of all your applications in HireME.

Format: `list`

### Editing an application : `edit`

<img width="946" height="790" alt="image" src="https://github.com/user-attachments/assets/e96fb283-4e14-4647-959a-bb26f75ccb5f" /> <br>

<img width="946" height="369" alt="image" src="https://github.com/user-attachments/assets/a591f2ed-e744-43db-85d5-e5a42e059827" />

Edits an existing application in HireME. Use this when you need to update details like a new status or corrected information.

Format: `edit INDEX [n/COMPANY_NAME] [r/ROLE] [e/EMAIL] [w/WEBSITE] [a/ADDRESS] [d/DATE] [s/STATUS] [t/TAG]…​`

* Edits the application at the specified `INDEX`. The index refers to the index number shown in the displayed application list. The index **must be a positive integer** 1, 2, 3, …​
* At least one of the optional fields must be provided.
* Existing values will be overwritten by the input values.
* When editing tags, the existing tags of the application will be **replaced entirely** — editing tags is not cumulative.
* You can remove all the application's tags by typing `t/` without specifying any tags after it.

Examples:
*  `edit 1 s/Offered` Updates the status of the 1st application to `Offered`. Congrats!
*  `edit 2 r/Backend Developer Intern e/johndoe@example.com` Edits the role and email of the 2nd application.
*  `edit 3 t/` Clears all existing tags from the 3rd application.

### Locating applications: `find`

<img width="946" height="374" alt="image" src="https://github.com/user-attachments/assets/5ebf6149-2fe2-4848-b894-a3646b87af0b" />

Finds applications that match the specified keywords.

Format: `find [n/NAME] [r/ROLE] [e/EMAIL] [w/WEBSITE] [a/ADDRESS] [d/DATE] [s/STATUS] [t/TAG]...`

* All fields are optional. At least one field must be provided.
* The search is case-insensitive.
  e.g. `find n/google` will match `Google`.
* Partial matching is supported.
  e.g. `find n/goog` will match `Google`.
* Multiple fields are combined using **AND** logic.
  e.g. `find n/Google r/Backend Developer` returns applications that match both name and role.
* For tags, multiple keywords are combined using **OR** logic.
  e.g. `find t/backend developer t/frontend developer` returns applications that match either tag.
* For optional fields (`email`, `website`, `address`):
  Using an empty prefix (e.g. `e/`) matches applications with no value for that field.

Examples:
* `find n/google`
  Returns applications with company names containing "google"
* `find r/intern s/applied`
  Returns applications with role containing "intern" and status containing "applied"
* `find e/gmail`
  Returns applications with email containing "gmail"
* `find e/`
  Returns applications that have no email
* `find t/oa t/fintech`
  Returns applications tagged with either "oa" or "fintech"
<br>
<br>
![find result for 'find t/oa t/fintech'](images/findOaFintech.png)

### Viewing archived applications

Displays all archived applications.

Format: `find t/archived`

* Shows all applications that are currently archived.
* You can use the `unarchive INDEX` command on this list to restore applications.

Example:
* `find t/archived`

### Deleting an application : `delete`

<img width="946" height="368" alt="image" src="https://github.com/user-attachments/assets/ed45abd6-390b-42e9-831d-d34dd9ce2a68" />

Deletes the specified application from HireME.

Format: `delete INDEX`

* Deletes the application at the specified `INDEX`.
* The index refers to the index number shown in the displayed application list.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `list` followed by `delete 2` deletes the 2nd application in the list.
* `find n/Google` followed by `delete 1` deletes the 1st application in the results of the `find` command.

### Archiving an application : `archive`

Archives the specified application so that it is hidden from the main list but still stored in the system.

Format: `archive INDEX`

* Archives the application at the specified `INDEX`.
* The index refers to the index number shown in the currently displayed application list.
* Archived applications will not appear in the normal `list` command.
* Archiving an application does not delete it. The application is tagged as `archived` and hidden from the main list.
* You can view archived applications using the `find t/archived` command.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `archive 2` archives the 2nd application in the current list.
* `find n/Google` followed by `archive 1` archives the 1st application in the search results.

### Unarchiving an application : `unarchive`

Restores an archived application back to the main application list.

Format: `unarchive INDEX`

* The `INDEX` refers to the index number shown in the archived applications list.
* You must first view archived applications (e.g. using `find t/archived`) before using `unarchive`.
* The application will be removed from archived status and will appear in the normal list again.
* The index **must be a positive integer** 1, 2, 3, …​

Examples:
* `find t/archived`
* `unarchive 1` restores the 1st archived application.

### Clearing all entries : `clear`

<img width="946" height="213" alt="image" src="https://github.com/user-attachments/assets/95e8ce4d-48ed-4f0d-81e7-beabc025b3e1" />

Clears all application entries from HireME. Useful if you want a fresh start (e.g. new internship cycle).

Format: `clear`

> [!CAUTION]
> This action is irreversible. All your application data will be permanently deleted.

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Saving the data

HireME data is saved to your hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

HireME data is saved automatically as a JSON file `[JAR file location]/data/HireME.json`. Advanced users are welcome to update data directly by editing that data file.

> [!CAUTION]
> If your changes to the data file make its format invalid, HireME will discard all data and start with an empty data file at the next run. It is recommended to take a backup of the file before editing it. Furthermore, certain edits can cause HireME to behave in unexpected ways (e.g., if a value entered is outside the acceptable range). Only edit the data file if you are confident you can update it correctly.

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install HireME on the other computer and overwrite the empty data file it creates with the file that contains the data from your previous HireME home folder.

**Q**: Can I add two applications to the same company?<br>
**A**: Yes, as long as the **role** is different. HireME identifies duplicates by the combination of company name and role.

**Q**: Is the email field mandatory?<br>
**A**: No, email is optional. You can always add it later with the `edit` command.

**Q**: What statuses can I use?<br>
**A**: The three supported statuses are `Offered`, `Pending`, and `Rejected`. They are case-insensitive, so `pending`, `PENDING`, and `Pending` all work.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

## Command summary

| Action | Format | Example |
|--------|--------|---------|
| **Add** | `add n/COMPANY_NAME r/ROLE [e/EMAIL] w/WEBSITE a/ADDRESS d/DATE s/STATUS [t/TAG]…​` | `add n/Google r/Software Engineer w/https://careers.google.com a/70 Pasir Panjang Rd d/15-03-2026 s/Pending t/tech` |
| **Edit** | `edit INDEX [n/COMPANY_NAME] [r/ROLE] [e/EMAIL] [w/WEBSITE] [a/ADDRESS] [d/DATE] [s/STATUS] [t/TAG]…​` | `edit 1 s/Offered` |
| **Delete** | `delete INDEX` | `delete 3` |
| **Find** | `find [n/NAME] [r/ROLE] [e/EMAIL] [w/WEBSITE] [a/ADDRESS] [d/DATE] [s/STATUS] [t/TAG]...` | `find n/Google` |
| **Archive** | `archive INDEX` | `archive 2` |
| **Unarchive** | `unarchive INDEX` | `unarchive 1` |
| **List** | `list` | |
| **Clear** | `clear` | |
| **Help** | `help` | |
| **Exit** | `exit` | |

--------------------------------------------------------------------------------------------------------------------

## Glossary

1. **CLI:** Command Line Interface
2. **GUI:** Graphical User Interface
3. **Index:** Position of an item in the displayed list
4. **Application Status:** Current stage of an internship application (`Pending`, `Rejected`, or `Offered`)
5. **Tag:** A label attached to an application for categorisation (e.g. `remote`, `tech`, `archived`)
