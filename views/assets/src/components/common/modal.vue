<template>
    <transition name="modal">
        <div class="modal-mask pm-common-modal-wrap" :class="classes"  v-show="isActive" >
            <div class="modal-wrapper">
                <div class="modal-container" :style="styles">
                    <div class="modal-header">
                        <span class="pm-right close-vue-modal"> 
                            <a href="#" class=""  @click.prevent="$emit('close')">X</a> </span>
                        <slot name="header"></slot>
                    </div>
                    <div class="modal-body">
                        <slot></slot>
                    </div>

                    <div class="modal-footer">
                        <slot name="footer"></slot>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: 'modal',
        props: {
            isActive: Boolean,
            fullWidth: {
                type: Boolean,
                default: false
            },
            maxWidth: {
              type: [String, Number],
              default: 'none'
            },
            width: {
              type: [String, Number],
              default: 'auto'
            }
        },

        computed: {
            classes () {
                return {
                    
                    'modal-active': this.isActive,
                    'modal-fullwidth': this.fullWidth
                    
                }
            },

            styles () {
                var style;
                if (!this.fullWidth) {

                      style = {
                        maxWidth: this.maxWidth === 'none' ? undefined : (isNaN(this.maxWidth) ? this.maxWidth : `${this.maxWidth}px`),
                        width: this.width === 'auto' ? undefined : (isNaN(this.width) ? this.width : `${this.width}px`)
                      }
                }else {
                    let pm = document.getElementById("wedevs-project-manager");
                        style = {
                            maxWidth : `${pm.clientWidth-100}px` ,
                            maxHeight:`${pm.clientHeight-100}px`
                        }
                }
                return style;
            }
        }
    }


</script>

<style lang="less">
    .pm-common-modal-wrap {
        .pm-filter-modal-header {
            padding: 12px !important;
        }

        .modal-header {
            margin-bottom: 0 !important;
            border-bottom: none !important;
        }
        .modal-footer {
            padding: 0 !important;
        }
        .modal-wrapper {
            vertical-align: baseline !important;

            .modal-container {
                top: 80px !important;
            }
        }
    }
</style>
    
