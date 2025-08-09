
2025-08-09 12:04

Status: #working

Tags: [[Guide]] [[Digital Aid Seattle]]

---
# Coda - Guide
https://coda.io/resources
### **Coda at a glance**
Think of **Coda** as a mix between:
- **Google Docs** (text-based collaboration)
- **Airtable/Excel** (structured data tables)
- **Notion** (flexible, all-in-one workspace)
- **Zapier** (lightweight automations inside your doc)

It’s designed so **one doc can run your whole workflow** — notes, databases, dashboards, forms, and even lightweight apps.
### **Key Building Blocks**

1. **Pages & Subpages**
    - Your doc is made up of **pages** (like Notion).
    - You can have subpages for organization.  
        _Example:_ A “Project Hub” page → “Tasks,” “Meetings,” “Roadmap.”
        
2. **Tables**
    - These are like databases in Airtable or spreadsheets in Excel — but **linked** to each other.
    - Each row is a “record” (like an entry for a task, person, or event).
    - Columns are fields with **types**: text, date, number, select list, checkbox, etc.
        
3. **Views**
    - You can display the **same table** in different ways:
        - **Table view**
        - **Kanban board**
        - **Calendar**
        - **Timeline**  
            _Example:_ One “Tasks” table → a Kanban for dev team, Calendar for marketing.
            
4. **Controls**
    - Dropdowns, sliders, buttons that filter data or trigger actions.
    - Used for dashboards or interactive tools inside your doc.
        
5. **Formulas**
    - Work like Excel functions, but **can reference other tables and pages** easily.
    - Example:  
        `Tasks.Filter(AssignedTo = User()).Count()` → counts how many tasks are assigned to you.
        
6. **Buttons & Automations**
    - Buttons can add rows, send emails, change values, or run multiple steps.
    - Automations can trigger based on:
        - Time
        - Row change (like “when Status changes to Done”)
        - Button press
            
7. **Packs**
    - Integrations with external tools like Gmail, Slack, Jira, Google Calendar, etc.
    - Lets your doc talk to the outside world.

### Tables
https://coda.io/resources/guides/getting-started-with-tables-in-coda

#### 1. Table Structure
- **Rows** = individual items (tasks, contacts, orders, etc.).
- **Columns** = properties/attributes of each row.  
    Examples:
    - **Text**: Name, description
    - **Number**: Price, quantity
    - **Date/Time**: Due date, event start time
    - **Select list**: Status (Pending, In Progress, Done)
    - **Checkbox**: Completed? Yes/No
    - **Person**: Assign to a Coda user
    - **Lookup**: Pull data from another table
#### 2. Column Types (Important!)
Coda’s power comes from its **column types** — they make data smart and linkable.
Common types:
1. **Text** → Freeform text.
2. **Number** → Supports formatting (currency, %, decimals).
3. **Date / Date & Time** → Works with Coda’s date formulas (e.g., `Today()`, `DaysUntil()`).
4. **Select List** → Dropdown from a fixed list of choices.
5. **Checkbox** → Boolean true/false.
6. **Person** → Links to Coda users (good for task assignment).
7. **Lookup** → This is key — lets you reference another table’s rows, turning it into a relational database. 
	1. There is no literal "lookup" column, its just that you can lookup things
8. **Button** → Each row can have its own button for actions (delete row, change value, send email, etc.).
9. **Image / File** → Store media.
#### 3. Linked Tables & Lookups
If you’ve used Airtable’s **linked records**, Coda’s **Lookup** column type does the same thing.
Example:
- **Tasks** table has a “Project” column.
- Instead of typing project names, you make “Project” a **Lookup** from the **Projects** table.
- This links each task to a real project record, so:
    - You can click a project name to see all related tasks.
    - You can use formulas like `Project.Tasks` to pull linked rows.
#### 4. Views (Same Table, Different Display)
Coda lets you create **multiple views** of the same table:
- **Table View** → Grid of data.
- **Kanban** → Board grouped by status.
- **Calendar** → Events by date.
- **Timeline** → Project schedule.
- **Card View** → Visual tiles.
When you edit in _any_ view, it updates all other views (since they’re the same table, not copies).
#### 5. Formulas in Tables
https://coda.io/formulas#MonthName
Coda formulas are **row-aware** and can reference other tables.
Example:  
If you have:
- **Quantity** column
- **Price** column  
    You can make **Total** column = `Quantity * Price`.
Or pull data from another table:  
`Projects.Filter(ProjectName = thisRow.Project).Manager`  
(Finds the project in the Projects table that matches this task’s linked Project, then returns its Manager.)
#### 6. Controls & Filtering
Tables can be filtered by:
- Static conditions (e.g., Status = "Open")
- Interactive controls (e.g., dropdown on the page that filters which tasks you see)
This makes Coda tables very dashboard-friendly.
#### 8. Tables vs. Pages in Coda
One thing that trips up beginners:
- Tables **live** somewhere in your doc — either on a page or as a hidden object.
- You can **reference a table anywhere** in the doc and show it as a view.
- But **don’t duplicate tables** unless you want separate data — instead, make views.

