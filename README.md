# qimmat-lughati
قمة لغتي
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>قمم لغتي</title>
<style>
body{
font-family:Arial,sans-serif;
background:#f3f7f5;
margin:0;
padding:20px;
color:#222;
}
.container{
max-width:700px;
margin:auto;
background:white;
padding:25px;
border-radius:20px;
box-shadow:0 4px 15px rgba(0,0,0,.1);
}
h1{
text-align:center;
color:#246b45;
font-size:32px;
}
.subtitle{
text-align:center;
color:#666;
margin-bottom:30px;
}
.choice{
display:block;
width:100%;
padding:18px;
margin:15px 0;
border:0;
border-radius:14px;
background:#246b45;
color:white;
font-size:20px;
cursor:pointer;
}
.choice:hover{
opacity:.9;
}
.passage{
margin:20px 0;
padding:18px;
background:#eaf4ee;
border-right:5px solid #246b45;
border-radius:10px;
line-height:1.9;
font-size:18px;
}
.question{
margin:25px 0;
padding:18px;
background:#f7faf8;
border-radius:14px;
}
.question h3{
margin-top:0;
}
.tag{
display:inline-block;
font-size:13px;
color:#246b45;
background:#dff1e6;
padding:3px 10px;
border-radius:20px;
margin-bottom:8px;
}
label{
display:block;
padding:12px;
margin:8px 0;
background:white;
border-radius:9px;
cursor:pointer;
}
label:hover{
background:#eaf4ee;
}
button{
width:100%;
padding:15px;
border:0;
border-radius:12px;
background:#246b45;
color:white;
font-size:19px;
cursor:pointer;
margin-top:10px;
}
.back{
background:#777;
}
#result{
margin-top:20px;
padding:18px;
text-align:center;
font-size:22px;
font-weight:bold;
border-radius:12px;
}
.nameBox{
margin:20px 0 30px 0;
}
.nameBox label{
display:block;
margin-bottom:8px;
font-weight:bold;
color:#246b45;
background:none;
padding:0;
cursor:default;
}
.nameBox input{
width:100%;
box-sizing:border-box;
padding:14px;
border:2px solid #246b45;
border-radius:12px;
font-size:18px;
font-family:Arial,sans-serif;
}
</style>
</head>
<body>
<div class="container">
<div id="home">
<h1>📚 قمم لغتي</h1>
<p class="subtitle">
موقع تفاعلي لمادة لغتي الخالدة
</p>
<h2 style="text-align:center;">
اختاري الصف الدراسي
</h2>
<button class="choice" onclick="startQuiz(1)">
🌸 أول متوسط
</button>
<button class="choice" onclick="startQuiz(2)">
🌷 ثاني متوسط
</button>
</div>

<div id="quizPage" style="display:none;">
<h1 id="quizTitle"></h1>
<div class="nameBox">
<label for="studentName">اسم الطالبة:</label>
<input type="text" id="studentName" placeholder="اكتبي اسمك هنا">
</div>
<div class="passage" id="passageBox"></div>
<form id="quizForm"></form>
<button onclick="checkAnswers()" type="button">
إظهار النتيجة ✅
</button>
<button onclick="goHome()" type="button" class="back">
العودة لاختيار الصف
</button>
<div id="result"></div>
</div>
</div>

<script>
let currentGrade = 1;

/* نص القراءة - أول متوسط */
const firstGradePassage =
"القراءة غذاء العقل، فهي تزيد معرفتنا وتوسع مداركنا. يحب أحمد القراءة كثيرًا، فهو يقرأ كل يوم قصة جديدة قبل النوم. وقد جعلته القراءة أكثر ذكاءً وثقة بنفسه.";

/* أسئلة أول متوسط - متنوعة: فهم قرائي / نحو / إملاء / خط */
const firstGrade = [
{
tag:"فهم قرائي",
q:"ماذا يفعل أحمد كل يوم قبل النوم؟",
a:["يشاهد التلفاز","يقرأ قصة جديدة","يلعب مع أصدقائه"],
correct:1
},
{
tag:"فهم قرائي",
q:"بم وصف النص فائدة القراءة؟",
a:["تزيد المعرفة وتوسع المدارك","تسبب النعاس","تُتعب العينين فقط"],
correct:0
},
{
tag:"فهم قرائي",
q:"كيف جعلت القراءة أحمد بحسب النص؟",
a:["أكثر خجلًا","أكثر نسيانًا","أكثر ذكاءً وثقة بنفسه"],
correct:2
},
{
tag:"نحو",
q:"ما نوع كلمة «القراءة» في «القراءة غذاء العقل»؟",
a:["فعل","اسم","حرف"],
correct:1
},
{
tag:"نحو",
q:"«يقرأ أحمد كل يوم» - كلمة «يقرأ» فعل:",
a:["ماضٍ","مضارع","أمر"],
correct:1
},
{
tag:"إملاء",
q:"ما الكتابة الصحيحة لهذه الكلمة؟",
a:["هاذا الكتاب","هذا الكتاب","هاذه الكتاب"],
correct:1
},
{
tag:"إملاء",
q:"أي الكلمات الآتية كُتبت بشكل صحيح؟",
a:["مدرسه جميلة","مدرسة جميلة","مدرستن جميلة"],
correct:1
},
{
tag:"خط",
q:"أي حرف من الحروف الآتية لا يتصل بما بعده؟",
a:["ب","د","ت"],
correct:1
},
{
tag:"خط",
q:"كم عدد نقاط حرف «ث»؟",
a:["واحدة","اثنتان","ثلاث"],
correct:2
},
{
tag:"خط",
q:"أي الحروف الآتية له أكثر من صورة (شكل) واحدة عند الكتابة؟",
a:["د","ع","ر"],
correct:1
}
];

