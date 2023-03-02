<template>
<div>
 <div class="btn-group" role="group" aria-label="Basic mixed styles example">
  <button type="button" class="btn btn-danger">Left</button>
  <button type="button" class="btn btn-warning">Middle</button>
  <button type="button" class="btn btn-success">Right</button>
</div>
<Todos/>
</div>
</template>

<script>
import Todos from "@/components/Todos.vue";
export default {
    name:"HomeName",
    components: {Todos},
    data() {
        return {
            
        }
    },

}
</script>

<style>

</style>