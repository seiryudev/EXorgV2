# EXorgV2
o Futuro é o nosso destino

<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#080808">
<title>EXorg | Command Center</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

<style>
:root {
  --bg:#080808;
  --panel:#111;
  --panel2:#171717;
  --gold:#d6ad55;
  --text:#f4f0e8;
  --muted:#999;
  --border:#292929;
}
*{box-sizing:border-box}
body{
  margin:0;background:var(--bg);color:var(--text);
  font-family:Inter,Arial,sans-serif;min-height:100vh
}
header{
  padding:20px 6%;border-bottom:1px solid var(--border);
  display:flex;justify-content:space-between;align-items:center;
  position:sticky;top:0;background:#080808ed;z-index:10
}
.logo{font-size:23px;font-weight:900;letter-spacing:4px}
.logo span{color:var(--gold)}
button{
  background:var(--gold);color:#090909;border:0;
  padding:12px 17px;border-radius:7px;font-weight:800;cursor:pointer
}
button.secondary{background:var(--panel2);color:var(--text);border:1px solid var(--border)}
button:disabled{opacity:.5;cursor:not-allowed}
input,select,textarea{
  width:100%;padding:13px;background:#090909;color:white;
  border:1px solid var(--border);border-radius:7px;margin:7px 0 14px
}
main{max-width:1150px;margin:auto;padding:35px 6%}
.hero{padding:45px 0}
.eyebrow{color:var(--gold);letter-spacing:3px;font-size:12px;font-weight:bold}
h1{font-size:clamp(35px,7vw,65px);margin:12px 0}
h2{font-size:23px}
p{color:var(--muted);line-height:1.6}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px}
.card{
  background:var(--panel);border:1px solid var(--border);
  border-radius:12px;padding:22px;margin-bottom:15px
}
.card h3{margin-top:0}
.card small{color:var(--gold)}
.section{margin-top:40px}
.hidden{display:none!important}
.actions{display:flex;gap:9px;flex-wrap:wrap}
.tag{font-size:11px;color:var(--gold);border:1px solid #57451e;padding:5px 8px;border-radius:20px}
footer{border-top:1px solid var(--border);padding:25px 6%;color:var(--muted);text-align:center}
#notice{padding:12px;border-radius:7px;background:#191919;color:var(--gold);margin:12px 0}
</style>
</head>

<body>
<header>
  <div class="logo">EX<span>ORG</span></div>
  <div class="actions">
    <button class="secondary" onclick="showPage('home')">Início</button>
    <button onclick="showPage('login')">Entrar</button>
  </div>
</header>

<main>
  <section id="home">
    <div class="hero">
      <div class="eyebrow">EXORG ECOSYSTEM</div>
      <h1>Um sistema.<br><span style="color:var(--gold)">Várias possibilidades.</span></h1>
      <p>Centro de controlo e integração das plataformas EXorg.</p>
      <div class="actions">
        <button onclick="showPage('student')">Portal do aluno</button>
        <button class="secondary" onclick="showPage('login')">Acesso administrativo</button>
      </div>
    </div>

    <div class="section">
      <h2>Plataformas integradas</h2>
      <div class="grid">
        <div class="card">
          <small>EDUCAÇÃO</small>
          <h3>EXorg MT</h3>
          <p>Portal académico, aprendizagem e acompanhamento de bem-estar.</p>
          <button onclick="showPage('student')">Aceder</button>
        </div>
        <div class="card">
          <small>GESTÃO</small>
          <h3>Áurea Manager</h3>
          <p>Gestão financeira, operações e negócios.</p>
          <button onclick="showPage('aurea')">Abrir módulo</button>
        </div>
        <div class="card">
          <small>COMÉRCIO</small>
          <h3>Áurea Lifestyle</h3>
          <p>Área comercial e organização de vendas.</p>
          <button onclick="showPage('aurea')">Abrir módulo</button>
        </div>
      </div>
    </div>
  </section>

  <section id="login" class="hidden">
    <div class="card" style="max-width:480px;margin:30px auto">
      <div class="eyebrow">IDENTIFICAÇÃO</div>
      <h2>Entrar no EXorg</h2>
      <label>Email</label>
      <input id="email" type="email" placeholder="teu@email.com">
      <label>Palavra-passe</label>
      <input id="password" type="password" placeholder="Palavra-passe">
      <button onclick="login()">Entrar</button>
      <button class="secondary" onclick="register()">Criar conta</button>
      <div id="authMessage"></div>
    </div>
  </section>

  <section id="student" class="hidden">
    <div class="eyebrow">EXORG MT · MADEIRA TRINDADE</div>
    <h1>Portal do aluno</h1>
    <p>Aprender, evoluir e acompanhar o teu percurso.</p>
    <div class="grid">
      <div class="card">
        <small>BEM-ESTAR</small>
        <h3>Check-in diário</h3>
        <p>Um espaço privado de reflexão. Não é diagnóstico médico nem avaliação clínica.</p>
        <button onclick="showPage('wellbeing')">Começar</button>
      </div>
      <div class="card">
        <small>APRENDIZAGEM</small>
        <h3>Academia Pixel</h3>
        <p>Desafios educativos de matemática e língua portuguesa.</p>
        <button onclick="showPage('academy')">Jogar</button>
      </div>
      <div class="card">
        <small>PROGRESSO</small>
        <h3>Meu percurso</h3>
        <p>Consulta o teu progresso de aprendizagem.</p>
        <button onclick="loadProgress()">Consultar</button>
      </div>
    </div>
    <div id="progress"></div>
  </section>

  <section id="wellbeing" class="hidden">
    <div class="eyebrow">EXORG MT · BEM-ESTAR</div>
    <h1>Como estás hoje?</h1>
    <p>Responde com sinceridade. As respostas são para reflexão e apoio, não para diagnóstico ou classificação.</p>
    <div class="card">
      <h3 id="wellQuestion">Como te sentes hoje?</h3>
      <select id="wellAnswer">
        <option value="">Escolhe uma resposta</option>
        <option value="1">Muito mal</option>
        <option value="2">Mal</option>
        <option value="3">Mais ou menos</option>
        <option value="4">Bem</option>
        <option value="5">Muito bem</option>
      </select>
      <button onclick="saveWellbeing()">Guardar resposta</button>
      <p id="wellMessage"></p>
    </div>
  </section>

  <section id="academy" class="hidden">
    <div class="eyebrow">ACADEMIA PIXEL</div>
    <h1>Desafio do dia</h1>
    <div class="card">
      <small>MATEMÁTICA</small>
      <h3 id="quizQuestion">Quanto é 12 × 8?</h3>
      <div id="quizOptions" class="grid"></div>
      <p id="quizResult"></p>
    </div>
  </section>

  <section id="aurea" class="hidden">
    <div class="eyebrow">ÁUREA ECOSYSTEM</div>
    <h1>Gestão e comércio</h1>
    <div class="grid">
      <div class="card"><h3>Áurea Manager</h3><p>Área de gestão financeira e administrativa.</p><span class="tag">Módulo preparado</span></div>
      <div class="card"><h3>Áurea Lifestyle</h3><p>Área comercial da marca.</p><span class="tag">Módulo preparado</span></div>
    </div>
  </section>

  <section id="admin" class="hidden">
    <div class="eyebrow">EXORG CORE</div>
    <h1>Command Center</h1>
    <div class="card">
      <h3>Registar plataforma</h3>
      <label>Nome</label>
      <input id="platformName" placeholder="Nome da plataforma">
      <label>Descrição</label>
      <input id="platformDescription" placeholder="Finalidade">
      <button onclick="createPlatform()">Registar</button>
      <p id="platformMessage"></p>
    </div>
    <div class="card">
      <h3>Plataformas registadas</h3>
      <div id="platformList">A carregar...</div>
    </div>
  </section>

  <div id="notice">Modo de demonstração: configura o Supabase antes de utilizar contas ou dados reais.</div>
</main>

<footer>EXORG CORE · Arquitetura integrada · 2026</footer>

<script>
// CONFIGURAÇÃO: substitui pelos dados públicos do teu projeto Supabase.
const SUPABASE_URL = "https://TEU-PROJETO.supabase.co";
const SUPABASE_ANON_KEY = "TUA-CHAVE-ANON";
const configured =
  !SUPABASE_URL.includes("TEU-PROJETO") &&
  !SUPABASE_ANON_KEY.includes("TUA-CHAVE");

const db = configured
  ? window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY)
  : null;

