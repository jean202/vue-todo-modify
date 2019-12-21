<template>
    <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
              default header
            </slot>
          </div>
        <span class="modal-body">
            <slot name="body">
                default body
            </slot>
        </span>
      </div>
    </div>
    </div>
  </transition>
</template>
<style scoped>
    .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
    display: table;
    transition: opacity .3s ease;
    }

    .modal-wrapper {
    display: table-cell;
    vertical-align: middle;
    }

    .modal-container {
    width: 300px;
    margin: 0px auto;
    padding: 30px 30px;
    background-color: #F6F6F6;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
    transition: all .3s ease;
     font-family: Helvetica, Arial, sans-serif;
    }

    .inputBox{
       background:white;
    }

    .modal-header{
      margin-bottom:20px;
    }

    .modal-body {
      height: 50px;
      margin:  0;
    }

    .modal-default-button {
    float: right;
    }

    .modal-enter {
    opacity: 0;
    }

    .modal-leave-active {
    opacity: 0;
    }

    .modal-enter .modal-container,
    .modal-leave-active .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
    }
</style>