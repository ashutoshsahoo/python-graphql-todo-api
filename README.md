# Build a GraphQL API with Python, Flask and Ariadne

## Setup

- Set virtualenv and install dependencies

```sh
$ virtualenv todo_api_env
$ source todo_api_env/bin/activate
(todo_api_env)$ pip install requirements.txt

```

- Create some Todos

```sh
python
>>> from main import db
>>> db.create_all()
>>>
>>> from datetime import datetime
>>> from api.models import Todo
>>> today = datetime.today().date()
>>> todo = Todo(description="Run a marathon", due_date=today, completed=False)
>>> todo.to_dict()
{'id': None, 'completed': False, 'description': 'Run a marathon', 'due_date': '2021-08-22'}
>>> db.session.add(todo)
>>> db.session.commit()
>>>
```

- Run application

```sh
export FLASK_APP=main.py
flask run

```

Open GraphQl Playground [http://127.0.0.1:5000/graphql](http://127.0.0.1:5000/graphql)

## Test

- fetchAllTodos

```graphql
query fetchAllTodos {
  todos {
    success
    errors
    todos {
      description
      completed
      id
    }
  }
}
```

- fetchTodo by Id

```graphql
query fetchTodo {
  todo(todoId: "1") {
    success
    errors
    todo {
      id
      completed
      description
      dueDate
    }
  }
}
```

- Create new todo

```graphql
mutation newTodo {
  createTodo(description: "Go to the dentist", dueDate: "24-08-2021") {
    success
    errors
    todo {
      id
      completed
      description
    }
  }
}
```

- mark todo completed

```graphql
mutation markDone {
  markDone(todoId: "1") {
    success
    errors
    todo {
      id
      completed
      description
      dueDate
    }
  }
}
```

- Delete todo

```graphql
mutation {
  deleteTodo(todoId: "1") {
    success
    errors
  }
}
```

- update due date

```graphql
mutation updateDueDate {
  updateDueDate(todoId: "2", newDate: "25-08-2021") {
    success
    errors
  }
}
```
