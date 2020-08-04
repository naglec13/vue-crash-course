<template>
  <li>
    Todo Item {{todo.id}}
    {{todo.title}}
  </li>
</template>

<script>
export default{
  props:['todo']
}
</script>