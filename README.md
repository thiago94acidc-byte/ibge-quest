<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <meta name="theme-color" content="#0b1020" />
  <title>IBGE Quest — Jogo de Estudos</title>
  <style>
    :root{
      --bg:#0b1020; --card:#111a33; --card2:#0e1630; --txt:#e8eeff; --mut:#a9b6e6;
      --pri:#5df2b2; --pri2:#7aa8ff; --warn:#ffcc66; --bad:#ff6b6b; --ok:#5df2b2;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
      --r: 18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 800px at 20% -10%, rgba(122,168,255,.18), transparent 50%),
                  radial-gradient(900px 700px at 90% 10%, rgba(93,242,178,.16), transparent 55%),
                  linear-gradient(180deg, #070a14, var(--bg));
      color:var(--txt);
      min-height:100vh;
    }
    header{
      position:sticky; top:0; z-index:5;
      background: linear-gradient(180deg, rgba(7,10,20,.92), rgba(7,10,20,.70));
      backdrop-filter: blur(10px);
      border-bottom:1px solid rgba(255,255,255,.08);
    }
    .wrap{max-width:1100px; margin:0 auto; padding:14px 14px 18px}
    .row{display:flex; gap:12px; align-items:center; flex-wrap:wrap}
    .brand{
      display:flex; gap:10px; align-items:center; font-weight:800; letter-spacing:.2px;
    }
    .logo{
      width:38px; height:38px; border-radius:12px;
      background: linear-gradient(135deg, rgba(93,242,178,.95), rgba(122,168,255,.95));
      box-shadow: var(--shadow);
    }
    .pill{
      padding:7px 10px; border-radius:999px;
      background: rgba(255,255,255,.08);
      border:1px solid rgba(255,255,255,.10);
      color:var(--mut); font-size:13px;
      display:flex; gap:8px; align-items:center;
    }
    .btn{
      appearance:none; border:none; cursor:pointer;
      padding:10px 12px; border-radius:12px;
      color:var(--txt); background: rgba(255,255,255,.10);
      border:1px solid rgba(255,255,255,.14);
      transition:.15s transform, .15s filter, .15s background;
      display:inline-flex; gap:8px; align-items:center;
      user-select:none;
    }
    .btn:hover{filter:brightness(1.05)}
    .btn:active{transform:scale(.99)}
    .btn.primary{background: linear-gradient(135deg, rgba(93,242,178,.95), rgba(122,168,255,.95)); color:#06101c; border:none; font-weight:700}
    .btn.warn{background: rgba(255,204,102,.16); border-color: rgba(255,204,102,.28); color:#ffe3a6}
    .btn.bad{background: rgba(255,107,107,.14); border-color: rgba(255,107,107,.28); color:#ffc6c6}
    main{padding:16px 0 80px}
    .grid{display:grid; gap:14px}
    @media(min-width:860px){ .grid.cols2{grid-template-columns: 1.2fr .8fr} }
    .card{
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border:1px solid rgba(255,255,255,.10);
      border-radius: var(--r);
      box-shadow: var(--shadow);
      padding:14px;
    }
    .card h2{margin:0 0 10px; font-size:18px}
    .sub{color:var(--mut); font-size:13px; margin-top:2px}
    .kpi{display:flex; gap:10px; flex-wrap:wrap}
    .kpi .box{flex:1; min-width:160px; padding:10px 12px; border-radius:14px; background: rgba(0,0,0,.20); border:1px solid rgba(255,255,255,.08)}
    .kpi b{font-size:18px}
    .bar{height:10px; background: rgba(255,255,255,.10); border-radius:999px; overflow:hidden; border:1px solid rgba(255,255,255,.10)}
    .bar > i{display:block; height:100%; width:0%; background: linear-gradient(90deg, rgba(93,242,178,.95), rgba(122,168,255,.95))}
    .tabs{display:flex; gap:10px; flex-wrap:wrap}
    .tab{padding:10px 12px; border-radius:14px; border:1px solid rgba(255,255,255,.12); background: rgba(255,255,255,.06); color:var(--mut); cursor:pointer}
    .tab.active{color:#06101c; background: linear-gradient(135deg, rgba(93,242,178,.95), rgba(122,168,255,.95)); border:none; font-weight:800}
    .list{display:flex; flex-direction:column; gap:10px}
    .item{
      padding:12px; border-radius:16px;
      background: rgba(0,0,0,.22);
      border:1px solid rgba(255,255,255,.10);
      display:grid; gap:10px;
    }
    .item-head{display:flex; justify-content:space-between; gap:10px; align-items:flex-start}
    .tag{font-size:12px; color:#06101c; background: rgba(93,242,178,.95); padding:5px 8px; border-radius:999px; font-weight:800}
    .tag.blue{background: rgba(122,168,255,.95)}
    .tag.gray{background: rgba(255,255,255,.12); color:var(--mut); border:1px solid rgba(255,255,255,.10)}
    .small{font-size:13px; color:var(--mut)}
    .actions{display:flex; gap:10px; flex-wrap:wrap}
    .qbox{
      padding:12px; border-radius:16px;
      background: rgba(14,22,48,.75);
      border:1px solid rgba(255,255,255,.10);
    }
    .qbox h3{margin:0 0 8px; font-size:16px}
    .opt{display:block; padding:10px; border-radius:12px; margin:8px 0; background: rgba(255,255,255,.06); border:1px solid rgba(255,255,255,.10); cursor:pointer}
    .opt:hover{filter:brightness(1.05)}
    .opt.correct{border-color: rgba(93,242,178,.65); background: rgba(93,242,178,.10)}
    .opt.wrong{border-color: rgba(255,107,107,.65); background: rgba(255,107,107,.10)}
    .modal{
      position:fixed; inset:0; background: rgba(0,0,0,.55);
      display:none; align-items:flex-end; justify-content:center; padding:14px;
      z-index:50;
    }
    .modal.on{display:flex}
    .sheet{
      width:min(980px, 100%); max-height: 88vh; overflow:auto;
      border-radius: 18px;
      background: linear-gradient(180deg, rgba(17,26,51,.96), rgba(14,22,48,.96));
      border:1px solid rgba(255,255,255,.14);
      box-shadow: var(--shadow);
      padding:14px;
    }
    .sheet header{position:sticky; top:0; background: transparent; border:0; backdrop-filter:none}
    textarea, input, select{
      width:100%; padding:10px 12px; border-radius:12px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(0,0,0,.25); color:var(--txt);
      outline:none;
    }
    textarea{min-height:120px; resize:vertical}
    .hint{font-size:12px; color:var(--mut); margin-top:6px}
    footer{
      position:fixed; left:0; right:0; bottom:0; z-index:6;
      background: linear-gradient(180deg, rgba(7,10,20,.0), rgba(7,10,20,.88));
      border-top: 1px solid rgba(255,255,255,.08);
      padding:10px 14px;
    }
    footer .wrap{padding:0}
    .nav{display:flex; gap:10px; flex-wrap:wrap}
    .nav .btn{flex:1; justify-content:center; min-width:160px}
    .mono{font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace}
  </style>
</head>

<body>
<header>
  <div class="wrap">
    <div class="row" style="justify-content:space-between">
      <div class="brand">
        <div class="logo"></div>
        <div>
          <div style="font-size:16px">IBGE Quest</div>
          <div class="sub">Jogo de estudos (site + app instalável)</div>
        </div>
      </div>
      <div class="row">
        <div class="pill" title="Progresso geral">
          <span>🎯</span><span id="hdrProgress">0%</span>
        </div>
        <div class="pill" title="Sequência de dias estudando">
          <span>🔥</span><span id="hdrStreak">0</span><span class="small">dias</span>
        </div>
        <button class="btn" id="btnBackup">⬇️ Backup</button>
        <button class="btn" id="btnRestore">⬆️ Restaurar</button>
        <button class="btn primary" id="btnImport">➕ Importar conteúdo</button>
      </div>
    </div>
  </div>
</header>

<main>
  <div class="wrap grid cols2">
    <section class="card">
      <h2>Seu painel</h2>
      <div class="kpi">
        <div class="box">
          <div class="small">Nível</div>
          <b id="kpiLevel">1</b>
          <div class="small">XP: <span id="kpiXP">0</span></div>
        </div>
        <div class="box">
          <div class="small">Missões feitas</div>
          <b id="kpiMissions">0</b>
          <div class="small">Acertos: <span id="kpiAccuracy">0%</span></div>
        </div>
        <div class="box">
          <div class="small">Tempo estudado</div>
          <b id="kpiTime">0 min</b>
          <div class="small">Hoje: <span id="kpiToday">0 min</span></div>
        </div>
      </div>

      <div style="margin:12px 0 8px" class="small">Progresso geral</div>
      <div class="bar"><i id="barOverall"></i></div>
      <div class="row" style="margin-top:10px; justify-content:space-between">
        <div class="small">Meta até 01/03: <span class="mono" id="goalText">50%+</span></div>
        <button class="btn warn" id="btnFocus">⚡ Plano rápido (até 01/03)</button>
      </div>

      <div style="margin-top:14px" class="tabs">
        <div class="tab active" data-tab="fases">🗺️ Fases</div>
        <div class="tab" data-tab="prova">🧪 Modo Prova</div>
        <div class="tab" data-tab="ranking">🏆 Ranking</div>
        <div class="tab" data-tab="config">⚙️ Config</div>
      </div>

      <div id="tab-fases" style="margin-top:12px">
        <div class="small">Complete fases para avançar. Cada fase tem: <b>Resumo</b> → <b>Áudio</b> → <b>Questões</b>.</div>
        <div class="list" id="phaseList" style="margin-top:10px"></div>
      </div>

      <div id="tab-prova" style="display:none; margin-top:12px">
        <div class="row" style="justify-content:space-between; align-items:flex-end">
          <div>
            <div style="font-weight:800">Simulado rápido</div>
            <div class="small">Gera uma prova aleatória com questões das fases.</div>
          </div>
          <button class="btn primary" id="btnStartExam">▶️ Começar</button>
        </div>
        <div class="row" style="margin-top:10px">
          <div style="flex:1">
            <div class="small">Quantidade</div>
            <select id="examCount">
              <option>10</option><option>15</option><option>20</option><option>30</option>
            </select>
          </div>
          <div style="flex:2">
            <div class="small">Filtrar por matéria</div>
            <select id="examSubject"></select>
          </div>
        </div>
        <div id="examArea" style="margin-top:12px"></div>
      </div>

      <div id="tab-ranking" style="display:none; margin-top:12px">
        <div class="small">Seu “ranking” é você contra você. Foque em: sequência + acertos + consistência.</div>
        <div class="item" style="margin-top:10px">
          <div class="item-head">
            <div>
              <div style="font-weight:900">🏅 Medalhas</div>
              <div class="small">Desbloqueie jogando.</div>
            </div>
            <span class="tag blue" id="medalCount">0</span>
          </div>
          <div id="medals" class="small"></div>
        </div>
      </div>

      <div id="tab-config" style="display:none; margin-top:12px">
        <div class="item">
          <div class="item-head">
            <div>
              <div style="font-weight:900">📌 Meta e rotina</div>
              <div class="small">Ajuste a meta e o tempo diário.</div>
            </div>
          </div>
          <div class="row">
            <div style="flex:1">
              <div class="small">Meta (%)</div>
              <input id="cfgGoal" type="number" min="1" max="100" value="50" />
            </div>
            <div style="flex:1">
              <div class="small">Min/dia</div>
              <input id="cfgMinDay" type="number" min="5" max="300" value="45" />
            </div>
          </div>
          <div class="row" style="justify-content:flex-end; margin-top:10px">
            <button class="btn primary" id="btnSaveCfg">💾 Salvar</button>
          </div>
        </div>

        <div class="item">
          <div class="item-head">
            <div>
              <div style="font-weight:900">🗑️ Reset</div>
              <div class="small">Zera tudo (só se você quiser recomeçar).</div>
            </div>
          </div>
          <button class="btn bad" id="btnReset">Apagar progresso</button>
        </div>

        <div class="hint">
          ✅ Dica: instale como app: no Chrome do Android → “Adicionar à tela inicial”.
        </div>
      </div>

    </section>

    <aside class="card">
      <h2>Jogar agora</h2>
      <div class="small">Escolha uma missão rápida para hoje (ganha XP e aumenta a % do edital).</div>

      <div class="list" style="margin-top:10px">
        <div class="item">
          <div class="item-head">
            <div>
              <div style="font-weight:900">🎧 Missão 1 — Ouvir + resumir</div>
              <div class="small">Ouça o resumo de uma fase e marque como “entendi”.</div>
            </div>
            <span class="tag">+20 XP</span>
          </div>
          <div class="actions">
            <button class="btn primary" id="btnQuickAudio">Ouvir uma fase</button>
            <button class="btn" id="btnMarkUnderstood">Marcar “entendi”</button>
          </div>
        </div>

        <div class="item">
          <div class="item-head">
            <div>
              <div style="font-weight:900">🧩 Missão 2 — 5 questões</div>
              <div class="small">Um quiz rápido de 5 questões aleatórias.</div>
            </div>
            <span class="tag blue">+35 XP</span>
          </div>
          <button class="btn primary" id="btnQuickQuiz">Começar quiz</button>
        </div>

        <div class="item">
          <div class="item-head">
            <div>
              <div style="font-weight:900">⏱️ Cronômetro de estudo</div>
              <div class="small">Foco 25 min (pomodoro). Ao terminar: XP extra.</div>
            </div>
            <span class="tag gray" id="timerLabel">25:00</span>
          </div>
          <div class="actions">
            <button class="btn primary" id="btnTimer">▶️ Iniciar</button>
            <button class="btn" id="btnTimerReset">↩️ Reset</button>
          </div>
        </div>
      </div>

      <div style="margin-top:12px" class="qbox" id="quizBox" hidden>
        <h3 id="qTitle">Questão</h3>
        <div class="small" id="qMeta"></div>
        <div style="margin-top:10px" id="qText"></div>
        <div id="qOpts" style="margin-top:10px"></div>
        <div class="row" style="justify-content:space-between; margin-top:10px">
          <button class="btn" id="btnSpeakQ">🔊 Ler</button>
          <button class="btn primary" id="btnNextQ">Próxima ➜</button>
        </div>
        <div class="small" id="qFeedback" style="margin-top:8px"></div>
      </div>

      <div class="hint" style="margin-top:12px">
        Áudio é por voz do celular (TTS). Se não falar, ative “Texto para fala” no Android:
        Configurações → Acessibilidade → Texto para fala.
      </div>
    </aside>
  </div>
</main>

<footer>
  <div class="wrap">
    <div class="nav">
      <button class="btn" id="navHome">🏠 Painel</button>
      <button class="btn" id="navStudy">🗺️ Fases</button>
      <button class="btn" id="navExam">🧪 Prova</button>
      <button class="btn" id="navInstall">📲 Instalar</button>
    </div>
  </div>
</footer>

<!-- Modal Import -->
<div class="modal" id="modalImport">
  <div class="sheet">
    <div class="row" style="justify-content:space-between">
      <div>
        <div style="font-weight:900; font-size:16px">➕ Importar conteúdo (modo simples)</div>
        <div class="small">Cole um resumo + questões. Isso vira uma “fase” no jogo.</div>
      </div>
      <button class="btn" id="btnCloseImport">✖️ Fechar</button>
    </div>

    <div style="margin-top:12px" class="item">
      <div class="small">Nome da fase</div>
      <input id="impTitle" placeholder="Ex: Português — Interpretação de Texto" />
      <div class="row" style="margin-top:10px">
        <div style="flex:1">
          <div class="small">Matéria</div>
          <input id="impSubject" placeholder="Ex: Língua Portuguesa" />
        </div>
        <div style="flex:1">
          <div class="small">Peso (%) no edital</div>
          <input id="impWeight" type="number" min="1" max="40" value="5" />
        </div>
      </div>
      <div class="small" style="margin-top:10px">Resumo (curto e direto)</div>
      <textarea id="impSummary" placeholder="Escreva um resumo simples, em tópicos. Ex: ideia principal, dicas, pegadinhas."></textarea>

      <div class="small" style="margin-top:10px">Questões (1 por bloco)</div>
      <textarea id="impQuestions" class="mono" placeholder="Formato:
PERGUNTA: ...
A) ...
B) ...
C) ...
D) ...
E) ...
GABARITO: C
EXPLICAÇÃO: ..."></textarea>

      <div class="row" style="justify-content:flex-end; margin-top:10px">
        <button class="btn primary" id="btnAddPhase">Adicionar fase</button>
      </div>

      <div class="hint">
        Você pode importar aos poucos. O jogo já calcula sua % geral com base no “Peso (%)”.
      </div>
    </div>
  </div>
