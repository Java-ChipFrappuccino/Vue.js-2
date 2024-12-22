<template>
  <Navbar />
  <Event :변수명="담을값[eventTextNum]" />
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)" />
  <button @click="showAllMovie()">전체보기</button>
  <Movies
    :data="data_temp"
    @openModal="
      isModal = true;
      selectedMovie = $event;
    "
    @increseLike="increseLike($event)"
  />
  <Modal
    :data="data_temp"
    :isModal="isModal"
    :selectedMovieData="selectedMovieData()"
    @closeModal="isModal = false"
  />
  <!-- 자식에게서 @이벤트가 발생하면 부모는 그에 걸맞는 데이터를 변경 시켜줄수있다 -->
</template>

<script>
import data from './assets/movies';
import Navbar from './components/Navbar.vue';
import Modal from './components/Modal.vue';
import Event from './components/Event.vue';
import Movies from './components/Movies.vue';
import SearchBar from './components/SearchBar.vue';
export default {
  name: 'App',
  data() {
    return {
      selectedMovie: 0,
      isModal: false,
      data: data, // 원본
      data_temp: [...data], // 구조분해할당으로 원본 배열을 새로운 배열에 그대로 복사
      담을값: [
        'NETPLIX 강렬한 운명의 드라마, 경기크리처',
        '디즈니 100주년 기념작, 위시',
        '그날, 대한민국의 운명이 바뀌었다, 서울의 봄',
      ],
      eventTextNum: 0,
      interval: null,
    };
  },
  methods: {
    increseLike(id) {
      // this.data[i].like += 1;
      this.data.find((movie) => {
        if (movie.id == id) {
          movie.like++;
        }
      });
    },
    searchMovie(search) {
      this.data_temp = data.filter((movie) => {
        return movie.title.includes(search);
      });
    },
    showAllMovie() {
      this.data_temp = [...data];
    },
    selectedMovieData() {
      return this.data.find((movie) => {
        return movie.id === this.selectedMovie;
      });
    },
  },
  components: {
    Navbar: Navbar,
    Modal: Modal,
    Event: Event,
    Movies: Movies,
    SearchBar: SearchBar,
  },
  mounted() {
    this.inteval = setInterval(() => {
      if (this.eventTextNum == this.담을값.length - 1) this.eventTextNum = 0;
      else this.eventTextNum += 1;
    }, 3000);
  },
  unmounted() {
    clearInterval(this.interval);
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}

p:has(.btn-all) {
  text-align: center;
}
</style>
