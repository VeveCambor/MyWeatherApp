<template>
  <div class="submit-btn">
        <button>Submit</button>
  </div>
</template>

<script>
export default {
  name: 'WButton',
  btnType: {
      type: String,
      default: 'button'
    }
}
</script>

<style scoped>
.submit-btn button {
  margin-top: 2rem;
  padding: .3em .8em;
  background:rgb(238, 226, 238);
  color:#808080;
  border: 1px solid #b6b2b5;
  border-radius: 10px;
  transition: background-color .4s linear;
  cursor: pointer;
  font-size: 18px;     
  }
.submit-btn button:hover {
  background: #f1d1eb;
  color:#6c6180;
  }
</style>