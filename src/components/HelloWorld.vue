<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <p>localStorage: {{varLocalStorage}}<span v-if="varLocalStorage"> - {{ typeof varLocalStorage }}</span></p>
    <p>sessionStorage: {{varSessionStorage}}<span v-if="varSessionStorage"> - {{ typeof varSessionStorage }}</span></p>

    <button class="getData" @click="funGetLocalStorage">get localStorage</button>
    <button class="setData" @click="funSetLocalStorage">set localStorage</button>

    <button class="getData" @click="funGetSessionStorage">get sessionStorage</button>
    <button class="setData" @click="funSetSessionStorage">set sessionStorage</button>

    <button class="showPopup" @click="showPopup">Show Success Popup</button>

    <button class="clear" @click="funClear">Clear</button>
    <div v-if="show">
      <div class="popup">
        <h2>Success!</h2>
        <p>Your action was successful.</p>
        <button @click="hidePopup">Close</button>
      </div>
    </div>
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
      varLocalStorage: '',
      varSessionStorage: '',
      show: false
    }
  },
  mounted() {
    this.show = localStorage.getItem('closePopup') ? JSON.parse(localStorage.getItem('closePopup')) : true
  },
  methods: {
    funGetLocalStorage() {
      this.varLocalStorage = localStorage.getItem('localStorage') || "Not found"
    },
    funSetLocalStorage() {
      localStorage.setItem('localStorage', 'Tom')
    },
    funGetSessionStorage() {
      this.varSessionStorage = sessionStorage.getItem('sessionStorage') || "Not found"
    },
    funSetSessionStorage() {
      sessionStorage.setItem('sessionStorage', JSON.stringify({"a": 1}))
    },
    funRemoveLocalStorage() {
      localStorage.removeItem('localStorage')
      this.varLocalStorage = ''
    },
    funRemoveSessionStorage() {
      sessionStorage.removeItem('sessionStorage')
      this.varSessionStorage = ''
    },
    funClear() {
      localStorage.clear()
      sessionStorage.clear()
      this.varLocalStorage = ''
      this.varSessionStorage = ''
    },
    showPopup() {
      this.show = true
    },
    hidePopup() {
      this.show = false
      localStorage.setItem('closePopup', false)
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.popup {
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
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

</style>
