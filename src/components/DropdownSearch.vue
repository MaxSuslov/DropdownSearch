<template>
  <div class="hello">
    <section class="dropdown-wrapper">
      <!-- <h2>{{ msg }}</h2> -->
      <div @click="isVisible = !isVisible" class="selected-item">
        <span></span>
        <svg
          class="dropdown-icon"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          width="24"
          height="24"
        >
          <path
            d="M11.9997 10.8284L7.04996 15.7782L5.63574 14.364L11.9997 8L18.3637 14.364L16.9495 15.7782L11.9997 10.8284Z"
          ></path>
        </svg>
      </div>
      <div v-if="isVisible" class="dropdown-popover">
        <input v-model="searchQuery" type="text" placeholder="Search Deal" />
        <div class="options">
          <ul>
            <li
              @click="selectItem(deal)"
              v-for="(user, index) in filteredUser"
              :key="`user-${index}`"
            >
              {{ user.name }}
            </li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "DropdownSearch",
  props: {
    msg: String,
  },
  data() {
    return {
      searchQuery: "",
      selectedItem: null,
      isVisible: false,
      userArray: [],
    };
  },
  computed: {
    filteredUser() {
      const query = this.searchQuery.toLowerCase();
      if (this.searchQuery === "") {
        return this.userArray;
      }
      return this.userArray.filter((deal) => {
        return Object.values(deal).some((word) =>
          String(word).toLowerCase().includes(query)
        );
      });
    },
  },
  methods: {
    selectItem(deal) {
      this.selectedItem = deal;
    },
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((json) => {
        console.log(json);
        this.userArray = json;
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.dropdown-wrapper {
  max-width: 350px;
  position: relative;
  margin: 0 auto;
  .selected-item {
    height: 40px;
    border: 2px solid lightgrey;
    border-radius: 5px;
    padding: 5px 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 18px;
    font-weight: 400;
  }
  .dropdown-popover {
    position: absolute;
    border: 2px solid lightgray;
    top: 46px;
    left: 0;
    right: 0;
    background-color: #fff;
    max-width: 100%;
    padding: 10px;

    input {
      width: 90%;
      height: 30px;
      border: 2px solid lightgray;
      font-size: 16px;
      padding-left: 8px;
    }

    .options {
      width: 100%;

      ul {
        list-style: none;
        text-align: left;
        padding-left: 8px;
        max-height: 180px;
        overflow-y: scroll;
        overflow-x: hidden;

        li {
          width: 100%;
          border-bottom: 1px solid lightgray;
          padding: 10px;
          background-color: #f1f1f1;
          cursor: pointer;
          font-size: 16px;
          &:hover {
            background: #70878a;
            color: #fff;
            font-weight: bold;
          }
        }
      }
    }
  }
}
</style>
