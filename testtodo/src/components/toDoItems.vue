<template>
  <div class="container center">
    <h1>toDoTest</h1>

    <div class="text">
      <input type="text" @keyup.enter="addItem" v-model="input" placeholder="Введите текст...">
      <button class="btn add" @click="addItem">+</button>
    </div>

    <span v-if="items.length>0" :style="{color:changeColor}">{{listSummary}}</span>
    <h2 v-else>Добавьте элемент</h2>

    <ul>
      <li :class="{completed: item.done}" v-for="(item,index) in items" :key='index' draggable="true">
          
          <div class="check" @click="takeItem(index)">
            <input type="checkbox" id="lbl" ref="mail" @click:="isFocus" :checked="item.done">
            {{item.title}}
          </div>

          <div class="buttons">
            <button class="btn edit" @click="changeItem(index)">
              <font-awesome-icon icon="edit" /></button>
            <button class="btn delete" @click="deleteItem(index)">
              <font-awesome-icon icon="trash" /></button>
          </div>

      </li>
    </ul>

    <button class="btn reset" v-if="this.items.length > 0" @click="items = []">Очистить лист</button>
  </div>
</template>


<script>
  export default {
    name: 'toDoItems',
    
    data() {
      return {
        activeIndex: 0,
        items: [{
          id:1,
          title: "title",
          done: false
        }],
        done: [],
        input: '',
        isChange: false
      }
    },

    methods: {
      addItem() {
        if (this.input) {
          this.items.push({
            title: this.input,
            done: false
          })
          this.input = ""
        }
      },

      takeItem(index) {
        this.activeIndex = index
        this.items[index].done = !this.items[index].done
      },

      deleteItem(index) {
        this.items.splice(index, 1)
      },
      changeItem(index){
        this.newContent = this.items[index].title
        this.isChange = !this.Change
      }
    },

    computed: {

      isDone() {
        return this.items.filter(item => item.done === true)
      },

      listSummary() {
        const numberFinishedItems = this.items.filter(item => item.done).length
        return `${numberFinishedItems} из ${this.items.length} задач завершены`
      },

      changeColor() {
        const numberForColor = this.items.filter(item => item.done).length
        if (numberForColor == (this.items.length)) {
          return '#50ef34'
        }
      }
    }

  }
</script>
<style lang="">

</style>