# Project 2: ToDo List version 2

Create a web application to store a to-do list.

## Basic characteristics

1. No user identification needed.
2. The current user can see all the tasks.

## Data

### Tasks

Each task consists of

1. Task description (required)
2. Due date (required)
3. Task category (optional)
4. Priority level (optional) (Values: 1-4, where 1 is the highest priority)
5. Status (active or completed)

(Optional) means is optional to the user. So, the user does not have to provided that information. However, the database must store that information, if provided.

### Categories

Each task category consists of

1. Name

## Functionalities

1. Current user can create.
2. Current user can edit tasks on Task description, Due date, Priority, and Task category.
3. Current user can mark a task as completed.
4. Current user can create categories.
5. Current user can edit categories on its name only.

## Views or reports

1. The default list view of the application will show overdue tasks and due-today tasks. Tasks will be sorted by priority.
2. The user can select other views based on categories. The tasks will be ordered by priority and due date.
3. The user can select a view for only completed tasks on a specific day. Tasks will be sorted by due date.
