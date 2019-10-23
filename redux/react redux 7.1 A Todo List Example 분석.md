### react redux 7.1 A Todo List Example 분석

------

**The React UI Components**

* TodoApp
  * AddTodo
  * TodoList
  * Todo
  * VisibilityFilters

------

**'AddTodo' Component**

- `onChange`를 이용하여 State를 set 한다.

- Add Todo 버튼을 누를시 store에 todo를 추가하기 위해 action을 dispatch한다. 

------

**'TodoList' Component**

- todo 리스트를 rendering 한다. 
- `VisibilityFilters`에 따라 filtered list를 렌더링 한다. 

-------

**'todo' Component**

- a single todo item
- todo의 완료 상태를 `onClick`을 이용하여, action을 dispatch한다.

---------

**'visibilityFilters' Component**

- filter기능을 한다. (all, completed, incomplete)
- `setFilter`action을 dispatch한다.