## Toggle Status

presentation : https://drive.google.com/open?id=1sVGFKDgr3Kd138my5XHJuJfwJMAuWPgH

1. In `TodoItem.js`, add an onClick event for the status icon with an alert like this to show them what will happen

```javascript
<i className={statIcon()} onClick={() => alert("CHANGE STATUS")} />
```

2. create a constructer and create a method with an alert and call this method in the onClick instead

```javascript
constructor(props) {
super(props)
this.toggleStatus = this.toggleStatus.bind(this);
}

...
toggleStatus(){
  alert('CHANGE STATUS')
}

...

<i className={statIcon()} onClick={this.toggleStatus} />
```

3. add a state using the values of the props.task

```javascript
constructor(props) {
  ...
  this.state = {
    done: props.task.done
  }
  ...
}
```

4. change the value (toggle) of the status state in the previously created function.

```javascript
toggleStatus() {
  const newStatus = !this.state.done;
  this.setState({done: newStatus});
}
```

5. change the used status in the render function from props to state

```javascript
render(){
  ...
  const statusIcon = () => {
    if (this.state.done) {
      return "fa fa-check-circle";
    } else {
      return "fa fa-times-circle";
    }
  };
  ...
}
```

### Delete Task

1. in `TodoItem.js`, add an onClick event for the delete icon with an alert

```javascript
<i className="fa fa-times" onClick={() => alert(`DELETE task #${task.id}`)} />
```

2. Discuss why this component cannot delete itself.

3. In `App.js`, add a method that recieves an `id` and alerts it

```javascript
deleteTask(id) {
  alert(`DELETE task #${id}`)
}
```

4. Pass this method down through `TodoList` to `TodoItem` as a prop

`App.js`

```javascript
<TodoList tasks={this.state.tasks} deleteTask={this.deleteTask} />
```

`TodoList.js`

```javascript
let taskRows = this.props.tasks.map(task => (
  <TodoItem task={task} key={task.task} deleteTask={this.props.deleteTask} />
));
```

5. Replace the alert with this method

`TodoItem.js`

```javascript
<i className="fa fa-times" onClick={() => deleteTask(task.id)} />
```

6. Rewrite `deleteTask` to actually modify state (don't forget to bind)

`App.js`

```javascript
deleteTask(id) {
  const tasks = this.state.tasks.filter(task => task.id !== id);
  this.setState({ tasks: tasks });
}
```
