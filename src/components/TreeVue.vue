<template>
  <div> 
    {{ rubrics }} 
      <span @click="isOpen=!isOpen" style="cursor:pointer" >{{ isOpen ? '-' : '+' }}</span>
        <div v-if='isOpen'>
          <input @change="changeValue" type="checkbox" id="allowEmpty"  />
          <label for="allowEmpty">Отображать пустые рубрики</label> 
          <p>{{ totalCount }}</p>
        </div>
  </div>
  
    <div v-if='isOpen' class="node" v-for="(elem, index) in node" :key="elem.id"> 
      <input type="checkbox" @change="sum(index)"/>
      
      <a style="text-decoration: none" class="button" target="_blank" ref="myInp"
         :href="`https://www.klerk.ru${elem.url}`">
         {{ elem.title }} - {{ elem.count }} - {{ elem.count + elem.children.reduce((acc, curr) => acc + curr.count, 0) }}</a> 
      
      <a v-if="!elem.children.length" style="visibility: hidden;" 
         :href="`https://www.klerk.ru${elem.url}`">
         {{ elem.title }}</a>
      
      <Disclosure v-else>
        <DisclosureButton class="button">
          <span style="cursor:pointer" >{{ '&#9658;' }}</span>
         </DisclosureButton>
           <DisclosurePanel >
            <div v-if="elem.children.length" class="node-child" 
                 v-for="child in elem.children" :key="child.id"> 
              <a style="text-decoration: none" class="button" target="_blank" 
                 :href="`https://www.klerk.ru${child.url}`">{{ child.title }}</a>
            </div>
           </DisclosurePanel>
       </Disclosure>
    </div>
</template>

<script>
import {Disclosure, DisclosureButton, DisclosurePanel} from "@headlessui/vue";
export default {
  name: 'TreeVue',
  emits: ["changeFlag"], 
  components: {
    Disclosure, DisclosureButton, DisclosurePanel
  },
  props: {
    node: Object,
  },
  data() {
    return {
      clicked: false,
      rubrics: 'Рубрики',
      isOpen: false,
      allowEmpty: false,
      totalCount: 0,
      checkArr: []
    }
  },
  methods: {
    changeClicked () {
      return this.clicked = !this.clicked
  },
  changeValue () {
    this.allowEmpty = !this.allowEmpty
    this.$emit('changeFlag', this.allowEmpty)
  },
  sum (index) {
    let value = Number(this.$refs.myInp[index].innerHTML.split('-').pop());
    if(this.checkArr.includes(index)) {      
        this.totalCount -= value;
        let myIndex = this.checkArr.indexOf(index);
          if (myIndex !== -1) {
            this.checkArr.splice(myIndex, 1);
          }
    } else {
      this.checkArr.push(index);
      this.totalCount += value
    }
  }
},
}
</script>

<style scoped>
@import '../assets/animationText.css';

.node {
  text-align: left;
  font-size: 15px;
  margin-left: 20px;
  cursor: pointer;
  font-size: 18px;
}
.node-child {
  margin-left: 30px;
  font-size: 15px;
  margin-top: 8px;
}
</style>
