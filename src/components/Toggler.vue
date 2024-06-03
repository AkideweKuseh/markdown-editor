<template>
    <label class="switch">
      <input type="checkbox" id="toggle-switch" @click="changeTheme">
      <span class="slider round"></span>
    </label>
</template>

<script lang="ts">
    export default{
        name: 'Toggler',
        methods: {
          changeTheme(){
            this.$emit('changeTheme')
          }
        }
    }
</script>

<style>
    /* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  margin: 0 5px;
  width: 40px;
  height: 20px;
}

/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: var(--togglerBackground);
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 10px;
  width: 10px;
  right: 6px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider:before {
  transform: translateX(-20px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>