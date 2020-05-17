<template>
  <div  class="footer sticky">
    <p>Footer</p>
  </div>
</template>

<style>
.footer {
  display: flex;
  flex-direction: column;
  background-color: #1abc9c;
  color: white;

  padding: 10px;
}
.sticky {
  position: -webkit-sticky; /* Safari */
  position: sticky;
  bottom: 0;
}


</style>