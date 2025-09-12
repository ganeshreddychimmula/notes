
2025-07-29 15:59

Status:

Tags: [Guide](../3%20-%20Tags/Guide.md) [Digital Aid Seattle](../3%20-%20Tags/Digital%20Aid%20Seattle.md)

---
# Airtable - Guide
[What is Airtable? And Is It For Me?](https://www.youtube.com/watch?v=BX61XKNYvIY&utm_source=chatgpt.com)

1. **What Airtable Is**
    - Airtable combines the **simplicity of a spreadsheet** with the **flexibility of a relational database**, making it accessible for both technical and non-technical users.
        
2. **Use Cases**
    - Ideal for project planning, team workflows, visual data management, event planning, and more. It suits users who prefer intuitive interfaces without sacrificing data structure.
        
3. **Core Features**
    - **Different Views**: Grid, Kanban, Calendar, Gallery, and more.
    - **Blocks & Automations**: Built-in tools and integrations help visualize and automate workflows.
    - **Templates & Extensions**: Start quickly with pre-built bases or customize to your team’s needs.
        
4. **Why It Resonates**
    - The presenter emphasizes Airtable’s versatility and how they've personally relied on it across work and personal projects. This suggests it's both robust and flexible enough for diverse domains.
### 🧩 How This Relates to Your Folder Structure Work

| Concept                        | Application to Your Airtable Navigation                                                                           |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| **Relational Structure**       | Use linked records to mirror folder redirections or cross-references in Airtable.                                 |
| **Visualization**              | Visual blocks and layouts can replace Mermaid-labeled diagrams for intuitive dashboards.                          |
| **Templates + Views**          | Create pre-built views for top-level folders like “External Orgs,” “HR,” or “Ventures” to standardize navigation. |
| **Automations & Integrations** | Set up automatic redirection when a user clicks on a folder record, linking to a detailed page or external docs.  |

---
## 1. Create a Database
### Base
- An Airtable base (short for "database") is the home for all the information you need for your workflow.
- Stores important data and workflows that depend on it.
	- Allows to organize, connect information and change as needed.

### Table
- A base is made up of tables, and each table contains a list of items of same type - like people, ideas or projects
### **Anatomy of a table**
- **Record**: An individual item in a table, usually represented by a row
    
- **Field**: A detail or piece of information for each record, usually represented by a column
    
- **View**: Different ways of viewing the information in a table

### Different field types
https://www.airtable.com/guides/build/organize-data-in-fields

### **What are linked records?**
Linked records are a powerful way of creating relationships between your data. You can use them to bring information from one field into another, or between multiple records, and even perform calculations between them.

![LearningPath_Guides_10.1.png](https://www.airtable.com/_next/image?url=https%3A%2F%2Fimages.ctfassets.net%2Fwl95ljfippl8%2Fruvy1jUh4twSnIgLzDFlE%2F88b3877b51b337ad0893c1de248d2028%2FLearningPath_Guides_10.1.png%3Ffm%3Dwebp&w=3840&q=100)

## 2. How a view is useful

Different views in Airtable are **functional filters and workflows**, not just different visualizations.  
They **change how the data behaves**, what you can do with it, and how it interacts with automations, without changing the underlying table.

Here’s the **functional usefulness** broken down:
### **1. Filtering → Functional Focus**
- **Functionality:** A view can **filter** data to show only the records that meet specific conditions.
- **Why Useful:**
    1. Keeps **irrelevant tasks hidden** to reduce cognitive load.
    2. Lets you **perform bulk actions** (update status, assign) only on relevant records.
- **Example in your base:**
    - “Today View” only shows tasks with `Due Date = Today` → prevents you from seeing backlog or future tasks when planning daily work.

### **2. Sorting & Grouping → Workflow Prioritization**
- **Functionality:** Sort by Priority, Due Date, or Status; Group by Task Group or Section.
- **Why Useful:**
    1. **Enforces a work order** automatically → e.g., high-priority or urgent items surface to the top.
    2. **Keeps related items together** for batch processing.
	    - Airtable allows you to **select multiple records in a view** → change a field, delete, or trigger an automation for **all selected records simultaneously**.
		- Functionally, this is like **applying one command to an entire filtered group of tasks**.
		- Go to a **Completed Tasks view** → Select all 10 → Mark `Status = Complete`
		- Mark 5 overdue tasks as `Today` → Your Airtable automation sends 5 calendar events at once.
- **Example:**
    - Task Group view grouped by `Status` → lets you drag/drop tasks between **In Progress**, **Blocked**, **Completed**, updating the field automatically.
        
### **3. Hidden Fields → Data Protection & Focus**
- **Functionality:** A view can **hide sensitive or irrelevant fields**.
- **Why Useful:**
    1. **Keeps the table uncluttered** for daily usage.
    2. **Protects reference fields** (like formulas or links) from accidental edits.
- **Example:**
    - A “Quick Add Task” view only shows `Task Name`, `Due Date`, `Section`. The heavy metadata like `Blocked By` and `Resources` are hidden to keep adding tasks frictionless.
        
### **4. Saved Conditions → Reusable Filters**
- **Functionality:** Views **store conditions** (filters, groups, sorts) permanently.
- **Why Useful:**
    1. Eliminates **re-creating filters every time** you want to check a status.
    2. Allows **automation triggers** (like email notifications) to rely on the view.
- **Example:**
    - “Overdue View” has `Due Date < Today` + `Status != Completed`.
    - Your automation triggers **only for tasks in that view**, sending a reminder or Slack message.
        
### **5. Automations & Integrations**
- **Functionality:** Certain **Airtable automations and synced interfaces** rely on specific views.
- **Why Useful:**
    1. You can **trigger workflows automatically** when a record enters or leaves a view.
    2. Reduces **manual tracking** by syncing filtered data with tools like Google Calendar or Notion.
- **Example:**
    - When a task moves to the “Today View”, Airtable sends a **Google Calendar event** or **reminder notification**.
### **6. Permissions & Collaboration**
- **Functionality:** **Shareable views** can be locked or read-only for others.
- **Why Useful:**
    1. Share only what’s relevant with teammates, clients, or your future self.
    2. Prevent accidental edits to core data.
- **Example:**
    - Share a read-only “Study Roadmap View” with a mentor without exposing unrelated tasks or private notes.
### **7. Efficient Bulk Updates**
- **Functionality:** A filtered view lets you **select all and update** fields without touching unrelated records.
- **Why Useful:**
    1. Avoids mistakes when updating 50+ tasks at once.
    2. Speeds up repeating workflows (like moving all completed tasks to archive).
- **Example:**
    - Switch to “Completed Tasks View” → select all → mark Task Groups as Completed → done in one step.

### **Bottom Line:**
Different views are **functional filters and workflows**, not just “visual rearrangements.”  
They **define how you work with the data**, enabling:
- **Focus** (filter what matters)
    
- **Efficiency** (batch updates, sorting, grouping)
    
- **Automation triggers** (when something enters a view)
    
- **Error prevention** (hidden fields and scoped updates)
    
- **Collaboration control** (share only the right slice of data)

### Syncs
![Pasted image 20250820225336](../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250820225336.png)
Short answer: **“Syncs” are the live data connections feeding your base.** Each sync creates a **synced table** that pulls rows from a source (another Airtable view or an external app). It auto-updates and shows “Last synced …” like in your screenshot.

What that panel means here:

- **DAS automations** → a synced table set up by Seamus. Click it to see the source and settings, or to “Sync now.”
    

How syncs behave (practical bits):

- **Read-only source fields.** You can’t edit the synced columns (unless two-way sync is enabled). Add your own extra columns in the destination—those stay local.
    
- **Update flow.** Change data **at the source**; it flows down on schedule or when you hit **Sync now** (actual frequency depends on plan).
    
- **Scope = source view.** Only records visible in the source view sync across (filters/hidden fields there control what arrives).
    
- **Two-way sync (optional).** Some sources let you enable edits in the destination that write back to the source—toggle this in Sync settings.
    
- **Stop/convert.** In settings, you can unsync (freeze the table as a static copy) or delete the sync.
    

Where to create one:

- **Add or import → Create synced table / Sync data from…**, pick Airtable (another base/view) or connectors (e.g., Google Calendar, Jira, etc.), then configure.
    

Common gotchas:

- You lack permission to the source → sync fails.
    
- Filters in the source view hide rows you expected.
    
- Field types that don’t map cleanly (check warnings in settings).

### Rollup Field
- A **Rollup field** in Airtable **summarizes data from linked records**.
- It’s like saying:  
    _“Look at all the Tasks linked to this Task Group, and show me a summary of something (like a count, sum, average, or custom formula) from them.”_
---
### Questions

**Q: If I link Sections and Task Groups to the Tasks table, do I need to manually add tasks to each table?**  
**A1:** No, Airtable **links are 2-way by default**.
- If you add a **Task** and link it to a **Task Group** or **Section**, it automatically appears in those tables.
- If you add a **Task** from the **Task Group or Section table**, it also automatically links in the **Tasks table**.

**Q: Can I create tasks from the Task Groups or Sections table instead?**  
**A3:** Yes, you can:
- Open **Task Group → Full List of Tasks** and add a task → It appears in Tasks table.
- Open **Section → Linked Tasks** and add a task → It appears in Tasks table.

**Q: What about free-floating tasks?**  
**A4:**
- Leave **Task Group** and **Section** blank when creating the task.
- It will stay independent in the Tasks table and won’t appear in other tables.

**Q: Can the Section auto-fill when I select a Task Group for a task?**  
**A5:**
- **Not automatically in the grid**.
- But you can use **Airtable Automation**: 
    1. **Trigger:** When Task Group is set in a Task.
    2. **Action:** Update the Task’s Section to match the Task Group’s Section.

**Q: Can we calculate total pending hours using just a formula in Task Groups or Sections table, without a Rollup?**  
**A:** ❌ **No, not directly.**
Here’s why:
1. Airtable formulas **cannot pull values from another table** automatically.
2. Formulas only work with **fields in the same record**.
3. To sum numbers from linked Tasks, you need a **Rollup field** first.

Q. why decimal is not showing?
- Airtable is **not ignoring your 0.5**—it’s **formatting the field as an integer**.
- By default, Airtable **formula fields with numeric output** often **round to whole numbers** unless you **format them to show decimals**.

---
## Tutorial
-> Structure of Airtable
- personal -> workspace (Outershell)
- Bases are shells where you can have interlinked tables
- 

![Pasted image 20250803125757](../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250803125757.png)
- Remember **Automation limit**

### Formulas Airtable
https://support.airtable.com/docs/formula-field-reference




### Scripting Extension





---
## References