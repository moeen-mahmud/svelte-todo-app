<script>
  // third party modules
  import {v4 as uuid} from 'uuid';
  import { afterUpdate } from 'svelte';

  // local modules
  import './app.css';
  import TodoInput from './components/todo-input.svelte';
  import TodoList from './components/todo-list.svelte';
  // import TodoReport from './components/todo-report.svelte';

  $:todoList = [];
  $:todoError = '';
  let todo = '';
  let editedTodo = '';

  const addTodo = () => {
    if(todo) {
      todoList = [...todoList, {id: uuid(), todo, isCompleted: false, isEditing: false}];
      todo = '';
      return;
    } 
    todoError = 'Please write something first!';
    return;
  }

  const deleteTodo = (id) => {
    const updatedTodo = todoList?.filter(todo => todo?.id !== id);
    todoList = updatedTodo;
  }

  const handleCompleteTodo = (id) => {
    const updatedTodo = todoList?.map(todo => {
      if(todo?.id === id) {
        todo.isCompleted = !todo.isCompleted;
      }
      return todo;
    });
    todoList = updatedTodo;
  }

  const handleEditTodo = (id) => {
    const updatedTodo = todoList?.map(todo => {
      if(todo?.id === id) {
        todo.isEditing = !todo.isEditing;
        editedTodo = todo.todo;
      }
      return todo;
    });

    todoList = updatedTodo;
  }

  const handleUpdateTodo = (id) => {
    const updatedTodo = todoList?.map(todo => {
      if(todo?.id === id) {
        todo.todo = editedTodo;
        todo.isEditing = false;
      }
      return todo;
    });

    todoList = updatedTodo;
  }
  
  afterUpdate(() => {
    if(todo?.length > 0) {
      todoError = '';
    }
  });
  
  // $:totalTodo = todoList?.length;
  // $:totalCompletedTodo = todoList?.filter(todo => todo?.isCompleted)?.length;
  // $:totalIncompleteTodo = todoList?.filter(todo => !todo?.isCompleted)?.length;

  // $:console.log("todoList", todoList);

</script>

<main class="container relative mx-auto">
  <div class="flex items-center justify-center h-full py-4">
    <h1 class="text-5xl font-bold text-teal-500">
      Svelte Todo App
    </h1>
  </div>
  <TodoInput bind:todo={todo} {addTodo} {todoError}/>
  <TodoList {todoList} {deleteTodo} {handleCompleteTodo} {handleEditTodo} {handleUpdateTodo} bind:editedTodo={editedTodo}/>
</main>