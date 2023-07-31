<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button class="getData" @click="funGetLocalStorage">get localStorage</button>
    <button class="clear" @click="funRemoveLocalStorage">remove localStorage</button>
    <ul>
      <li v-for="(value, key) in localStorage" :key="key">
        {{ key }}: <span v-if="value"> {{ value }} - type {{ typeof value }}</span>
      </li>
    </ul>
    <button class="setData" @click="funSetStringLocalStorage">set string localStorage</button>
    <button class="setData" @click="funSetNumberLocalStorage">set number localStorage</button>
    <button class="setData" @click="funSetBooleanLocalStorage">set boolean localStorage</button>
    <button class="setData" @click="funSetObjectLocalStorage">set object localStorage</button>

    <button class="getData" @click="funGetSessionStorage">get sessionStorage</button>
    <button class="clear" @click="funRemoveSessionStorage">remove sessionStorage</button>
    <ul>
      <li v-for="(value, key) in sessionStorage" :key="key">
        {{ key }}: <span v-if="value"> {{ value }} - type {{  typeof value }}</span>
      </li>
    </ul>
    <button class="setData" @click="funSetStringSessionStorage">set string sessionStorage</button>
    <button class="setData" @click="funSetNumberSessionStorage">set number sessionStorage</button>
    <button class="setData" @click="funSetBooleanSessionStorage">set boolean sessionStorage</button>
    <button class="setData" @click="funSetObjectSessionStorage">set object sessionStorage</button>

    <button class="showPopup" @click="showPopup">Show Success Popup</button>

    <button class="clear" @click="funClear">Clear</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data: function () {
    return {
      localStorage: {
        string: null,
        number: null,
        boolean: null,
        object: null
      },
      sessionStorage: {
        string: null,
        number: null,
        boolean: null,
        object: null
      },
    }
  },
  mounted() {
    this.funGetLocalStorage()
    this.funGetSessionStorage()
  },
  methods: {
    // remove the localStorage
    funRemoveLocalStorage() {
      Object.keys(this.localStorage).forEach(key => {
        localStorage.removeItem(`local-${key}`)
      });
      this.localStorage = { string: null, number: null, boolean: null, object: null }
    },
    // get the localStorage
    funGetLocalStorage() {
      this.localStorage.string = localStorage.getItem('local-string')
      this.localStorage.number = localStorage.getItem('local-number')
      this.localStorage.boolean = localStorage.getItem('local-boolean')
      this.localStorage.object = localStorage.getItem('local-object')
    },
    // set local storage
    funSetStringLocalStorage() {
      localStorage.setItem('local-string', 'Tom')
    },
    funSetNumberLocalStorage() {
      localStorage.setItem('local-number', 1)
    },
    funSetBooleanLocalStorage() {
      localStorage.setItem('local-boolean', true)
    },
    funSetObjectLocalStorage() {
      localStorage.setItem('local-object', JSON.stringify({a: 1}))
    },

    // Session storage
    // get session storage
    funGetSessionStorage() {
      this.sessionStorage.string = sessionStorage.getItem('session-string')
      this.sessionStorage.number = sessionStorage.getItem('session-number')
      this.sessionStorage.boolean = sessionStorage.getItem('session-boolean')
      this.sessionStorage.object = sessionStorage.getItem('session-object')
    },
    // set session storage
    funSetStringSessionStorage() {
      sessionStorage.setItem('session-string', 'Tom Session')
    },
    funSetNumberSessionStorage() {
      sessionStorage.setItem('session-number', 2)
    },
    funSetBooleanSessionStorage() {
      sessionStorage.setItem('session-boolean', false)
    },
    funSetObjectSessionStorage() {
      sessionStorage.setItem('session-object', JSON.stringify({b: 1}))
    },

    // remove sessionStorage
    funRemoveSessionStorage() {
      Object.keys(this.sessionStorage).forEach(key => {
        sessionStorage.removeItem(`session-${key}`)
      });
      this.sessionStorage = { string: null, number: null, boolean: null, object: null }
    },

    // clear all
    funClear() {
      localStorage.clear()
      sessionStorage.clear()
      this.localStorage = { string: null, number: null, boolean: null, object: null }
      this.sessionStorage = { string: null, number: null, boolean: null, object: null }
    },
    showPopup() {
      const windowFeatures = "left=100,top=100,width=1500,height=700";
      window.open("HelloWorld", "", windowFeatures);
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  width: 60%;
  margin: auto;
  ul > li {
    text-align: left;
  }

  button {
    border: none;
    color: #fff;
    padding: 10px 20px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin-top: 10px;
    margin-left: 10px;
    cursor: pointer;
    background-color: #4caf50;
  }
  .getData {
    background-color: #4caf50;
  }
  .setData {
    background-color: #0032f8;
  }
  .showPopup {
    background-color: red;
  }
  .clear {
    background-color: rgb(255, 190, 190);
  }
}

</style>
