<template>
 <form @submit.prevent="handleSubmit">
     <label> Email:</label>
     <input type="text" required v-model="email">
     <label>Password:</label>
     <input type="password" required v-model="password">
     <div class="err">{{passwordError}}</div>
     <label >Role:</label>
     <select v-model='role'>
         <option value="developer">Web Developer</option>
         <option value="android">Android Developer</option>
         <option value="flutter">Flutter Developer</option>
     </select>
     <label > Skills:</label>
     <input type="text" v-model="tempSkill" @keyup="addskill">
       <div>
         <span v-for="skill in skills" :key="skill" class="pill" @click=deleteSkill(skill)> {{skill }}  </span>  
       </div>
     <div class="terms">
         <input type="checkbox" required v-model="terms">
         <label > Accept terms and conditions </label>
     </div>
     <div class="submit">
         <button> Create account</button>
     </div>
    
     
 </form>
 
</template>

<script>
export default {
    data(){
        return{
            email:'',
            password:'',
            role:'developer',
            terms:false,
            tempSkill:'',
            skills:[],
            passwordError:''
        }
    },
    methods:{
        addskill(e){
            if( e.key==="," && this.tempSkill && this.tempSkill.charAt(0)!==','){
                this.tempSkill=this.tempSkill.substring(0, this.tempSkill.length-1)
                this.skills.push(this.tempSkill)
                console.log(this.skills)
                this.tempSkill=null
            }
        },
        deleteSkill(item){
           let indexItem=this.skills.indexOf(item)
           this.skills.splice(indexItem,1)
        },
        handleSubmit(){
          this.passwordError=this.password.length>5?'':'Password characters must be at least 5'
         
        }
    }
}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    padding: 40px;
    text-align: left;
   border-radius: 10px;

}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6 rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;

}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;


}
input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;

}
.pill{
    display: inline-block;
    margin: 20px 10px  0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 10px;
    font-size: 12px;
    letter-spacing: 1px;
    color: #777;
    font-weight: bold;
    cursor: pointer;
}
button{
    display: inline-block;
    margin-top: 15px;
    padding: 10px 14px;
    background: crimson;
    color: white;
    border-radius: 10px;
    border: none;
    font-size: 14px;
    cursor: pointer;
}
.submit{
    text-align: center;
}
button:hover{
    transform: scale(1.05);
    background: orange;
}
.err{
    color: red;
    margin-top: 5px;
}
</style>