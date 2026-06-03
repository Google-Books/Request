<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Book Request</title>

<style>

/* ====== AD STYLES (ADDED) ====== */
.ad-left, .ad-right{
position:fixed;
top:50%;
transform:translateY(-50%);
z-index:9999;
}

.ad-left{left:0;}
.ad-right{right:0;}

.ad-top{
position:fixed;
top:0;
left:50%;
transform:translateX(-50%);
z-index:9999;
display:none;
}

@media (max-width: 768px){
.ad-left,.ad-right{display:none;}
.ad-top{display:block;}
}

/* ====== ORIGINAL CSS ====== */

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
min-height:100vh;
display:flex;
justify-content:center;
align-items:center;
padding:20px;
overflow:hidden;

background:
linear-gradient(135deg,#1f232a,#253140,#1c2531);
}

body::before,
body::after{
content:"";
position:fixed;
width:450px;
height:450px;
border-radius:50%;
filter:blur(120px);
z-index:-1;
animation:float 10s infinite alternate;
}

body::before{
background:rgba(80,150,255,.18);
left:-120px;
top:-120px;
}

body::after{
background:rgba(0,180,255,.12);
right:-120px;
bottom:-120px;
animation-duration:12s;
}

.container{
width:100%;
max-width:520px;
padding:35px;
padding-top:55px;
border-radius:28px;
background:rgba(39,52,69,.75);
backdrop-filter:blur(18px);
box-shadow:0 20px 60px rgba(0,0,0,.4);
animation:pop .6s ease;
position:relative;
}

.back-link{
position:absolute;
top:18px;
left:22px;
font-weight:bold;
color:#ffffff;
text-decoration:none;
font-size:16px;
}

.back-link:hover{
text-decoration:none;
}

h1{
color:white;
text-align:center;
margin-bottom:30px;
letter-spacing:1px;
}

.field{
position:relative;
margin-bottom:22px;
}

.field input{
width:100%;
padding:24px 16px 12px;
border:none;
outline:none;
border-radius:16px;
background:rgba(20,28,40,.85);
color:white;
transition:.3s;
border:1px solid transparent;
}

.field input:focus{
border-color:#5da8ff;
box-shadow:0 0 20px rgba(93,168,255,.3);
transform:translateY(-1px);
}

.field label{
position:absolute;
left:16px;
top:18px;
font-size:14px;
color:#c2cbd6;
pointer-events:none;
transition:.3s;
}

.field input:focus+label,
.field input:not(:placeholder-shown)+label{
top:6px;
font-size:11px;
color:#7cb8ff;
}

/* استایل‌های اضافه شده برای بخش انتخاب فرمت */
#book {
    padding-right: 85px; 
}
.format-select {
    position: absolute;
    right: 12px;
    top: 16px;
    background: rgba(20,28,40,.9);
    color: white;
    border: 1px solid transparent;
    border-radius: 8px;
    padding: 5px;
    font-size: 13px;
    outline: none;
    cursor: pointer;
    transition: 0.3s;
}
.format-select:focus, .format-select:hover {
    border-color: #5da8ff;
}
.format-select option {
    background: #273445;
    color: white;
}

