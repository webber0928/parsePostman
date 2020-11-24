<template>
  <div class="container">
    <!-- Styled -->
    <b-form-file
      v-model="file1"
      :state="Boolean(file1)"
      head-variant="dark"
      :bordered="true"
      placeholder="Choose a file or drop it here..."
      drop-placeholder="Drop file here..."
      isRowHeader="false"
      @change="update"
      @input="input"
    ></b-form-file>
    <br>
    <br>
    <div
      v-for="(item, index) in parseText.api"
      :key="index"
    >
      <h2>{{index}}</h2>
      <b-table
        striped
        hover
        :items="item"
      ></b-table>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      file1: null,
      parseText: {},
    }
  },
  methods: {
    update(file) {
      console.log('L34')
      console.log(file)
    },
    input(file) {
      console.log('L35')
      console.log(file)
      const reader = new FileReader() //建立FileReader 監聽 Load 事件
      reader.addEventListener('load', this.imageLoader)
      reader.readAsText(file)
    },
    imageLoader(event) {
      let obj = JSON.parse(event.target.result)
      console.log('L50', event.target.result)

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
    },
  },
}
</script>
