<template>
  <transition name="fade">
    <div class="modal align-baseline" v-show="isActive" :class="{ 'is-active': isActive }">
      <div class="modal-background" v-if="backdrop" @click="backdropClose"></div>
      <transition :name="transition">
        <div class="modal-card" :style="modalWidth" v-show="isActive">
        <header class="modal-card-head" v-if="showHeader">
          <slot name="header">
            <p class="modal-card-title">{{ title }}</p>
            <span class="close" @click="handleCancel">×</span>
          </slot>
        </header>
        <section class="modal-card-body">
          <slot></slot>
        </section>
        <footer class="modal-card-foot" v-if="showFooter">
          <slot name="footer">
            <a class="button" @click="handleCancel" v-if="showCancel">{{ cancelText }}</a>
            <a class="button is-primary" :class="{'is-loading': isLoading}" @click="handleOk" v-if="showOk">{{ okText }}</a>
          </slot>
        </footer>
      </div>
      </transition>
    </div>
  </transition>
</template>
<script>
import ModalMixin from './ModalMixin';

export default {
  mixins: [ModalMixin],
};
</script>
<style lang="scss">
.modal{
  transition: all .3s ease;
  &.align-baseline{
    align-items: baseline;
  }
}
.modal-background{
  transition: opacity .3s ease;
}
.modal-card{
  box-shadow: 0 1px 4px rgba(0,0,0,.2);
  border-radius: 5px;
}
.modal-card-head, .modal-card-foot{
  background-color: #fff;
  padding: 16px;
}
.modal-card-head{
  border-bottom: 1px solid rgba(120,130,140,.13);
}
.modal-card-foot{
  border-top: 1px solid rgba(120,130,140,.13);
  justify-content: flex-end;
}
.modal-card-title{
  font-size: 16px;
  font-weight: 500;
}
.align-baseline{
  .modal-card{
    margin-top: 120px;
  }
}
.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-card,
.modal-leave-active .modal-card {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
.close{
  font-size: 21px;
  font-weight: 700;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  cursor: pointer;
  filter: alpha(opacity=20);
  opacity: .2;
  font-family: Arial,sans-serif;
}
.close:focus, .close:hover{
  filter: alpha(opacity=50);
  opacity: .5;
}

</style>
