<template>
  <b-container class="mt-4 mb-4">
    <h1 class="text-center">{{ msg }}</h1>
    <div class="db-todoapp">
      <div @click="switchOn=!switchOn" class="db-switch">
        <span class="db-switch-slide" :class="switchOn ? '': 'active'"></span>
        <span class="db-switch-text">Open search</span>
      </div>
      <div class="db-search" v-show="!switchOn">
        <b-form-input v-model="filter" placeholder="Type to Search" class="db-search-input" />
      </div>
      <div class="db-add">
        <input class="db-newtodo" v-model="newTodo" @keyup.enter="addTodo" placeholder="type new todo here and then press enter" />
      </div>
      <b-table striped hover :items="todos" :fields="fields" :filter="filter">
        <template slot="title" slot-scope="row">
          <p class="m-0">{{row.item.title}}</p>
        </template>
        <template slot="remove" slot-scope="row" class="db-remove-wrapper">
          <button class="db-remove" @click="removeTodo(row)"></button>
        </template>
      </b-table>
    </div>
  </b-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      fields: [
        {
          key: 'id',
          label: '#',
          sortable: true
        },
        {
          key: 'title',
          label: 'Todo title',
          sortable: true
        },
        {
          key: 'remove',
          label: 'Remove',
          sortable: false,
          'class': 'text-right'
        }
      ],
      currentOrder: 'id',
      switchOn: true,
      msg: 'Welcome to my list',
      newTodo: [],
      todos: [{
        id: '1',
        title: 'test example first'
      }],
      filter: null
    }
  },
  methods: {
    addTodo: function () {
      let value = this.newTodo && this.newTodo.trim()
      if (!value) {
        return
      }
      this.todos.push({
        id: this.todos.length + 1,
        title: value
      })
      this.newTodo = ''
    },
    removeTodo: function (row) {
      this.todos.splice(this.todos.indexOf(row), 1)
    }
  }
}
</script>

<style scoped lang="scss">
  * {
    color: #8b8f97;
    outline: none;
  }

  /* begin style for search */
  .db-search {
    display: inline-block;
    vertical-align: top;
    margin-left: 60px;
    width: calc(100% - 125px);

    .db-search-input {
      width: 40%;
      border: none;
      height: 34px;
      border-bottom: 1px dashed #d0d0d0;
      margin-right: 60px;
    }
  }
  /* end style for search */

  /* begin style for todoapp */
  .db-todoapp {
    font-size: 12px;
    width: 80%;
    margin: auto;
    background: #fff;
    position: relative;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
    border: 1px solid rgba(0, 0, 0, 0.2);
    &::before {
      content: '';
      position: absolute;
      right: 0;
      bottom: 0;
      left: 0;
      height: 50px;
      overflow: hidden;
      box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6, 0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6, 0 17px 2px -6px rgba(0, 0, 0, 0.2);
    }
  }

  .db-add {
    position: relative;
    &::before {
      content: '';
      position: absolute;
      background: url("../assets/img/icon-add.png") no-repeat;
      height: 8px;
      width: 8px;
      left: 10px;
      top: 43%;
    }
    .db-newtodo {
      border: none;
      width: 100%;
      cursor: pointer;
      height: 38px;
      padding-left: 30px;
      &:focus {
        box-shadow: 0 0 4px 2px #80bdff;
        cursor: default;
      }
    }
  }
  .db-remove {
    display: inline-block;
    position: relative;
    top: 0;
    right: 20px;
    bottom: 0;
    width: 10px;
    height: 10px;
    margin: auto;
    transition: color 0.2s ease-out;
    background: none;
    border: none;
    cursor: pointer;
    &::after {
      content: '';
      background: url("../assets/img/icon-trash.png") no-repeat center;
      height: 12px;
      width: 11px;
      display: block;
    }
  }
  /* end style for todoapp */

  /* begin style for switcher */
  .db-switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }

  .db-switch-slide {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: .4s;
    transition: .4s;
    &::before {
      position: absolute;
      content: "";
      height: 26px;
      width: 26px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      -webkit-transition: .4s;
      transition: .4s;
      border-radius: 50%;
    }
  }

  .db-switch-slide.active {
    background-color: #2196F3;
    &::before {
      -webkit-transform: translateX(26px);
      -ms-transform: translateX(26px);
      transform: translateX(26px);
    }
  }

  .db-switch-text {
    display: inline-block;
    margin-left: 65px;
  }
  /* end style for switcher */
</style>
