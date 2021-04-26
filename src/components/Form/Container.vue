<template>
  <div class="row justify-content-center mt-3">
    <div class="col-12 col-md-12 col-lg-8">
      <div class="result res-card rounded">
        <div class="row justify-content-center">
          <slot></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.result {
  img {
    width: 100% !important;
  }
  hr {
    width: 100% !important;
    background-color: #acacac !important;
  }
  padding: 20px 15px;
  background-color: #0d1117;
  border: 1px solid #acacac;
}
</style>
