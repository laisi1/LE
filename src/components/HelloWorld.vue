<!--
 * @Author: your name
 * @Date: 2021-11-25 09:48:34
 * @LastEditTime: 2021-11-25 14:20:51
 * @LastEditors: Please set LastEditors
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: \Le Wei\le-dom\src\components\HelloWorld.vue
-->
<template>
  <div>
    <div class="hello_qj">
      <div class="searchuser">
          <input type="text" placeholder="请输入用户名" class="inp"  />
          <button>搜索</button>
      </div>
      <div class="newuser">
           <div class="newuser_bat" @click="newuser_bat">新增用户</div>
           <div class="newlyadded" v-if="Isuse == true">
             <div class="x">
               <div class="textuser">新增用户</div>
               <span @click="hide">X</span>
             </div>
             <div class="useyh">
               <div class="username">
                 <span>用户名:</span>
                 <input type="text" placeholder="请输入用户名" class="username_inp" v-model="inpuse" />
               </div>
               <div class="useyh_qd">
                 <button class="useyh_qd_bat" @click="useyh_qd_bat">确定</button>
               </div>
             </div>
           </div>
      </div>
      <div class="userlist">
           <div class="userlist_top">
               <ul class="userlist_top_ul">
                 <li class="userlist_top_list" v-for="(item,index) in Serialnumber" :key="index">{{item}}</li>
               </ul>
           </div>
           <div class="userlist_buttom">
               <ul class="userlist_buttom_ul">
                 <li class="userlist_buttom_list" v-for="(item,index) in userarr" :key="index">
                   <div class="userlist_buttom_list_ind wih">{{index+1}}</div>
                   <div class="userlist_buttom_list_nama wih">{{item.usernama}}</div>
                   <div class="userlist_buttom_list_operation wih">
                     <span class="modify" @click="modify(index)">修改</span>
                     <div :class="modiuser?'modifypopup':'modifypopupA'">
                         <div class="modifypopup_x">
                           <div class="textuser">修改用户名</div>
                             <span @click="hide1">X</span>
                        </div> 
                        <div class="modify_user">
                          <div class="">
                            <span>用户名:</span>
                            <input type="text" placeholder="请输入用户名" v-model="modiinuser" class="username_inp" />
                          </div>
                          <div class="modify_buttom">
                            <button class="modify_buttom_bat" @click="confirm1()">确定</button>
                          </div>
                        </div>
                     </div>
                     <span class="del" @click="del(index)">删除</span>
                   </div>
                 </li>
               </ul>
           </div>
      </div>
     
      </div>
       <div :class="Isuse?'hello':''"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      nabn:0,
      modiuser:false,
      inpuse:"",
      modiinuser:"",
      Isuse:false,
      Serialnumber:["序号","用户名","操作"],
      userarr:[
        {
          id:0,
          usernama:"用户1"
          
        },
        {
          id:1,
          usernama:"用户2"
        }
      ]
    }
  },
  methods:{
    del(index){
    this.userarr.splice(index,1)
    },
    newuser_bat(){
      this.Isuse = !this.Isuse
      console.log(this.Isuse);
    },
    hide(){
      this.Isuse = !this.Isuse
    },
    useyh_qd_bat(){
      let vg = {
         id:3,
        usernama:""
      }
      vg.usernama = this.inpuse
      this.userarr.push(vg)
      this.inpuse = "";
      this.Isuse = !this.Isuse
    },
    modify(id){
      this.nabn = id
       this.modiinuser = this.userarr[id].usernama
      this.modiuser = true
      this.Isuse = true
    },
    confirm1(){
     this.userarr[this.nabn].usernama = this.modiinuser
       this.modiinuser = ""
      this.modiuser = false
      this.Isuse = false
    },
    hide1(){
      this.modiinuser = ""
      this.modiuser = false
      this.Isuse = false
    }
  }
}
</script>