let currentUser = null;

function showPage(page){
  document.querySelectorAll("main section").forEach(s=>s.classList.add("hidden"));
  document.getElementById(page)?.classList.remove("hidden");
}

function message(id,text){
  document.getElementById(id).textContent=text;
}

async function register(){
  if(!db)return message("authMessage","Configura primeiro o Supabase.");
  const email=document.getElementById("email").value.trim();
  const password=document.getElementById("password").value;
  if(!email || password.length<8)
    return message("authMessage","Introduz um email e uma palavra-passe com pelo menos 8 caracteres.");
  const {error}=await db.auth.signUp({email,password});
  message("authMessage",error?error.message:"Registo iniciado. Confirma o email, se solicitado.");
}

async function login(){
  if(!db)return message("authMessage","Configura primeiro o Supabase.");
  const email=document.getElementById("email").value.trim();
  const password=document.getElementById("password").value;
  const {data,error}=await db.auth.signInWithPassword({email,password});
  if(error)return message("authMessage",error.message);
  currentUser=data.user;
  message("authMessage","Sessão iniciada.");
  await routeUser();
}

async function routeUser(){
  if(!db || !currentUser)return;
  const {data}=await db.from("profiles").select("role").eq("id",currentUser.id).maybeSingle();
  if(data?.role==="admin")showPage("admin");
  else showPage("student");
}

