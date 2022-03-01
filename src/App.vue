<template>
  <score-generator
    :score=8
    :size=50
    :lineWeight=5
    :lineColor="'blue'"
    :direction="'row'"
  />
</template>

<script>
import ScoreGenerator from "./components/ScoreGenerator"

export default {
  name: 'App',
  components: {
    ScoreGenerator
  }
}
</script>

<style>

</style>
