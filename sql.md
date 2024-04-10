## SQL Commands within Functionalities (async function)

You can find our worker code [here](worker.js). The functions are located at the bottom of the file.

### getTasks(view, categoryId, selectedDate, env)

#### Default View

- This is the default view which only shows past due or due-today tasks (before and upto today (entire day)). Tasks are sorted by priority (nulls at bottom of the table).

```sql
SELECT 
  * 
FROM 
  tasks 
WHERE 
  DATE(due_date) <= ? 
  AND status = 'active' 
ORDER BY 
  priority_level IS NULL, 
  priority_level
```

#### Category View

- This is a view showing only those tasks associated with a category. Ordered by priority first (nulls at bottom of table) and then due date.

```sql
SELECT 
  * 
FROM 
  tasks 
WHERE 
  category_id = ? 
ORDER BY 
  priority_level IS NULL, 
  priority_level, 
  due_date
```

#### Completed View

- This view only shows the completed tasks on that (entire) day. The tasks are sorted by due date.

```sql
SELECT 
  * 
FROM 
  tasks 
WHERE 
  status = 'completed' 
  AND DATE(due_date) = ? 
ORDER BY 
  due_date
```

#### Everything View

- Since the user must be able to see all the tasks, we have developed this view that shows all the tasks in that table.

```sql
SELECT 
  * 
FROM 
  tasks 
ORDER BY 
  due_date, 
  priority_level
```

### getAllCategories(env)

- To display all the categories that exist, so the user can operate upon them.

```sql
SELECT 
  * 
FROM 
  categories 
ORDER BY 
  name
```

### addTask(formData, env)

- The user may add new tasks

```sql
INSERT INTO tasks (
  description, due_date, category_id, 
  priority_level, status
) 
VALUES 
  (?, ?, ?, ?, ?)
```

### addCategory(formData, env)

- The user may add new categories.

```sql
INSERT INTO categories (name) 
VALUES 
  (?)
```

### deleteTask(id, env)

- The user may delete tasks.

```sql
DELETE FROM 
  tasks 
WHERE 
  id = ?
```

### updateTask(id, formData, env)

- The user may update tasks.

```sql
UPDATE 
  tasks 
SET 
  description = ?, 
  due_date = ?, 
  category_id = ?, 
  priority_level = ?, 
  status = ? 
WHERE 
  id = ?
```

### updateCategory(id, formData, env)

- The user may change a name of a category; since they are identified by Id.

```sql
UPDATE 
  categories 
SET 
  name = ? 
WHERE 
  id = ?
```

### resetCategory(id, env)

- We disassociate all of the tasks from this category.

```sql
UPDATE 
  tasks 
SET 
  category_id = NULL 
WHERE 
  category_id = ?
```

### deleteCategory(id, env)

1. First: all of the tasks associated with this Category are deleted from their Tasks table.
2. Second: We delete the category from its table.

```sql
DELETE FROM 
  tasks 
WHERE 
  category_id = ? 

DELETE FROM 
  categories 
WHERE 
  id = ?
```
