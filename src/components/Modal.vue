<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ selectedMovieData.title }}</h3>
      <h3>{{ selectedMovieData.year }}</h3>
      <h3>{{ selectedMovieData.category }}</h3>

      <p>영화상세보기</p>
      <button @click="$emit('closeModal')">닫기</button>
      <!-- 프롭스로 넘겨받은 부모데이터를 직접 변경할 권리(즉 다시 부모에게 전달x, 그래서 단방향 데이터 흐름)는 자식에겐 없다, 오직 사용만 가능 
       그래서 자식은 부모에게 데이터를 변경해줄것을 이벤트를 발생시켜서 요구할수있다 (closeModal 이벤트를 부모에게 전달함) -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalComponent',
  props: {
    data: Array,
    isModal: Boolean,
    selectedMovieData: Object,
  },
};
</script>

<style></style>