## Refs

### Callouts
- Callout is a highlighted area
- The text within a callout can be further customized, including using basic text formatting, adding headings and lists, inserting images, and more.
### Relation vs Table field type in  Coda
In **Coda**, “Relation” and “Table” both appear in the **Column type** menu, but they mean very different things:
 ![[Pasted image 20250811153249.png]]
 
 **1. Relation Column Type**
- A **Relation** column is **linked to another table** (just like Airtable’s linked record field).
- Each cell stores a **row reference** — not just the text you see, but a pointer to the actual row.
- Can store one or multiple row references (depending on settings).
- You can pull related data with `.ColumnName` on that relation.
- If you delete a row in the source table, all relations pointing to it will break.
- Formula results in a relation column **must** be a list of row references from the linked table.
	**Example:**  
	Column: `Project` (Relation → Projects table)  
	Value in a row: `Project A` (actually a row link)  
	Formula:
	
	```coda
	`thisRow.Project.DueDate`
	```
	
	→ returns the due date from the linked project.

**2. Table (as a column type)**
- This is not “link to another table.”
- It means **the column stores an entire subtable inside a single cell**.
- You can create a mini-table (grid) inside a row — useful for nested data structures, but it’s **independent** of your other tables.
- It’s not relational — the rows inside that mini-table aren’t tied to your main tables unless you link them with formulas.

### Calculated values are selectable in coda
- Coda treats **calculated values** as **real cell values** in most contexts — meaning they are selectable and can be referenced just like static values.
- The fields can be accessed as objects.
- If you have a formula column in a table, you can:
    - Use it as a **display column** in lookups.
    - Filter or select rows based on that calculated value without needing to duplicate it.
    - Even use it as the **value** in a select list column in another table.

### Prefill form button in Coda

Step 1: Get the URL of Your Published Form
First, you need the public link to your form.
1. Go to your `Tasks` table and create a **Form view** if you don't have one.
2. With the form view open, click the **Share Form** button at the top right.
3. Click **Publish** and copy the provided form URL. It will look something like `https://coda.io/form/New-Task_dAbcDeF123`. Keep this link handy.    

Step 2: Construct a Dynamic URL with Pre-filled Data
Now, you'll create a formula that takes your base form URL and adds the pre-filled data as parameters. The key is to use the `Format()` and `EncodeForUrl()` functions.
Let's say you want to pre-fill the `Related Project` and `Assignee` columns.
The formula will look like this:

```
Format(
  "https://coda.io/form/Your-Form-URL?Related%20Project={1}&Assignee={2}",
  EncodeForUrl(thisRow),
  EncodeForUrl(User())
)
```

 Step 3: Create a Button to Open the Hyperlink
Finally, create a button that uses this formula to open the pre-filled form in a new tab.
1. Create a new button and give it a label like "Submit New Task".
2. Set the **Action** to **Open hyperlink**.
3. Paste the `Format()` formula you built in Step 2 into the **URL** field (use formula option).
Now, when a user clicks this button:
4. The formula builds the unique URL with the project and user pre-filled.
5. The published form opens in a new browser tab.
6. The `Related Project` and `Assignee` fields will already be filled in.
7. The user fills out the remaining fields and clicks "Submit". All your column validations (e.g., "Required") will be enforced by the form itself. ✅
### Compose - feature
https://help.coda.io/en/articles/8032777-build-dynamic-text-columns-with-compose
- The compose feature lets you build dynamic formatted text in table columns
- It is used to generate rich formatted text based on values
- @ - Reference other columns

### Calculation Builder - feature
- Use the calculation builder - or write your own formulas - to automatically fill column values


## Plan limits

| Feature                   | Free Plan Limit                  |
| ------------------------- | -------------------------------- |
| Unshared doc size         | Unlimited                        |
| Shared doc objects        | 50 objects                       |
| Shared doc table rows     | 1,000 rows                       |
| Total attachments per doc | 1 GB                             |
| Max attachment size       | 10 MB                            |
| Version history           | 7 days                           |
| Time-based automations    | 35 per doc/month                 |
| Event-based automations   | 100 per doc/month                |
| Sync table rows           | 100 rows per pack/cross-doc sync |
| Auto-refresh for sync     | Not available (manual only)      |
| API rate limits           | Standard across all plans        |
- **50 objects** per doc (includes pages, tables, views, canvas buttons, canvas formulas)

