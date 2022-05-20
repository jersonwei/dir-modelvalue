<script  lang='ts'>
import { ref } from "vue";
export default {
        directives:{
          myModel:{
            mounted(el: any,binding:any,vnode:any) {
              if(typeof binding.value === 'undefined'){
                return new Error('v-myModel未绑定值')
              }
              // 获取组件实例对象
              let vm = binding.instance
              console.log(vm)
              // 获取type属性
              const type = vnode.props.type
              let event = ''
              let targetValue = ''
              switch (type) {
                case 'text':
                    event = 'input'
                    targetValue = 'value'
                    break;
                case 'textarea' :
                    event = 'input'
                    targetValue = 'value'
                    break;
                case 'checkbox' :
                    event = 'change'
                    targetValue = 'checked'
                    break;
                case 'radio' :
                    event = 'change'
                    targetValue = 'checked'
                    break;
                case 'select' :
                    event = 'change'
                    targetValue = 'value'
                    break;
                default:
                    break;
              }
              el.value = binding.value
              el.addEventListener(event,function(e:any){
                vm[binding.arg] = e.target[targetValue]
              })
            },
          },
          setup() {
            const value = ref('11')
            const checked = ref(true)
            return {
              value,
              checked
            }
          }
        }
}
</script>
<template>
<div>
  <input type="text" v-myModel:value="value" />
  {{value}}
  <input type="checkbox" v-myModel:checked="checked" />
  {{checked}}
</div>
</template>
<style></style>