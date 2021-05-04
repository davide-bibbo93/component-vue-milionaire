<template>
    <div class="answer">{{ aText }}</div>
</template>

<script>

    export default {
        name: "Answer",
        props: ["aText"],
    };
    
</script>

<style lang="scss" scoped>

    .answer {
        padding: 1rem;
        color: #fff;
        border: 1px solid white;
        border-radius: 40px;
        cursor: pointer;
        font-size: 1.2rem;
        text-align: center;
    }

</style>