<template>
    <div class="alert-main" v-if="alertStatus" @click="$emit('close')">
        <div class="alertContent" @click.stop>
            <slot></slot>
        </div>
    </div>
</template>
<script>
export default {
    name: "DeleteAlert",
    props: {
        alertStatus: {
            type: Boolean,
            required: true,
            default: false,
        },
    },
    data() {
        return {};
    },
};
</script>
<style scoped>
.alert-main {
    position: fixed;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100vh;
    background-color: rgba(0, 0, 0,0.4);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
}
.alertContent {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1px solid rgb(236, 234, 234);
    background-color: #f3f4f6;
    padding: 30px;
    border-radius: 5px;
    animation-name: alertBox;
    animation-duration: 0.3s;
    animation-iteration-count: 1;
    animation-timing-function: ease-in-out;

}
@keyframes alertBox {
    from {
        width: 0%;
    }
    to {
        width: 75%;
    }
}
</style>
