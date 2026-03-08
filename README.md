# Herlan-avalia-o-fisica
Site de avaliação física com cálculo de IMC, percentual de gordura, massa magra e medidas antropométricas.
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Calculadora de Avaliação Física</title>

<style>

body{
font-family: Arial;
background:#f4f4f4;
padding:30px;
}

.container{
max-width:600px;
margin:auto;
background:white;
padding:25px;
border-radius:10px;
box-shadow:0 0 10px rgba(0,0,0,0.1);
}

h1{
text-align:center;
}

input,select{
width:100%;
padding:8px;
margin:5px 0 15px;
}

button{
width:100%;
padding:12px;
background:#28a745;
color:white;
border:none;
font-size:16px;
cursor:pointer;
}

button:hover{
background:#218838;
}

.resultado{
margin-top:20px;
padding:15px;
background:#e9ecef;
border-radius:8px;
}

</style>
</head>

<body>

<div class="container">

<h1>Avaliação Física</h1>

<label>Sexo</label>
<select id="sexo">
<option value="homem">Homem</option>
<option value="mulher">Mulher</option>
</select>

<label>Idade</label>
<input type="number" id="idade">

<label>Peso (kg)</label>
<input type="number" id="peso">

<label>Altura (m)</label>
<input type="number" step="0.01" id="altura">

<label>Soma das 7 dobras (mm)</label>
<input type="number" id="dobras">

<label>Cintura (cm)</label>
<input type="number" id="cintura">

<label>Quadril (cm)</label>
<input type="number" id="quadril">

<button onclick="calcular()">Calcular Avaliação</button>

<div class="resultado" id="resultado"></div>

</div>

<script>

function calcular(){

let sexo = document.getElementById("sexo").value;
let idade = parseFloat(document.getElementById("idade").value);
let peso = parseFloat(document.getElementById("peso").value);
let altura = parseFloat(document.getElementById("altura").value);
let dobras = parseFloat(document.getElementById("dobras").value);
let cintura = parseFloat(document.getElementById("cintura").value);
let quadril = parseFloat(document.getElementById("quadril").value);

let densidade;

if(sexo=="homem"){

densidade = 1.112
- (0.00043499 * dobras)
+ (0.00000055 * (dobras*dobras))
- (0.00028826 * idade);

}else{

densidade = 1.097
- (0.00046971 * dobras)
+ (0.00000056 * (dobras*dobras))
- (0.00012828 * idade);

}

let gordura = (495 / densidade) - 450;

let massaGorda = peso * (gordura/100);
let massaMagra = peso - massaGorda;

let imc = peso / (altura*altura);

let rcq = cintura / quadril;

let classIMC;

if(imc < 18.5) classIMC = "Baixo peso";
else if(imc < 25) classIMC = "Normal";
else if(imc < 30) classIMC = "Sobrepeso";
else if(imc < 35) classIMC = "Obesidade I";
else if(imc < 40) classIMC = "Obesidade II";
else classIMC = "Obesidade III";

let classGordura;

if(sexo=="homem"){

if(gordura < 14) classGordura = "Atleta";
else if(gordura < 18) classGordura = "Fitness";
else if(gordura < 25) classGordura = "Normal";
else classGordura = "Alto";

}else{

if(gordura < 21) classGordura = "Atleta";
else if(gordura < 25) classGordura = "Fitness";
else if(gordura < 32) classGordura = "Normal";
else classGordura = "Alto";

}

let classRCQ;

if(sexo=="homem"){

if(rcq < 0.9) classRCQ = "Baixo risco";
else if(rcq < 1.0) classRCQ = "Risco moderado";
else classRCQ = "Alto risco";

}else{

if(rcq < 0.8) classRCQ = "Baixo risco";
else if(rcq < 0.86) classRCQ = "Risco moderado";
else classRCQ = "Alto risco";

}

document.getElementById("resultado").innerHTML =

"<b>IMC:</b> " + imc.toFixed(2) + " (" + classIMC + ")<br><br>" +

"<b>Densidade corporal:</b> " + densidade.toFixed(3) + "<br><br>" +

"<b>% Gordura:</b> " + gordura.toFixed(2) + "% (" + classGordura + ")<br><br>" +

"<b>Massa gorda:</b> " + massaGorda.toFixed(2) + " kg<br><br>" +

"<b>Massa magra:</b> " + massaMagra.toFixed(2) + " kg<br><br>" +

"<b>RCQ:</b> " + rcq.toFixed(2) + " (" + classRCQ + ")";

}

</script>

</body>
</html>
