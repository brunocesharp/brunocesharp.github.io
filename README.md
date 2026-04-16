<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IA não é somente Prompt — Cartilha para Devs</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#0f172a;color:#e5e7eb}
.cartilha{width:100%;max-width:820px;margin:0 auto;padding:1.5rem 1rem}
.nav{display:flex;align-items:center;justify-content:space-between;padding:0.75rem 1rem;border-bottom:1px solid #1e293b;margin-bottom:1.5rem;position:sticky;top:0;background:#0f172a;z-index:10;border-radius:12px}
.nav-dots{display:flex;gap:6px;flex-wrap:wrap}
.dot{width:10px;height:10px;border-radius:50%;border:1.5px solid #334155;cursor:pointer;transition:all 0.2s}
.dot.active{background:#7C3AED;border-color:#7C3AED}
.nav-btns{display:flex;gap:8px}
.nav-btns button{padding:6px 16px;font-size:13px;border:1px solid #334155;border-radius:8px;background:transparent;color:#94a3b8;cursor:pointer;transition:all 0.2s}
.nav-btns button:hover{background:#1e293b;color:#e5e7eb}
.slide{display:none;animation:fadeIn 0.3s ease}
.slide.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.slide-inner{border:1px solid #1e293b;border-radius:16px;overflow:hidden;background:#0f172a}
.slide-tag{display:inline-block;font-size:11px;font-weight:600;padding:4px 12px;border-radius:999px;margin-bottom:1rem;background:#1e1b4b;color:#a78bfa;letter-spacing:0.06em;text-transform:uppercase}
.cover-bg{background:linear-gradient(135deg,#1e1b4b 0%,#312e81 40%,#0f172a 100%);padding:3.5rem 3rem 3rem;min-height:420px;position:relative;overflow:hidden}
.cover-circle{position:absolute;border-radius:50%;pointer-events:none}
.cover-title{font-size:clamp(40px,7vw,64px);font-weight:700;color:#fff;line-height:1.05;margin-bottom:1rem}
.cover-title span{color:#a78bfa}
.cover-sub{font-size:clamp(15px,2vw,18px);color:#c4b5fd;margin-bottom:2rem;line-height:1.7}
.cover-badge{display:inline-block;background:rgba(124,58,237,0.3);border:1px solid #7c3aed;color:#ddd6fe;font-size:12px;padding:5px 14px;border-radius:999px;margin-bottom:1.5rem;letter-spacing:0.04em}
.cover-tag-row{display:flex;gap:8px;flex-wrap:wrap}
.cover-tag{font-size:11px;padding:4px 12px;border-radius:999px;border:1px solid #4c1d95;color:#a78bfa;background:rgba(124,58,237,0.1)}
.cover-bottom{height:5px;background:linear-gradient(90deg,#7c3aed,#06b6d4)}
.big-quote{font-size:clamp(20px,3vw,28px);font-weight:600;color:#e5e7eb;border-left:4px solid #7c3aed;padding-left:1.25rem;margin-bottom:2rem;line-height:1.5}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:1.25rem}
.col-card{background:#1e293b;border-radius:12px;padding:1.25rem;border:1px solid #334155}
.col-card h3{font-size:13px;font-weight:600;color:#64748b;margin-bottom:0.75rem;text-transform:uppercase;letter-spacing:0.07em}
.col-card p{font-size:14px;color:#94a3b8;line-height:1.7}
.myth-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.25rem;margin-top:1rem}
.myth-card{padding:1.5rem;border-radius:12px;border:1px solid}
.myth-card.wrong{background:#1c0a0a;border-color:#7f1d1d}
.myth-card.right{background:#052e16;border-color:#14532d}
.myth-label{font-size:12px;font-weight:600;margin-bottom:1rem;display:flex;align-items:center;gap:8px;text-transform:uppercase;letter-spacing:0.05em}
.myth-label.wrong-l{color:#f87171}
.myth-label.right-l{color:#4ade80}
.myth-icon{width:20px;height:20px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0}
.myth-icon.x{background:#dc2626;color:#fff}
.myth-icon.ok{background:#16a34a;color:#fff}
.myth-item{display:flex;align-items:flex-start;gap:8px;margin-bottom:0.65rem}
.myth-item p{font-size:14px;color:#cbd5e1;line-height:1.5}
.myth-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;margin-top:5px}
.myth-dot.r{background:#ef4444}
.myth-dot.g{background:#22c55e}
.cards-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1rem;margin-top:1rem}
.comp-card{background:#1e293b;border-radius:12px;padding:1.25rem;border:1px solid #334155;border-top:3px solid}
.comp-card h3{font-size:16px;font-weight:600;margin-bottom:0.5rem;color:#e2e8f0}
.comp-card p{font-size:13px;color:#94a3b8;line-height:1.6}
.comp-pill{display:inline-block;font-size:10px;padding:3px 9px;border-radius:999px;margin-bottom:0.5rem;font-weight:600;letter-spacing:0.05em}
.p1{background:#2e1065;color:#ddd6fe}.p2{background:#164e63;color:#a5f3fc}.p3{background:#451a03;color:#fde68a}.p4{background:#052e16;color:#a7f3d0}.p5{background:#450a0a;color:#fecaca}.p6{background:#2e1065;color:#e9d5ff}
.arch-flow{display:flex;flex-direction:column;gap:0;align-items:center;margin:1.5rem 0}
.arch-node{background:#1e293b;border:1px solid #334155;border-radius:12px;padding:0.75rem 2rem;font-size:15px;font-weight:500;color:#e2e8f0;min-width:220px;text-align:center}
.arch-node.hl{background:#1e1b4b;border-color:#7c3aed;color:#ddd6fe}
.arch-node.ok{background:#052e16;border-color:#22c55e;color:#86efac}
.arch-arrow{width:2px;height:28px;background:#334155;position:relative;margin:0 auto}
.arch-arrow::after{content:'';position:absolute;bottom:-6px;left:-4px;border-left:5px solid transparent;border-right:5px solid transparent;border-top:7px solid #475569}
.arch-label{font-size:11px;color:#64748b;text-align:center;margin:3px 0}
.arch-split{display:flex;gap:1rem}
.prob-list{display:flex;flex-direction:column;gap:0.75rem;margin-top:1rem}
.prob-item{display:flex;align-items:flex-start;gap:1rem;padding:1rem 1.25rem;background:#1e293b;border-radius:12px;border:1px solid #334155;border-left:3px solid #ef4444}
.prob-icon-wrap{width:32px;height:32px;border-radius:8px;background:#450a0a;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:15px;font-weight:700;color:#ef4444}
.prob-title{font-size:14px;font-weight:600;color:#e2e8f0;margin-bottom:3px}
.prob-desc{font-size:13px;color:#94a3b8;line-height:1.5}
.check-list{display:flex;flex-direction:column;gap:0.75rem;margin-top:1rem}
.check-item{display:flex;align-items:flex-start;gap:1rem;padding:1rem 1.25rem;background:#1e293b;border-radius:12px;border:1px solid #334155;border-left:3px solid #22c55e}
.check-box{width:24px;height:24px;border-radius:6px;background:#22c55e;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px}
.check-mark{width:10px;height:6px;border-left:2.5px solid #fff;border-bottom:2.5px solid #fff;transform:rotate(-45deg);margin-top:-2px}
.check-text{font-size:15px;font-weight:500;color:#e2e8f0}
.check-sub{font-size:13px;color:#94a3b8;margin-top:3px}
.ex-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;margin-top:1rem}
.ex-col h3{font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:0.08em;margin-bottom:0.75rem}
.ex-col.before h3{color:#f87171}
.ex-col.after h3{color:#4ade80}
.code-block{background:#0d1117;border-radius:12px;padding:1.25rem;font-family:'SF Mono','Fira Code',monospace;font-size:13px;line-height:1.9;border:1px solid #1e293b}
.code-key{color:#a78bfa}
.code-val{color:#c4b5fd}
.code-comment{color:#4a4870;font-size:12px}
.result-box{margin-top:0.75rem;padding:0.75rem 1rem;border-radius:8px;font-size:13px;font-weight:500}
.result-box.bad{background:#450a0a;color:#fca5a5;border:1px solid #7f1d1d}
.result-box.good{background:#052e16;color:#86efac;border:1px solid #14532d}
.evo-track{display:flex;align-items:flex-start;margin:2rem 0;gap:0;position:relative}
.evo-track::before{content:'';position:absolute;top:22px;left:22px;right:22px;height:2px;background:linear-gradient(90deg,#7c3aed,#06b6d4);z-index:0}
.evo-step{flex:1;display:flex;flex-direction:column;align-items:center;position:relative;z-index:1}
.evo-circle{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:700;border:2px solid}
.evo-label{font-size:12px;text-align:center;margin-top:0.75rem;color:#94a3b8;font-weight:500;line-height:1.4}
.e1{background:#2e1065;border-color:#7c3aed;color:#ddd6fe}
.e2{background:#1e3a5f;border-color:#3b82f6;color:#93c5fd}
.e3{background:#164e63;border-color:#06b6d4;color:#a5f3fc}
.e4{background:#052e16;border-color:#22c55e;color:#86efac}
.evo-info{display:grid;grid-template-columns:repeat(4,1fr);gap:1rem;margin-top:1.5rem}
.evo-info-card{padding:1rem;background:#1e293b;border-radius:12px;border:1px solid #334155}
.evo-info-card h4{font-size:11px;font-weight:600;margin-bottom:0.4rem;color:#64748b;text-transform:uppercase;letter-spacing:0.06em}
.evo-info-card p{font-size:12px;color:#94a3b8;line-height:1.5}
.concl-body{padding:3rem 2.5rem;text-align:center}
.concl-big{font-size:clamp(28px,4vw,40px);font-weight:700;line-height:1.3;color:#e2e8f0;margin-bottom:1.5rem}
.concl-big span{color:#a78bfa}
.concl-sub{font-size:16px;color:#94a3b8;max-width:500px;margin:0 auto 2rem;line-height:1.7}
.concl-tags{display:flex;gap:8px;justify-content:center;flex-wrap:wrap}
.concl-tag{font-size:12px;padding:5px 14px;border-radius:999px;background:#1e293b;border:1px solid #334155;color:#94a3b8}
.author-footer{position:absolute;bottom:16px;right:24px;font-size:12px;color:#64748b;font-weight:500;letter-spacing:0.03em}
.slide-inner{position:relative}
.slide-header{padding:2rem 2.5rem 0}
.slide-title{font-size:clamp(20px,3vw,26px);font-weight:700;color:#e2e8f0;margin-bottom:0.25rem}
.slide-sub{font-size:14px;color:#64748b}
.body-pad{padding:1.5rem 2.5rem 2.5rem}
@media(max-width:600px){
  .two-col,.myth-grid,.cards-grid,.ex-grid,.evo-info{grid-template-columns:1fr}
  .evo-track{flex-direction:column;align-items:flex-start;gap:12px}
  .evo-track::before{display:none}
  .cover-bg{padding:2rem 1.5rem}
  .body-pad{padding:1rem 1.25rem 1.5rem}
  .slide-header{padding:1.25rem 1.25rem 0}
  .arch-split{flex-direction:column}
}
</style>
</head>
<body>
<div class="cartilha">

<div class="nav">
  <div class="nav-dots" id="dots"></div>
  <div style="font-size:13px;color:#64748b" id="slide-counter">1 / 10</div>
  <div class="nav-btns">
    <button onclick="changeSlide(-1)">← Anterior</button>
    <button onclick="changeSlide(1)">Próximo →</button>
  </div>
</div>

<!-- SLIDE 1: COVER -->
<div class="slide active" id="slide-0">
  <div class="slide-inner">
    <div class="cover-bg">
      <div class="cover-circle" style="width:500px;height:500px;background:#7c3aed;opacity:0.1;top:-150px;right:-150px"></div>
      <div class="cover-circle" style="width:350px;height:350px;background:#06b6d4;opacity:0.08;bottom:-100px;left:-80px"></div>
      <div style="position:relative;z-index:1">
        <div class="cover-badge">GUIA PARA DEVS — v1.0</div>
        <div class="cover-title">IA NÃO É<br><span>SOMENTE</span><br>PROMPT</div>
        <div class="cover-sub">Um guia para desenvolvedores que querem<br>construir sistemas reais com inteligência artificial</div>
        <div class="cover-tag-row">
          <span class="cover-tag">sistemas de IA</span>
          <span class="cover-tag">engenharia</span>
          <span class="cover-tag">agentes</span>
          <span class="cover-tag">ferramentas</span>
        </div>
      </div>
    </div>
    <div class="cover-bottom"></div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 2: INTRO -->
<div class="slide" id="slide-1">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">introdução</div>
      <div class="slide-title">IA é engenharia de sistemas</div>
      <div class="slide-sub">Não apenas uma caixa de texto inteligente</div>
    </div>
    <div class="body-pad">
      <div class="big-quote">Prompt é só a interface.<br>O sistema é muito maior.</div>
      <div class="two-col">
        <div class="col-card">
          <h3>Visão limitada</h3>
          <p>Muitos devs tratam IA como uma API mágica: você manda um texto, recebe uma resposta. Isso funciona para demos — não para produtos reais.</p>
        </div>
        <div class="col-card">
          <h3>Visão sistêmica</h3>
          <p>Um sistema de IA bem construído combina LLMs, ferramentas externas, contexto persistente, controle de execução e validação de resultados.</p>
        </div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 3: MYTH -->
<div class="slide" id="slide-2">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">desmistificando</div>
      <div class="slide-title">O mito do prompt mágico</div>
      <div class="slide-sub">A diferença entre IA como truque e IA como sistema</div>
    </div>
    <div class="body-pad">
      <div class="myth-grid">
        <div class="myth-card wrong">
          <div class="myth-label wrong-l"><div class="myth-icon x">✕</div> Visão equivocada</div>
          <div class="myth-item"><div class="myth-dot r"></div><p>IA = só o prompt</p></div>
          <div class="myth-item"><div class="myth-dot r"></div><p>Resultado = mágico e imprevisível</p></div>
          <div class="myth-item"><div class="myth-dot r"></div><p>Melhorar = reescrever o prompt</p></div>
          <div class="myth-item"><div class="myth-dot r"></div><p>Sem estrutura, sem controle</p></div>
        </div>
        <div class="myth-card right">
          <div class="myth-label right-l"><div class="myth-icon ok">✓</div> Visão correta</div>
          <div class="myth-item"><div class="myth-dot g"></div><p>IA = sistema completo</p></div>
          <div class="myth-item"><div class="myth-dot g"></div><p>Prompt = interface de entrada</p></div>
          <div class="myth-item"><div class="myth-dot g"></div><p>Melhorar = arquitetar melhor</p></div>
          <div class="myth-item"><div class="myth-dot g"></div><p>Com ferramentas, validação e contexto</p></div>
        </div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 4: COMPONENTS -->
<div class="slide" id="slide-3">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">arquitetura</div>
      <div class="slide-title">Componentes do sistema</div>
      <div class="slide-sub">Os blocos fundamentais de qualquer sistema de IA robusto</div>
    </div>
    <div class="body-pad">
      <div class="cards-grid">
        <div class="comp-card" style="border-top-color:#7c3aed"><div class="comp-pill p1">NÚCLEO</div><h3>LLM</h3><p>O modelo de linguagem. Raciocina, gera e interpreta — mas sozinho não faz nada real.</p></div>
        <div class="comp-card" style="border-top-color:#06b6d4"><div class="comp-pill p2">INTERFACE</div><h3>Prompt</h3><p>A instrução estruturada que guia o comportamento do modelo em cada chamada.</p></div>
        <div class="comp-card" style="border-top-color:#f59e0b"><div class="comp-pill p3">MEMÓRIA</div><h3>Contexto</h3><p>Histórico, documentos, estado atual. Define o que o modelo "sabe" naquele momento.</p></div>
        <div class="comp-card" style="border-top-color:#10b981"><div class="comp-pill p4">AÇÃO</div><h3>Tools</h3><p>Funções reais: buscar na web, consultar banco de dados, chamar APIs externas.</p></div>
        <div class="comp-card" style="border-top-color:#ef4444"><div class="comp-pill p5">LÓGICA</div><h3>Skills</h3><p>Capacidades especializadas e reutilizáveis: resumir, extrair, classificar, planejar.</p></div>
        <div class="comp-card" style="border-top-color:#8b5cf6"><div class="comp-pill p6">CONTROLE</div><h3>Hooks</h3><p>Pontos de interceptação para validar, transformar ou redirecionar saídas do modelo.</p></div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 5: ARCHITECTURE -->
<div class="slide" id="slide-4">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">fluxo</div>
      <div class="slide-title">Arquitetura de um agente</div>
      <div class="slide-sub">Como o dado flui por um sistema real de IA</div>
    </div>
    <div class="body-pad">
      <div class="arch-flow">
        <div class="arch-node hl">Prompt do usuário</div>
        <div class="arch-arrow"></div>
        <div class="arch-label">instrução + contexto</div>
        <div class="arch-node hl">LLM — raciocínio</div>
        <div class="arch-arrow"></div>
        <div class="arch-label">seleciona skill ou tool</div>
        <div class="arch-split">
          <div class="arch-node" style="min-width:160px;font-size:14px">Skill</div>
          <div class="arch-node" style="min-width:160px;font-size:14px">Tool / API</div>
        </div>
        <div class="arch-arrow"></div>
        <div class="arch-label">resultado bruto</div>
        <div class="arch-node" style="font-size:14px">Validação + Hook</div>
        <div class="arch-arrow"></div>
        <div class="arch-node ok">Resposta final</div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 6: PROBLEMS -->
<div class="slide" id="slide-5">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">problemas</div>
      <div class="slide-title">Os riscos do prompt-only</div>
      <div class="slide-sub">Por que depender só do prompt não escala</div>
    </div>
    <div class="body-pad">
      <div class="prob-list">
        <div class="prob-item"><div class="prob-icon-wrap">~</div><div><div class="prob-title">Inconsistência</div><div class="prob-desc">O mesmo prompt pode gerar resultados completamente diferentes. Sem estrutura, não há garantia.</div></div></div>
        <div class="prob-item"><div class="prob-icon-wrap">!</div><div><div class="prob-title">Sem ação real</div><div class="prob-desc">O modelo gera texto, mas não executa. Para agir no mundo, você precisa de tools integradas.</div></div></div>
        <div class="prob-item"><div class="prob-icon-wrap">?</div><div><div class="prob-title">Sem dados externos</div><div class="prob-desc">O LLM só sabe o que está no treino + contexto. Sem RAG ou tools, não acessa dados atuais.</div></div></div>
        <div class="prob-item"><div class="prob-icon-wrap">×</div><div><div class="prob-title">Sem controle de execução</div><div class="prob-desc">Não dá para parar, redirecionar ou validar em tempo real. Você reza e espera a resposta.</div></div></div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 7: BEST PRACTICES -->
<div class="slide" id="slide-6">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">boas práticas</div>
      <div class="slide-title">Como construir certo</div>
      <div class="slide-sub">Princípios de engenharia para sistemas de IA</div>
    </div>
    <div class="body-pad">
      <div class="check-list">
        <div class="check-item"><div class="check-box"><div class="check-mark"></div></div><div><div class="check-text">Separe responsabilidades</div><div class="check-sub">LLM raciocina, tools executam, hooks validam — cada parte tem seu papel</div></div></div>
        <div class="check-item"><div class="check-box"><div class="check-mark"></div></div><div><div class="check-text">Use tools para ações reais</div><div class="check-sub">Conecte o modelo ao mundo: bancos de dados, APIs, sistemas externos</div></div></div>
        <div class="check-item"><div class="check-box"><div class="check-mark"></div></div><div><div class="check-text">Controle a execução</div><div class="check-sub">Defina fluxos, tratamento de erro e pontos de validação explícitos</div></div></div>
        <div class="check-item"><div class="check-box"><div class="check-mark"></div></div><div><div class="check-text">Gerencie o contexto</div><div class="check-sub">Injete dados relevantes, histórico e estado — não confie na memória do modelo</div></div></div>
        <div class="check-item"><div class="check-box"><div class="check-mark"></div></div><div><div class="check-text">Pense como engenheiro</div><div class="check-sub">IA é infraestrutura. Projete com observabilidade, testes e modularidade</div></div></div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 8: EXAMPLE -->
<div class="slide" id="slide-7">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">exemplo prático</div>
      <div class="slide-title">Antes vs. Depois</div>
      <div class="slide-sub">Criando uma API — prompt-only vs. sistema estruturado</div>
    </div>
    <div class="body-pad">
      <div class="ex-grid">
        <div class="ex-col before">
          <h3>Antes — prompt direto</h3>
          <div class="code-block">
            <div><span class="code-key">Prompt:</span></div>
            <div style="color:#c4b5fd;margin:4px 0 12px 12px">"Crie uma API REST<br>para cadastro de usuários"</div>
            <div class="code-comment">// sem contexto</div>
            <div class="code-comment">// sem estrutura</div>
            <div class="code-comment">// sem validação</div>
          </div>
          <div class="result-box bad">Resultado: código genérico, incompleto, sem testes</div>
        </div>
        <div class="ex-col after">
          <h3>Depois — sistema estruturado</h3>
          <div class="code-block">
            <div><span class="code-key">Skill:</span> <span class="code-val">api-generator</span></div>
            <div><span class="code-key">Tool:</span> <span class="code-val">read-codebase</span></div>
            <div><span class="code-key">Tool:</span> <span class="code-val">run-tests</span></div>
            <div><span class="code-key">Hook:</span> <span class="code-val">validate-schema</span></div>
            <div><span class="code-key">Context:</span> <span class="code-val">stack-info</span></div>
          </div>
          <div class="result-box good">Resultado: API real, com testes, alinhada ao stack</div>
        </div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 9: EVOLUTION -->
<div class="slide" id="slide-8">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">carreira</div>
      <div class="slide-title">A evolução do dev com IA</div>
      <div class="slide-sub">Da experimentação à arquitetura de agentes</div>
    </div>
    <div class="body-pad">
      <div class="evo-track">
        <div class="evo-step"><div class="evo-circle e1">1</div><div class="evo-label">Prompt<br>User</div></div>
        <div class="evo-step"><div class="evo-circle e2">2</div><div class="evo-label">Builder</div></div>
        <div class="evo-step"><div class="evo-circle e3">3</div><div class="evo-label">AI<br>Engineer</div></div>
        <div class="evo-step"><div class="evo-circle e4">4</div><div class="evo-label">Agent<br>Architect</div></div>
      </div>
      <div class="evo-info">
        <div class="evo-info-card"><h4>Prompt User</h4><p>Usa ChatGPT. Itera no prompt até funcionar. Sem código.</p></div>
        <div class="evo-info-card"><h4>Builder</h4><p>Integra API, cria fluxos básicos. Começa a usar tools.</p></div>
        <div class="evo-info-card"><h4>AI Engineer</h4><p>Projeta sistemas com RAG, contexto, validação e testes.</p></div>
        <div class="evo-info-card"><h4>Agent Architect</h4><p>Cria agentes autônomos com orquestração e multi-step.</p></div>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

<!-- SLIDE 10: CONCLUSION -->
<div class="slide" id="slide-9">
  <div class="slide-inner">
    <div class="slide-header">
      <div class="slide-tag">conclusão</div>
    </div>
    <div class="concl-body">
      <div class="concl-big">Prompt é só a <span>interface</span>.<br>O sistema é muito maior.</div>
      <div class="concl-sub">Desenvolvedores que entendem isso não apenas usam IA — eles constroem com IA. E essa diferença define a próxima geração de engenharia de software.</div>
      <div class="concl-tags">
        <span class="concl-tag">LLM</span>
        <span class="concl-tag">Tools</span>
        <span class="concl-tag">Skills</span>
        <span class="concl-tag">Hooks</span>
        <span class="concl-tag">Contexto</span>
        <span class="concl-tag">Agentes</span>
        <span class="concl-tag">Engenharia de IA</span>
      </div>
    </div>
    <div class="author-footer">Bruno Alves - Analista de Sistemas</div>
  </div>
</div>

</div>

<script>
let current = 0;
const total = 10;
const dotsEl = document.getElementById('dots');
const counter = document.getElementById('slide-counter');

for(let i = 0; i < total; i++){
  const d = document.createElement('div');
  d.className = 'dot' + (i === 0 ? ' active' : '');
  d.onclick = () => goTo(i);
  dotsEl.appendChild(d);
}

function goTo(n){
  document.getElementById('slide-' + current).classList.remove('active');
  dotsEl.children[current].classList.remove('active');
  current = (n + total) % total;
  document.getElementById('slide-' + current).classList.add('active');
  dotsEl.children[current].classList.add('active');
  counter.textContent = (current + 1) + ' / ' + total;
  window.scrollTo({top: 0, behavior: 'smooth'});
}

function changeSlide(dir){ goTo(current + dir); }

document.addEventListener('keydown', e => {
  if(e.key === 'ArrowRight') changeSlide(1);
  if(e.key === 'ArrowLeft') changeSlide(-1);
});
</script>
</body>
</html>

