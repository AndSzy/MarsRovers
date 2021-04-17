<template>
  <b-card :class="width" :header="header">
      <b-card-text>
            <slot></slot>
      
    </b-card-text>
    </b-card>
</template>

<script>
export default {
    name: "TheCard",
    props: {
        width: String,
        header: String
    }
}
</script>

<style>
.card-body {
    height: 200px;
}
</style>