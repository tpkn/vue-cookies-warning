<!-- Vue Cookies Warning, http://tpkn.me/ -->
<template>
   <transition :name="animate ? 'up' : ''" mode="out-in" appear>
      <div v-if="show" :class="[ 'cookies-warning', theme ]">
         <slot></slot>
         <span @click="acceptAndForget">
            <slot name="acceptButton"></slot>
         </span>
      </div>
   </transition>
</template>
<script>

   export default {
      name: 'CookiesWarning',

      data: () => {
         return {
            show: false
         }
      },

      props: {
         cookie_name: {
            type: String,
            default: () => 'cookies-accepted'
         },

         expires: {
            type: String,
            default: () => 'Fri, 31 Dec 9999 23:59:59 GMT'
         },

         animate: {
            default: () => true
         },

         theme: {
            default: () => 'default'
         }
      },

      methods: {
         acceptAndForget(){
            this.show = false;
            this.$emit('accepted');
            document.cookie = this.cookie_name + '=true; expires=' + this.expires;
         },
         
         getCookie(name){
            let rule = new RegExp("(?:^|; )" + name.replace(/([.$?*|{}()[]\\\/\+^])/g, '\\$1') + "=([^;]*)");
            let matches = document.cookie.match(rule);
            return matches ? decodeURIComponent(matches[1]) : undefined;
         }
      },

      mounted(){
         let accepted = !!this.getCookie(this.cookie_name);
         if(!accepted){
            this.show = true;
         }
      }
   }

</script>
<style lang="scss" scoped>

   .cookies-warning {
      position: fixed;
      left: 0; right: 0; bottom: 0;

      z-index: 99999;
      overflow-x: hidden;
      overflow-y: auto;
      max-height: 100%;
   }

   .default {
      padding: 20px 15px;

      color: white;
      background: #000000;

      color: #fff;
      font-size: 16px;
      line-height: 1.4;
      text-align: center;
   }

   .up-enter-active, .up-leave-active {
      transition: transform .3s cubic-bezier(0.490, 0.265, 0.450, 1);
   }

   .up-enter, .up-leave-to {
      transform: translate(0, 100%);
   }

</style>
