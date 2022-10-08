<!-- eslint-disable vue/multi-word-component-names -->
<script>
export default {
    props: {
        show: Boolean
    }
}
</script>
    
<template>
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-wrapper"  @click="$emit('close')">
                <div class="modal-container" @click.stop>
                    <div class="modal-header">
                        <slot name="header">default header</slot>
                    </div>
                    <div class="modal-footer">
                        <slot name="footer">
                            <button class="modal-default-button" @click="$emit('close')">OK</button>
                        </slot>
                    </div>
                </div>
            </div>
        </div>
    </Transition>
</template>


<style>

.modal-mask {
    width: 20%;
    margin-left: 40%;
    position: relative;
}

.modal-container {
    display: block;
    text-align: center;
    width: 300px;
    margin-top: 30px;
    margin-left: 40px;
    padding: 20px 30px;
    background-color:gainsboro;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
}

.modal-wrapper {
    display: table-cell;
    vertical-align: middle;
}
.modal-body {
    margin: 20px 0;
}
.modal-default-button{
    border: 1px solid black;
    width: 50px;
}


</style>

