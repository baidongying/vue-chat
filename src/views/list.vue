<template>
  <div class="m-list">
    <ul>
      <li v-for="item in searchedUserList" :class="{ active: session.userId === item.id }" @click="select(item)">
        <img class="avatar"  width="30" height="30" :alt="item.name" :src="item.img">
        <p class="name">{{item.name}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {

      }
    },
    props: ['userList', 'sessionIndex', 'session', 'search'],
    methods: {
      select (value) {
          let subSessionIndex = this.userList.indexOf(value);
          this.$emit('update-sessionIndex', subSessionIndex);
      }
    },
    computed: {
      searchedUserList() {
        let arr = [];
        this.userList.map((item, index) => {
          if (item.name.indexOf(this.search) !== -1) {
            arr.push(item)
          }
        })
        return arr;
      }
    },
  };
</script>

<style lang="less">
  .m-list {
    li {
      padding: 12px 15px;
      border-bottom: 1px solid #292C33;
      cursor: pointer;
      transition: background-color .1s;
      &:hover {
          background-color: rgba(255, 255, 255, 0.03);
      }
      &.active {
          background-color: rgba(255, 255, 255, 0.1);
      }
    }
    .avatar, .name {
      vertical-align: middle;
    }
    .avatar {
      border-radius: 2px;
    }
    .name {
      display: inline-block;
      margin: 0 0 0 15px;
    }
  }
</style>