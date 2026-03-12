# Js
document.getElementById("loginForm")?.addEventListener("submit", async function(e){

e.preventDefault()

let username=document.getElementById("username").value
let password=document.getElementById("password").value
let role=document.getElementById("role").value

let res=await fetch("/login",{
method:"POST",
headers:{"Content-Type":"application/json"},
body:JSON.stringify({username,password,role})
})

let data=await res.json()

if(data.success){
window.location="dashboard.html"
}else{
alert("Login Failed")
}

})


async function loadAssignments(){

let res=await fetch("/assignments")
let data=await res.json()

let list=document.getElementById("list")
list.innerHTML=""

data.forEach(a=>{
list.innerHTML+=`<li>${a.title} - ${a.course}</li>`
})

}


async function submitAssignment(){

let title=document.getElementById("title").value
let answer=document.getElementById("answer").value

await fetch("/submit",{
method:"POST",
headers:{"Content-Type":"application/json"},
body:JSON.stringify({title,answer})
})

alert("Submitted")

}
