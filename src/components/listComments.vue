<template>
    <div class="wrapper-user">
        <div class="user" @click.stop="isControlPanel = !isControlPanel" v-if="isUser">
            <transition name="animation-controlPanel">
            <div class="controlPanel" v-if="isControlPanel">
                <button class="btn btn-edit" @click.capture.stop="editComment">
                    <svg class="icon icon-edit">
                        <use xlink:href="#pencil"></use>
                    </svg>
                    <span>Edit</span>
                </button>
                <button class="btn btn-delete" @click.capture.stop="deleteComment">
                    <svg class="icon icon-delete">
                        <use xlink:href="#bin"></use>
                    </svg>
                    <span>Delete</span>
                </button>
            </div>
            </transition>

 
            <img :src="commentItem.avatar" alt="" class="user__image">
            <div class="user__info">
                <div class="user__name">
                    {{commentItem.name}}
                </div>
                <div class="user__comment">
                    {{commentItem.comment}}
                </div>
            </div>
            <transition name="animation-controlPanel">
            <div class="confirm-delete" v-if="isConfirmDelete">
                <div class="confirm-message">
                    Delete comment?
                </div>
                <div>
                    <button class="btn btn-discard" @click.capture.stop="discardDelete">No</button>
                    <button class="btn btn-accept" @click.capture.stop="acceptDelete">Yes</button>
                </div>
            </div>
            </transition>
      
        </div>
        <transition name="animation-EditArea">
        <div class="area-comment" v-if="isEditCommentArea">
            <form action="" @submit.prevent="updateComment">
                <label for="commentInputEdit">
                    <input id="commentInputEdit" type="text" placeholder="Write a new comment" class="input-comment" v-model="commentItem.comment">
                    <transition name="btn-send">
                    <button v-if="commentItem.comment.length > 0" @click.capture.stop="updateComment">
                        <svg class="icon">
                            <use xlink:href="#telegram"></use>
                        </svg>
                         <span>Send</span>
                    </button>
                    </transition>
                </label>
            </form>
        </div>
        </transition>
    </div>
</template>

<script>
export default {
    props: ['commentItem', 'index'],
    created(){
        document.addEventListener('click', (e) => {
            this.disabledAll();
            if(e.target.getAttribute('id') != 'commentInputEdit'){
                this.isEditCommentArea = false
                this.isUser = true
            }
        });
    },
    data(){
        return{
            isControlPanel: false,
            controlBlock: false,
            isConfirmDelete: false,
            isEditCommentArea: false,
            isUser: true,
            // newComment: this.commentItem.comment
        }
    },
    methods:{
        editComment(){
            this.isEditCommentArea = true
            this.isUser = false
        },
        deleteComment(){
            this.isControlPanel = false
            this.isConfirmDelete = true
        },
        discardDelete(){
            this.isConfirmDelete = false
        },
        acceptDelete(){
            this.$emit('deleteComment', this.index)
            this.isConfirmDelete = false
        },
        updateComment(){
            this.$emit('updatedComment', [this.commentItem.comment, this.index])           
            this.isEditCommentArea = false
            this.isControlPanel = false
            this.isUser = true
        },
        disabledAll(){
            this.isControlPanel = false
            this.controlBlock = false
            this.isConfirmDelete = false
            // this.isUser = true
            // this.isEditCommentArea = false
        }
    }
}
</script>

<style lang="scss" scoped>

    .user{
        position: relative;
        margin: 20px 0;
        display: flex;
        align-items: center;
        padding: 10px;
        border-radius: 5px;
        cursor: pointer;
        transition: all .4s ease;
        overflow: hidden;
        &__image{
            width: 50px;
            height: 50px;
            border-radius: 50%;
        }

        &__info{
            margin-left: 20px;
        }

        &__comment{
            font-weight: 500;
        }


        &:hover{
            background-color: #ebe7ff;
        }
    }
    .controlPanel{
        margin-right: 10px;
        display: flex;
        align-items: center;
    }

    .btn-edit{
        color: #0088cc;
        border: none;
        background: none;
        font-weight: 500;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .btn-delete{
        color: #e53935;
        border: none;
        background: none;
        font-weight: 500;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .icon-delete{
        fill: #e53935;
    }

    .icon-edit{
        fill: #0088cc;
    }

    .confirm-delete{
        margin-left: auto;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        display: flex;
        justify-content: space-between;
        background-color: #ebe7ff;
        border-radius: 5px;
    }

    .confirm-message{
        display: flex;
        align-items: center;
        padding-left: 20px;
    }

            
    .btn-discard{
        color: #fff;
        background-color: #0088cc;
        border: none;
        height: 100%;
        width: 70px;
        border-radius: 0 5px 5px 0;
    }
        
    .btn-accept{
        color: #fff;
        background-color: #e53935;
        border: none;
        height: 100%;
        width: 70px;
        border-radius: 0 5px 5px 0;
    }

    .animation-controlPanel-enter-active, .animation-controlPanel-leave-active, 
    .animation-userData-enter-active, .animation-userData-leave-active, 
    .animation-EditArea-enter-active, .animation-EditArea-leave-active
    .animation-confirmDelete-enter-active, .animation-confirmDelete-leave-active{
        transition: all .4s ease;
    }

    .animation-controlPanel-enter, .animation-controlPanel-leave-to{
        transform: translateX(-50px);
        opacity: 0;
    }

    .animation-EditArea-enter, .animation-EditArea-leave-to, .animation-confirmDelete-enter, .animation-confirmDelete-leave-to{
        transform: translateX(100%);
        opacity: 0;
    }


    



</style>