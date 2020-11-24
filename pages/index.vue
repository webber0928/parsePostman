<template>
  <div>
    <b-form-textarea
      id="textarea"
      v-model="text"
      placeholder="Enter something..."
      rows="3"
      max-rows="6"
      @update="parseFormat"
    ></b-form-textarea>

    <pre class="mt-3 mb-0">{{ parseText }}</pre>
    <pre class="mt-3 mb-0">{{ errorMsg }}</pre>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      parseText: '',
      errorMsg: '',
    }
  },
  methods: {
    parseFormat() {
      console.log('L25')
      let obj = ''
      try {
        obj = JSON.parse(this.text)
      } catch (error) {
        console.log(error)
        this.errorMsg = error
        return
      }

      this.parseText = {
        name: obj.info.name,
        api: list,
      }

      let list = {}
      obj = obj.item.map((o, index) => {
        console.log(o)
        list[o.name] = []
        o.item.forEach((x, y) => {
          list[o.name].push({
            name: `[${x.request.method}] ${x.name}`,
          })
        })
        return o
      })

      this.parseText.api = list

      this.errorMsg = ''
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
