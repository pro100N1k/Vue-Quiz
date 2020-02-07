<template>
<div class="">
   <b-nav tabs>
       <b-nav-item disabled active>Fancy Quiz App</b-nav-item>
       <b-nav-item disabled>Counter: {{numCurrent}}/{{numTotal}} | Correct: {{numCorrect}}</b-nav-item>
   </b-nav>
</div>
</template>

<script>
    export default {
        name: "Header",
        props: [
            'numCorrect',
            'numCurrent',
            'numTotal'
        ]
    }
</script>

<style scoped>

</style>