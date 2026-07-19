<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DataViz — Architecture Scheme</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #09090f;
      --surface: #111118;
      --surface2: #18181f;
      --border: rgba(255,255,255,0.07);
      --text: #f0f0f8;
      --muted: #8888a8;

      --frontend:  #6366f1;
      --backend:   #10b981;
      --db:        #f59e0b;
      --external:  #ec4899;
      --infra:     #3b82f6;

      --frontend-dim:  rgba(99,102,241,.12);
      --backend-dim:   rgba(16,185,129,.12);
      --db-dim:        rgba(245,158,11,.12);
      --external-dim:  rgba(236,72,153,.12);
      --infra-dim:     rgba(59,130,246,.12);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Inter', sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      overflow-x: hidden;
    }

    header {
      padding: 2.5rem 3rem 2rem;
      border-bottom: 1px solid var(--border);
      background: linear-gradient(135deg, rgba(99,102,241,.06) 0%, rgba(16,185,129,.04) 100%);
      position: relative;
      overflow: hidden;
    }
    header::before {
      content: '';
      position: absolute; inset: 0;
      background: radial-gradient(ellipse 60% 80% at 50% -20%, rgba(99,102,241,.18) 0%, transparent 70%);
      pointer-events: none;
    }
    header h1 {
      font-size: 2.4rem;
      font-weight: 800;
      background: linear-gradient(135deg, #a5b4fc 0%, #34d399 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      letter-spacing: -0.04em;
    }
    header p { margin-top: .5rem; color: var(--muted); font-size: .95rem; }
    .badges { display: flex; gap: .5rem; flex-wrap: wrap; margin-top: 1.2rem; }
    .badge {
      padding: .3rem .75rem; border-radius: 999px; font-size: .72rem;
      font-weight: 600; letter-spacing: .03em; text-transform: uppercase; border: 1px solid;
    }
    .badge.fe  { color: var(--frontend);  border-color: var(--frontend);  background: var(--frontend-dim);  }
    .badge.be  { color: var(--backend);   border-color: var(--backend);   background: var(--backend-dim);   }
    .badge.db  { color: var(--db);        border-color: var(--db);        background: var(--db-dim);        }
    .badge.ext { color: var(--external);  border-color: var(--external);  background: var(--external-dim);  }
    .badge.inf { color: var(--infra);     border-color: var(--infra);     background: var(--infra-dim);     }

    .legend {
      display: flex; gap: 1.5rem; flex-wrap: wrap;
      padding: 1rem 3rem; border-bottom: 1px solid var(--border); background: var(--surface);
    }
    .legend-item { display: flex; align-items: center; gap: .45rem; font-size: .8rem; color: var(--muted); }
    .legend-dot { width: 10px; height: 10px; border-radius: 50%; }

    main { padding: 2.5rem 3rem; display: flex; flex-direction: column; gap: 2rem; }

    .flow-row { display: flex; align-items: stretch; gap: 1.5rem; flex-wrap: wrap; }

    .arrow-h { display: flex; align-items: center; color: var(--muted); font-size: 1.4rem; flex-shrink: 0; opacity: .5; }

    .section-card {
      flex: 1; min-width: 240px; border-radius: 16px; border: 1px solid var(--border);
      overflow: hidden; background: var(--surface); transition: box-shadow .25s, transform .25s;
    }
    .section-card:hover { box-shadow: 0 0 0 1px var(--border), 0 8px 40px rgba(0,0,0,.4); transform: translateY(-2px); }

    .section-header {
      padding: .9rem 1.2rem; display: flex; align-items: center; gap: .7rem;
      border-bottom: 1px solid var(--border); font-weight: 700; font-size: .9rem; letter-spacing: -.01em;
    }
    .section-icon { font-size: 1.2rem; }
    .section-body { padding: 1rem 1.2rem; display: flex; flex-direction: column; gap: .55rem; }

    .fe .section-header  { background: var(--frontend-dim); color: var(--frontend); }
    .be .section-header  { background: var(--backend-dim);  color: var(--backend);  }
    .db .section-header  { background: var(--db-dim);       color: var(--db);       }
    .ext .section-header { background: var(--external-dim); color: var(--external); }
    .inf .section-header { background: var(--infra-dim);    color: var(--infra);    }

    .module {
      display: flex; align-items: flex-start; gap: .55rem; padding: .55rem .7rem;
      border-radius: 10px; background: var(--surface2); border: 1px solid var(--border);
      cursor: pointer; transition: all .2s; position: relative;
    }
    .module:hover { border-color: rgba(255,255,255,.18); background: rgba(255,255,255,.04); transform: translateX(2px); }
    .module-icon { font-size: 1rem; flex-shrink: 0; margin-top: .05rem; }
    .module-name { font-size: .8rem; font-weight: 600; line-height: 1.25; }
    .module-desc { font-size: .7rem; color: var(--muted); line-height: 1.4; margin-top: .1rem; }
    .module-tag {
      font-family: 'JetBrains Mono', monospace; font-size: .62rem; padding: .15rem .4rem;
      border-radius: 5px; margin-left: auto; flex-shrink: 0; margin-top: .05rem;
    }
    .fe .module-tag  { background: var(--frontend-dim); color: var(--frontend); }
    .be .module-tag  { background: var(--backend-dim);  color: var(--backend);  }
    .db .module-tag  { background: var(--db-dim);       color: var(--db);       }
    .ext .module-tag { background: var(--external-dim); color: var(--external); }

    .endpoints-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: .6rem; }
    .endpoint {
      display: flex; align-items: center; gap: .45rem; padding: .45rem .65rem;
      border-radius: 8px; background: var(--surface2); border: 1px solid var(--border);
      font-family: 'JetBrains Mono', monospace; font-size: .72rem; cursor: pointer; transition: all .2s;
    }
    .endpoint:hover { border-color: rgba(255,255,255,.18); background: rgba(255,255,255,.04); }
    .method { font-weight: 700; font-size: .62rem; padding: .1rem .35rem; border-radius: 4px; flex-shrink: 0; }
    .method.GET  { background: rgba(16,185,129,.2); color: #34d399; }
    .method.POST { background: rgba(99,102,241,.2); color: #a5b4fc; }
    .method.DEL  { background: rgba(239,68,68,.2);  color: #f87171; }
    .method.PUT  { background: rgba(245,158,11,.2); color: #fbbf24; }

    .routes-grid { display: grid; grid-template-columns: 1fr 1fr; gap: .5rem; }
    .route-item {
      display: flex; align-items: center; gap: .5rem; padding: .4rem .65rem;
      border-radius: 8px; background: var(--surface2); border: 1px solid var(--border);
      font-size: .75rem; transition: all .2s;
    }
    .route-item:hover { border-color: rgba(255,255,255,.14); }
    .route-badge { font-size: .62rem; padding: .1rem .35rem; border-radius: 4px; font-weight: 600; flex-shrink: 0; }
    .route-badge.public { background: rgba(16,185,129,.15); color: #34d399; }
    .route-badge.auth   { background: rgba(99,102,241,.15); color: #a5b4fc; }
    .route-badge.admin  { background: rgba(245,158,11,.15); color: #fbbf24; }

    .db-tables { display: flex; gap: 1rem; flex-wrap: wrap; }
    .db-table { flex: 1; min-width: 180px; border-radius: 10px; border: 1px solid var(--border); overflow: hidden; }
    .db-table-header {
      padding: .5rem .75rem; font-weight: 700; font-size: .78rem;
      background: var(--db-dim); color: var(--db); border-bottom: 1px solid var(--border);
    }
    .db-field {
      padding: .3rem .75rem; font-family: 'JetBrains Mono', monospace; font-size: .68rem;
      color: var(--muted); border-bottom: 1px solid var(--border); display: flex; gap: .4rem;
    }
    .db-field:last-child { border-bottom: none; }
    .field-type { color: var(--db); font-size: .62rem; }
    .pk { color: #fbbf24; }

    .flow-steps { display: flex; gap: 0; overflow-x: auto; padding-bottom: .5rem; }
    .flow-step { display: flex; flex-direction: column; align-items: center; position: relative; flex: 1; min-width: 110px; }
    .flow-step:not(:last-child)::after {
      content: '→'; position: absolute; right: -10px; top: 18px; color: var(--muted); font-size: 1.2rem; z-index: 1;
    }
    .flow-bubble {
      width: 44px; height: 44px; border-radius: 12px; display: flex; align-items: center;
      justify-content: center; font-size: 1.3rem; border: 2px solid; background: var(--surface2); transition: transform .2s;
    }
    .flow-bubble:hover { transform: scale(1.1); }
    .flow-label { margin-top: .4rem; font-size: .68rem; font-weight: 600; text-align: center; color: var(--muted); }
    .flow-sub { font-size: .6rem; color: #55557a; text-align: center; margin-top: .15rem; }

    .flow-bubble.fe  { border-color: var(--frontend);  color: var(--frontend);  }
    .flow-bubble.be  { border-color: var(--backend);   color: var(--backend);   }
    .flow-bubble.ext { border-color: var(--external);  color: var(--external);  }
    .flow-bubble.db  { border-color: var(--db);        color: var(--db);        }
    .flow-bubble.inf { border-color: var(--infra);     color: var(--infra);     }

    .tech-grid { display: flex; gap: .5rem; flex-wrap: wrap; }
    .tech-chip {
      padding: .4rem .8rem; border-radius: 8px; font-size: .75rem; font-weight: 600;
      background: var(--surface2); border: 1px solid var(--border); color: var(--muted); transition: all .2s;
    }
    .tech-chip:hover { color: var(--text); border-color: rgba(255,255,255,.18); }
    .tech-chip span { margin-right: .3rem; }

    .sep-label {
      display: flex; align-items: center; gap: 1rem; color: var(--muted);
      font-size: .78rem; font-weight: 600; letter-spacing: .05em; text-transform: uppercase;
    }
    .sep-label::before, .sep-label::after { content: ''; flex: 1; height: 1px; background: var(--border); }

    @media (max-width: 768px) {
      header, main, .legend { padding-left: 1.2rem; padding-right: 1.2rem; }
      header h1 { font-size: 1.6rem; }
      .routes-grid { grid-template-columns: 1fr; }
      .db-tables { flex-direction: column; }
    }
  </style>
</head>
<body>

<header>
  <h1>⚡ DataViz — Architecture Scheme</h1>
  <p>Full-stack SaaS data visualization platform · React + FastAPI · v3.0.0</p>
  <div class="badges">
    <span class="badge fe">React + Vite</span>
    <span class="badge be">FastAPI · Python</span>
    <span class="badge db">SQLite / PostgreSQL</span>
    <span class="badge ext">Firebase Auth</span>
    <span class="badge ext">Google Gemini AI</span>
    <span class="badge inf">JWT · CORS · HTTPS</span>
  </div>
</header>

<div class="legend">
  <div class="legend-item"><div class="legend-dot" style="background:var(--frontend)"></div> Frontend (React)</div>
  <div class="legend-item"><div class="legend-dot" style="background:var(--backend)"></div> Backend (FastAPI)</div>
  <div class="legend-item"><div class="legend-dot" style="background:var(--db)"></div> Database / Storage</div>
  <div class="legend-item"><div class="legend-dot" style="background:var(--external)"></div> External Services</div>
  <div class="legend-item"><div class="legend-dot" style="background:var(--infra)"></div> Infrastructure / Security</div>
</div>

<main>

  <!-- DATA FLOW -->
  <div class="sep-label">🔄 Request Data Flow</div>

  <div style="background:var(--surface); border:1px solid var(--border); border-radius:16px; padding:1.4rem 1.2rem;">
    <div class="flow-steps">
      <div class="flow-step">
        <div class="flow-bubble fe">🌐</div>
        <div class="flow-label">User Browser</div>
        <div class="flow-sub">React + Vite</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble fe">🔑</div>
        <div class="flow-label">Auth Check</div>
        <div class="flow-sub">JWT / Firebase</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble inf">📡</div>
        <div class="flow-label">API Layer</div>
        <div class="flow-sub">api.js / CORS</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble be">⚙️</div>
        <div class="flow-label">FastAPI Server</div>
        <div class="flow-sub">Uvicorn ASGI</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble be">🗂️</div>
        <div class="flow-label">Routers</div>
        <div class="flow-sub">auth/stats/ai…</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble be">🧠</div>
        <div class="flow-label">Services</div>
        <div class="flow-sub">engine/anomaly…</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble db">💾</div>
        <div class="flow-label">Database</div>
        <div class="flow-sub">SQLite/Postgres</div>
      </div>
      <div class="flow-step">
        <div class="flow-bubble ext">🤖</div>
        <div class="flow-label">External APIs</div>
        <div class="flow-sub">Gemini · Firebase</div>
      </div>
    </div>
  </div>

  <!-- SYSTEM OVERVIEW -->
  <div class="sep-label">🏗️ System Overview</div>

  <div class="flow-row">

    <div class="section-card fe">
      <div class="section-header"><span class="section-icon">🖥️</span> Frontend — React + Vite</div>
      <div class="section-body">
        <div class="module">
          <span class="module-icon">🔐</span>
          <div><div class="module-name">Auth Layer</div><div class="module-desc">AuthContext, ProtectedRoute, firebase.js · JWT token handling</div></div>
          <span class="module-tag">auth/</span>
        </div>
        <div class="module">
          <span class="module-icon">🌍</span>
          <div><div class="module-name">Context Providers</div><div class="module-desc">DataContext (dataset state) · ThemeContext (dark/light)</div></div>
          <span class="module-tag">context/</span>
        </div>
        <div class="module">
          <span class="module-icon">📡</span>
          <div><div class="module-name">API Client</div><div class="module-desc">Axios instance · api.js, contact.js, gemini.js</div></div>
          <span class="module-tag">api/</span>
        </div>
        <div class="module">
          <span class="module-icon">🪝</span>
          <div><div class="module-name">Custom Hooks</div><div class="module-desc">useAIAnalysis · useSmartCleaning</div></div>
          <span class="module-tag">hooks/</span>
        </div>
        <div class="module">
          <span class="module-icon">⚙️</span>
          <div><div class="module-name">Client Services</div><div class="module-desc">aiAdvisorService · ruleEngine (data-cleaning rules)</div></div>
          <span class="module-tag">services/</span>
        </div>
      </div>
    </div>

    <div class="arrow-h">⟺</div>

    <div class="section-card be">
      <div class="section-header"><span class="section-icon">🐍</span> Backend — FastAPI v3.0</div>
      <div class="section-body">
        <div class="module">
          <span class="module-icon">🗄️</span>
          <div><div class="module-name">App Core (app/)</div><div class="module-desc">models, database, user_store, data_context, dataset_manager, cache</div></div>
          <span class="module-tag">app/</span>
        </div>
        <div class="module">
          <span class="module-icon">🔀</span>
          <div><div class="module-name">Routers (10 modules)</div><div class="module-desc">auth · admin · stats · analyze · charts · ai_advisor · firebase_auth · gemini · profiling · contact</div></div>
          <span class="module-tag">routers/</span>
        </div>
        <div class="module">
          <span class="module-icon">🧩</span>
          <div><div class="module-name">Services (7 modules)</div><div class="module-desc">engine · anomaly · quality_score · stats_service · chart_service · analyzer_service · main</div></div>
          <span class="module-tag">services/</span>
        </div>
        <div class="module">
          <span class="module-icon">🛡️</span>
          <div><div class="module-name">Utils</div><div class="module-desc">security (bcrypt, JWT) · file_utils</div></div>
          <span class="module-tag">utils/</span>
        </div>
        <div class="module">
          <span class="module-icon">🔧</span>
          <div><div class="module-name">Core Config</div><div class="module-desc">config · firebase_config · supabase_client</div></div>
          <span class="module-tag">core/</span>
        </div>
      </div>
    </div>

    <div class="arrow-h">⟺</div>

    <div class="section-card ext">
      <div class="section-header"><span class="section-icon">☁️</span> External Services</div>
      <div class="section-body">
        <div class="module">
          <span class="module-icon">🔥</span>
          <div><div class="module-name">Firebase Auth</div><div class="module-desc">Google OAuth · email/password · firebase-admin SDK</div></div>
          <span class="module-tag">ext</span>
        </div>
        <div class="module">
          <span class="module-icon">🤖</span>
          <div><div class="module-name">Google Gemini AI</div><div class="module-desc">AI chat assistant · AI advisor · data insights generation</div></div>
          <span class="module-tag">ext</span>
        </div>
        <div class="module">
          <span class="module-icon">📦</span>
          <div><div class="module-name">Supabase (optional)</div><div class="module-desc">Remote PostgreSQL backend · file storage</div></div>
          <span class="module-tag">ext</span>
        </div>
        <div class="module">
          <span class="module-icon">⚡</span>
          <div><div class="module-name">Redis Cache</div><div class="module-desc">In-memory dataset cache · session TTL</div></div>
          <span class="module-tag">ext</span>
        </div>
      </div>
    </div>

  </div>

  <!-- PAGES & ROUTES -->
  <div class="sep-label">📄 Frontend Pages &amp; Routes</div>

  <div style="background:var(--surface); border:1px solid var(--border); border-radius:16px; padding:1.4rem 1.2rem;">
    <div class="routes-grid">
      <div class="route-item"><span class="route-badge public">public</span> / — Home Page</div>
      <div class="route-item"><span class="route-badge public">public</span> /about — About</div>
      <div class="route-item"><span class="route-badge public">public</span> /login — Auth (Login / Register)</div>
      <div class="route-item"><span class="route-badge public">public</span> /forgot-password</div>
      <div class="route-item"><span class="route-badge public">public</span> /features — Features</div>
      <div class="route-item"><span class="route-badge public">public</span> /pricing — Pricing</div>
      <div class="route-item"><span class="route-badge public">public</span> /faq, /contact</div>
      <div class="route-item"><span class="route-badge public">public</span> /privacy, /terms, /cookies</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /upload — File Upload</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /dashboard — Main Dashboard</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /analytics — Analytics</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /stats — CSV Stats</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /data-quality — Data Quality</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /3d-visualizations — 3D Charts</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /model — ML Model Builder</div>
      <div class="route-item"><span class="route-badge auth">auth</span> /user — Profile</div>
      <div class="route-item"><span class="route-badge admin">admin</span> /admin — Admin Panel</div>
      <div class="route-item"><span class="route-badge public">404</span> * — Not Found</div>
    </div>
  </div>

  <!-- COMPONENTS -->
  <div class="sep-label">🧱 Key Frontend Components</div>

  <div class="flow-row" style="flex-wrap:wrap; gap:1rem;">

    <div class="section-card fe" style="flex:0 0 auto; width:215px;">
      <div class="section-header"><span class="section-icon">🤖</span> AIAdvisor</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">💬</span><div><div class="module-name">AIChatAssistant</div></div></div>
        <div class="module"><span class="module-icon">📋</span><div><div class="module-name">AIAdvisorPanel</div></div></div>
        <div class="module"><span class="module-icon">🚨</span><div><div class="module-name">IssueCard</div></div></div>
        <div class="module"><span class="module-icon">🎯</span><div><div class="module-name">MLReadinessScore</div></div></div>
        <div class="module"><span class="module-icon">🔧</span><div><div class="module-name">SmartFixButton</div></div></div>
      </div>
    </div>

    <div class="section-card fe" style="flex:0 0 auto; width:215px;">
      <div class="section-header"><span class="section-icon">📊</span> DataQuality</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">🔍</span><div><div class="module-name">ColumnProfiler</div></div></div>
        <div class="module"><span class="module-icon">📈</span><div><div class="module-name">QualityMetrics</div></div></div>
        <div class="module"><span class="module-icon">💡</span><div><div class="module-name">RecommendationEngine</div></div></div>
      </div>
    </div>

    <div class="section-card fe" style="flex:0 0 auto; width:215px;">
      <div class="section-header"><span class="section-icon">📉</span> Charts &amp; Viz</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">🎨</span><div><div class="module-name">ChartBuilder</div></div></div>
        <div class="module"><span class="module-icon">📦</span><div><div class="module-name">ChartContainer</div></div></div>
        <div class="module"><span class="module-icon">🐍</span><div><div class="module-name">MatplotlibChart</div></div></div>
        <div class="module"><span class="module-icon">🌡️</span><div><div class="module-name">HeatmapDisplay</div></div></div>
      </div>
    </div>

    <div class="section-card fe" style="flex:0 0 auto; width:215px;">
      <div class="section-header"><span class="section-icon">🧹</span> Data Tools</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">🛠️</span><div><div class="module-name">CleaningToolbar</div></div></div>
        <div class="module"><span class="module-icon">🤖</span><div><div class="module-name">AutoCleanAgent</div></div></div>
        <div class="module"><span class="module-icon">📝</span><div><div class="module-name">ExcelGrid</div></div></div>
        <div class="module"><span class="module-icon">📤</span><div><div class="module-name">FileUploader</div></div></div>
      </div>
    </div>

    <div class="section-card fe" style="flex:0 0 auto; width:215px;">
      <div class="section-header"><span class="section-icon">🧮</span> Stats &amp; Models</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">📊</span><div><div class="module-name">StatsPanel</div></div></div>
        <div class="module"><span class="module-icon">📋</span><div><div class="module-name">CsvStatsTable</div></div></div>
        <div class="module"><span class="module-icon">📐</span><div><div class="module-name">DescriptiveStatsTable</div></div></div>
        <div class="module"><span class="module-icon">🤖</span><div><div class="module-name">ModelBuilderSection</div></div></div>
        <div class="module"><span class="module-icon">🔮</span><div><div class="module-name">PredictionSection</div></div></div>
      </div>
    </div>

  </div>

  <!-- API ENDPOINTS -->
  <div class="sep-label">🔌 Backend API Endpoints</div>

  <div style="background:var(--surface); border:1px solid var(--border); border-radius:16px; padding:1.4rem 1.2rem;">
    <div class="endpoints-grid">
      <div class="endpoint"><span class="method POST">POST</span> /api/auth/login</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/auth/register</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/auth/refresh</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/auth/firebase</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/analyze/upload</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/analyze/info</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/analyze/preview</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/analyze/reset</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/stats/describe</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/stats/correlation</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/stats/distribution</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/stats/outliers</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/charts/build</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/charts/matplotlib</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/ai-advisor/analyze</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/ai-advisor/chat</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/ai-advisor/fix</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/gemini/chat</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/profiling/report</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/admin/users</div>
      <div class="endpoint"><span class="method DEL">DEL</span> /api/admin/users/{id}</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/admin/metrics</div>
      <div class="endpoint"><span class="method GET">GET</span> /api/health</div>
      <div class="endpoint"><span class="method POST">POST</span> /api/contact</div>
    </div>
  </div>

  <!-- DATABASE SCHEMA -->
  <div class="sep-label">🗄️ Database Schema</div>

  <div class="db-tables">

    <div class="db-table">
      <div class="db-table-header">👤 users</div>
      <div class="db-field"><span class="pk">id</span><span class="field-type">UUID PK</span></div>
      <div class="db-field">firebase_uid<span class="field-type">VARCHAR?</span></div>
      <div class="db-field">name<span class="field-type">VARCHAR</span></div>
      <div class="db-field">email<span class="field-type">VARCHAR UNIQUE</span></div>
      <div class="db-field">password_hash<span class="field-type">VARCHAR?</span></div>
      <div class="db-field">role<span class="field-type">user/admin</span></div>
      <div class="db-field">is_active<span class="field-type">BOOL</span></div>
      <div class="db-field">uploads<span class="field-type">INT</span></div>
      <div class="db-field">api_calls_count<span class="field-type">INT</span></div>
      <div class="db-field">last_login<span class="field-type">DATETIME</span></div>
    </div>

    <div class="db-table">
      <div class="db-table-header">📁 datasets</div>
      <div class="db-field"><span class="pk">id</span><span class="field-type">UUID PK</span></div>
      <div class="db-field">user_id<span class="field-type">FK→users</span></div>
      <div class="db-field">filename<span class="field-type">VARCHAR</span></div>
      <div class="db-field">file_path<span class="field-type">TEXT</span></div>
      <div class="db-field">rows<span class="field-type">INT</span></div>
      <div class="db-field">columns<span class="field-type">INT</span></div>
      <div class="db-field">file_size<span class="field-type">BIGINT</span></div>
      <div class="db-field">created_at<span class="field-type">DATETIME</span></div>
    </div>

    <div class="db-table">
      <div class="db-table-header">🔑 sessions</div>
      <div class="db-field"><span class="pk">id</span><span class="field-type">UUID PK</span></div>
      <div class="db-field">user_id<span class="field-type">FK→users</span></div>
      <div class="db-field">token<span class="field-type">TEXT</span></div>
      <div class="db-field">expires_at<span class="field-type">DATETIME</span></div>
      <div class="db-field">is_revoked<span class="field-type">BOOL</span></div>
      <div class="db-field">created_at<span class="field-type">DATETIME</span></div>
    </div>

    <div class="db-table">
      <div class="db-table-header">📋 activity_logs</div>
      <div class="db-field"><span class="pk">id</span><span class="field-type">INT PK</span></div>
      <div class="db-field">user_id<span class="field-type">FK→users</span></div>
      <div class="db-field">action<span class="field-type">VARCHAR</span></div>
      <div class="db-field">resource<span class="field-type">VARCHAR</span></div>
      <div class="db-field">details<span class="field-type">JSON</span></div>
      <div class="db-field">ip_address<span class="field-type">VARCHAR</span></div>
      <div class="db-field">created_at<span class="field-type">DATETIME</span></div>
    </div>

  </div>

  <!-- BACKEND SERVICES -->
  <div class="sep-label">🧠 Backend Services Layer</div>

  <div class="flow-row">

    <div class="section-card be">
      <div class="section-header"><span class="section-icon">⚙️</span> Analysis Engine</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">🚂</span><div><div class="module-name">engine.py</div><div class="module-desc">Core data processing pipeline · Pandas/Polars</div></div></div>
        <div class="module"><span class="module-icon">🔍</span><div><div class="module-name">analyzer_service.py</div><div class="module-desc">Column type inference · data profiling</div></div></div>
        <div class="module"><span class="module-icon">📊</span><div><div class="module-name">stats_service.py</div><div class="module-desc">Descriptive stats · correlation · distribution</div></div></div>
        <div class="module"><span class="module-icon">🎨</span><div><div class="module-name">chart_service.py</div><div class="module-desc">Plotly / Matplotlib chart generation</div></div></div>
      </div>
    </div>

    <div class="section-card be">
      <div class="section-header"><span class="section-icon">🔬</span> Quality &amp; AI</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">⭐</span><div><div class="module-name">quality_score.py</div><div class="module-desc">Data quality scoring · completeness · consistency</div></div></div>
        <div class="module"><span class="module-icon">🚨</span><div><div class="module-name">anomaly.py</div><div class="module-desc">Anomaly detection · outlier flagging</div></div></div>
        <div class="module"><span class="module-icon">🤖</span><div><div class="module-name">ai_advisor.py</div><div class="module-desc">Gemini-powered analysis · chat · auto-fix</div></div></div>
        <div class="module"><span class="module-icon">📊</span><div><div class="module-name">stats.py</div><div class="module-desc">87 KB · Comprehensive statistics module</div></div></div>
      </div>
    </div>

    <div class="section-card be">
      <div class="section-header"><span class="section-icon">🔐</span> Auth &amp; Admin</div>
      <div class="section-body">
        <div class="module"><span class="module-icon">🔑</span><div><div class="module-name">routers/auth.py</div><div class="module-desc">Register / login / refresh · bcrypt + PyJWT</div></div></div>
        <div class="module"><span class="module-icon">🔥</span><div><div class="module-name">firebase_auth.py</div><div class="module-desc">Firebase token verify · user sync</div></div></div>
        <div class="module"><span class="module-icon">🛡️</span><div><div class="module-name">admin.py</div><div class="module-desc">User management · metrics · activity logs</div></div></div>
        <div class="module"><span class="module-icon">🔒</span><div><div class="module-name">utils/security.py</div><div class="module-desc">Password hashing · JWT encode/decode</div></div></div>
      </div>
    </div>

  </div>

  <!-- INFRASTRUCTURE -->
  <div class="sep-label">🏛️ Infrastructure &amp; Security</div>

  <div style="background:var(--surface); border:1px solid var(--border); border-radius:16px; padding:1.4rem 1.2rem;">
    <div class="tech-grid">
      <div class="tech-chip"><span>🔄</span> CORS Middleware</div>
      <div class="tech-chip"><span>🔒</span> HTTPS Redirect (prod)</div>
      <div class="tech-chip"><span>🛡️</span> XSS / CSRF Headers</div>
      <div class="tech-chip"><span>⏱️</span> Request Logging</div>
      <div class="tech-chip"><span>🚫</span> Global Exception Handler</div>
      <div class="tech-chip"><span>🔑</span> JWT Auth (PyJWT)</div>
      <div class="tech-chip"><span>🔐</span> bcrypt Password Hashing</div>
      <div class="tech-chip"><span>🔥</span> Firebase Admin SDK</div>
      <div class="tech-chip"><span>⚡</span> Redis In-Memory Cache</div>
      <div class="tech-chip"><span>📄</span> SQLAlchemy ORM</div>
      <div class="tech-chip"><span>🐘</span> PostgreSQL (prod)</div>
      <div class="tech-chip"><span>🗂️</span> SQLite (dev)</div>
      <div class="tech-chip"><span>🔢</span> Pagination Headers</div>
      <div class="tech-chip"><span>📋</span> OpenAPI / Swagger Docs</div>
      <div class="tech-chip"><span>🌐</span> Uvicorn ASGI</div>
      <div class="tech-chip"><span>🌱</span> dotenv Config</div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="sep-label">📦 Technology Stack</div>

  <div class="flow-row">

    <div class="section-card fe">
      <div class="section-header"><span class="section-icon">🖥️</span> Frontend Stack</div>
      <div class="section-body">
        <div class="tech-grid">
          <div class="tech-chip"><span>⚛️</span> React 18</div>
          <div class="tech-chip"><span>⚡</span> Vite</div>
          <div class="tech-chip"><span>🎨</span> TailwindCSS</div>
          <div class="tech-chip"><span>🔀</span> React Router v6</div>
          <div class="tech-chip"><span>📡</span> Axios</div>
          <div class="tech-chip"><span>🔥</span> Firebase SDK</div>
          <div class="tech-chip"><span>📊</span> Plotly.js</div>
          <div class="tech-chip"><span>🌙</span> Dark/Light Theme</div>
        </div>
      </div>
    </div>

    <div class="section-card be">
      <div class="section-header"><span class="section-icon">🐍</span> Backend Stack</div>
      <div class="section-body">
        <div class="tech-grid">
          <div class="tech-chip"><span>🚀</span> FastAPI</div>
          <div class="tech-chip"><span>🌐</span> Uvicorn</div>
          <div class="tech-chip"><span>🐼</span> Pandas</div>
          <div class="tech-chip"><span>🔢</span> NumPy</div>
          <div class="tech-chip"><span>⚡</span> Polars</div>
          <div class="tech-chip"><span>📊</span> Plotly</div>
          <div class="tech-chip"><span>🐍</span> Matplotlib</div>
          <div class="tech-chip"><span>🧬</span> SciPy</div>
          <div class="tech-chip"><span>🤖</span> scikit-learn</div>
          <div class="tech-chip"><span>🔍</span> rapidfuzz</div>
        </div>
      </div>
    </div>

    <div class="section-card ext">
      <div class="section-header"><span class="section-icon">☁️</span> External / AI</div>
      <div class="section-body">
        <div class="tech-grid">
          <div class="tech-chip"><span>🤖</span> Google Gemini AI</div>
          <div class="tech-chip"><span>🔥</span> Firebase Auth</div>
          <div class="tech-chip"><span>📦</span> Supabase</div>
          <div class="tech-chip"><span>⚡</span> Redis</div>
          <div class="tech-chip"><span>🐘</span> PostgreSQL</div>
        </div>
      </div>
    </div>

  </div>

  <div style="height:2rem"></div>

  <footer style="text-align:center; color:var(--muted); font-size:.78rem; padding:1rem 0 2rem; border-top:1px solid var(--border);">
    DataViz Architecture Scheme · FastAPI v3.0.0 + React 18 + Vite
  </footer>

</main>

<script>
  document.querySelectorAll('.endpoint, .module').forEach(el => {
    el.addEventListener('click', () => {
      el.style.outline = '2px solid rgba(165,180,252,.6)';
      setTimeout(() => el.style.outline = '', 1200);
    });
  });
</script>

</body>
</html>