async function createPlatform(){
  if(!db)return message("platformMessage","Configura o Supabase.");
  const name=document.getElementById("platformName").value.trim();
  const description=document.getElementById("platformDescription").value.trim();
  if(!name)return message("platformMessage","Indica o nome.");
  const {error}=await db.from("applications").insert({
    name,description
  });
  message("platformMessage",error?error.message:"Pedido de registo enviado.");
  loadPlatforms();
}

async function loadPlatforms(){
  if(!db)return;
  const {data,error}=await db.from("applications").select("name,description").order("name");
  if(error)return message("platformList","Não foi possível carregar.");
  document.getElementById("platformList").innerHTML="";
  data.forEach(item=>{
    const div=document.createElement("div");
    div.className="card";
    const h=document.createElement("strong");
    h.textContent=item.name;
    const p=document.createElement("p");
    p.textContent=item.description||"";
    div.append(h,p);
    document.getElementById("platformList").append(div);
  });
}

const questions=[
 "Como te sentes hoje?",
 "Conseguiste descansar?",
 "Tiveste alguém com quem conversar?",
 "Sentiste-te apoiado na escola?",
 "O que gostarias que melhorasse amanhã?"
];
let questionIndex=0;

async function saveWellbeing(){
  const answer=document.getElementById("wellAnswer").value;
  if(!answer)return message("wellMessage","Escolhe uma resposta.");
  if(!db || !currentUser)return message("wellMessage","Inicia sessão e configura o Supabase para guardar a resposta.");
  const {error}=await db.from("wellbeing_answers").insert({
    student_id:currentUser.id,
    question_text:questions[questionIndex],
    answer_value:Number(answer)
  });
  if(error)return message("wellMessage",error.message);
  questionIndex++;
  if(questionIndex>=questions.length){
    message("wellMessage","Check-in concluído. Obrigado por responderes.");
    return;
  }
  document.getElementById("wellQuestion").textContent=questions[questionIndex];
  document.getElementById("wellAnswer").value="";
  message("wellMessage","Resposta guardada.");
}

function loadProgress(){
  message("progress","O progresso será apresentado quando a tabela learning_progress estiver configurada.");
}

const quiz=[
 {q:"Quanto é 12 × 8?",options:["86","96","108"],answer:"96"},
 {q:"Quanto é √144?",options:["10","12","14"],answer:"12"},
 {q:"Quanto é 25% de 200?",options:["25","40","50"],answer:"50"}
];
let quizIndex=0;
let points=0;

function renderQuiz(){
  const item=quiz[quizIndex];
  document.getElementById("quizQuestion").textContent=item.q;
  const area=document.getElementById("quizOptions");
  area.innerHTML="";
  item.options.forEach(option=>{
    const btn=document.createElement("button");
    btn.className="secondary";
    btn.textContent=option;
    btn.onclick=()=>answerQuiz(option);
    area.append(btn);
  });
}

function answerQuiz(answer){
  if(answer===quiz[quizIndex].answer){
    points+=10;
    message("quizResult","Correcto. +10 pontos.");
  }else message("quizResult","Não foi desta. Continua a aprender.");
  quizIndex=(quizIndex+1)%quiz.length;
  setTimeout(renderQuiz,900);
}

renderQuiz();

if(db){
  db.auth.onAuthStateChange((_event,session)=>{
    currentUser=session?.user||null;
  });
  document.getElementById("notice").textContent=
    "Supabase ligado. As permissões e tabelas ainda precisam de configuração.";
}
</script>
</body>
</html>
