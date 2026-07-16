# Massage-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Massage Booking</title>

<style>
body{
    font-family:Arial,Helvetica,sans-serif;
    background:#ffeef6;
    margin:0;
    text-align:center;
}

header{
    background:#ff69b4;
    color:white;
    padding:20px;
    font-size:40px;
    font-weight:bold;
}

#calendar{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(120px,1fr));
    gap:10px;
    padding:20px;
    max-width:1200px;
    margin:auto;
}

.day{
    padding:15px;
    border-radius:12px;
    cursor:pointer;
    color:white;
    font-weight:bold;
    transition:.2s;
}

.day:hover{
    transform:scale(1.05);
}

.year2026{
    background:#ff66b3;
}

.year2027{
    background:#b86bff;
}

.year2028{
    background:#66b3ff;
}

#booking{
    display:none;
    margin:30px auto;
    background:white;
    width:90%;
    max-width:600px;
    border-radius:15px;
    padding:20px;
    box-shadow:0 0 15px rgba(0,0,0,.2);
}

#times{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:10px;
    margin-top:20px;
}

.time{
    background:#ff99cc;
    padding:10px;
    border-radius:10px;
    cursor:pointer;
}

.time:hover{
    background:#ff69b4;
    color:white;
}

.selected{
    background:#ff1493 !important;
    color:white;
}

button{
    margin-top:20px;
    padding:15px 35px;
    font-size:18px;
    border:none;
    border-radius:10px;
    background:#ff1493;
    color:white;
    cursor:pointer;
}

button:hover{
    background:#d6006f;
}
</style>
</head>

<body>

<header>Massage</header>

<div id="calendar"></div>

<div id="booking">
<h2 id="selectedDate"></h2>

<div id="times"></div>

<button onclick="book()">Book</button>

</div>

<script>

const start=new Date(2026,6,1);
const end=new Date(2028,6,22);

const calendar=document.getElementById("calendar");

let current=new Date(start);

let chosenDate="";
let chosenTime="";

while(current<=end){

let div=document.createElement("div");

div.classList.add("day");

if(current.getFullYear()==2026) div.classList.add("year2026");
if(current.getFullYear()==2027) div.classList.add("year2027");
if(current.getFullYear()==2028) div.classList.add("year2028");

let options={
weekday:'short',
day:'numeric',
month:'short',
year:'numeric'
};

div.innerHTML=current.toLocaleDateString('en-GB',options);

div.onclick=()=>selectDate(new Date(current));

calendar.appendChild(div);

current.setDate(current.getDate()+1);

}

function selectDate(date){

chosenDate=date.toDateString();

document.getElementById("booking").style.display="block";

document.getElementById("selectedDate").innerHTML=
"Selected Date:<br>"+chosenDate;

const times=document.getElementById("times");

times.innerHTML="";

chosenTime="";

for(let hour=9;hour<=21;hour++){

let btn=document.createElement("div");

let display=(hour<=12?hour:hour-12)+":00 "+(hour<12?"AM":"PM");

if(hour==12) display="12:00 PM";

btn.innerHTML=display;

btn.className="time";

btn.onclick=function(){

document.querySelectorAll(".time").forEach(x=>x.classList.remove("selected"));

btn.classList.add("selected");

chosenTime=display;

}

times.appendChild(btn);

}

window.scrollTo({
top:document.body.scrollHeight,
behavior:"smooth"
});

}

function book(){

if(chosenDate==""||chosenTime==""){

alert("Please select a date and time.");

return;

}

const email="32lhirata@bst.ac.jp";

const subject="Massage Booking";

const body=
"New Massage Booking%0D%0A%0D%0ADate: "+chosenDate+
"%0D%0ATime: "+chosenTime;

window.location.href=
`mailto:${email}?subject=${subject}&body=${body}`;

}

</script>

</body>
</html>
