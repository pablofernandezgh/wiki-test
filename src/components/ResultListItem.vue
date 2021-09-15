<template>
  <div v-if="item"
       class="item">
    <div>
      <a href="#">
        <template v-if="item.thumbnail">
          <img
              class="thumbnail"
              :src="item.thumbnail.url"
              :alt="item.title">
        </template>
        <template v-else>
          <div class="thumbnail no-image">
          </div>
        </template>
      </a>
    </div>
    <div>
      <h2>
        {{ item.title }}
      </h2>
      <p v-if="item.description">
        description : {{ item.description }}
      </p>
    </div>
  </div>
</template>

<script>

export default {

  props: {
    item: {
      required: true,
      type: Object
    }
  },
}
</script>
<style>

/*
I would've normally put this in a dedicated css file,
but since it's a prototype, I'm taking advantage of the <style> tags
*/
.item {
  border: 1px solid lightgray;
  min-height: 250px;
  display: flex;
  align-items: center;
}

.thumbnail {
  margin-right: 20px;
  margin-left: 20px;
  float: left;
  object-fit: cover;
  width: 200px;
  height: 200px;
}

.no-image {
  background-color: lightgray;
  width: 200px;
  height: 200px;
}
</style>