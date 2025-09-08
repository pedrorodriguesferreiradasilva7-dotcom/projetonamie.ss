
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jornada Interativa 💖</title>
<style>
  body{margin:0;font-family:sans-serif;overflow-y:auto;background:linear-gradient(180deg,#0f172a,#071133);color:white;-webkit-tap-highlight-color:transparent;}
  .heart{position:fixed;top:-30px;color:#ef476f;font-size:20px;animation:fall linear forwards;user-select:none;pointer-events:none;}
  @keyframes fall{to{transform:translateY(110vh) rotate(360deg);opacity:0}}
  section, .card{position:relative;display:flex;flex-direction:column;align-items:center;justify-content:center;}
  h1{text-align:center;margin-bottom:20px;font-size:1.8rem;}
  .hidden{display:none;}
  button{padding:12px 24px;border:none;border-radius:12px;font-weight:700;cursor:pointer;margin:5px;}
  .secondary{background:#eef2ff;color:#6b21a8;border:1px solid rgba(107,33,168,0.2);}
  .final{background:#ffeff5;color:#333;padding:40px;border-radius:20px;text-align:center;font-size:1.2rem;}
  /* Slider */
  .rail{position:relative;width:80%;max-width:300px;height:60px;border-radius:40px;background:rgba(255,255,255,0.1);display:flex;align-items:center;overflow:hidden;margin-top:50px;}
  .thumb{width:52px;height:52px;border-radius:50%;background:#fff;color:#000;display:flex;align-items:center;justify-content:center;cursor:grab;position:relative;z-index:2;touch-action:none;}
  .progress{position:absolute;top:0;left:0;bottom:0;background:#ff4d85;width:0;border-radius:40px;z-index:1;}
  /* Memória */
  .grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;width:90%;max-width:360px;margin-bottom:20px;}
  .memCard{padding-top:100%;position:relative;background:#fff;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:2rem;cursor:pointer;box-shadow:0 2px 6px rgba(0,0,0,0.2);}
  .memCard span{position:absolute;top:0;left:0;right:0;bottom:0;display:flex;align-items:center;justify-content:center;}
  .matched{background:#ffb3c6;cursor:default;}
  /* Labirinto */
  canvas{background:#fff;border:2px solid #333;margin-top:20px;touch-action:none;}
  .controls{display:flex;flex-direction:column;align-items:center;margin-top:10px;}
  .controls div{display:flex;gap:10px;}
  .controls button{padding:10px 15px;font-size:1.2rem;border-radius:8px;border:none;background:#ff4d85;color:white;cursor:pointer;}
  /* Botões antes do pedido */
  .buttonRoom{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin:20px 0;}
  .buttonRoom button{background:#ff4d85;color:white;}
  /* Pedido namoro */
  .pedido{display:flex;flex-direction:column;align-items:center;justify-content:center;margin-top:20px;}
  .pedidoButtons{display:flex;gap:20px;margin-top:20px;}
</style>
</head>
<body>

<!-- Cadeado -->
<div class="card" id="cadeado" style="background: rgba(255,255,255,0.1); padding: 40px; border-radius: 25px; max-width: 350px; margin: 60px auto; text-align:center; box-shadow:0 12px 25px rgba(0,0,0,0.4);">
  <h1 style="font-size:2.2rem; color:#ff4d85; text-shadow:1px 1px 6px #ffb3c6; margin-bottom:30px;">🔒 Digite a senha</h1>Qual  foi dia da sua festa?

  
  <div class="pins" style="display:flex; justify-content:center; gap:15px; margin-bottom:25px;">
    <input id="d0" maxlength="1" inputmode="numeric" style="width:65px; height:65px; font-size:2.2rem; text-align:center; border-radius:15px; border:2px solid #ff4d85; background: rgba(255,255,255,0.15); color:white; transition:0.25s;">
    <input id="d1" maxlength="1" inputmode="numeric" style="width:65px; height:65px; font-size:2.2rem; text-align:center; border-radius:15px; border:2px solid #ff4d85; background: rgba(255,255,255,0.15); color:white; transition:0.25s;">
    <input id="d2" maxlength="1" inputmode="numeric" style="width:65px; height:65px; font-size:2.2rem; text-align:center; border-radius:15px; border:2px solid #ff4d85; background: rgba(255,255,255,0.15); color:white; transition:0.25s;">
    <input id="d3" maxlength="1" inputmode="numeric" style="width:65px; height:65px; font-size:2.2rem; text-align:center; border-radius:15px; border:2px solid #ff4d85; background: rgba(255,255,255,0.15); color:white; transition:0.25s;">
  </div>

  <div style="display:flex; justify-content:center; gap:15px; margin-bottom:20px;">
    <button id="check" style="padding:15px 32px; font-size:1.1rem; border-radius:14px; font-weight:800; background:#ff4d85; color:white; cursor:pointer;">Entrar</button>
    <button id="clear" style="padding:15px 32px; font-size:1.1rem; border-radius:14px; font-weight:800; background:#eee; color:#6b21a8; cursor:pointer;">Limpar</button>
  </div>

  <div class="msg" id="msg" style="margin-top:18px; font-weight:800; color:#ff4d85; display:inline-block;"></div>
</div>



<!-- Quiz -->
<section id="quizCard" class="hidden">
  <h1 id="quizQuestion"></h1>
  <div>
    <button id="yesBtn">Sim</button>
    <button id="noBtn">Não</button>
  </div>
</section>

<!-- Slider Inicial -->
<section id="inicio" class="hidden">
  <h1>Arraste a bolinha para continuar 💖</h1>
  <div class="rail" id="rail">
    <div class="progress" id="progress"></div>
    <div class="thumb" id="thumb">→</div>
  </div>
</section>

<!-- Memória -->
<section id="memoria" class="hidden">
  <h1>Encontre os pares 💖</h1>
  <div class="grid" id="grid"></div>
</section>

<!-- Labirinto -->
<section id="labirinto" class="hidden">
  <h1>Encontre o coração no labirinto 💘</h1>
  <canvas id="game" width="400" height="400"></canvas>
  <div class="controls">
    <div><button id="upBtn">⬆</button></div>
    <div>
      <button id="leftBtn">⬅</button>
      <button id="downBtn">⬇</button>
      <button id="rightBtn">➡</button>
    </div>
  </div>
</section>

<!-- Sala de botões -->
<section id="salaBotoes" class="hidden">
  <h1>Escolha o botão certo para continuar 💖</h1>
  <div class="buttonRoom">
    <button>1</button><button>2</button><button>3</button>
    <button id="nextToPedido">4</button><button>5</button><button>6</button>
  </div>
</section>

<!-- Pedido namoro -->
<section id="pedido" class="hidden">
  <h1>Quer namorar comigo? 💖</h1>
  <div class="pedido">
    <div class="pedidoButtons">
      <button id="pedidoYes">Sim</button>
      <button id="pedidoNo">Não</button>
    </div>
  </div>
</section>

<!-- Não aceito não -->
<section id="naoAceito" class="hidden">
  <h1>Não aceito não como resposta rs.. 💖</h1>
  <div class="pedido">
    <div class="pedidoButtons">
      <button id="naoAceitoYes">Sim</button>
    </div>
  </div>
</section>

<!-- Final -->
<section id="final" class="hidden">
  <div class="final">
    <h1>Parabéns! 💖</h1>
    <p>Você completou todos os jogos e chegou ao coração final!</p>
  </div>
</section>

<script>
// ===== Corações caindo =====
function createHeart(){
  const h=document.createElement('div');
  h.className='heart';h.textContent='❤';
  h.style.left=Math.random()*100+'vw';
  h.style.fontSize=(14+Math.random()*26)+'px';
  h.style.animationDuration=(3+Math.random()*4)+'s';
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(createHeart,450);

// ===== Cadeado =====
const inputs = [0,1,2,3].map(i=>document.getElementById('d'+i));
const msg = document.getElementById('msg');
const checkBtn = document.getElementById('check');
const clearBtn = document.getElementById('clear');
const quizCard = document.getElementById('quizCard');
const inicio = document.getElementById('inicio');
inputs[0].focus();

// ===== Funções do quiz =====
const questions = [
  "Você é lésbica? 🌈",
  "Você é guy? 👦",
  "Você é racista? ✊🏽",
  "Você é uma Geladeira Samsung French Door Family Hub RF27? 🧊"
];
let currentQuestion = 0;
const quizQuestion = document.getElementById('quizQuestion');
const yesBtn = document.getElementById('yesBtn');
const noBtn = document.getElementById('noBtn');

function showQuestion() { quizQuestion.textContent = questions[currentQuestion]; }

function nextQuestion(answer){
  if(currentQuestion === questions.length-1 && answer==='yes'){
    quizCard.classList.add('hidden');
    inicio.classList.remove('hidden');
    return;
  }
  currentQuestion++;
  if(currentQuestion<questions.length){ showQuestion(); }
  else{ quizCard.classList.add('hidden'); inicio.classList.remove('hidden'); }
}

// ===== Funções do cadeado =====
function getValue(){ return inputs.map(i=>i.value||'').join(''); }
function attempt(){
  const val = getValue();
  if(val.length<4){ msg.textContent='Preencha os 4 dígitos.'; return; }
  if(val==='2806'){ document.getElementById('cadeado').style.display='none'; quizCard.classList.remove('hidden'); currentQuestion=0; showQuestion(); }
  else if(val==='0006'){ alert("Painel admin (exemplo)"); }
  else{ msg.textContent='Senha incorreta.'; inputs.forEach(i=>i.classList.add('shake')); setTimeout(()=>inputs.forEach(i=>i.classList.remove('shake')),300); inputs[0].focus();}
}
checkBtn.addEventListener('click', attempt);
clearBtn.addEventListener('click', ()=>{inputs.forEach(i=>i.value=''); msg.textContent=''; inputs[0].focus();});
inputs.forEach((inp,idx)=>{
  inp.addEventListener('input', e=>{ e.target.value=e.target.value.replace(/[^0-9]/g,'').slice(-1); if(e.target.value && idx<3) inputs[idx+1].focus(); });
  inp.addEventListener('keydown', e=>{ if(e.key==='Backspace'&&!e.target.value&&idx>0) inputs[idx-1].focus(); if(e.key==='ArrowLeft'&&idx>0) inputs[idx-1].focus(); if(e.key==='ArrowRight'&&idx<3) inputs[idx+1].focus(); if(e.key==='Enter') attempt(); });
});
yesBtn.addEventListener('click',()=>nextQuestion('yes'));
noBtn.addEventListener('click',()=>nextQuestion('no'));

// ===== Slider Inicial =====
const rail=document.getElementById('rail');
const thumb=document.getElementById('thumb');
const progress=document.getElementById('progress');
let dragging=false, startX=0, thumbX=0;
function updateThumb(pos){
  const max=rail.offsetWidth - thumb.offsetWidth;
  const pct=Math.max(0,Math.min(1,pos/max));
  progress.style.width=(pct*100)+'%';
  thumb.style.transform=`translateX(${pct*max}px)`;
  if(pct>0.7){inicio.classList.add('hidden'); startMemoria();}
}
thumb.addEventListener('touchstart',e=>{dragging=true; startX=e.touches[0].clientX; thumbX=parseInt(thumb.style.transform.replace('translateX(','')||0);});
thumb.addEventListener('touchmove',e=>{if(!dragging)return; updateThumb(thumbX+(e.touches[0].clientX-startX));});
thumb.addEventListener('touchend',()=>{dragging=false; if(parseInt(progress.style.width)<70) updateThumb(0);});
thumb.addEventListener('mousedown',e=>{dragging=true; startX=e.clientX; thumbX=parseInt(thumb.style.transform.replace('translateX(','')||0);});
window.addEventListener('mousemove',e=>{if(!dragging)return; updateThumb(thumbX+(e.clientX-startX));});
window.addEventListener('mouseup',()=>{dragging=false; if(parseInt(progress.style.width)<70) updateThumb(0);});

// ===== Memória =====
function startMemoria(){
  const memoria=document.getElementById('memoria');
  memoria.classList.remove('hidden');
  const emojis=['💖','🌟','🍀','🐱','🐶','🎵','⚡','🍎'];
  let cards=[...emojis,...emojis].sort(()=>Math.random()-0.5);
  const grid=document.getElementById('grid'); grid.innerHTML='';
  let first=null,lock=false,matched=0;
  cards.forEach(sym=>{
    const c=document.createElement('div'); c.className='memCard';
    const span=document.createElement('span'); span.textContent=''; c.appendChild(span); c.dataset.sym=sym;
    function flipCard(){
      if(lock||c.classList.contains('matched')||span.textContent) return;
      span.textContent=sym; c.style.background='#ffe4e1';
      if(!first){ first={card:c,span:span}; }
      else{
        if(first.card.dataset.sym===c.dataset.sym){
          first.card.classList.add('matched'); c.classList.add('matched'); matched+=2; first=null;
          if(matched===cards.length){ setTimeout(()=>{memoria.classList.add('hidden'); startLabirinto();},500); }
        }else{
          lock=true;
          setTimeout(()=>{ first.span.textContent=''; first.card.style.background='#fff'; span.textContent=''; c.style.background='#fff'; first=null; lock=false; },600);
        }
      }
    }
    c.addEventListener('click',flipCard); c.addEventListener('touchstart',flipCard);
    grid.appendChild(c);
  });
}

// ===== Labirinto =====
function startLabirinto(){
  const lab=document.getElementById('labirinto'); lab.classList.remove('hidden');
  const canvas=document.getElementById('game'); const ctx=canvas.getContext('2d');
  const size=40, rows=10, cols=10;
  const player={x:0,y:0}, goal={x:9,y:9};
  const maze=[
    [0,1,0,0,0,1,0,0,0,0],[0,1,0,1,0,1,0,1,1,0],[0,0,0,1,0,0,0,1,0,0],
    [1,1,0,0,1,1,0,1,0,1],[0,0,0,1,0,0,0,0,0,0],[0,1,1,1,0,1,1,1,1,0],
    [0,0,0,0,0,0,0,1,0,0],[1,1,0,1,1,1,0,1,1,0],[0,0,0,0,0,0,0,0,0,0],[0,1,1,1,1,1,1,1,1,0]
  ];
  function draw(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    for(let y=0;y<rows;y++){for(let x=0;x<cols;x++){ if(maze[y][x]===1){ctx.fillStyle='#333';ctx.fillRect(x*size,y*size,size,size);}}}
    ctx.fillStyle='blue'; ctx.fillRect(player.x*size,player.y*size,size,size);
    ctx.fillStyle='gold'; ctx.font='30px sans-serif'; ctx.fillText('❤', goal.x*size+8, goal.y*size+28);
  }
  draw();
  function movePlayer(dx,dy){
    let nx=player.x+dx, ny=player.y+dy;
    if(nx>=0&&ny>=0&&nx<cols&&ny<rows&&maze[ny][nx]===0){ player.x=nx; player.y=ny; draw();
      if(player.x===goal.x && player.y===goal.y){ setTimeout(()=>{lab.classList.add('hidden'); document.getElementById('salaBotoes').classList.remove('hidden');},200); }
    }
  }
  window.addEventListener('keydown',e=>{ if(e.key==='ArrowUp') movePlayer(0,-1); if(e.key==='ArrowDown') movePlayer(0,1); if(e.key==='ArrowLeft') movePlayer(-1,0); if(e.key==='ArrowRight') movePlayer(1,0);});
  document.getElementById('upBtn').addEventListener('click',()=>movePlayer(0,-1));
  document.getElementById('downBtn').addEventListener('click',()=>movePlayer(0,1));
  document.getElementById('leftBtn').addEventListener('click',()=>movePlayer(-1,0));
  document.getElementById('rightBtn').addEventListener('click',()=>movePlayer(1,0));
}

// ===== Sala de botões =====
document.querySelectorAll('.buttonRoom button').forEach(btn => {
  btn.addEventListener('click', () => {
    if(btn.id === 'nextToPedido'){ 
      document.getElementById('salaBotoes').classList.add('hidden');
      document.getElementById('pedido').classList.remove('hidden');
    } else {
      // Mensagem de erro para botão errado
      const msg = document.createElement('div');
      msg.textContent = 'Ops, errado!';
      msg.style.color = '#ff4d85';
      msg.style.fontWeight = '700';
      msg.style.marginTop = '10px';
      document.getElementById('salaBotoes').appendChild(msg);
      setTimeout(()=>msg.remove(),1500); // some após 1,5s
    }
  });
});


// ===== Pedido namoro =====
let noCount=0;
const pedidoNo = document.getElementById('pedidoNo');
const pedidoYes = document.getElementById('pedidoYes');
const pedido = document.getElementById('pedido');
const naoAceito = document.getElementById('naoAceito');
const naoAceitoYes = document.getElementById('naoAceitoYes');

pedidoNo.addEventListener('click', ()=>{
  noCount++;
  const msg = document.createElement('div');
  msg.style.color = '#ff4d85';
  msg.style.fontWeight = '700';
  msg.style.marginTop = '10px';
  pedido.appendChild(msg);
  setTimeout(()=>msg.remove(),1500);

  // Faz o botão fugir
  pedidoNo.style.position='absolute';
  pedidoNo.style.left=Math.random()*80+'vw';
  pedidoNo.style.top=(100 + Math.random()*200)+'px';

  if(noCount>=5){
    pedido.classList.add('hidden');
    naoAceito.classList.remove('hidden');
  }
});

pedidoYes.addEventListener('click',()=>{
  pedido.classList.add('hidden');
  document.getElementById('final').classList.remove('hidden');
});

naoAceitoYes.addEventListener('click',()=>{
  naoAceito.classList.add('hidden');
  document.getElementById('final').classList.remove('hidden');
});
</script>
</body>
</html>
