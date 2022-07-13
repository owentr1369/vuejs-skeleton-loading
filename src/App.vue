<template>
  <div id="app">
    <div class="grid"></div>
    <template id="card-template">
      <div class="card">
        <div class="header">
          <img
            class="header-img skeleton"
            src="https://source.unsplash.com/100x100/?nature"
          />
          <div class="title" data-title>
            <div class="skeleton skeleton-text"></div>
            <div class="skeleton skeleton-text"></div>
          </div>
        </div>
        <div data-body>
          <div class="skeleton skeleton-text"></div>
          <div class="skeleton skeleton-text"></div>
          <div class="skeleton skeleton-text"></div>
          <div class="skeleton skeleton-text"></div>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      posts: null,
    };
  },
  mounted() {
    axios.get("https://jsonplaceholder.typicode.com/posts").then((response) => {
      this.posts = response.data;
      console.log("this.posts", this.posts);
    });
  },
  // watch: {
  //   posts: function () {
  //     const grid = document.querySelector(".grid");
  //     const cardTemplate = document.getElementById("card-template");
  //     for (let i = 0; i < 10; i++) {
  //       grid.append(cardTemplate.content.cloneNode(true));
  //     }
  //     console.log("Hello");
  //   },
  // },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  .skeleton {
    opacity: 0.7;
    animation: skeleton-loading 1s linear infinite alternate;
  }

  .skeleton-text {
    width: 100%;
    height: 0.5rem;
    margin-bottom: 0.25rem;
    border-radius: 0.125rem;
  }

  .skeleton-text:last-child {
    margin-bottom: 0;
    width: 80%;
  }

  @keyframes skeleton-loading {
    0% {
      background-color: hsl(200, 20%, 70%);
    }

    100% {
      background-color: hsl(200, 20%, 95%);
    }
  }

  .grid {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    padding: 1rem;
  }

  .card {
    background-color: white;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px,
      rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
    padding: 16px;
    border-radius: 4px;
  }

  .header {
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
  }

  .header-img {
    width: 50px;
    height: 50px;
    object-fit: cover;
    border-radius: 100%;
    margin-right: 1rem;
    flex-shrink: 0;
  }

  .title {
    font-weight: bold;
    font-size: 1.25rem;
    text-transform: capitalize;
    word-wrap: none;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    flex-grow: 1;
  }
}
</style>