</div>

<script>
/** =========================
 *  IBGE Quest — Jogo de estudos (PWA-ready)
 *  Tudo em 1 arquivo (index.html) para você só colar e usar.
 *  ========================= */

const LS_KEY = "ibgequest_state_v1";

const DEFAULT_STATE = {
  cfg: { goal: 50, minDay: 45 },
  xp: 0,
  level: 1,
  missionsDone: 0,
  correct: 0,
  answered: 0,
  understood: {},       // phaseId -> true
  progress: {},         // phaseId -> 0..100
  time: { totalMin: 0, todayMin: 0, lastDay: null },
  streak: { days: 0, lastStudyDay: null },
  phases: [
    // Fases iniciais (modelo). Você pode apagar e importar suas fases.
    {
      id: uid(),
      subject: "Língua Portuguesa",
      title: "Interpretação de Texto (modelo)",
      weight: 8,
      summary:
`• Encontre a ideia principal (tese).
• Cuidado com “palavras absolutas” (sempre, nunca).
• Inferência: conclusão baseada no texto, sem inventar.`,
      questions: [
        q("No texto, a ideia principal é:", ["Um detalhe do exemplo", "O tema central defendido", "Uma opinião do leitor", "Um fato isolado", "Uma regra gramatical"], 1,
          "Ideia principal = mensagem central do autor.")
      ]
    },
    {
      id: uid(),
      subject: "Raciocínio Lógico",
      title: "Conjuntos (modelo)",
      weight: 8,
      summary:
`• União (A ∪ B): tudo que está em A ou B.
• Interseção (A ∩ B): só o que está nos dois.
• Complementar: o que está fora do conjunto.`,
      questions: [
        q("Se A={1,2,3} e B={3,4}, então A ∩ B é:", ["{1,2}", "{3}", "{4}", "{1,4}", "{1,2,3,4}"], 1,
          "Interseção = elementos comuns aos dois conjuntos.")
      ]
    },
    {
      id: uid(),
      subject: "Conhecimentos Específicos",
      title: "Rotina de coleta (modelo)",
      weight: 10,
      summary:
`• Siga instruções do supervisor.
• Registre dados com fidelidade.
• Respeito + postura profissional em campo.`,
      questions: [
        q("Em coleta de dados, o mais correto é:", ["Inventar dado para bater meta", "Registrar conforme orientação e realidade", "Alterar respostas para “padronizar”", "Pular domicílios sem motivo", "Registrar sem checar"], 1,
          "O princípio é fidelidade + norma técnica.")
      ]
    },
  ],
  medals: {}
};

