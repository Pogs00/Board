Team Task Boards
A single-page team task manager (`index.html`) in the style of Monday.com. It syncs live between teammates through Firebase (Google sign-in and Firestore). All of the app code is in `index.html`.
Features
Boards
Create multiple boards, rename them by editing the title, and reorder them in the sidebar by dragging (or Alt+Up/Down).
Archive a board and restore it from the sidebar, or delete it forever.
Group boards under teams, which can be collapsed in the sidebar.
Overdue counts and item counts show next to each board.
Groups, sub groups and items (Table view)
Groups hold items. Create, rename, collapse, color-code and delete them.
Sub groups: use + Sub group in a group header to nest a group inside another group (up to 3 levels deep). Each sub group has its own table and "add item" row.
Items have these columns: Name, Owner, Status, Priority, Start, Due, Estimated hours, Actual hours, Last updated, and Notes (update count).
Subtasks: use + Sub on an item to add subtasks inline. Subtasks have all the same columns as items and are indented under their parent. A parent shows a done count such as `2/3`, and its subtasks can be collapsed or expanded.
Drag the ⋮⋮ handle (or use the Up/Down arrow keys) to reorder items. Drag an item into another group to move it, and its subtasks move with it.
A progress bar under each group shows the mix of statuses.
Automatic roll-ups
Dates: a parent task's Start and Due are set automatically from its subtasks (earliest start, latest due). Those two fields are locked while the subtasks have dates.
Completion: when every subtask is Done, the parent task is set to Done automatically. If a subtask is reopened or a new one is added, a parent that was auto-completed goes back to "Working on it".
Group dates: each group header shows its date range, worked out from all items and sub groups inside it. Gantt shows a summary bar for it.
Group completion: each group header shows `done/total`, which becomes a green ✓ Complete badge when everything inside it (including sub groups) is done.
On load, the app checks all existing parents once and fixes any that are out of date.
Views
Table: the main editable view.
Kanban: one column per status. Drag cards between columns to change status, and use + Add to create an item.
Gantt: drag a bar to move it and drag its edges to resize it. Click a bar for notes, click an empty row to set a date, and zoom between Day, Week, Month and Quarter (or Fit all and Today). Parent bars with dated subtasks are locked.
Calendar: a month grid showing items across their date span, with overdue and due-soon highlights.
Filtering, sorting and search
Search items by name or owner.
Filter by Owner (including "Me" and "Unassigned"), Status, Priority, and Show (Overdue, Due in 3 days, No due date).
Sort by manual order, Due date, Priority, Status, Name, or Recently updated.
Clear filters resets everything.
Statuses, priorities and people
Statuses: add, rename, recolor and reorder statuses (applies to every board). Each status is set to count as Done, Stuck, In progress or Not started for the dashboard and roll-ups.
Priority: Low, Medium, High, Critical.
People: maintain a team list that becomes the Owner dropdown on every board.
Due dates are flagged overdue (red) and due soon (amber).
Updates, activity and time tracking
Updates panel (💬) per item: post comments, and see an automatic activity log of changes such as status, priority, dates, owner and estimate.
Time logging: log hours with a date and a note, set an estimated-hours value, and see Actual vs Estimate in the table (colored when near or over budget).
Dashboard
Combined view across all boards with KPIs: boards, items, % done, in progress, stuck, due soon, overdue, estimated hours, and logged hours.
Charts and tables for status, priority, open work by owner, per-board progress, items needing attention, hours by board, hours by person, over-budget items, and recent activity.
Filter by team and owner, and switch to a combined calendar.
Reports and backup
Report: export to Excel (.xlsx) or PDF, as a Table, Kanban or Gantt layout. Choose this board, all boards, or all boards in a team.
Export backup / Import backup: download everything as JSON and restore it later. Importing overwrites matching records and deletes nothing.
Deleted items can be restored with Undo, including their subtasks.
Access and teams
Sign in with Google (Firebase Authentication).
Admins manage teams and an access list of allowed emails. Each team's boards are visible only to the emails listed for that team, and an empty list means everyone can see them.
Changes sync live to everyone ("● Shared, live").
Works with light and dark mode, and is responsive on mobile.
Setup
Create a Firebase project and enable Google sign-in and Firestore.
Put your Firebase settings in `firebase-config.js` next to `index.html`, as `FIREBASE_CONFIG`.
Add your Firestore security rules. Items must allow the fields `parentId` and `autoDone`, and groups must allow `parentId`, otherwise subtasks, sub groups and auto-complete won't save.
Host the files (Firebase Hosting, GitHub Pages, etc.) and open `index.html`.
Data model (Firestore collections)
`boards`, `groups` (with optional `parentId` for sub groups), `items` (with optional `parentId` for subtasks and `autoDone`), `updates`, `settings`.
