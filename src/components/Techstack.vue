<template>
  <div class="tech-stack">
    <h1>Technology Stack</h1>
    <div class="vue"><ion-icon name="logo-vue"></ion-icon></div>
    <div class="javascript"><ion-icon name="logo-javascript"></ion-icon></div>
    <div class="html5"><ion-icon name="logo-html5"></ion-icon></div>
    <div class="sass"><ion-icon name="logo-sass"></ion-icon></div>
    <div class="css3"><ion-icon name="logo-css3"></ion-icon></div>
  </div>
</template>

<script>
export default {
  name: "Technology",
};
</script>

<style lang="scss">
@mixin icon-color($color) {
  &:hover {
    color: $color;
  }
}

.tech-stack {
  display: flex;
  flex-direction: column;
  margin-top: 30px;

  h1 {
    color: rgb(211, 211, 211);
  }

  ion-icon {
    font-size: 60px;
    color: rgb(189, 189, 189);
    margin: 20px 0;
    transition: color 0.3s;
  }

  .vue > ion-icon {
    @include icon-color(#41b883);
  }
  .javascript > ion-icon {
    @include icon-color(#f0db4f);
  }
  .html5 > ion-icon {
    @include icon-color(#f06529);
  }
  .sass > ion-icon {
    @include icon-color(#cc6699);
  }
  .css3 > ion-icon {
    @include icon-color(#2965f1);
  }
}
</style>