function q(text, options, answerIndex, explain){
  return { id: uid(), text, options, answerIndex, explain };
}
function uid(){ return Math.random().toString(16).slice(2) + Date.now().toString(16); }

function loadState(){
  try{
    const raw = localStorage.getItem(LS_KEY);
    if(!raw) return structuredClone(DEFAULT_STATE);
    const s = JSON.parse(raw);
    // Merge leve
    return { ...structuredClone(DEFAULT_STATE), ...s, cfg: { ...DEFAULT_STATE.cfg, ...(s.cfg||{}) } };
  }catch(e){
    return structuredClone(DEFAULT_STATE);
  }
}
function saveState(){ localStorage.setItem(LS_KEY, JSON.stringify(state)); renderAll(); }

let state = loadState();

/** ======= UI refs ======= */
const $ = sel => document.querySelector(sel);
const $$ = sel => Array.from(document.querySelectorAll(sel));

const hdrProgress = $("#hdrProgress");
const hdrStreak = $("#hdrStreak");

const kpiLevel = $("#kpiLevel");
const kpiXP = $("#kpiXP");
const kpiMissions = $("#kpiMissions");
const kpiAccuracy = $("#kpiAccuracy");
const kpiTime = $("#kpiTime");
const kpiToday = $("#kpiToday");
const barOverall = $("#barOverall");
const goalText = $("#goalText");

