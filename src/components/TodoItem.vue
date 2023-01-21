<script setup>
import { ref } from 'vue'

const props = defineProps({
    todo: Object
})

</script>

<template>
    <li>
       {{ todo.text }} 
    </li>
</template>