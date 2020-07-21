<template>
  <div>
    <b-table striped hover :items="items" :fields="fields" @row-clicked="rowClick"></b-table>
    <b-button @click="writeContent">글쓰기</b-button>
  </div>
</template>

<script>
import data from "@/data";
// 정렬 : https://blog.naver.com/haskim0716n/221681695401
let items = data.Content.sort((a, b) => {
  return b.content_id - a.content_id;
}); // 내림차순
const user_name = "운영자";

export default {
  name: "Board",
  data() {
    return {
      // bootstrap 'b-table' 필드 설정
      fields: [
        {
          key: "content_id",
          label: "NUMBER"
        },
        {
          key: "title",
          label: "TITLE"
        },
        {
          key: "user_name",
          label: "AUTHOR"
        },
        {
          key: "created_at",
          label: "DATE"
        }
      ],
      items: items
    };
  },
  methods: {
    rowClick(item, index, e) {
      this.$router.push({
        path: `/detail/${item.content_id}`
      });
    },

    writeContent() {
      this.$router.push({
        path: `/create`
      });
    }
  },
  computed: {
    rows() {
      return this.items;
    }
  }
};
</script>