const phaseList = $("#phaseList");
const quizBox = $("#quizBox");
const qTitle = $("#qTitle");
const qMeta = $("#qMeta");
const qText = $("#qText");
const qOpts = $("#qOpts");
const qFeedback = $("#qFeedback");
const btnNextQ = $("#btnNextQ");

const examArea = $("#examArea");
const examCount = $("#examCount");
const examSubject = $("#examSubject");

/** ======= Tabs ======= */
$$(".tab").forEach(t => t.addEventListener("click", () => setTab(t.dataset.tab)));
function setTab(name){
  $$(".tab").forEach(t => t.classList.toggle("active", t.dataset.tab===name));
  $("#tab-fases").style.display = name==="fases" ? "" : "none";
  $("#tab-prova").style.display = name==="prova" ? "" : "none";
  $("#tab-ranking").style.display = name==="ranking" ? "" : "none";
  $("#tab-config").style.display = name==="config" ? "" : "none";
}

/** ======= Helpers ======= */
function clamp(n,min,max){ return Math.max(min, Math.min(max, n)); }

function calcOverallProgress(){
  const totalWeight = state.phases.reduce((a,p)=>a+(Number(p.weight)||0),0) || 1;
  let done = 0;
  for(const p of state.phases){
    const pr = Number(state.progress[p.id] ?? 0);
    done += (Number(p.weight)||0) * (pr/100);
  }
  return Math.round((done/totalWeight)*100);
}

function levelFromXP(xp){
  // curva simples: lvl sobe a cada 120 xp no começo, e vai aumentando levemente
  let lvl=1, need=120;
  let rest=xp;
  while(rest>=need){
    rest-=need; lvl++;
    need = Math.round(120 + (lvl-1)*18);
  }
  return { lvl, nextNeed: need, into: rest };
}

