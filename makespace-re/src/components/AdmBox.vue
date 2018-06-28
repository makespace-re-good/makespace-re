<template>
  <div style="height:1000px;margin:0px;padding: 0px">
  <div id="head">
  </div>
  <div id="aside">
    <div class="title" id="title1" @click="title1"><i class="el-icon-arrow-up" id="title1icon"></i>后台首页</div>
    <el-collapse-transition>
      <div v-show="show1">
        <div class="part" id="part11" @click="part11">首页</div>
      </div>
    </el-collapse-transition>

    <div class="title" id="title2" @click="title2"><i class="el-icon-arrow-up" id="title2icon"></i>审核流程</div>
    <el-collapse-transition>
      <div v-show="show2">
      <div class="part" id="part21" @click="part21">管理申请</div>
      <div class="part" id="part22" @click="part22">办理入驻</div>
      <div class="part" id="part23" @click="part23">中期审核</div>
      <div class="part" id="part24" @click="part24">期满审核</div>
      </div>
    </el-collapse-transition>

    <div class="title" id="title3" @click="title3"><i class="el-icon-arrow-up" id="title3icon"></i>管理事项</div>
    <el-collapse-transition>
      <div v-show="show3">
      <div class="part" id="part31" @click="part31">导师管理</div>
      <div class="part" id="part32" @click="part32">团队管理</div>
      <div class="part" id="part33" @click="part33">资源管理</div>
      </div>
    </el-collapse-transition>
  </div>
  <div id="body">
    <component :is="currentView" keep-alive></component>
  </div>
  </div>
</template>

<script>
  import TeacherManager from '@/components/AdmComponents/HomeMage'
    export default {
        name: "AdmBox",
      components:{ TeacherManager },
      data(){
          return{
            currentView:'',
            show1:true,
            show2:true,
            show3:true
          }
      },
      methods:{
          changeCom:function(){
            this.$data.currentView='TeacherManager';
          },
          title1:function () {
            var title1icon=document.getElementById("title1icon")
            if(title1icon.className=='el-icon-arrow-down')
            {
              this.$data.show1=!this.$data.show1
              title1icon.className="el-icon-arrow-up"
            }
            else
            {
              this.$data.show1=!this.$data.show1
              title1icon.className="el-icon-arrow-down"
            }
          },
          title2:function () {
            var title2icon=document.getElementById("title2icon")
            if(title2icon.className=='el-icon-arrow-down')
            {
              title2icon.className="el-icon-arrow-up"
              this.$data.show2=!this.$data.show2
            }
            else
            {
              this.$data.show2=!this.$data.show2
              title2icon.className="el-icon-arrow-down"
            }
          },
          title3:function () {
            var title3icon=document.getElementById("title3icon")
            if(title3icon.className=='el-icon-arrow-up')
            {
              this.$data.show3=! this.$data.show3
              title3icon.className='el-icon-arrow-down'
            }
            else
            {
              this.$data.show3=! this.$data.show3
              title3icon.className='el-icon-arrow-up'
            }
          },
          part11:function () {
            var part11=document.getElementById("part11")
            var part21=document.getElementById("part21")
            var part22=document.getElementById("part22")
            var part23=document.getElementById("part23")
            var part24=document.getElementById("part24")
            var part31=document.getElementById("part31")
            var part32=document.getElementById("part32")
            var part33=document.getElementById("part33")
            part11.className='choosepart'
            part21.className='part'
            part22.className='part'
            part23.className='part'
            part24.className='part'
            part31.className='part'
            part32.className='part'
            part33.className='part'
          },
          part21:function () {
            var part11=document.getElementById("part11")
            var part21=document.getElementById("part21")
            var part22=document.getElementById("part22")
            var part23=document.getElementById("part23")
            var part24=document.getElementById("part24")
            var part31=document.getElementById("part31")
            var part32=document.getElementById("part32")
            var part33=document.getElementById("part33")
            part11.className='part'
            part21.className='choosepart'
            part22.className='part'
            part23.className='part'
            part24.className='part'
            part31.className='part'
            part32.className='part'
            part33.className='part'
          },
        part22:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='choosepart'
          part23.className='part'
          part24.className='part'
          part31.className='part'
          part32.className='part'
          part33.className='part'
        },
        part23:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='part'
          part23.className='choosepart'
          part24.className='part'
          part31.className='part'
          part32.className='part'
          part33.className='part'
        },
        part24:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='part'
          part23.className='part'
          part24.className='choosepart'
          part31.className='part'
          part32.className='part'
          part33.className='part'
        },
        part31:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='part'
          part23.className='part'
          part24.className='part'
          part31.className='choosepart'
          part32.className='part'
          part33.className='part'
          this.$data.currentView='teacherManager'
        },
        part32:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='part'
          part23.className='part'
          part24.className='part'
          part31.className='part'
          part32.className='choosepart'
          part33.className='part'
        },
        part33:function () {
          var part11=document.getElementById("part11")
          var part21=document.getElementById("part21")
          var part22=document.getElementById("part22")
          var part23=document.getElementById("part23")
          var part24=document.getElementById("part24")
          var part31=document.getElementById("part31")
          var part32=document.getElementById("part32")
          var part33=document.getElementById("part33")
          part11.className='part'
          part21.className='part'
          part22.className='part'
          part23.className='part'
          part24.className='part'
          part31.className='part'
          part32.className='part'
          part33.className='choosepart'
        }
      }
    }
</script>

<style scoped>
#head{
  width: 100%;
  height:20%;
  padding: 0px;
  margin: 0px;
  border-bottom: solid cornflowerblue 5px;
}
  #aside{
    width: 15%;
    height: 80%;
    float:left;
    background-color: cornflowerblue;
  }
  #body{
    width: 85%;
    height: 80%;
    float: right;

  }
  .title{
    width: 100%;
    height:7%;
    font-size: 35px;
    color: white;
    background-color:cornflowerblue;
    text-align: center;
  }
  .part{
    width: 100%;
    font-size: 25px;
    color: white;
    transition: 1s;
    height:50px;
  }
  .part:hover{
    background-color: white;
    color: cornflowerblue;
    cursor:pointer;
    font-size: 30px;
  }
  .title{
    cursor:pointer;
  }
  .choosepart{
    color: cornflowerblue;
    background-color: white;
    width: 100%;
    font-size: 25px;
    transition: 1s;
    height: 50px;
  }
</style>
