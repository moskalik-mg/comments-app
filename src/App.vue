<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <img src="./assets/mount.jpg" alt="" class="card__image">
        <div class="card__info">
          <h2 class="card__name">Beautiful landscape</h2>
          <button disabled class="btn btn-donate">
            <svg class="icon icon-donate">
              <use xlink:href="#cash"></use>
            </svg>
            <span>Donate Author</span>
          </button>
        </div>
        <div class="area-comment">
          <form action="" @submit.prevent="sendComment">
          <label for="commentInput">
            <input id="commentInput" type="text" placeholder="Write a new comment" class="input-comment" v-model="commentMessage">
            <transition name="btn-send">
              <button v-if="commentMessage.length > 0" @click="sendComment">
                <svg class="icon">
                  <use xlink:href="#telegram"></use>
                </svg>
                <span>Send</span>
              </button>
            </transition>
          </label>
          </form>
        </div>

        <transition-group name="animation-list" tag="div"> 
        <appListComments v-for="(item, index) in userComment" 
        :key="item" 
        :commentItem="item"
        :index="index"
        @deleteComment="deleteComment"
        @updatedComment="updatedComment"></appListComments>
        </transition-group>
      </div>
    </div>
    <svg width="0" height="0" class="hidden">
      <symbol xmlns="http://www.w3.org/2000/svg" viewBox="0 0 469.336 469.336" id="pencil">
        <path d="M456.836 76.168l-64-64.054c-16.125-16.139-44.177-16.17-60.365.031L45.763 301.682a10.733 10.733 0 0 0-2.688 4.587L.409 455.73a10.682 10.682 0 0 0 10.261 13.606c.979 0 1.969-.136 2.927-.407l149.333-42.703a10.714 10.714 0 0 0 4.583-2.69l289.323-286.983c8.063-8.069 12.5-18.787 12.5-30.192s-4.437-22.124-12.5-30.193zM285.989 89.737l39.264 39.264-204.996 204.997-14.712-29.434a10.671 10.671 0 0 0-9.542-5.896H78.921L285.989 89.737zm-259.788 353.4L40.095 394.5l34.742 34.742-48.636 13.895zm123.135-35.177l-51.035 14.579-51.503-51.503 14.579-51.035h28.031l18.385 36.771a10.671 10.671 0 0 0 4.771 4.771l36.771 18.385v28.032zm21.334-17.543v-17.082c0-4.042-2.281-7.729-5.896-9.542l-29.434-14.712 204.996-204.996 39.264 39.264-208.93 207.068zM441.784 121.72l-47.033 46.613-93.747-93.747 46.582-47.001c8.063-8.063 22.104-8.063 30.167 0l64 64c4.031 4.031 6.25 9.385 6.25 15.083s-2.219 11.052-6.219 15.052z"></path>
      </symbol>
      <symbol xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512.004 512.004" id="telegram">
        <path d="M508.194 20.517c-4.43-4.96-11.42-6.29-17.21-3.76l-482 211a15.01 15.01 0 0 0-8.98 13.41 15.005 15.005 0 0 0 8.38 13.79l115.09 56.6 28.68 172.06c.93 6.53 6.06 11.78 12.74 12.73 4.8.69 9.57-1 12.87-4.4l90.86-90.86 129.66 92.62a15.02 15.02 0 0 0 14.24 1.74 15.01 15.01 0 0 0 9.19-11.01l90-451c.89-4.47-.26-9.26-3.52-12.92zm-372.84 263.45l-84.75-41.68 334.82-146.57-250.07 188.25zm46.94 44.59l-13.95 69.75-15.05-90.3 183.97-138.49-150.88 151.39c-2.12 2.12-3.53 4.88-4.09 7.65zm9.13 107.3l15.74-78.67 36.71 26.22-52.45 52.45zm205.41 19.94l-176.73-126.23 252.47-253.31-75.74 379.54z"></path>
      </symbol>
      <symbol viewBox="-40 0 427 427.001" xmlns="http://www.w3.org/2000/svg" id="bin">
        <path d="M232.398 154.703c-5.523 0-10 4.477-10 10v189c0 5.52 4.477 10 10 10 5.524 0 10-4.48 10-10v-189c0-5.523-4.476-10-10-10zm-118 0c-5.523 0-10 4.477-10 10v189c0 5.52 4.477 10 10 10 5.524 0 10-4.48 10-10v-189c0-5.523-4.476-10-10-10zm0 0"></path>
        <path d="M28.398 127.121V373.5c0 14.563 5.34 28.238 14.668 38.05A49.246 49.246 0 0 0 78.796 427H268a49.233 49.233 0 0 0 35.73-15.45c9.329-9.812 14.668-23.487 14.668-38.05V127.121c18.543-4.922 30.559-22.836 28.079-41.863-2.485-19.024-18.692-33.254-37.88-33.258h-51.199V39.5a39.289 39.289 0 0 0-11.539-28.031A39.288 39.288 0 0 0 217.797 0H129a39.288 39.288 0 0 0-28.063 11.469A39.289 39.289 0 0 0 89.398 39.5V52H38.2C19.012 52.004 2.805 66.234.32 85.258c-2.48 19.027 9.535 36.941 28.078 41.863zM268 407H78.797c-17.098 0-30.399-14.688-30.399-33.5V128h250v245.5c0 18.813-13.3 33.5-30.398 33.5zM109.398 39.5a19.25 19.25 0 0 1 5.676-13.895A19.26 19.26 0 0 1 129 20h88.797a19.26 19.26 0 0 1 13.926 5.605 19.244 19.244 0 0 1 5.675 13.895V52h-128zM38.2 72h270.399c9.941 0 18 8.059 18 18s-8.059 18-18 18h-270.4c-9.941 0-18-8.059-18-18s8.059-18 18-18zm0 0"></path>
        <path d="M173.398 154.703c-5.523 0-10 4.477-10 10v189c0 5.52 4.477 10 10 10 5.524 0 10-4.48 10-10v-189c0-5.523-4.476-10-10-10zm0 0"></path>
      </symbol>
      <symbol viewBox="0 -54 512 511" xmlns="http://www.w3.org/2000/svg" id="cash">
        <path d="M502.992 246.445a38.39 38.39 0 0 0-43.687-11.035l-78.528 31.242a46.736 46.736 0 0 1-31.148 1.176L229.03 230.016a74.21 74.21 0 0 0-22.246-3.407h-39.223c-2.21-4.191-6.605-7.058-11.664-7.058h-27.093v-.305c0-7.41-6.028-13.441-13.442-13.441H13.441c-7.41 0-13.441 6.03-13.441 13.441V376.34c0 7.41 6.031 13.441 13.441 13.441h101.926c7.41 0 13.442-6.031 13.442-13.441v-.305h27.09c5.007 0 9.37-2.805 11.601-6.922 37.793 21.434 102.633 29.844 140.078 33.02 3.617.304 7.25.457 10.879.457 15.543 0 31.05-2.797 45.398-8.235 16.918-6.414 34.344-15.199 51.793-26.117a7.502 7.502 0 0 0-7.957-12.719c-16.617 10.395-33.156 18.739-49.152 24.805-15.613 5.918-32.797 8.285-49.695 6.856-88.332-7.496-125.836-25.438-139.758-34.73V241.612h37.7a59.28 59.28 0 0 1 17.757 2.719l120.562 37.805.141.043c.004 0 .113.035.113.035 8.368 2.586 13.543 10.898 12.043 19.336l-.175.988c-1.543 8.652-9.594 14.793-18.356 13.965l-99.73-9.371c-4.106-.387-7.782 2.644-8.172 6.77a7.505 7.505 0 0 0 6.77 8.171l99.73 9.371c.992.094 1.98.14 2.96.14 15.29 0 28.844-11.116 31.567-26.417l.18-.988c1.215-6.836.117-13.625-2.762-19.52a61.551 61.551 0 0 0 16.91-4.062l78.528-31.243a23.402 23.402 0 0 1 26.64 6.727 23.4 23.4 0 0 1-1.113 31.36c-11.992 12.417-31.246 30.968-54.86 48.84a7.5 7.5 0 0 0-1.453 10.507 7.5 7.5 0 0 0 10.508 1.457c24.38-18.45 44.235-37.578 56.598-50.379a38.38 38.38 0 0 0 1.82-51.422zm-389.191-19.39v147.722H15.004V220.81H113.8zm40.281 129.27v4.702h-25.277V234.555h25.277zm0 0"></path>
        <path d="M355.176 234.555c64.527 0 117.027-52.496 117.027-117.028S419.703.5 355.176.5C290.645.5 238.148 53 238.148 117.527c0 64.532 52.497 117.028 117.028 117.028zm0-219.051c56.254 0 102.023 45.77 102.023 102.023 0 56.258-45.765 102.024-102.023 102.024-56.258 0-102.024-45.766-102.024-102.024 0-56.257 45.77-102.023 102.024-102.023zm0 0"></path>
        <path d="M355.176 69.934a7.504 7.504 0 0 0-7.504 7.504v3.726c-4.61 1.621-8.508 4.66-10.985 8.711-5.41 8.855-3.886 19.809 3.704 26.645 3.539 3.187 7.347 5.378 11.027 7.5 3.152 1.816 6.129 3.53 8.5 5.668 2.238 2.015 2.602 4.957.941 7.671-.988 1.614-3.093 2.703-5.492 2.844-1.601.09-3.722-.82-5.058-2.176-.442-.449-1.176-1.336-1.114-2.226.301-4.133-2.808-7.723-6.941-8.024-4.133-.293-7.727 2.809-8.024 6.942-.363 5.031 1.555 9.949 5.399 13.844 2.258 2.292 5.055 4.074 8.043 5.214v3.844c0 4.14 3.36 7.5 7.504 7.5s7.504-3.36 7.504-7.5v-3.73c4.61-1.621 8.507-4.66 10.984-8.711 5.406-8.852 3.883-19.809-3.703-26.645-3.55-3.195-7.363-5.394-11.055-7.515-3.144-1.813-6.113-3.524-8.476-5.653-2.239-2.015-2.598-4.953-.938-7.668.985-1.617 3.09-2.707 5.492-2.844 1.606-.097 3.72.82 5.055 2.172.441.45 1.18 1.336 1.113 2.227a7.499 7.499 0 0 0 6.942 8.023c4.133.293 7.726-2.808 8.023-6.941.363-5.031-1.55-9.945-5.394-13.844-2.262-2.289-5.059-4.066-8.047-5.207v-3.847a7.498 7.498 0 0 0-7.5-7.504zm0 0"></path>
        <path d="M355.176 195.46c42.972 0 77.93-34.96 77.93-77.933s-34.958-77.93-77.93-77.93c-10.535 0-20.758 2.067-30.387 6.15-3.812 1.612-5.594 6.019-3.98 9.831a7.503 7.503 0 0 0 9.836 3.98c7.765-3.288 16.015-4.956 24.53-4.956 34.696 0 62.927 28.226 62.927 62.925 0 34.7-28.23 62.926-62.926 62.926-34.7 0-62.93-28.226-62.93-62.926 0-14.332 4.691-27.828 13.57-39.035a7.502 7.502 0 0 0-1.222-10.539 7.499 7.499 0 0 0-10.54 1.223c-11 13.883-16.812 30.605-16.812 48.351.004 42.973 34.961 77.934 77.934 77.934zm0 0"></path>
      </symbol>
    </svg>
  </div>
