Here are simple examples of a REST API implemented in both Python (using Flask) and JavaScript (using Express.js).

### Python Example (Flask)
```
from flask import Flask, jsonify, request

app = Flask(__name__)

# Sample data
tasks = [
    {'id': 1, 'title': 'Do the laundry', 'done': False},
    {'id': 2, 'title': 'Write some code', 'done': False}
]

@app.route('/tasks', methods=['GET'])
def get_tasks():
    return jsonify(tasks)

@app.route('/tasks/<int:task_id>', methods=['GET'])
def get_task(task_id):
    task = next((task for task in tasks if task['id'] == task_id), None)
    return jsonify(task) if task else ('', 404)

@app.route('/tasks', methods=['POST'])
def create_task():
    new_task = request.get_json()
    tasks.append(new_task)
    return jsonify(new_task), 201

if __name__ == '__main__':
    app.run(debug=True)
```
### JavaScript Example (Express.js)

```
const express = require('express');
const app = express();
app.use(express.json());

// Sample data
let tasks = [
    { id: 1, title: 'Do the laundry', done: false },
    { id: 2, title: 'Write some code', done: false }
];

app.get('/tasks', (req, res) => {
    res.json(tasks);
});

app.get('/tasks/:taskId', (req, res) => {
    const taskId = parseInt(req.params.taskId);
    const task = tasks.find(t => t.id === taskId);
    if (task) {
        res.json(task);
    } else {
        res.status(404).send();
    }
});

app.post('/tasks', (req, res) => {
    const newTask = req.body;
    tasks.push(newTask);
    res.status(201).json(newTask);
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

### Explanation

-   **Python (Flask)**:
    -   The Flask app defines three routes:
        -   `GET /tasks`: Returns a list of tasks.
        -   `GET /tasks/<task_id>`: Returns a specific task by its ID.
        -   `POST /tasks`: Creates a new task.
-   **JavaScript (Express.js)**:
    -   The Express app has similar routes with the same functionality:
        -   `GET /tasks`: Returns all tasks.
        -   `GET /tasks/:taskId`: Returns a specific task based on the provided ID.
        -   `POST /tasks`: Adds a new task to the list.

Both examples use in-memory data for simplicity. In a real application, you would typically connect to a database for persistent storage.

To run the JavaScript (Express.js) API, you need to follow these steps:

### Steps to Run the JavaScript (Express.js) API

1.  **Install Node.js**: Make sure you have Node.js installed on your machine. You can download it from [nodejs.org](https://nodejs.org/).
    
2.  **Create a New Directory**: Create a new directory for your project and navigate into it.

```
mkdir my-express-api
cd my-express-api
```
3. **Initialize a New Node.js Project**: Run the following command to create a `package.json` file.
```
npm init -y
```
4. **Install Express**: Install the Express framework using npm.
```
npm install express
```
5.  **Create Your API File**: Create a new file called `app.js` (or any name you prefer) and copy the Express.js code into that file.
    
6.  **Run the Server**: Start your server by running the following command in the terminal:

```
node app.js
```
7.  **Access the API**: Open your web browser and navigate to the following URLs to see the API in action:
    
    -   To get all tasks:  `http://localhost:3000/tasks`
    -   To get a specific task (e.g., task with ID 1):  `http://localhost:3000/tasks/1`

### Note

-   Make sure the server is running in the terminal before trying to access it in the browser.
-   You can also use tools like Postman or curl to test the API endpoints, especially for  `POST`  requests. For example, to create a new task, you would send a  `POST`  request to  `http://localhost:3000/tasks`  with the task data in the request body.