<style scoped>
   *{
  margin: 0px;
  padding: 0px;
  list-style: none;
   }
   .hello{
      position: fixed;
      z-index: 10;
     width: 100%;
     height: 100%;
     margin: 0px;
     top: 0px;
     padding: 0px;
     background-color: rgba(0, 0, 0, 0.5);
    
     
   }
   .hello_qj{
       width: 50%;
     /* height: 100px; */
     padding-bottom: 80px;
     border: 1px solid #000000;
     border-radius: 10px;
     /* background-color: antiquewhite; */
     margin: 20px auto;
   }
   .searchuser{
    width: 100%;
    display: flex;
    justify-content: center;
     margin-top: 20px;
   }
   .inp{
    
     width: 20%;
     height: 30px;
     border: 1px solid #d3d7d4;
     padding-left: 10px;
     outline: none;
   }
   .newuser{

   }
   .newuser_bat{
     width: 100px;
     height: 30px;
     background-color: darkturquoise;
     border: 1px solid darkturquoise;
     border-radius: 5px;
     color: #ffffff;
     font-size: 18px;
     text-align: center;
     line-height: 30px;
     cursor: pointer;
     margin-left: 50px;
     margin-top: 50px;
   }
   .newlyadded{
     position: fixed;
     top: 100px;
      z-index: 20;
     left: 650px;
     width: 600px;
     height: 300px;
     background-color: #ffffff;
     border: 1xp solid #000000;
     border-radius: 10px;
     /* display: none; */
   }
  .x{
    display: flex;
    justify-content: space-between;
    padding: 0px 20px;
    margin-top: 10px;
    /* margin-right: 30px;
    margin-top: 20px; */
  
  }
  .x span{
    cursor: pointer;
  }
  .useyh{
    
    width: 50%;
    padding-bottom: 20px;
    margin: 0px auto;
    margin-top: 50px;
    /* margin: 0px auto; */
    /* display: flex;
    justify-content: center;
    align-content: center; */
  }
  .username_inp{
    width: 180px;
    padding-left: 10px;
    height: 30px;
    border: 1px solid #d3d7d4;
    margin-left: 20px;
    outline: none;
  }
  .useyh_qd{
    width: 100%;
    margin-top: 50px;
  }
  .useyh_qd_bat{
    width: 80px;
    height: 40px;
    background-color: aqua;
    border: 1px solid aqua;
    border-radius: 10px;
    font-size: 16px;
    margin-left: 70px;
    /* color: #ffffff; */
  }
  .modifypopup{
     position: fixed;
     top: 100px;
      z-index: 20;
     left: 650px;
     width: 600px;
     height: 300px;
     background-color: #ffffff;
     border: 1xp solid #000000;
     border-radius: 10px;
  }
  .modifypopupA{
    display: none;
  }
  .modifypopup_x{
    display: flex;
    justify-content: space-between;
    padding: 0px 20px;
    margin-top: 10px;
  }
  .textuser{
    font-weight: bold;
  }
  .modifypopup_x span{
    cursor: pointer;
  }
  .modify_user{
    width: 50%;
    padding-bottom: 20px;
    margin: 0px auto;
    margin-top: 50px;
  }
  .modify_buttom{
    width: 100%;
  }
  .modify_buttom_bat{
    width: 90px;
     height: 30px;
     background-color: darkturquoise;
     border: 1px solid darkturquoise;
     border-radius: 5px;
     color: #ffffff;
     font-size: 18px;
     text-align: center;
     line-height: 30px;
     cursor: pointer;
     margin-left: 50px;
     margin-top: 50px;
  }
  .userlist{
    width: 100%;
    /* padding-bottom: 20px; */
  }
   .userlist_top{
     width: 95%;
     height: 30px;
     margin: 0px auto;
     margin-top: 30px;
     line-height: 30px;
     background-color: aquamarine;
   }
   .userlist_top_ul{
     margin: 0px;
     padding: 0px;
     display: flex;
     justify-content: space-between;
     padding: 0px 30px;
   }
   .userlist_top_list{
     /* width: 50%; */
   }
   .userlist_buttom{
     width: 90%;
     /* height: 30px; */
     margin: 0px auto;
     margin-top: 20px;
     line-height: 30px;
   }
   .userlist_buttom_ul{
     margin: 0px;
      padding: 0px;
   }
   .userlist_buttom_list{
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
   }
   .wih{
    
   }
   .userlist_buttom_list_ind{
     margin-left: 15px;
   }
   .userlist_buttom_list_nama{
     margin-left: 65px;
   }
   .userlist_buttom_list_operation{
     margin-right: 10px;
   }
   .modify{
     display: inline-block;
     width: 50px;
     height: 20px;
     background-color: cadetblue;
     font-size: 16px;
     text-align: center;
     line-height: 20px;
     border: none;
     border-radius: 5px;
     color: #ffffff;
     margin-right: 10px;
     cursor: pointer;
   }
   .del{
      display: inline-block;
     width: 50px;
     height: 20px;
     background-color: red;
     font-size: 16px;
     text-align: center;
     line-height: 20px;
     border: none;
     border-radius: 5px;
     color: #ffffff;
     margin-right: -30px;
     cursor: pointer;
   }
      /* .mask{
   
   } */
</style>
