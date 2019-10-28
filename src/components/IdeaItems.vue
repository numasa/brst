<template>
  <div class="text-center">
    <ul class="list">
      <transition-group name="flip">
        <template v-for="item in this.$data.list">
          <li :key="item" class="item">
            <v-chip
              class="item__text"
              large
              close
              color="teal"
              text-color="white"
              @click:close="onDeleteClick(item)"
            >{{ item }}</v-chip>
          </li>
        </template>
      </transition-group>
    </ul>
    <v-btn
      large
      @click="onShuffleClick"
      color="normal"
    >shuffle</v-btn>
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  data() {
    return {
      list: this.$props.ideas
    }
  },
  props: [
    'ideas',
  ],
  methods: {
    onShuffleClick() {
      this.$data.list = _.shuffle(this.$data.list);
    },
    onDeleteClick(item) {
      const index = this.$data.list.indexOf(item);
      this.$data.list.splice(index, 1);
    }
  },
  watch: {
    ideas: function (newVal) {
      this.list = newVal;
    }
  }
}
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.list {
  position: relative;
  margin: 20px 0 0;
  padding: 0;
}

.item {
  position: relative;
  display: inline-block;
  padding: 10px 20px;
  transition: all 0.5s;
  
  &__delete {
    position: absolute;
    top: 0;
    right: 0;
    width: 20px;
    height: 20px;
    
    &::before, &::after {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 70%;
      height: 2px;
      background-color: #ccc;
      content: '';
    }
    
    &::before {
      transform: translate3d(-50%, -50%, 0) rotate(45deg);
    }
    
    &::after {
      transform: translate3d(-50%, -50%, 0) rotate(135deg);
    }
  }
}

.flip {
  /*
  // 要素が動くときにtransitionを設定する（.itemでtransitionを設定しているため-moveで書く必要はない）
  // &-move {
  //   transition: transform 0.5s;
  // }
  
  // 要素が入るときのアニメーション */
  &-enter {
    &-active {
      opacity: 0;
      transform: translate3d(0, -30px, 0);
    }
    &-to {
      opacity: 1;
      transform: translate3d(0, 0, 0);
    }
  }

  // 要素が消える時のアニメーション
  &-leave {
    &-active {
      position: absolute;
    }
    &-to {
      opacity: 0;
      transform: translate3d(0, -30px, 0);
    }
  }
}
</style>
