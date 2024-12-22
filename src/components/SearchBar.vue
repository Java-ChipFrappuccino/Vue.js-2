<template>
  <div class="search-box">
    <input
      type="search"
      name=""
      id=""
      placeholder="검색어 입력"
      @change="
        $emit('searchMovie', $event.target.value);
        inputText = $event.target.value;
        $event.target.value = ''; //검색을 완료하면 타겟값을 초기화 (검색창 비움)
      "
    />
    <!-- v-model="inputText" 
     이걸 사용하면 편하지만 한 글자씩 실시간으로 반응하기 때문에 지금 사용하기는 애매하다
     우리는 사용자가 모든값을 입력한 후에 검색버튼을 누르면 그 값을 가지고 비교를 해야한다-->
    <button>검색</button>
  </div>
  <p>{{ inputText }}</p>
</template>

<script>
export default {
  name: 'SearchBarComponent',
  data() {
    return {
      inputText: '',
    };
  },
  watch: {
    inputText(name) {
      //감시하고 싶은 데이터변수명(매개변수는 2개가 올수있다 / (현재 입력값, 이전값))
      const findName = this.data.filter((movie) => movie.title.includes(name));

      if (findName.length == 0) {
        alert('해당하는 자료가 없습니다');
      }
    },
  },
  props: {
    data: Array, //담겨온 값의 타입 작성,
  },
};
</script>

<style>
.search-box {
  padding: 10px;
  display: flex;
  justify-content: center;
}

.search-box input {
  padding: 5px 10px;
}

.search-box button {
  margin: 0;
}
</style>