| Plan           | Price (per Doc Maker, annual billing) | Doc & Attachment Limits                                                                                                                                                                                                                                                                                                                                         | Version History                                                                                                                                                                                                                                                                                            | Automations                                                                                                                                                                                                                                                                                                                                                                                                                                             | Advanced Features                                                                     |
| -------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Free**       | $0                                    | Shared docs limited                                                                                                                                                                                                                                                                                                                                             | 7 days                                                                                                                                                                                                                                                                                                     | Limited (35 time + events)                                                                                                                                                                                                                                                                                                                                                                                                                              | Basic — limited sync, manual refresh, no hidden pages, no custom branding             |
| **Pro**        | ~$10/month                            | Unlimited doc size                                                                                                                                                                                                                                                                                                                                              | 30 days ([Bardeen AI](https://www.bardeen.ai/answers/how-much-does-coda-cost?utm_source=chatgpt.com "How Much Does Coda Cost? 2025 Pricing Guide"))                                                                                                                                                        | Higher limits (e.g. up to 100 time-based, 500 event-based) ([TechRepublic](https://www.techrepublic.com/article/coda-review/?utm_source=chatgpt.com "Coda.io Review: Features, Pricing and Alternatives"))                                                                                                                                                                                                                                              | Hidden pages, custom branding & domains, Pro Packs, AI credits                        |
| **Team**       | ~$30/month                            | Unlimited                                                                                                                                                                                                                                                                                                                                                       | Unlimited version history ([TechRepublic](https://www.techrepublic.com/article/coda-review/?utm_source=chatgpt.com "Coda.io Review: Features, Pricing and Alternatives"), [Saufter AI](https://saufter.io/coda-pricing/?utm_source=chatgpt.com "Coda Pricing: Which Is The Best Plan For Your Business?")) | **Unlimited automations** ([The Digital Project Manager](https://thedigitalprojectmanager.com/tools/coda-pricing/?utm_source=chatgpt.com "Coda Pricing Tiers & Costs"), [TechRepublic](https://www.techrepublic.com/article/coda-review/?utm_source=chatgpt.com "Coda.io Review: Features, Pricing and Alternatives"), [Saufter AI](https://saufter.io/coda-pricing/?utm_source=chatgpt.com "Coda Pricing: Which Is The Best Plan For Your Business?")) | Doc locking, folder access control, cross-doc syncing, Team Packs, training & support |
| **Enterprise** | Custom pricing                        | All Team features + SSO, SCIM, audit logs, enterprise Packs, top-tier AI credits ([The Digital Project Manager](https://thedigitalprojectmanager.com/tools/coda-pricing/?utm_source=chatgpt.com "Coda Pricing Tiers & Costs"), [Saufter AI](https://saufter.io/coda-pricing/?utm_source=chatgpt.com "Coda Pricing: Which Is The Best Plan For Your Business?")) |                                                                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                                       |
## Problems
https://coda.io/compare/airtable
### Cross base Syncing 
- Coda can “sync” tables from one doc into another using **Cross-doc** or **Cross-doc 2.0**.
- These **do not update instantly** — they refresh on a schedule (hourly, daily, or manual refresh depending on your plan).
- This is different from Airtable’s base-wide linking where all tables are live together.

### Form defaults are not showing up
- Default values set during form creation are not showing up when the form is being filled.
### **External data (Google Sheets, Jira, etc.)**
- In Airtable, an integration like Google Sheets syncs on Airtable’s schedule.
- In Coda, **Packs** pull in data from external tools — each Pack has its own refresh rate (some hourly, some daily, some manual).
- Not all external data is live; it depends on the Pack.

| **Feature / Scenario**                                   | **Airtable**                                                                                            | **Coda**                                                                                                   |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Within the same doc/base** (tables, formulas, lookups) | **Instant** — all data recalculates live for all collaborators.                                         | **Instant** — all data recalculates live for all collaborators.                                            |
| **Between tables in the same doc/base**                  | Live linked records update immediately.                                                                 | Live lookups & formulas update immediately.                                                                |
| **Between different docs/bases**                         | Can’t natively link bases (need sync tables) → Syncs automatically every few minutes (Pro plan ~5 min). | Cross-doc / Cross-doc 2.0 → Syncs hourly/daily or on-demand (manual refresh), not instant.                 |
| **External integrations (Google Sheets, Jira, etc.)**    | Sync schedule depends on Airtable Sync type; most refresh every few minutes to hourly.                  | Packs fetch data on a schedule (varies by Pack; often hourly, daily, or manual refresh).                   |
| **Two people editing at once**                           | See changes instantly in real-time.                                                                     | See changes instantly in real-time.                                                                        |
| **Automation triggers**                                  | Runs right after trigger conditions are met.                                                            | Runs right after trigger conditions are met (within doc). Cross-doc/Pack triggers only after sync refresh. |


## Resources
https://coda.io/resources/guides/what-is-coda
https://coda.io/resources
https://help.coda.io/en/articles/1223025-calculate-column-values
https://coda.io/formulas#SumIf
https://www.youtube.com/watch?v=y9ca42_yRIk
https://coda.io/resources


---
## References