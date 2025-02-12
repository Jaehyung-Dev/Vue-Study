<template>
  <Navbar/>
  <Event :text="text"/>
  <Movies 
    :data="data" 
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
        selectedMovie: 0,
        text: 'NEPLIX 강렬한 운명의 드라마, 경기크리처!!!',
      }
    },
    methods: {
      increaseLike(i) {
        this.data[i].like += 1;
      }
    },
    components: {
      Navbar: Navbar,
      Modal: Modal,
      Event: Event,
      Movies: Movies,
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