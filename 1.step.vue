<template>
  <div>
    <Modal v-model="assissement.show">
      <template v-slot:content>
        <transition-group
          class="assissment"
          :name="assissement.isSlideBack ? 'slide-back' : 'slide-next'"
          tag="div"
        >
          <div class="step block-1" v-if="assissement.steps.step_1" :key="1">
            <h1 @click="slideNext(1)">Вперед</h1>
            <h3 class="text-center">step 1</h3>
          </div>
          <div class="step block-2" v-if="assissement.steps.step_2" :key="2">
            <div>
              <h1 @click="slideBack(2)">Назад</h1>
              <h1 @click="slideNext(2)">Вперед</h1>
            </div>
            <h3 class="text-center">step 2</h3>
          </div>
          <div class="step block-3" v-if="assissement.steps.step_3" :key="3">
            <h1 @click="slideBack(3)">Назад</h1>
            <h3 class="text-center">step 3</h3>
          </div>
        </transition-group>
      </template>
    </Modal>
  </div>
</template>

<script>
import Modal from '@/components/modal/Modal'

export default {
  name: 'Google',
  data() {
    return {
      assissement: {
        show: true,
        isSlideBack: false,
        steps: {
          step_1: true,
          step_2: false
        }
      }
    }
  },
  components: { Modal },
  methods: {
    slideNext(item) {
      this.assissement.isSlideBack = false
      this.assissement.steps[`step_${item}`] = false
      this.assissement.steps[`step_${item + 1}`] = true
    },
    slideBack(item) {
      this.assissement.isSlideBack = true
      this.assissement.steps[`step_${item}`] = false
      this.assissement.steps[`step_${item - 1}`] = true
    }
  }
}
</script>

<style lang="scss">
.modal {
  overflow: hidden;
  padding: 0 !important;
}

.assissment {
  position: relative;
  width: 400px;
  height: 400px;
  overflow: hidden;

  .step {
    width: 100%;
    height: 100%;
    padding: 20px;

    h1 {
      cursor: pointer;
      margin: 0;
    }

    & > div {
      display: flex;
      justify-content: space-between;
    }
  }
}

.slide-next-leave-active,
.slide-next-enter-active {
  position: absolute;
  transition: 0.4s;
}
.slide-next-enter {
  transform: translate(100%, 0);
}
.slide-next-leave-to {
  transform: translate(-100%, 0);
  opacity: 0;
}

.slide-back-leave-active,
.slide-back-enter-active {
  position: absolute;
  transition: 0.4s;
}
.slide-back-enter {
  transform: translate(-100%, 0);
}
.slide-back-leave-to {
  transform: translate(100%, 0);
  opacity: 0;
}
</style>
