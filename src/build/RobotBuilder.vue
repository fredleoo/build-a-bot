<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <h1>{{name}}</h1>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectPrevHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm"/>
        <button @click="selectPrevLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="torso"/>
        <button @click="selectPrevTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="right arm"/>
        <button @click="selectPrevRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="base"/>
        <button @click="selectPrevBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/parts'
function getPrevValidIndex(index, length) {
    const deprecatedIndex = index - 1
    return deprecatedIndex < 0 ? length - 1 : deprecatedIndex
}

function getNextValidIndex(index, length) {
    const incrementedIndex = index + 1
    return incrementedIndex > length - 1 ? 0 : incrementedIndex
}

export default {
    name: 'RobotBuilder',
    data() {
        return { 
                name: 'fred',
                availableParts,
                selectedHeadIndex : 0,
                selectedLeftArmIndex : 0,
                selectedRightArmIndex : 0,
                selectedTorsoIndex : 0,
                selectedBaseIndex : 0,
            }        
        },
    computed: {
      selectedRobot() {
        return {
          head: availableParts.heads[this.selectedHeadIndex],
          leftArm: availableParts.arms[this.selectedLeftArmIndex],
          torso: availableParts.torsos[this.selectedTorsoIndex],
          rightArm: availableParts.arms[this.selectedRightArmIndex],
          base: availableParts.bases[this.selectedBaseIndex],
        }
      }
    },
    methods: {
        selectPrevHead(){
            this.selectedHeadIndex = getPrevValidIndex(this.selectedHeadIndex, availableParts.heads.length)
        },
        selectNextHead(){
            this.selectedHeadIndex = getNextValidIndex(this.selectedHeadIndex, availableParts.heads.length)
        },
        selectPrevLeftArm(){
            this.selectedLeftArmIndex = getPrevValidIndex(this.selectedLeftArmIndex, availableParts.heads.length)
        },
        selectNextLeftArm(){
            this.selectedLeftArmIndex = getNextValidIndex(this.selectedLeftArmIndex, availableParts.heads.length)
        },
        selectPrevRightArm(){
            this.selectedRightArmIndex = getPrevValidIndex(this.selectedRightArmIndex, availableParts.heads.length)
        },
        selectNextRightArm(){
            this.selectedRightArmIndex = getNextValidIndex(this.selectedRightArmIndex, availableParts.heads.length)
        },
        selectPrevTorso(){
            this.selectedTorseIndex = getPrevValidIndex(this.selectedTorsoIndex, availableParts.heads.length)
        },
        selectNextTorso(){
            this.selectedTorsoIndex = getNextValidIndex(this.selectedTorsoIndex, availableParts.heads.length)
        },
        selectPrevBase(){
            this.selectedBaseIndex = getPrevValidIndex(this.selectedBaseIndex, availableParts.heads.length)
        },
        selectNextBase(){
            this.selectedBaseIndex = getNextValidIndex(this.selectedBaseIndex, availableParts.heads.length)
        }
    }
}
</script>

<style scoped>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
} 
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;    
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;  
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;    
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
</style>