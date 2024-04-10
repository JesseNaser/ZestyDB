## SQL Commands within Functionalities (async function)

You can find our worker code [here](worker.js). The functions are located at the bottom of the file.

### getTasks(view, categoryId, selectedDate, env)

#### Default View

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

```sql
SELECT 
  * 
FROM 
  categories 
ORDER BY 
  name
```

### addTask(formData, env)

```sql
INSERT INTO tasks (
  description, due_date, category_id, 
  priority_level, status
) 
VALUES 
  (?, ?, ?, ?, ?)
```

### addCategory(formData, env)

```sql
INSERT INTO categories (name) 
VALUES 
  (?)
```

### deleteTask(id, env)

```sql
DELETE FROM 
  tasks 
WHERE 
  id = ?
```

### updateTask(id, formData, env)

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

```sql
UPDATE 
  categories 
SET 
  name = ? 
WHERE 
  id = ?
```

### resetCategory(id, env)

```sql
UPDATE 
  tasks 
SET 
  category_id = NULL 
WHERE 
  category_id = ?
```

### deleteCategory(id, env)

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
