<template>
    <div class="header">
        <span>rent credit</span>
        <i class="fas fa-hotel"></i>
    </div>
</template>
<script>
export default {
    name: "Header",
    data() {
        return {};
    },
};
</script>
<style scoped>
.header {
    background-color: slategrey;
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
}
.header span {
    font-size: 28px;
    text-transform: uppercase;
    color: #db2777;
    font-weight: 900;
}
.header i {
    font-size: 30px;
    color: burlywood;
}
</style>
