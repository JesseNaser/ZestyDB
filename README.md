# ZestyDB

We have implemented a web app to store a to-do list using a realtime database. You can visit it by clicking here: [todo.zestydb.com](https://todo.zestydb.com).

### Database Setup

1. Create a Cloudflare D1 database. We named ours "todo".
2. Execute the following SQL commands to create the tables we need for our to-do list.

```
CREATE TABLE categories (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT UNIQUE NOT NULL
);

CREATE TABLE tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    description TEXT NOT NULL,
    due_date DATE NOT NULL,
    category_id INTEGER,
    priority_level INTEGER CHECK(priority_level BETWEEN 1 AND 4),
    status TEXT DEFAULT 'active' CHECK(status IN ('active', 'completed')),
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

3. Create a Cloudflare Worker. We named ours "todo".
4. Set the D1 Database Binding for the Worker. We connected our "todo" database to the environment variable "TODO_DB".
5. Insert the code into the worker. You can find our worker code [here](worker.js).
6. Map the worker to a custom domain. You can find our worker running at [todo.zestydb.com](https://todo.zestydb.com).

### Creator Profiles

##### [Jesse Naser](jesse)

##### [Timothy Kosinski](timothy)

##### [Rory Jolliff](rory)

##### [George Ebaugh](george)