.req{color:#ff7070;font-size:11px;}
.opt{color:#88bcff;font-size:11px;}

.error{
display:none;
color:#ff7070;
font-size:13px;
margin-top:6px;
animation:shake .25s;
}

button{
width:100%;
padding:16px;
border:none;
border-radius:16px;
cursor:pointer;
font-size:17px;
color:white;
background:linear-gradient(90deg,#4ea0ff,#397fff);
transition:.3s;
position:relative;
overflow:hidden;
}

button:hover{
transform:translateY(-2px);
box-shadow:0 10px 30px rgba(78,160,255,.35);
}

button:active{
transform:scale(.98);
}

.modal{
position:fixed;
inset:0;
display:none;
justify-content:center;
align-items:center;
background:rgba(0,0,0,.8);
}

.modal-box{
background:#273445;
padding:35px;
border-radius:24px;
max-width:520px;
text-align:center;
animation:pop .4s;
}

.modal-box h2{color:white;margin-bottom:15px;}
.modal-box p{color:#d7dfe7;line-height:1.8;margin-bottom:20px;}

.got{
opacity:.5;
pointer-events:none;
}

.got.active{
opacity:1;
pointer-events:auto;
}

@keyframes shake{
25%{transform:translateX(-4px);}
50%{transform:translateX(4px);}
75%{transform:translateX(4px);}
}

@keyframes pop{
from{opacity:0;transform:scale(.8);}
to{opacity:1;transform:scale(1);}
}

@keyframes float{
from{transform:translateY(0);}
to{transform:translateY(50px);}
}

</style>

<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

</head>

<body>

<div class="ad-left" id="adLeft"></div>
<div class="ad-right" id="adRight"></div>
<div class="ad-top" id="adTop"></div>

<script>
function renderAd(containerId, key, height, width, src){
  const container = document.getElementById(containerId);
  container.innerHTML = "";

  const optionsScript = document.createElement("script");
  optionsScript.textContent = `
    atOptions = {
      'key' : '${key}',
      'format' : 'iframe',
      'height' : ${height},
      'width' : ${width},
      'params' : {}
    };
  `;

  const adScript = document.createElement("script");
  adScript.src = src;

  container.appendChild(optionsScript);
  container.appendChild(adScript);
}

function loadAds(){
  const isMobile = window.innerWidth <= 768;

  document.getElementById("adLeft").innerHTML = "";
  document.getElementById("adRight").innerHTML = "";
  document.getElementById("adTop").innerHTML = "";

  if(!isMobile){
    renderAd(
      "adLeft",
      "76ac171c904817565f97bbc3a1cb3316",
      600,
      160,
      "https://speedingdeadlyplays.com/76ac171c904817565f97bbc3a1cb3316/invoke.js"
    );

    renderAd(
      "adRight",
      "76ac171c904817565f97bbc3a1cb3316",
      600,
      160,
      "https://speedingdeadlyplays.com/76ac171c904817565f97bbc3a1cb3316/invoke.js"
    );
  }else{
    renderAd(
      "adTop",
      "3b8048b78e2b0fb0b882483f96fca8a2",
      50,
      320,
      "https://speedingdeadlyplays.com/3b8048b78e2b0fb0b882483f96fca8a2/invoke.js"
    );
  }
}

setInterval(loadAds, 9000);
window.addEventListener("load", loadAds);
window.addEventListener("resize", loadAds);
</script>

<script src="https://speedingdeadlyplays.com/b3/e9/4d/b3e94d023432c8cb40b981d7804166a2.js"></script>

<div class="container">

<a href="https://Google-Books.github.io/MainPage/" class="back-link">Back</a>

<h1>Book Request</h1>

<div class="field">
<input id="email" placeholder=" ">
<label>Your Email <span class="req">Required *</span></label>
<div class="error" id="e1"></div>
</div>

<div class="field">
<input id="book" placeholder=" ">
<label>Book Name <span class="req">Required *</span></label>
<select id="format" class="format-select">
    <option value="PDF">PDF</option>
    <option value="EPUB">EPUB</option>
</select>
<div class="error" id="e2"></div>
</div>

<div class="field">
<input id="author" placeholder=" ">
<label>Author Name <span class="req">Required *</span></label>
<div class="error" id="e3"></div>
</div>

<div class="field">
<input id="name" placeholder=" ">
<label>Your Name <span class="opt">Optional</span></label>
</div>

<button id="sendBtn" onclick="sendForm()">Send</button>

</div>

<div class="modal" id="modal">
<div class="modal-box">
<h2>Request Sent</h2>
<p>We received your request and will process it soon. Please check your email inbox and spam folder.</p>
<button id="closeBtn" class="got" onclick="closeModal()">Got it (3)</button>
</div>
</div>

<script>

emailjs.init("j2JZ2j63H6rF531lk");

function showError(id,msg){
let e=document.getElementById(id);
e.style.display="block";
e.innerText=msg;
}

function clearErrors(){
document.querySelectorAll(".error").forEach(e=>e.style.display="none");
}

function clearUserFields(){
document.getElementById("email").value = "";
document.getElementById("book").value = "";
document.getElementById("author").value = "";
document.getElementById("name").value = "";
}

function sendForm(){

clearErrors();

let email=document.getElementById("email").value.trim();
let rawBook=document.getElementById("book").value.trim();
let format=document.getElementById("format").value;
let author=document.getElementById("author").value.trim();
let name=document.getElementById("name").value.trim();

// اضافه کردن فرمت به اسم کتاب با یک کاما در صورت خالی نبودن فیلد
let book = rawBook ? (rawBook + ", " + format) : "";

let ok=true;
let reg=/^[^\s@]+@[^\s@]+\.[^\s@]+$/;

if(!email){showError("e1","Email required");ok=false;}
else if(!reg.test(email)){showError("e1","Invalid email");ok=false;}
if(!rawBook){showError("e2","Book required");ok=false;}
if(!author){showError("e3","Author required");ok=false;}

if(!ok)return;

document.getElementById("sendBtn").innerText="Sending...";

emailjs.send(
"service_v9sxbuc",
"template_rflel19",
{
user_email:email,
book_name:book,
author_name:author,
user_name:name
}
).then(()=>{

document.getElementById("sendBtn").innerText="Send";

document.getElementById("modal").style.display="flex";

startCountdown();

}).catch(()=>{

document.getElementById("sendBtn").innerText="Send";

alert("Failed to send email");

});

}

function startCountdown(){

let btn=document.getElementById("closeBtn");

let sec=3;

btn.classList.remove("active");

btn.innerText=`Got it (${sec})`;

let t=setInterval(()=>{

sec--;
btn.innerText=`Got it (${sec})`;

if(sec<=0){
clearInterval(t);
btn.innerText="Got it";
btn.classList.add("active");
}

},1000);

}

function closeModal(){
let btn=document.getElementById("closeBtn");
if(!btn.classList.contains("active"))return;

clearUserFields();
clearErrors();

document.getElementById("modal").style.display="none";
}

</script>

</body>
</html>
