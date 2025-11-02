---
layout: post
title: "Building RESTful APIs with Python and Flask"
date: 2024-10-15 09:00:00 -0500
author: Mason Fox
tags: [python, flask, api, backend]
---

# Building RESTful APIs with Python and Flask

Flask is a lightweight and flexible Python web framework that's perfect for building RESTful APIs. In this post, I'll walk you through creating a simple but functional API.

## Why Flask?

Flask is:
- **Lightweight** - Minimal setup required
- **Flexible** - Choose your own tools and libraries
- **Well-documented** - Extensive documentation and community support
- **Pythonic** - Feels natural if you know Python

## Setting Up

First, install Flask:

```bash
pip install flask flask-restful
```

## Basic API Structure

Here's a simple Flask API for managing a todo list:

```python
from flask import Flask, jsonify, request
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

# In-memory storage (use a database in production!)
todos = {}

class TodoList(Resource):
    def get(self):
        return jsonify(todos)
    
    def post(self):
        todo_id = len(todos) + 1
        todos[todo_id] = request.json
        return jsonify({todo_id: todos[todo_id]}), 201

class Todo(Resource):
    def get(self, todo_id):
        return jsonify({todo_id: todos.get(todo_id)})
    
    def put(self, todo_id):
        todos[todo_id] = request.json
        return jsonify({todo_id: todos[todo_id]})
    
    def delete(self, todo_id):
        if todo_id in todos:
            del todos[todo_id]
            return '', 204
        return '', 404

api.add_resource(TodoList, '/todos')
api.add_resource(Todo, '/todos/<int:todo_id>')

if __name__ == '__main__':
    app.run(debug=True)
```

## Testing the API

You can test your API using `curl`:

```bash
# Create a new todo
curl -X POST http://localhost:5000/todos \
  -H "Content-Type: application/json" \
  -d '{"task": "Learn Flask", "completed": false}'

# Get all todos
curl http://localhost:5000/todos

# Update a todo
curl -X PUT http://localhost:5000/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"task": "Learn Flask", "completed": true}'

# Delete a todo
curl -X DELETE http://localhost:5000/todos/1
```

## Best Practices

1. **Use HTTP status codes correctly**
   - 200 OK for successful GET requests
   - 201 Created for successful POST requests
   - 204 No Content for successful DELETE requests
   - 404 Not Found when resource doesn't exist

2. **Validate input data**
   ```python
   from flask_restful import reqparse
   
   parser = reqparse.RequestParser()
   parser.add_argument('task', required=True, help='Task cannot be blank')
   parser.add_argument('completed', type=bool, default=False)
   ```

3. **Use proper error handling**
   ```python
   @app.errorhandler(404)
   def not_found(error):
       return jsonify({'error': 'Not found'}), 404
   ```

4. **Implement authentication and authorization**
   - Use JWT tokens or OAuth
   - Never store sensitive data in plain text

## Next Steps

To take this further, consider:
- Adding a database (SQLAlchemy)
- Implementing authentication (Flask-JWT)
- Adding input validation (Marshmallow)
- Writing tests (pytest)
- Deploying to production (Heroku, AWS, etc.)

## Conclusion

Flask makes it easy to build RESTful APIs in Python. With just a few lines of code, you can create a functional API that follows REST principles.

Happy building! 🎉