/* نص القراءة - ثاني متوسط */
const secondGradePassage =
"الصداقة الحقيقية كنزٌ لا يقدَّر بثمن، فالصديق الوفي يقف بجانبك في السراء والضراء، ويسعى دائمًا لمساعدتك دون انتظار مقابل. لذلك ينبغي على الإنسان أن يُحسن اختيار أصدقائه.";

/* أسئلة ثاني متوسط - متنوعة: فهم قرائي / نحو / إملاء / خط */
const secondGrade = [
{
tag:"فهم قرائي",
q:"بم وصف الكاتب الصداقة الحقيقية؟",
a:["عبئًا ثقيلًا","كنزًا لا يقدَّر بثمن","أمرًا عاديًا"],
correct:1
},
{
tag:"فهم قرائي",
q:"متى يقف الصديق الوفي بجانبك بحسب النص؟",
a:["في السراء فقط","في الضراء فقط","في السراء والضراء"],
correct:2
},
{
tag:"فهم قرائي",
q:"بم ينصح الكاتب في نهاية النص؟",
a:["بعدم الثقة بأحد","بإحسان اختيار الأصدقاء","بالابتعاد عن الناس"],
correct:1
},
{
tag:"نحو",
q:"ما إعراب كلمة «كنزٌ» في «الصداقة كنزٌ»؟",
a:["مبتدأ","خبر مرفوع","مفعول به"],
correct:1
},
{
tag:"نحو",
q:"«يسعى الصديق لمساعدتك» - الفعل «يسعى» فعل:",
a:["ماضٍ","مضارع","أمر"],
correct:1
},
{
tag:"إملاء",
q:"ما الكتابة الصحيحة لهمزة هذه الكلمة؟",
a:["اصدقاء","أصدقاء","إصدقاء"],
correct:1
},
{
tag:"إملاء",
q:"أي الكلمات الآتية كُتبت بألف لينة صحيحة؟",
a:["مشى","مشا","مشاء"],
correct:0
},
{
tag:"خط",
q:"أي حرف من الحروف الآتية لا يتصل بما بعده مطلقًا؟",
a:["س","ر","م"],
correct:1
},
{
tag:"خط",
q:"كم عدد نقاط حرف «ش»؟",
a:["واحدة","اثنتان","ثلاث"],
correct:2
},
{
tag:"خط",
q:"عند كتابة حرف الواو في وسط الكلمة، فإنه:",
a:["يتصل بما قبله فقط","يتصل بما بعده فقط","يتصل بما قبله وبما بعده"],
correct:0
}
];

function startQuiz(grade){
currentGrade = grade;
let questions;
let passage;
if(grade === 1){
questions = firstGrade;
passage = firstGradePassage;
document.getElementById("quizTitle").innerHTML =
"🌸 اختبار لغتي - أول متوسط";
}
else{
questions = secondGrade;
passage = secondGradePassage;
document.getElementById("quizTitle").innerHTML =
"🌷 اختبار لغتي - ثاني متوسط";
}
document.getElementById("studentName").value = "";
document.getElementById("passageBox").innerHTML =
"📖 " + passage;
let form = document.getElementById("quizForm");
form.innerHTML = "";
questions.forEach((item,index)=>{
let html = `
<div class="question">
<span class="tag">${item.tag}</span>
<h3>${index+1}. ${item.q}</h3>
`;
item.a.forEach((answer,i)=>{
html += `
<label>
<input type="radio"
name="q${index}"
value="${i}">
${answer}
</label>
`;
});
html += `</div>`;
form.innerHTML += html;
});
document.getElementById("home").style.display="none";
document.getElementById("quizPage").style.display="block";
window.scrollTo(0,0);
}

function checkAnswers(){
let name = document.getElementById("studentName").value.trim();
if(name === ""){
alert("الرجاء كتابة اسمك أولًا");
return;
}
let questions =
currentGrade === 1 ? firstGrade : secondGrade;
let score = 0;
questions.forEach((item,index)=>{
let selected =
document.querySelector(
'input[name="q'+index+'"]:checked'
);
if(selected &&
Number(selected.value) === item.correct){
score++;
}
});
document.getElementById("result").innerHTML =
"🌟 " + name + "، نتيجتك: " + score + " من " + questions.length;
}

function goHome(){
document.getElementById("quizPage").style.display="none";
document.getElementById("home").style.display="block";
document.getElementById("result").innerHTML="";
window.scrollTo(0,0);
}
</script>
</body>
</html>