</template>

<script>
import listComments from './components/listComments.vue'

export default {
  name: 'app',
  mounted(){
    if(!localStorage.getItem('arrayComments')){
      let userComment = JSON.stringify(this.userComment);
      localStorage.setItem('arrayComments', userComment);
    }
    else{
      this.userComment = JSON.parse(localStorage.getItem('arrayComments'));
    }
  
  },
  data(){
    return{
      commentMessage: '',
      userComment: [{
        name: 'Maks',
        comment: 'Comment lol',
        avatar: require('@/assets/avatar.jpg')
      },
      {
        name: 'Maks',
        comment: "That's awesome",
        avatar: require('@/assets/avatar.jpg')
      }
      ]
    }
  },
  components: {
    appListComments: listComments 
  },
  methods:{
    sendComment(){
      if(this.commentMessage.length > 0){
        let item = {
          name: 'Maks',
          comment: this.commentMessage,
          avatar: require('@/assets/avatar.jpg')
        }
        this.userComment.unshift(item);
        let userComment = JSON.stringify(this.userComment);
        localStorage.setItem('arrayComments', userComment);
        this.commentMessage = '';
      }
      else{
        return false;
      }
    },
    deleteComment(index){
      this.userComment.splice(index, 1);
      let newArray = JSON.stringify(this.userComment);
      localStorage.setItem('arrayComments', newArray);
    },
    updatedComment(data){
      let index = data[1];
      let newComment = data[0];
      this.userComment[index].comment = newComment;
      let newArray = JSON.stringify(this.userComment);
      localStorage.setItem('arrayComments', newArray);
    }
  }
  
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,500,600&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Montserrat','Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container{
  max-width: 800px;
  margin: 0 auto;
  position: relative;
  overflow-x: hidden;
}

input, button, a{
font-family: 'Montserrat', sans-serif;
}

.card{
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 5px 32px rgba(103,122,141,.17);

  &__image{
    max-height: 340px;
    width: 100%;
    object-fit: cover;
    border-radius: 5px;
  }

  &__info{
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 20px 0;
  }

  &__name{
    font-weight: 300;
  }

  .btn{
    border-radius: 5px;
    padding: 7px 10px;
    font-family: 'Montserrat', sans-serif;
    cursor: pointer;
  }

  .btn-donate{
    border: none;
    color: #000;
    background: rgb(207,196,240);
    background: linear-gradient(138deg, rgba(207,196,240,1) 0%, rgba(241,201,236,1) 100%);
    font-weight: 500;
    cursor: auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .icon-donate{
    fill: #000;
  }



  .input-comment{
    width: 100%;
    border-radius: 5px;
    padding: 20px 20px;
    border: 1px solid #000;
    font-size: 18px;
  }

  .area-comment{
    margin-bottom: 20px;
    label{
      position: relative;
      display: flex;
      overflow: hidden;
      button{
        position: absolute;
        right: 0;
        background-color: #2C3BFF;
        color: #fff;
        border: none;
        height: 100%;
        width: 120px;
        border-radius: 0 5px 5px 0;

        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
  }
}


.btn-send-enter-active, .btn-send-leave-active{
  transition: all .4s ease;
}

.btn-send-enter, .btn-send-leave-to{
  transform: translateX(50px);
  opacity: 0;
}


.animation-list-enter, .animation-list-leave-to{
  transform: translateX(-100%);
}

.animation-list-enter-active, .animation-list-leave-active{
  transition: all .4s;
}

svg.icon{
    width: 20px;
    fill: #fff;
    height: 20px;
    margin-right: 10px;
}


</style>