function awardXP(amount){
  state.xp += amount;
  const before = state.level;
  const { lvl } = levelFromXP(state.xp);
  state.level = lvl;
  if(lvl>before) medalCheck();
}

function todayKey(){
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,"0")}-${String(d.getDate()).padStart(2,"0")}`;
}

function markStudyMinutes(min){
  const tk = todayKey();
  if(state.time.lastDay !== tk){
    state.time.lastDay = tk;
    state.time.todayMin = 0;
  }
  state.time.totalMin += min;
  state.time.todayMin += min;

  // streak
  if(state.streak.lastStudyDay === tk) return;

  // se estudou ontem e hoje, mantém sequência
  const last = state.streak.lastStudyDay;
  state.streak.lastStudyDay = tk;

  if(!last){
    state.streak.days = 1;
    return;
  }
  const lastDate = new Date(last+"T00:00:00");
  const nowDate = new Date(tk+"T00:00:00");
  const diffDays = Math.round((nowDate-lastDate)/(1000*60*60*24));

  if(diffDays === 1) state.streak.days += 1;
  else state.streak.days = 1;
}

function speak(text){
  try{
    if(!("speechSynthesis" in window)) return alert("Seu navegador não suporta áudio TTS.");
    window.speechSynthesis.cancel();
    const u = new SpeechSynthesisUtterance(text);
    u.lang = "pt-BR";
    u.rate = 1.02;
    u.pitch = 1.0;
    window.speechSynthesis.speak(u);
  }catch(e){
    alert("Não consegui tocar o áudio aqui. Veja se TTS está ativo no Android.");
  }
}

/** ======= Render ======= */
function renderAll(){
  // KPI
  const overall = calcOverallProgress();
  hdrProgress.textContent = overall + "%";
  hdrStreak.textContent = state.streak.days;

  kpiLevel.textContent = state.level;
  kpiXP.textContent = state.xp;
  kpiMissions.textContent = state.missionsDone;
  const acc = state.answered ? Math.round((state.correct/state.answered)*100) : 0;
  kpiAccuracy.textContent = acc + "%";

  kpiTime.textContent = `${state.time.totalMin} min`;
  kpiToday.textContent = `${state.time.todayMin} min`;
  barOverall.style.width = overall + "%";
  goalText.textContent = `${state.cfg.goal}%+`;

  // phases list
  phaseList.innerHTML = "";
  state.phases.forEach((p, idx) => {
    const pr = Number(state.progress[p.id] ?? 0);
    const understood = !!state.understood[p.id];
    const box = document.createElement("div");
    box.className = "item";

    box.innerHTML = `
      <div class="item-head">
        <div>
          <div style="font-weight:900">${idx+1}. ${escapeHtml(p.title)}</div>
          <div class="small">${escapeHtml(p.subject)} • Peso: <b>${p.weight}%</b></div>
        </div>
        <span class="tag ${pr>=100?'':'blue'}">${pr}%</span>
      </div>
      <div class="bar"><i style="width:${pr}%"></i></div>
      <div class="small">${escapeHtml(p.summary).replaceAll("\n","<br>")}</div>
      <div class="actions">
        <button class="btn" data-act="audio">🎧 Ouvir</button>
        <button class="btn primary" data-act="quiz">🧩 Questões</button>
        <button class="btn ${understood?'warn':''}" data-act="understood">✅ ${understood?'Entendi (feito)':'Marcar “entendi”'}</button>
        <button class="btn" data-act="plus">➕ +10%</button>
        <button class="btn bad" data-act="minus">➖ -10%</button>
      </div>
    `;

    box.querySelectorAll("button").forEach(b=>{
      b.addEventListener("click", ()=>{
        const act = b.dataset.act;
        if(act==="audio"){
          speak(`${p.title}. Resumo: ${p.summary}`);
          awardXP(10);
          markStudyMinutes(3);
          state.missionsDone += 1;
        }
        if(act==="quiz"){
          startPhaseQuiz(p.id);
        }
        if(act==="understood"){
          state.understood[p.id] = true;
          state.progress[p.id] = Math.max(Number(state.progress[p.id]||0), 50); // entender = pelo menos 50%
          awardXP(20);
          markStudyMinutes(5);
          state.missionsDone += 1;
          medalCheck();
        }
        if(act==="plus"){
          state.progress[p.id] = clamp(Number(state.progress[p.id]||0) + 10, 0, 100);
          awardXP(6);
        }
        if(act==="minus"){
          state.progress[p.id] = clamp(Number(state.progress[p.id]||0) - 10, 0, 100);
        }
        saveState();
      });
    });

    phaseList.appendChild(box);
  });

  // subjects for exam filter
  const subjects = ["Todas", ...Array.from(new Set(state.phases.map(p=>p.subject)))];
  examSubject.innerHTML = subjects.map(s=>`<option>${escapeHtml(s)}</option>`).join("");

  // medals
  renderMedals();
}

function escapeHtml(s){
  return (s??"").toString()
    .replaceAll("&","&amp;").replaceAll("<","&lt;")
    .replaceAll(">","&gt;").replaceAll('"',"&quot;")
    .replaceAll("'","&#039;");
}

/** ======= Quiz engine ======= */
let currentQuiz = null;

function startPhaseQuiz(phaseId){
  const p = state.phases.find(x=>x.id===phaseId);
  if(!p || !p.questions?.length){
    alert("Essa fase ainda não tem questões. Use “Importar conteúdo” para adicionar.");
    return;
  }
  const qs = shuffle([...p.questions]).slice(0, Math.min(5, p.questions.length));
  currentQuiz = { mode:"phase", phaseId, subject:p.subject, title:p.title, qs, i:0, score:0 };
  quizBox.hidden = false;
  renderQ();
}

function startQuickQuiz(){
  const all = state.phases.flatMap(p => (p.questions||[]).map(q=>({q, p})));
  if(all.length<1){ alert("Ainda não há questões suficientes. Importe conteúdo."); return; }
  const pick = shuffle(all).slice(0,5).map(x=>({...x.q, _meta:{subject:x.p.subject, title:x.p.title}}));
  currentQuiz = { mode:"quick", qs: pick, i:0, score:0 };
  quizBox.hidden = false;
  renderQ();
}

function renderQ(){
  const q = currentQuiz.qs[currentQuiz.i];
  const meta = q._meta ? `${q._meta.subject} • ${q._meta.title}` : (currentQuiz.title ? `${currentQuiz.subject} • ${currentQuiz.title}` : "");
  qTitle.textContent = `Questão ${currentQuiz.i+1} de ${currentQuiz.qs.length}`;
  qMeta.textContent = meta;
  qText.textContent = q.text;

  qOpts.innerHTML = "";
  qFeedback.textContent = "";
  btnNextQ.disabled = true;

  q.options.forEach((op, idx)=>{
    const b = document.createElement("div");
    b.className="opt";
    b.textContent = `${String.fromCharCode(65+idx)}) ${op}`;
    b.addEventListener("click", ()=>{
      // lock
      if(b.classList.contains("correct") || b.classList.contains("wrong")) return;

      state.answered += 1;
      const correct = idx===q.answerIndex;
      if(correct){ state.correct += 1; currentQuiz.score += 1; awardXP(18); }
      else awardXP(6);

      // show
      Array.from(qOpts.children).forEach((el, i)=>{
        if(i===q.answerIndex) el.classList.add("correct");
      });
      if(!correct) b.classList.add("wrong");

      qFeedback.innerHTML = correct
        ? `✅ <b>Certo!</b> ${escapeHtml(q.explain||"")}`
        : `❌ <b>Errado.</b> Resposta: <b>${String.fromCharCode(65+q.answerIndex)}</b>. ${escapeHtml(q.explain||"")}`;

      btnNextQ.disabled = false;
      markStudyMinutes(2);
      medalCheck();
      saveState();
    });
    qOpts.appendChild(b);
  });
}

btnNextQ.addEventListener("click", ()=>{
  if(!currentQuiz) return;
  currentQuiz.i += 1;
  if(currentQuiz.i >= currentQuiz.qs.length){
    // finish
    const pct = Math.round((currentQuiz.score/currentQuiz.qs.length)*100);
    awardXP(20);
    state.missionsDone += 1;

    // bump progress if it was a phase quiz
    if(currentQuiz.mode==="phase"){
      const phaseId = currentQuiz.phaseId;
      const cur = Number(state.progress[phaseId]||0);
      const add = pct>=80 ? 25 : pct>=60 ? 18 : 10;
      state.progress[phaseId] = clamp(cur + add, 0, 100);
    }

    quizBox.hidden = true;
    alert(`Fim do quiz! Você acertou ${currentQuiz.score}/${currentQuiz.qs.length} (${pct}%). +XP!`);
    currentQuiz = null;
    saveState();
    return;
  }
  renderQ();
});

$("#btnSpeakQ").addEventListener("click", ()=>{
  if(!currentQuiz) return;
  const q = currentQuiz.qs[currentQuiz.i];
  speak(`${q.text}. Alternativas: ${q.options.map((o,i)=>`${String.fromCharCode(65+i)}. ${o}`).join(". ")}`);
});

/** ======= Exam mode ======= */
$("#btnStartExam").addEventListener("click", ()=>{
  const count = Number(examCount.value||10);
  const filter = examSubject.value;

  let pool = [];
  for(const p of state.phases){
    if(filter!=="Todas" && p.subject!==filter) continue;
    for(const qq of (p.questions||[])){
      pool.push({...qq, _meta:{subject:p.subject, title:p.title}});
    }
  }
  if(pool.length < 5){
    examArea.innerHTML = `<div class="item">Poucas questões para gerar prova. Importe mais conteúdo.</div>`;
    return;
  }
  const qs = shuffle(pool).slice(0, Math.min(count, pool.length));
  startExam(qs);
});

function startExam(qs){
  let i=0, score=0;
  examArea.innerHTML = "";
  const card = document.createElement("div");
  card.className = "qbox";
  examArea.appendChild(card);

  const render = ()=>{
    const q = qs[i];
    card.innerHTML = `
      <div class="small">${escapeHtml(q._meta.subject)} • ${escapeHtml(q._meta.title)}</div>
      <h3 style="margin:6px 0 8px">Questão ${i+1} / ${qs.length}</h3>
      <div>${escapeHtml(q.text)}</div>
      <div id="examOpts" style="margin-top:10px"></div>
      <div class="row" style="justify-content:space-between; margin-top:10px">
        <button class="btn" id="exSpeak">🔊 Ler</button>
        <button class="btn primary" id="exNext" disabled>Próxima ➜</button>
      </div>
      <div class="small" id="exFb" style="margin-top:8px"></div>
    `;
    const opts = card.querySelector("#examOpts");
    const fb = card.querySelector("#exFb");
    const next = card.querySelector("#exNext");

    card.querySelector("#exSpeak").onclick = ()=>{
      speak(`${q.text}. Alternativas: ${q.options.map((o,j)=>`${String.fromCharCode(65+j)}. ${o}`).join(". ")}`);
    };

    q.options.forEach((op, idx)=>{
      const b = document.createElement("div");
      b.className="opt";
      b.textContent = `${String.fromCharCode(65+idx)}) ${op}`;
      b.onclick = ()=>{
        state.answered += 1;
        const ok = idx===q.answerIndex;
        if(ok){ score++; state.correct += 1; awardXP(18); }
        else awardXP(6);

        Array.from(opts.children).forEach((el, j)=>{
          if(j===q.answerIndex) el.classList.add("correct");
        });
        if(!ok) b.classList.add("wrong");

        fb.innerHTML = ok ? `✅ <b>Certo!</b>` : `❌ <b>Errado.</b> Correto: ${String.fromCharCode(65+q.answerIndex)}. ${escapeHtml(q.explain||"")}`;
        next.disabled = false;

        markStudyMinutes(2);
        saveState();
      };
      opts.appendChild(b);
    });

    next.onclick = ()=>{
      i++;
      if(i>=qs.length){
        const pct = Math.round((score/qs.length)*100);
        awardXP(40);
        state.missionsDone += 1;
        markStudyMinutes(8);
        alert(`Simulado finalizado: ${score}/${qs.length} (${pct}%).`);
        examArea.innerHTML = `<div class="item"><b>Resultado:</b> ${score}/${qs.length} (${pct}%).</div>`;
        saveState();
        return;
      }
      render();
    };
  };

  render();
}

/** ======= Quick buttons ======= */
$("#btnQuickQuiz").addEventListener("click", ()=>{ startQuickQuiz(); });
$("#btnQuickAudio").addEventListener("click", ()=>{
  const p = pickPhaseToStudy();
  if(!p) return;
  speak(`${p.title}. Resumo: ${p.summary}`);
  awardXP(20); markStudyMinutes(5); state.missionsDone += 1;
  saveState();
});
$("#btnMarkUnderstood").addEventListener("click", ()=>{
  const p = pickPhaseToStudy();
  if(!p) return;
  state.understood[p.id] = true;
  state.progress[p.id] = Math.max(Number(state.progress[p.id]||0), 50);
  awardXP(25); markStudyMinutes(6); state.missionsDone += 1;
  medalCheck();
  saveState();
});

function pickPhaseToStudy(){
  if(!state.phases.length){ alert("Sem fases. Importe conteúdo."); return null; }
  // pega a fase com menor progresso
  let best = state.phases[0];
  let bestPr = Number(state.progress[best.id]||0);
  for(const p of state.phases){
    const pr = Number(state.progress[p.id]||0);
    if(pr < bestPr){ best=p; bestPr=pr; }
  }
  return best;
}

/** ======= Pomodoro ======= */
let timerOn=false;
let timerLeft=25*60;
let timerInt=null;
const timerLabel = $("#timerLabel");

function renderTimer(){
  const m = String(Math.floor(timerLeft/60)).padStart(2,"0");
  const s = String(timerLeft%60).padStart(2,"0");
  timerLabel.textContent = `${m}:${s}`;
}
renderTimer();

$("#btnTimer").addEventListener("click", ()=>{
  if(timerOn){
    timerOn=false;
    clearInterval(timerInt); timerInt=null;
    $("#btnTimer").textContent="▶️ Iniciar";
    return;
  }
  timerOn=true;
  $("#btnTimer").textContent="⏸️ Pausar";
  timerInt=setInterval(()=>{
    timerLeft--;
    renderTimer();
    if(timerLeft<=0){
      timerOn=false; clearInterval(timerInt); timerInt=null;
      timerLeft=25*60; renderTimer();
      awardXP(60);
      markStudyMinutes(25);
      state.missionsDone += 1;
      medalCheck();
      saveState();
      alert("Pomodoro concluído! +XP.");
      speak("Pomodoro concluído. Excelente!");
      $("#btnTimer").textContent="▶️ Iniciar";
    }
  },1000);
});
$("#btnTimerReset").addEventListener("click", ()=>{
  timerOn=false;
  clearInterval(timerInt); timerInt=null;
  timerLeft=25*60; renderTimer();
  $("#btnTimer").textContent="▶️ Iniciar";
});

/** ======= Import modal ======= */
const modalImport = $("#modalImport");
$("#btnImport").addEventListener("click", ()=> modalImport.classList.add("on"));
$("#btnCloseImport").addEventListener("click", ()=> modalImport.classList.remove("on"));

$("#btnAddPhase").addEventListener("click", ()=>{
  const title = $("#impTitle").value.trim();
  const subject = $("#impSubject").value.trim();
  const weight = Number($("#impWeight").value||5);
  const summary = $("#impSummary").value.trim();
  const rawQ = $("#impQuestions").value.trim();

  if(!title || !subject || !summary){
    alert("Preencha: Nome da fase, Matéria e Resumo.");
    return;
  }

  const questions = parseQuestions(rawQ);
  const p = { id: uid(), title, subject, weight: clamp(weight,1,40), summary, questions };
  state.phases.push(p);
  state.progress[p.id] = 0;

  // limpa
  $("#impTitle").value=""; $("#impSubject").value=""; $("#impSummary").value=""; $("#impQuestions").value="";
  modalImport.classList.remove("on");

  awardXP(10);
  saveState();
});

function parseQuestions(raw){
  if(!raw) return [];
  // separa blocos por duas quebras
  const blocks = raw.split(/\n\s*\n+/g).map(s=>s.trim()).filter(Boolean);
  const out = [];
  for(const b of blocks){
    // procura linhas
    const lines = b.split("\n").map(x=>x.trim()).filter(Boolean);
    let qtext = "";
    let opts = [];
    let ans = null;
    let explain = "";

    for(const ln of lines){
      if(/^PERGUNTA:/i.test(ln)) qtext = ln.replace(/^PERGUNTA:\s*/i,"").trim();
      else if(/^[A-E]\)/.test(ln)) opts.push(ln.replace(/^[A-E]\)\s*/,"").trim());
      else if(/^GABARITO:/i.test(ln)){
        const letter = ln.replace(/^GABARITO:\s*/i,"").trim().toUpperCase();
        ans = "ABCDE".indexOf(letter[0]);
      }else if(/^EXPLICAÇÃO:/i.test(ln)){
        explain = ln.replace(/^EXPLICAÇÃO:\s*/i,"").trim();
      }
    }
    if(qtext && opts.length>=2 && ans!==null && ans>=0){
      // garante 5 opções (se tiver menos, completa com vazio)
      while(opts.length<5) opts.push("(opção)");
      out.push(q(qtext, opts.slice(0,5), clamp(ans,0,4), explain));
    }
  }
  return out;
}

/** ======= Config ======= */
$("#btnSaveCfg").addEventListener("click", ()=>{
  state.cfg.goal = clamp(Number($("#cfgGoal").value||50), 1, 100);
  state.cfg.minDay = clamp(Number($("#cfgMinDay").value||45), 5, 300);
  saveState();
  alert("Config salva.");
});
$("#cfgGoal").value = state.cfg.goal;
$("#cfgMinDay").value = state.cfg.minDay;

$("#btnReset").addEventListener("click", ()=>{
  if(!confirm("Tem certeza? Isso apaga seu progresso.")) return;
  localStorage.removeItem(LS_KEY);
  state = loadState();
  saveState();
});

/** ======= Backup / Restore ======= */
$("#btnBackup").addEventListener("click", ()=>{
  const blob = new Blob([JSON.stringify(state,null,2)], {type:"application/json"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = "ibgequest_backup.json";
  a.click();
});

$("#btnRestore").addEventListener("click", async ()=>{
  const inp = document.createElement("input");
  inp.type="file";
  inp.accept=".json,application/json";
  inp.onchange = async ()=>{
    const f = inp.files?.[0];
    if(!f) return;
    const txt = await f.text();
    try{
      const s = JSON.parse(txt);
      state = { ...structuredClone(DEFAULT_STATE), ...s, cfg: { ...DEFAULT_STATE.cfg, ...(s.cfg||{}) } };
      saveState();
      alert("Backup restaurado!");
    }catch(e){
      alert("Arquivo inválido.");
    }
  };
  inp.click();
});

/** ======= Medals ======= */
function medalCheck(){
  const overall = calcOverallProgress();
  const acc = state.answered ? (state.correct/state.answered) : 0;
  const medals = [
    { id:"start", name:"Primeiro passo", rule: ()=> state.missionsDone>=1 },
    { id:"streak3", name:"Sequência 3 dias", rule: ()=> state.streak.days>=3 },
    { id:"streak7", name:"Sequência 7 dias", rule: ()=> state.streak.days>=7 },
    { id:"lvl5", name:"Nível 5", rule: ()=> state.level>=5 },
    { id:"acc70", name:"Acerto 70%+", rule: ()=> state.answered>=20 && acc>=0.70 },
    { id:"half", name:"50% do edital", rule: ()=> overall>=50 },
    { id:"full", name:"100% do edital", rule: ()=> overall>=100 },
  ];
  for(const m of medals){
    if(m.rule() && !state.medals[m.id]){
      state.medals[m.id] = { unlockedAt: Date.now(), name:m.name };
      try{ speak(`Medalha desbloqueada: ${m.name}`); }catch(e){}
    }
  }
}

function renderMedals(){
  const entries = Object.values(state.medals||{});
  $("#medalCount").textContent = entries.length;
  $("#medals").innerHTML = entries.length
    ? entries.map(m=>`• 🏅 <b>${escapeHtml(m.name)}</b>`).join("<br>")
    : "Nenhuma ainda. Comece com uma missão hoje 🙂";
}

/** ======= Focus plan ======= */
$("#btnFocus").addEventListener("click", ()=>{
  const overall = calcOverallProgress();
  const goal = state.cfg.goal;
  const missing = Math.max(0, goal - overall);

  const plan =
`Plano rápido até 01/03 (meta ${goal}%):
1) Todo dia: 1 Pomodoro (25 min) + 5 questões.
2) Priorize fases com menor %.
3) Ao “entendi” uma fase: marque e faça 5 questões.

