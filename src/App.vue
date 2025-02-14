<template>
  <Navbar/>
  <Event :text="text[eventTextNum]"/>
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies 
    :data="data_temp" 
    @openModal="isModal=true;selectedMovie=$event"
    @increaseLike="increaseLike($event)"/>
  <!-- props의 속성명과 변수명은 관례적으로 동일하게 사용한다. -->
  <Modal 
    :data="data"
    :isModal="isModal" 
    :selectedMovie="selectedMovie"
    @closeModal="isModal=false"/>
</template>

<script>
  import data from './assets/movies';
  import Navbar from './components/Navbar.vue';
  import Modal from './components/Modal.vue';
  import Event from './components/Event.vue';
  import Movies from './components/Movies.vue';
  import SearchBar from './components/SearchBar.vue';

  export default {
    // 이 안에 기능을 정의할 수 있음 Vue 문법임
    // name에 컴포넌트 이름이 들어간다.
    name: 'App',
    data() {
      // data안에 반드시 return문이 들어가야한다
      // return문 안에 변수를 정의의
      return {
        isModal: false,
        data: data,
        data_temp: [...data],
        selectedMovie: 0,
        text: [
          'NEPLIX 강렬한 운명의 드라마, 경기크리처!!!',
          '디즈니 100주년 기념작, 위시',
          '그날, 대한민국의 운명이 바뀌었다, 서울의 봄'
        ],
        eventTextNum: 0,
        interval: null,
      }
    },
    methods: {
      increaseLike(id) {
        // this.data[i].like += 1;
        this.data.find(movie => {
          if(movie.id == id) {
            movie.like += 1;
          }
        })
      },
      searchMovie(title) {
        // 영화제목이 포함된 데이터를 가져옴
        this.data_temp = this.data.filter(movie => {
          return movie.title.includes(title);
        })
      },
      showAllMovie() {
        this.data_temp = [...this.data]
      }
    },
    components: {
      Navbar: Navbar,
      Modal: Modal,
      Event: Event,
      Movies: Movies,
      SearchBar: SearchBar,
    },
    mounted() {
      console.log('mounted!!');
      this.interval = setInterval(() => {
        if(this.eventTextNum == this.text.length - 1) {
          this.eventTextNum = 0;
        } else {
          this.eventTextNum += 1;
        }
      }, 3000);
    },
    unmounted() {
      clearInterval(this.interval);
    }
  }
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
  }

  body {
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
  }

  h1, h2, h3 {
    margin-bottom: 1rem;
  }

  p {
    margin-bottom: .5rem;
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
</style>