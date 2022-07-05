<template>
  <tr>
    <th><input type="checkbox" v-model="list.checked" /></th>
    <th>{{ list.name }}</th>
    <th>{{ list.price }}</th>
    <th>
      <button @click="list.num--">-</button>{{ list.num
      }}<button @click="list.num++">+</button>
    </th>
    <th>{{ list.num * list.price }}</th>
    <th><button @click="del(list.name)">删除</button></th>
  </tr>
</template>

<script>
export default {
  props: {
    list: {
      type: Object,
      default: () => {
        return {};
      },
    },
  },
  methods: {
    del(val) {
      // console.log(val);
      const index = this.$parent.goodList.findIndex((ele) => ele.name == val);
      this.$parent.goodList.splice(index, 1);
    },
  },
};
</script>

<style></style>