Você está em ${overall}%. Faltam ~${missing}% para bater a meta.`;

  alert(plan);
  speak(plan);
});

/** ======= Footer nav ======= */
$("#navHome").addEventListener("click", ()=> window.scrollTo({top:0,behavior:"smooth"}));
$("#navStudy").addEventListener("click", ()=>{
  setTab("fases");
  window.scrollTo({top:0,behavior:"smooth"});
});
$("#navExam").addEventListener("click", ()=>{
  setTab("prova");
  window.scrollTo({top:0,behavior:"smooth"});
});
$("#navInstall").addEventListener("click", ()=>{
  alert("Para instalar como app:\n\nAndroid/Chrome:\n1) Abra seu link do GitHub Pages\n2) Menu ⋮\n3) “Adicionar à tela inicial”\n\nIsso cria um ícone como aplicativo.");
});

/** ======= Utils ======= */
function shuffle(arr){
  for(let i=arr.length-1;i>0;i--){
    const j=Math.floor(Math.random()*(i+1));
    [arr[i],arr[j]]=[arr[j],arr[i]];
  }
  return arr;
}

/** ======= Init ======= */
function init(){
  // garante dia
  const tk = todayKey();
  if(state.time.lastDay !== tk){
    state.time.lastDay = tk;
    state.time.todayMin = 0;
  }
  medalCheck();
  renderAll();
}
init();
</script>
</body>
</html>
