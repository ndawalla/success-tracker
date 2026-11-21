&lt;!doctype html&gt;
&lt;html lang=&quot;en&quot; class=&quot;dark&quot;&gt;
&lt;head&gt;
  &lt;meta charset=&quot;UTF-8&quot; /&gt;
  &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0, viewport-fit=cover&quot; /&gt;
  &lt;title&gt;Success Tracker + Baba AI — Live Interactive Preview&lt;/title&gt;
  &lt;script src=&quot;\[suspicious link removed\]&quot;&gt;&lt;/script&gt;
  &lt;script&gt;
    tailwind.config = {
      darkMode: &#39;class&#39;,
      theme: {
        extend: {
          fontFamily: { sans: [&#39;Inter&#39;, &#39;system-ui&#39;, &#39;-apple-system&#39;, &#39;sans-serif&#39;] }
        }
      }
    };
  &lt;/script&gt;
  &lt;style&gt;
    html, body { overscroll-behavior-y: contain; font-family: Inter, system-ui, -apple-system, sans-serif; }
    .glass-card {
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      background: rgba(255, 255, 255, 0.78);
      border: 1px solid rgba(255, 255, 255, 0.65);
      box-shadow: 0 8px 28px rgba(15, 23, 42, 0.14);
    }
    .dark .glass-card {
      background: rgba(15, 23, 42, 0.68);
      border: 1px solid rgba(255, 255, 255, 0.16);
      box-shadow: 0 8px 28px rgba(0, 0, 0, 0.42);
    }
    .glass-pill {
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      background: rgba(255, 255, 255, 0.8);
      border: 1px solid rgba(255, 255, 255, 0.65);
    }
    .dark .glass-pill {
      background: rgba(30, 41, 59, 0.75);
      border: 1px solid rgba(255, 255, 255, 0.18);
    }
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-thumb { background: rgba(148,163,184,0.45); border-radius: 9999px; }
  &lt;/style&gt;
&lt;/head&gt;
&lt;body class=&quot;min-h-screen text-slate-900 dark:text-slate-100 antialiased&quot;&gt;
  &lt;!-- Background Layers --&gt;
  &lt;div id=&quot;bg-layer&quot; class=&quot;fixed inset-0 -z-20 transition-all duration-300&quot;&gt;&lt;/div&gt;
  &lt;div id=&quot;overlay-layer&quot; class=&quot;fixed inset-0 -z-10 transition-colors duration-300&quot;&gt;&lt;/div&gt;

  &lt;!-- Toast Container --&gt;
  &lt;div id=&quot;toast-box&quot; class=&quot;fixed top-4 right-4 z-50 flex flex-col gap-2 max-w-xs w-full pointer-events-none px-2&quot;&gt;&lt;/div&gt;

  &lt;!-- In-page Modal --&gt;
  &lt;div id=&quot;modal-root&quot; class=&quot;hidden fixed inset-0 z-50 flex items-center justify-center bg-slate-950/65 backdrop-blur-sm p-4&quot;&gt;&lt;/div&gt;

  &lt;!-- App Shell --&gt;
  &lt;div class=&quot;flex min-h-screen max-w-6xl mx-auto&quot;&gt;
    &lt;!-- Desktop Sidebar --&gt;
    &lt;aside class=&quot;hidden lg:flex flex-col w-60 shrink-0 p-4 gap-3&quot;&gt;
      &lt;div class=&quot;glass-card rounded-3xl p-4 flex items-center gap-3&quot;&gt;
        &lt;div id=&quot;brand-badge-side&quot; class=&quot;w-11 h-11 rounded-full flex items-center justify-center text-white font-bold shadow border-2 border-white/60 shrink-0&quot;&gt;☸&lt;/div&gt;
        &lt;div class=&quot;min-w-0&quot;&gt;
          &lt;div class=&quot;font-extrabold text-sm tracking-tight truncate&quot;&gt;SUCCESS TRACKER&lt;/div&gt;
          &lt;div class=&quot;text-[11px] opacity-80 truncate&quot;&gt;जय हिन्द 🇮🇳 • Baba AI&lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;nav id=&quot;desktop-nav&quot; class=&quot;glass-card rounded-3xl p-2.5 flex-1 flex flex-col gap-1&quot;&gt;&lt;/nav&gt;
      &lt;div class=&quot;glass-card rounded-3xl p-3 text-xs space-y-1&quot;&gt;
        &lt;div class=&quot;font-bold&quot;&gt;Interactive Preview&lt;/div&gt;
        &lt;div class=&quot;text-[11px] opacity-75&quot;&gt;Changes save locally in this browser. Deploy zip to Vercel + Firebase for cloud sync.&lt;/div&gt;
      &lt;/div&gt;
    &lt;/aside&gt;

    <!-- Main Content Column -->
    <div class="flex-1 flex flex-col min-w-0 pb-24 lg:pb-8">
      <!-- Sticky Top Header -->
      <header class="sticky top-0 z-30 px-3 pt-3 pb-2 lg:px-5 lg:pt-4">
        <div class="glass-card rounded-3xl px-4 py-3 flex items-center justify-between gap-2">
          <div class="flex items-center gap-3 min-w-0">
            <div id="brand-badge-top" class="w-10 h-10 rounded-full flex items-center justify-center text-white font-bold shadow border-2 border-white/60 shrink-0">☸</div>
            <div class="min-w-0">
              <h1 class="font-extrabold text-base sm:text-lg leading-tight truncate">SUCCESS TRACKER</h1>
              <p class="text-[11px] sm:text-xs opacity-80 truncate">जय हिन्द 🇮🇳 • Exam Preparation</p>
            </div>
          </div>
          <div class="flex items-center gap-2 shrink-0">
            <span id="header-exam-pill" class="px-3 py-1 rounded-full text-xs font-bold text-white shadow">IAF</span>
            <button id="btn-quick-theme" class="glass-pill px-2.5 py-1.5 rounded-full text-xs font-bold" title="Toggle Light/Dark">🌙</button>
          </div>
        </div>
      </header>

      <!-- Main View -->
      <main id="main-view" class="flex-1 px-3 sm:px-4 lg:px-5 pt-2"></main>
    </div>
  &lt;/div&gt;

  &lt;!-- Mobile Bottom Navigation --&gt;
  &lt;nav id=&quot;mobile-nav&quot; class=&quot;lg:hidden fixed bottom-2 left-2 right-2 z-30 glass-card rounded-3xl px-1.5 py-1.5 flex items-center justify-around&quot;&gt;&lt;/nav&gt;

&lt;script&gt;
(function() {
  // ===== DATA: MASTER SYLLABUS (Starter — Verification Pending) =====
  const makeChapters = (prefix, names) =&gt; names.map((name, i) =&gt; ({
    id: `${prefix}-ch-${String(i+1).padStart(2,&#39;0&#39;)}`,
    name,
    order: i + 1,
    status: &#39;not_started&#39;,
    resources: { pw: false, rwa: false, youtube: false, tests: false },
    notes: &#39;&#39;,
    priority: &#39;medium&#39;,
    difficulty: &#39;medium&#39;,
    targetDate: &#39;&#39;,
    revisionCount: 0,
    lastRevisedAt: &#39;&#39;
  }));

  const GAT_SUBJECTS = [
    { id: &#39;gat-polity&#39;, name: &#39;Polity&#39;, chapters: makeChapters(&#39;gat-pol&#39;, [
      &#39;Making of Indian Constitution&#39;,&#39;Constitutent Assembly&#39;,&#39;Schdules of Indian Constitution&#39;,
      &#39;Borrrowing Features of Indian Constitution&#39;,&#39;Salient Features of Constitution&#39;,&#39;Preamble&#39;,
      &#39;Fundamental Rights&#39;,&#39;Writs &amp; Fundamental Duties&#39;,&#39;DPSP&#39;,&#39;Union &amp; Citizenship&#39;,&#39;Parliment&#39;,
      &#39;State Lagislature&#39;,&#39;Election Process&#39;,&#39;CAG &amp; AGI&#39;,&#39;PRESIDENT&#39;,&#39;Vice President &amp; Governor&#39;,
      &#39;Panchayat Raj &amp; Muncipalities&#39;,&#39;Amendments &amp; Panchsheel&#39;,&#39;SC &amp; HC&#39;
    ])},
    { id: &#39;gat-geo&#39;, name: &#39;Geography&#39;, chapters: makeChapters(&#39;gat-geo&#39;, [
      &#39;Universe&#39;,&#39;Solar System&#39;,&#39;Latitude Longitude&#39;,&#39;Interior of the Earth&#39;,&#39;Plate Tectonism&#39;,
      &#39;Geomorphic Process&#39;,&#39;Earthquake Volcano&#39;,&#39;Atmosphere&#39;,&#39;Temperature&#39;,&#39;Pressure Belt&#39;,&#39;Winds&#39;,
      &#39;Humidity Condensation&#39;,&#39;Condensation Precipitation&#39;,&#39;Cyclone&#39;,
      &#39;World Climatic Region and Moment of Ocean Water&#39;,&#39;Season Of India&#39;,&#39;Physiography of India&#39;,
      &#39;Drainage of India&#39;,&#39;Natural Vegetation of India&#39;,&#39;Soil of India and Agriculture of India&#39;,
      &#39;Minerals and the Industry of India&#39;,&#39;Population and Transport of India&#39;,&#39;World geography&#39;
    ])},
    { id: &#39;gat-bio&#39;, name: &#39;Biology&#39;, chapters: makeChapters(&#39;gat-bio&#39;, [
      &#39;Cell&#39;,&#39;Tissues&#39;,&#39;Life Processes&#39;,&#39;Control and Coordination&#39;,&#39;Reproduction&#39;,&#39;Diversity&#39;,
      &#39;Human Health and Diseases&#39;,&#39;Important Vitamins and Minerals&#39;,&#39;Genetics&#39;
    ])},
    { id: &#39;gat-hist&#39;, name: &#39;History&#39;, chapters: makeChapters(&#39;gat-hist&#39;, [
      &#39;Origin of Humans&#39;,&#39;Indus Valley Civilization&#39;,&#39;Vedic Civilization&#39;,&#39;Mahajanpada&#39;,
      &#39;Mauryan Empire&#39;,&#39;Post Mauryan Age&#39;,&#39;Gupta Empire&#39;,&#39;Post Gupta Age&#39;,&#39;Rajput Period&#39;,
      &#39;Triplite Struggle and Chola Empire&#39;,&#39;Establishment of Sultanate&#39;,&#39;Decline of Sultanate&#39;,
      &#39;Bhakti Movement&#39;,&#39;Vijaynagar Empire&#39;,&#39;Rise of Mughals and Sher Shah Suri&#39;,
      &#39;Expansion of Mughal Empire&#39;,&#39;Aurangzeb and Decline of Mughals&#39;,
      &#39;The Rise of Maratha Empire Under Shivaji&#39;,&#39;Arrival of Europeans in India&#39;,
      &#39;British Conquest in India&#39;,&#39;Early Revolts Against British Rule&#39;,&#39;Revolt of 1857&#39;,
      &#39;Indian Renaissance&#39;,&#39;India Between 1911 – 1930&#39;,&#39;Rise of political Activsm&#39;,
      &#39;India Between 1930 – 1940&#39;,&#39;India Between 1940 – 1947&#39;,&#39;Revolutionary&#39;,
      &#39;British Legislature&#39;,&#39;World History&#39;
    ])},
    { id: &#39;gat-phy&#39;, name: &#39;Physics (GAT)&#39;, chapters: makeChapters(&#39;gat-phy&#39;, [
      &#39;Unit and Measurement&#39;,&#39;Motion in 1 D&#39;,&quot;Newton&#39;s Law of Motion&quot;,&#39;Friction&#39;,&#39;Relative Velocity&#39;,
      &#39;Average Velocity&#39;,&#39;Projectile Motion&#39;,&#39;Work, Power, Energy&#39;,&#39;Basics of Rotational Motion&#39;,
      &#39;Gravitation&#39;,&#39;Sound and Waves&#39;,&#39;Current Electricity&#39;,&#39;Electrostatics&#39;,&#39;Electromagnetism&#39;,
      &#39;Light&#39;,&#39;Heat and Thermodynamics&#39;,&#39;Hydrodynamics&#39;
    ])}
  ];

  const cloneSubjects = (subs, examPrefix) =&gt; subs.map(s =&gt; ({
    ...s,
    id: `${examPrefix}__${s.id}`,
    chapters: s.chapters.map(c =&gt; ({ ...c, id: `${examPrefix}__${c.id}`, resources: { ...c.resources } }))
  }));

  const DEFAULT_EXAMS = [
    {
      id: &#39;iaf-xy&#39;, code: &#39;IAF&#39;, name: &#39;Air Force X &amp; Y Group — Combined Starter Syllabus&#39;,
      verificationNote: &#39;Starter syllabus — verification pending&#39;,
      subjects: [
        { id: &#39;iaf-eng&#39;, name: &#39;English&#39;, chapters: makeChapters(&#39;iaf-eng&#39;, [
          &#39;Noun&#39;,&#39;Pronoun&#39;,&#39;Adjective&#39;,&#39;Article&#39;,&#39;Conjunction&#39;,&#39;Adverb&#39;,&#39;Preposition&#39;,
          &#39;Subject Verb Agreement&#39;,&#39;Verb&#39;,&#39;Tense&#39;,&#39;Question Tag&#39;,&#39;Narration&#39;,&#39;Para Jumbles&#39;,
          &#39;Comprehension&#39;,&#39;Word Formation&#39;,&#39;Vocabulary&#39;,&#39;Practice Session&#39;
        ])},
        { id: &#39;iaf-phy&#39;, name: &#39;Physics&#39;, chapters: makeChapters(&#39;iaf-phy&#39;, [
          &#39;Unit and Dimensions&#39;,&#39;Vector Scalar&#39;,&#39;Motion in Straight Line&#39;,
          &#39;Graph or Numerical Approach (Basics)&#39;,&#39;Law of Motion&#39;,&#39;Projectile Motion&#39;,
          &#39;Circular Motion&#39;,&#39;Friction&#39;,&#39;Work Power Energy&#39;,&#39;Rotational Motion and Moment of Inertia&#39;,
          &#39;Gravitation&#39;,&#39;Elasticity&#39;,&#39;Viscosity&#39;,&#39;Surface Tension&#39;,&#39;Oscillation&#39;,&#39;Heat&#39;,
          &#39;Calorimetry&#39;,&#39;Transmission of Heat&#39;,&#39;Thermodynamics&#39;,&#39;Wave Motion&#39;,
          &#39;Superposition of Wave (Interference)&#39;,&#39;Speed of Sound&#39;,&#39;Vibration of Air Column&#39;,
          &#39;Doppler Effect&#39;,&#39;Electric Charge and Field&#39;,&quot;Gauss&#39; Theorem&quot;,&#39;Electric Capacitance&#39;,
          &#39;Electric Conduction, Ohm Law&#39;,&quot;Kirchhoff&#39;s Law or Potential Meter and Electric Cell&quot;,
          &#39;Heating Effect of Current&#39;,&#39;Magnetic Effect of Electric&#39;,&#39;Electric Inst (Ammeter)&#39;,
          &#39;Magnetic Field&#39;,&#39;Magnetic Properties of Matter&#39;,&#39;Magnetic Induction&#39;,&#39;Alternative Current&#39;,
          &#39;Reflection of Light&#39;,&#39;Refraction of Light&#39;,&#39;Lens&#39;,&#39;Prism&#39;,&#39;Interference or Diffraction&#39;,
          &#39;Polarisation&#39;,&#39;Dual Nature of Light&#39;,&#39;Electro Magnetic Wave&#39;,&#39;Structure of Atom&#39;,
          &#39;Radioactivity&#39;,&#39;Nuclear Fusion or Fission&#39;,&#39;Semiconductor&#39;,&#39;Logic Gate&#39;
        ])},
        { id: &#39;iaf-math&#39;, name: &#39;Mathematics&#39;, chapters: makeChapters(&#39;iaf-math&#39;, [
          &#39;Complex Numbers&#39;,&#39;Logarithms&#39;,&#39;Permutations and Combinations&#39;,&#39;Binomial Theorem&#39;,
          &#39;Set Theory&#39;,&#39;Probability&#39;,&#39;Matrices and Determinants&#39;,&#39;Trigonometric Ratios and Identities&#39;,
          &#39;Applications of Trigonometry&#39;,&#39;Inverse Trigonometric&#39;,&#39;Three Dimensional Geometry&#39;,
          &#39;Statistics&#39;,&#39;Quadratic Equations&#39;,&#39;Sequence and Series&#39;,&#39;Straight Lines&#39;,&#39;Circle &amp; Sphere&#39;,
          &#39;Conic Sections&#39;,&#39;Limits, Continuity and Differentiability&#39;,&#39;Differentiability&#39;,
          &#39;Applications of Derivatives&#39;,&#39;Indefinite Integration&#39;,&#39;Definite Integration&#39;,
          &#39;Area Under curves&#39;,&#39;Differential Equations&#39;,&#39;Relations &amp; Functions&#39;
        ])}
      ]
    },
    {
      id: &#39;nda&#39;, code: &#39;NDA&#39;, name: &#39;NDA — Starter Syllabus&#39;,
      verificationNote: &#39;Starter syllabus — verification pending&#39;,
      subjects: [
        { id: &#39;nda-math&#39;, name: &#39;Mathematics&#39;, chapters: makeChapters(&#39;nda-math&#39;, [
          &#39;Basic Maths (Basic Algebra and Exponents, HCF and LCM, Inequalities, Wavy Curve Method)&#39;,
          &#39;Logarithm&#39;,&#39;Quadratic Equations&#39;,&#39;Complex Numbers&#39;,&#39;Sequence and Series&#39;,
          &#39;Permutation and Combination&#39;,&#39;Binomial Theorem&#39;,&#39;Set Theory&#39;,&#39;Probability&#39;,&#39;Statistics&#39;,
          &#39;Matrices and Determinants&#39;,&#39;Trigonometry&#39;,&#39;Inverse Trigonometric Functions&#39;,
          &#39;Applications of Trigonometry (Properties of Triangle, Height and Distance)&#39;,
          &#39;2D Geometry (Coordinates, Equations of Line, Foot of Perpendicular, Quadrilateral, Pair of Straight Line)&#39;,
          &#39;Conic Sections (Circle, Parabola, Ellipse, Hyperbola)&#39;,&#39;Vectors&#39;,
          &#39;3D Geometry (Plane, Line, Sphere)&#39;,&#39;Relation and Function&#39;,&#39;Differentiation&#39;,
          &#39;Application of Derivatives (AOD)&#39;,&#39;Limits, Continuity&#39;,&#39;Indefinite Integrals&#39;,
          &#39;Definite Integrals&#39;,&#39;Area Under Integral (AOI)&#39;,&#39;Differential Equation&#39;,&#39;Binary Numbers&#39;
        ])},
        ...cloneSubjects(GAT_SUBJECTS, &#39;nda&#39;)
      ]
    },
    {
      id: &#39;cds&#39;, code: &#39;CDS&#39;, name: &#39;CDS — Starter Syllabus&#39;,
      verificationNote: &#39;Starter syllabus — verification pending (references shared GAT)&#39;,
      subjects: [
        { id: &#39;cds-math&#39;, name: &#39;Mathematics&#39;, chapters: makeChapters(&#39;cds-math&#39;, [
          &#39;Height and Distance&#39;,&#39;Average&#39;,&#39;Set Theory&#39;,&#39;Percentage&#39;,&#39;Profit and loss&#39;,
          &#39;Simple Interest&#39;,&#39;Compound Interest&#39;,&#39;Instalment&#39;,&#39;Algebra&#39;,&#39;Time and Work&#39;,
          &#39;Pipe and Cistern&#39;,&#39;Logarithm&#39;,&#39;Statistics and DI&#39;,&#39;Ratio and Proportion&#39;,
          &#39;Problem on Ages &amp; Partnership&#39;,&#39;Mixture&#39;,&#39;Allegation&#39;,&#39;Geometry&#39;,&#39;Mensuration&#39;,
          &#39;Speed Distance and Time&#39;,&#39;Number System&#39;,&#39;Trigonometry&#39;
        ])},
        ...cloneSubjects(GAT_SUBJECTS, &#39;cds&#39;)
      ]
    }
  ];

  const PRESET_BACKGROUNDS = [
    { id: &#39;tiranga&#39;, name: &#39;🇮🇳 Tiranga Dawn&#39;, css: &#39;linear-gradient(155deg, #0b1e4d 0%, #1e40af 24%, #ff9933 52%, #f8fafc 66%, #138808 88%, #064e3b 100%)&#39; },
    { id: &#39;iaf-sky&#39;, name: &#39;✈️ IAF Horizon&#39;, css: &#39;radial-gradient(circle at 80% 18%, rgba(255,153,51,0.55), transparent 42%), radial-gradient(circle at 18% 82%, rgba(19,136,8,0.45), transparent 45%), linear-gradient(135deg, #091534 0%, #1d3b72 52%, #0f172a 100%)&#39; },
    { id: &#39;army-olive&#39;, name: &#39;🪖 Army Tactical&#39;, css: &#39;radial-gradient(circle at 75% 20%, rgba(163,230,53,0.22), transparent 42%), linear-gradient(155deg, #142212 0%, #273c22 48%, #0f1712 100%)&#39; },
    { id: &#39;navy-deep&#39;, name: &#39;⚓ Navy Ocean&#39;, css: &#39;radial-gradient(circle at 25% 20%, rgba(56,189,248,0.35), transparent 45%), linear-gradient(160deg, #04152d 0%, #0c356a 52%, #020b18 100%)&#39; },
    { id: &#39;midnight&#39;, name: &#39;🌙 Midnight Focus&#39;, css: &#39;radial-gradient(circle at 20% 20%, rgba(56,189,248,0.22), transparent 40%), linear-gradient(160deg, #020617 0%, #0f172a 55%, #1e293b 100%)&#39; },
    { id: &#39;saffron-sunset&#39;, name: &#39;🌅 Saffron Sunset&#39;, css: &#39;linear-gradient(145deg, #7c2d12 0%, #ea580c 42%, #f59e0b 78%, #fef3c7 100%)&#39; },
    { id: &#39;royal-indigo&#39;, name: &#39;🌌 Royal Nebula&#39;, css: &#39;radial-gradient(circle at 80% 15%, rgba(192,132,252,0.45), transparent 45%), linear-gradient(150deg, #1e1b4b 0%, #312e81 50%, #0f172a 100%)&#39; },
    { id: &#39;emerald-forest&#39;, name: &#39;🌲 Forest Calm&#39;, css: &#39;radial-gradient(circle at 20% 80%, rgba(52,211,153,0.32), transparent 45%), linear-gradient(155deg, #022c22 0%, #065f46 50%, #064e3b 100%)&#39; },
    { id: &#39;crimson-valor&#39;, name: &#39;🔥 Valor Red&#39;, css: &#39;radial-gradient(circle at 75% 25%, rgba(251,113,133,0.35), transparent 45%), linear-gradient(155deg, #450a0a 0%, #991b1b 48%, #1f0a14 100%)&#39; },
    { id: &#39;cyber-grid&#39;, name: &#39;⚡ Cyber Glow&#39;, css: &#39;radial-gradient(circle at 15% 20%, rgba(6,182,212,0.4), transparent 42%), radial-gradient(circle at 85% 80%, rgba(168,85,247,0.4), transparent 42%), linear-gradient(160deg, #030712 0%, #111827 100%)&#39; },
    { id: &#39;warm-cream&#39;, name: &#39;📒 Study Desk&#39;, css: &#39;linear-gradient(165deg, #fef3c7 0%, #fde68a 45%, #fed7aa 100%)&#39; },
    { id: &#39;paper&#39;, name: &#39;📄 Clean Light&#39;, css: &#39;linear-gradient(180deg, #f1f5f9 0%, #e2e8f0 50%, #cbd5e1 100%)&#39; }
  ];

  const ACCENTS = [
    { name: &#39;Saffron&#39;, hex: &#39;#f97316&#39; },
    { name: &#39;IAF Blue&#39;, hex: &#39;#2563eb&#39; },
    { name: &#39;Emerald&#39;, hex: &#39;#16a34a&#39; },
    { name: &#39;Indigo&#39;, hex: &#39;#4f46e5&#39; },
    { name: &#39;Crimson&#39;, hex: &#39;#dc2626&#39; },
    { name: &#39;Gold&#39;, hex: &#39;#d97706&#39; },
    { name: &#39;Teal&#39;, hex: &#39;#0d9488&#39; },
    { name: &#39;Violet&#39;, hex: &#39;#7c3aed&#39; },
    { name: &#39;Rose&#39;, hex: &#39;#e11d48&#39; },
    { name: &#39;Cyan&#39;, hex: &#39;#0891b2&#39; },
    { name: &#39;Olive&#39;, hex: &#39;#4d7c0f&#39; }
  ];

  const MOCK_SOURCES = [&#39;PW&#39;, &#39;RWA&#39;, &#39;Testbook&#39;, &#39;YouTube&#39;, &#39;Offline&#39;];

  const PRESET_BATCHES = [
    { id: &#39;pb1&#39;, exam: &#39;IAF&#39;, name: &#39;IAF X &amp; Y Starter Study Batch&#39;, desc: &#39;Core English, Physics &amp; Maths starter chapters.&#39; },
    { id: &#39;pb2&#39;, exam: &#39;NDA&#39;, name: &#39;NDA Maths + GAT Starter Batch&#39;, desc: &#39;High-weightage Maths + Polity/History starter set.&#39; },
    { id: &#39;pb3&#39;, exam: &#39;CDS&#39;, name: &#39;CDS Quantitative + GAT Starter Batch&#39;, desc: &#39;Arithmetic, Geometry &amp; shared GAT starter set.&#39; }
  ];

  // ===== STATE =====
  let state = {
    tab: &#39;syllabus&#39;,
    exams: DEFAULT_EXAMS,
    activeExamId: &#39;iaf-xy&#39;,
    activeSubjectId: &#39;iaf-eng&#39;,
    statusFilter: &#39;all&#39;,
    expandedChapterId: null,
    batches: [],
    attempts: [],
    sessions: [],
    goals: [],
    theme: {
      mode: &#39;dark&#39;,
      accent: &#39;#f97316&#39;,
      bgId: &#39;tiranga&#39;,
      customBg: &#39;&#39;,
      blur: 3,
      overlay: 0.34,
      pos: &#39;center&#39;,
      babaLang: &#39;hinglish&#39;,
      dailyGoal: 180
    },
    pomo: { preset: 25, secLeft: 25 * 60, running: false },
    mockExamFilter: &#39;ALL&#39;,
    babaMessages: [
      { role: &#39;assistant&#39;, text: &#39;Jai Hind! Main Baba AI hoon (Preview Mode). Aap Hinglish, Hindi ya English mein study questions, revision tips, ya progress summary pooch sakte hain!&#39; }
    ]
  };

  try {
    const saved = localStorage.getItem(&#39;st_preview_v1&#39;);
    if (saved) {
      const parsed = JSON.parse(saved);
      state = { ...state, ...parsed, pomo: { preset: 25, secLeft: 1500, running: false } };
    }
  } catch (e) {}

  function saveState() {
    try {
      const { pomo, ...persist } = state;
      localStorage.setItem(&#39;st_preview_v1&#39;, JSON.stringify(persist));
    } catch (e) {}
  }

  function toast(msg, type = &#39;success&#39;) {
    const box = document.getElementById(&#39;toast-box&#39;);
    const el = document.createElement(&#39;div&#39;);
    el.className = &#39;pointer-events-auto glass-card rounded-2xl px-3.5 py-2.5 text-xs font-semibold flex items-center gap-2&#39;;
    el.innerHTML = `&lt;span&gt;${type === &#39;error&#39; ? &#39;⚠️&#39; : &#39;✅&#39;}&lt;/span&gt;&lt;span&gt;${msg}&lt;/span&gt;`;
    box.appendChild(el);
    setTimeout(() =&gt; el.remove(), 3200);
  }

  function esc(str) {
    return String(str || &#39;&#39;).replace(/[&amp;&lt;&gt;&quot;&#39;]/g, m =&gt; ({ &#39;&amp;&#39;:&#39;&amp;amp;&#39;,&#39;&lt;&#39;:&#39;&amp;lt;&#39;,&#39;&gt;&#39;:&#39;&amp;gt;&#39;,&#39;&quot;&#39;:&#39;&amp;quot;&#39;,&quot;&#39;&quot;:&#39;&amp;#39;&#39; }[m]));
  }

  function getActiveExam() {
    return state.exams.find(e =&gt; e.id === state.activeExamId) || state.exams[0];
  }

  function getActiveSubject() {
    const ex = getActiveExam();
    return ex.subjects.find(s =&gt; s.id === state.activeSubjectId) || ex.subjects[0];
  }

  function chapterStats(chapters) {
    const total = chapters.length;
    const completed = chapters.filter(c =&gt; c.status === &#39;completed&#39;).length;
    const inProgress = chapters.filter(c =&gt; c.status === &#39;in_progress&#39;).length;
    const revReq = chapters.filter(c =&gt; c.status === &#39;revision_required&#39;).length;
    return {
      total, completed, inProgress, revReq,
      baaki: total - completed,
      pct: total ? Math.round((completed / total) * 100) : 0
    };
  }

  function getStreak() {
    const dates = new Set(state.sessions.map(s =&gt; s.date));
    return dates.size;
  }

  // ===== THEME SYNC =====
  function applyTheme() {
    const root = document.documentElement;
    if (state.theme.mode === &#39;dark&#39;) root.classList.add(&#39;dark&#39;);
    else root.classList.remove(&#39;dark&#39;);

    const bgLayer = document.getElementById(&#39;bg-layer&#39;);
    const ovLayer = document.getElementById(&#39;overlay-layer&#39;);
    const preset = PRESET_BACKGROUNDS.find(b =&gt; b.id === state.theme.bgId) || PRESET_BACKGROUNDS[0];

    bgLayer.style.backgroundImage = state.theme.customBg ? `url(&quot;${state.theme.customBg}&quot;)` : preset.css;
    bgLayer.style.backgroundSize = state.theme.customBg ? &#39;cover&#39; : &#39;100% 100%&#39;;
    bgLayer.style.backgroundPosition = state.theme.pos;
    bgLayer.style.filter = state.theme.blur &gt; 0 ? `blur(${state.theme.blur}px)` : &#39;none&#39;;
    bgLayer.style.transform = state.theme.blur &gt; 0 ? &#39;scale(1.04)&#39; : &#39;none&#39;;

    ovLayer.style.backgroundColor = state.theme.mode === &#39;dark&#39;
      ? `rgba(2, 6, 23, ${state.theme.overlay})`
      : `rgba(248, 250, 252, ${state.theme.overlay})`;

    document.getElementById(&#39;brand-badge-side&#39;).style.backgroundColor = state.theme.accent;
    document.getElementById(&#39;brand-badge-top&#39;).style.backgroundColor = state.theme.accent;
    const pill = document.getElementById(&#39;header-exam-pill&#39;);
    pill.style.backgroundColor = state.theme.accent;
    pill.textContent = getActiveExam().code;
    document.getElementById(&#39;btn-quick-theme&#39;).textContent = state.theme.mode === &#39;dark&#39; ? &#39;☀️&#39; : &#39;🌙&#39;;
  }

  // ===== NAVIGATION =====
  const NAV_ITEMS = [
    { id: &#39;dashboard&#39;, label: &#39;Dashboard&#39;, icon: &#39;📊&#39; },
    { id: &#39;syllabus&#39;, label: &#39;My Syllabus&#39;, icon: &#39;📘&#39; },
    { id: &#39;batches&#39;, label: &#39;Batches&#39;, icon: &#39;🗂️&#39; },
    { id: &#39;mock-tests&#39;, label: &#39;Mock Tests&#39;, icon: &#39;📝&#39; },
    { id: &#39;planner&#39;, label: &#39;Study Planner&#39;, icon: &#39;⏱️&#39; },
    { id: &#39;analytics&#39;, label: &#39;Analytics&#39;, icon: &#39;📈&#39; },
    { id: &#39;baba-ai&#39;, label: &#39;Baba AI&#39;, icon: &#39;🤖&#39; },
    { id: &#39;settings&#39;, label: &#39;Settings&#39;, icon: &#39;⚙️&#39; }
  ];

  function renderNav() {
    const dNav = document.getElementById(&#39;desktop-nav&#39;);
    dNav.innerHTML = NAV_ITEMS.map(it =&gt; {
      const act = state.tab === it.id;
      return `&lt;button data-nav=&quot;${it.id}&quot; class=&quot;flex items-center gap-2.5 px-3.5 py-2.5 rounded-2xl text-sm font-semibold transition ${act ? &#39;text-white shadow&#39; : &#39;hover:bg-white/30 dark:hover:bg-slate-800/50&#39;}&quot; style=&quot;${act ? `background:${state.theme.accent}` : &#39;&#39;}&quot;&gt;&lt;span&gt;${it.icon}&lt;/span&gt;&lt;span&gt;${it.label}&lt;/span&gt;&lt;/button&gt;`;
    }).join(&#39;&#39;);

    const mNav = document.getElementById(&#39;mobile-nav&#39;);
    const mobileTabs = [
      { id: &#39;dashboard&#39;, label: &#39;Home&#39;, icon: &#39;📊&#39; },
      { id: &#39;syllabus&#39;, label: &#39;Syllabus&#39;, icon: &#39;📘&#39; },
      { id: &#39;mock-tests&#39;, label: &#39;Mocks&#39;, icon: &#39;📝&#39; },
      { id: &#39;planner&#39;, label: &#39;Planner&#39;, icon: &#39;⏱️&#39; },
      { id: &#39;baba-ai&#39;, label: &#39;Baba AI&#39;, icon: &#39;🤖&#39; },
      { id: &#39;settings&#39;, label: &#39;Theme&#39;, icon: &#39;⚙️&#39; }
    ];
    mNav.innerHTML = mobileTabs.map(it =&gt; {
      const act = state.tab === it.id;
      return `&lt;button data-nav=&quot;${it.id}&quot; class=&quot;flex flex-col items-center px-2.5 py-1.5 rounded-2xl text-[10px] font-bold ${act ? &#39;text-white shadow&#39; : &#39;opacity-85&#39;}&quot; style=&quot;${act ? `background:${state.theme.accent}` : &#39;&#39;}&quot;&gt;&lt;span class=&quot;text-sm leading-none mb-0.5&quot;&gt;${it.icon}&lt;/span&gt;&lt;span&gt;${it.label}&lt;/span&gt;&lt;/button&gt;`;
    }).join(&#39;&#39;);

    document.querySelectorAll(&#39;[data-nav]&#39;).forEach(btn =&gt; {
      btn.addEventListener(&#39;click&#39;, () =&gt; {
        state.tab = btn.getAttribute(&#39;data-nav&#39;);
        render();
      });
    });
  }

  // ===== MODAL HELPER =====
  function openModal(title, fieldsHtml, onSubmit) {
    const root = document.getElementById(&#39;modal-root&#39;);
    root.classList.remove(&#39;hidden&#39;);
    root.innerHTML = `
      &lt;form id=&quot;dyn-modal-form&quot; class=&quot;glass-card bg-white/95 dark:bg-slate-900/95 rounded-3xl max-w-md w-full p-5 space-y-3&quot;&gt;
        &lt;div class=&quot;font-extrabold text-base&quot;&gt;${esc(title)}&lt;/div&gt;
        ${fieldsHtml}
        &lt;div class=&quot;flex justify-end gap-2 pt-2&quot;&gt;
          &lt;button type=&quot;button&quot; id=&quot;modal-cancel&quot; class=&quot;px-4 py-2 rounded-xl text-xs font-bold bg-slate-200 dark:bg-slate-800&quot;&gt;Cancel&lt;/button&gt;
          &lt;button type=&quot;submit&quot; class=&quot;px-4 py-2 rounded-xl text-xs font-bold text-white&quot; style=&quot;background:${state.theme.accent}&quot;&gt;Confirm&lt;/button&gt;
        &lt;/div&gt;
      &lt;/form&gt;`;
    document.getElementById(&#39;modal-cancel&#39;).onclick = () =&gt; root.classList.add(&#39;hidden&#39;);
    document.getElementById(&#39;dyn-modal-form&#39;).onsubmit = (e) =&gt; {
      e.preventDefault();
      onSubmit(new FormData(e.target));
      root.classList.add(&#39;hidden&#39;);
    };
  }

  // ===== VIEWS =====
  function renderSyllabus(container) {
    const ex = getActiveExam();
    const sub = getActiveSubject();
    const st = chapterStats(sub.chapters);
    const filtered = sub.chapters.filter(c =&gt; state.statusFilter === &#39;all&#39; ? true : c.status === state.statusFilter);

    container.innerHTML = `
      &lt;div class=&quot;space-y-4&quot;&gt;
        &lt;!-- Hero Subject Progress Card + Streak Badge --&gt;
        &lt;div class=&quot;relative&quot;&gt;
          &lt;div class=&quot;glass-card rounded-3xl p-5 space-y-2.5&quot;&gt;
            &lt;div class=&quot;flex items-center justify-between gap-2&quot;&gt;
              &lt;div&gt;
                &lt;div class=&quot;text-lg sm:text-xl font-extrabold&quot;&gt;${esc(sub.name)} Progress&lt;/div&gt;
                &lt;span class=&quot;inline-block text-[10px] font-bold px-2.5 py-0.5 rounded-full bg-amber-500/20 text-amber-800 dark:text-amber-200 mt-0.5&quot;&gt;⚠️ ${esc(ex.verificationNote)}&lt;/span&gt;
              &lt;/div&gt;
              &lt;div class=&quot;text-3xl font-black&quot;&gt;${st.pct}%&lt;/div&gt;
            &lt;/div&gt;
            &lt;div class=&quot;h-3 rounded-full bg-slate-900/15 dark:bg-white/15 overflow-hidden&quot;&gt;
              &lt;div class=&quot;h-full rounded-full transition-all duration-300&quot; style=&quot;width:${st.pct}%;background:${state.theme.accent}&quot;&gt;&lt;/div&gt;
            &lt;/div&gt;
          &lt;/div&gt;
          &lt;div class=&quot;inline-flex items-center gap-1 px-3.5 py-1 rounded-full text-xs font-bold text-white bg-gradient-to-r from-orange-500 to-amber-500 shadow-lg absolute -bottom-3 right-4&quot;&gt;🔥 Streak ${getStreak()}&lt;/div&gt;
        &lt;/div&gt;

        &lt;!-- 3 Stat Cards: Chapters | Complete | Baaki --&gt;
        &lt;div class=&quot;grid grid-cols-3 gap-2.5 pt-2&quot;&gt;
          &lt;div class=&quot;glass-card rounded-2xl p-3 flex items-center gap-2 bg-orange-500/15 border-orange-400/50&quot;&gt;
            &lt;div class=&quot;w-8 h-8 rounded-xl bg-orange-500 text-white flex items-center justify-center shrink-0&quot;&gt;📖&lt;/div&gt;
            &lt;div&gt;&lt;div class=&quot;text-lg font-black leading-none&quot;&gt;${st.total}&lt;/div&gt;&lt;div class=&quot;text-[11px] font-semibold opacity-80&quot;&gt;Chapters&lt;/div&gt;&lt;/div&gt;
          &lt;/div&gt;
          &lt;div class=&quot;glass-card rounded-2xl p-3 flex items-center gap-2&quot;&gt;
            &lt;div class=&quot;w-8 h-8 rounded-xl bg-emerald-600 text-white flex items-center justify-center shrink-0&quot;&gt;✓&lt;/div&gt;
            &lt;div&gt;&lt;div class=&quot;text-lg font-black leading-none&quot;&gt;${st.completed}&lt;/div&gt;&lt;div class=&quot;text-[11px] font-semibold opacity-80&quot;&gt;Complete&lt;/div&gt;&lt;/div&gt;
          &lt;/div&gt;
          &lt;div class=&quot;glass-card rounded-2xl p-3 flex items-center gap-2 bg-emerald-500/15 border-emerald-400/50&quot;&gt;
            &lt;div class=&quot;w-8 h-8 rounded-xl bg-emerald-500 text-white flex items-center justify-center shrink-0&quot;&gt;🚀&lt;/div&gt;
            &lt;div&gt;&lt;div class=&quot;text-lg font-black leading-none&quot;&gt;${st.baaki}&lt;/div&gt;&lt;div class=&quot;text-[11px] font-semibold opacity-80&quot;&gt;Baaki&lt;/div&gt;&lt;/div&gt;
          &lt;/div&gt;
        &lt;/div&gt;

        &lt;!-- Exam Selector Pills --&gt;
        &lt;div class=&quot;flex items-center gap-2 overflow-x-auto pb-1&quot;&gt;
          ${state.exams.map(e =&gt; {
            const act = e.id === ex.id;
            return `&lt;button data-exam=&quot;${e.id}&quot; class=&quot;px-4 py-2 rounded-full text-xs sm:text-sm font-bold shrink-0 ${act ? &#39;text-white shadow&#39; : &#39;glass-pill&#39;}&quot; style=&quot;${act ? `background:${state.theme.accent}` : &#39;&#39;}&quot;&gt;${esc(e.code)}&lt;/button&gt;`;
          }).join(&#39;&#39;)}
        &lt;/div&gt;

        &lt;!-- Quick Action Pills --&gt;
        &lt;div class=&quot;flex flex-wrap gap-2&quot;&gt;
          &lt;button id=&quot;btn-add-exam&quot; class=&quot;glass-pill px-3.5 py-2 rounded-2xl text-xs font-bold&quot;&gt;+ Add Exam&lt;/button&gt;
          &lt;button id=&quot;btn-add-subject&quot; class=&quot;glass-pill px-3.5 py-2 rounded-2xl text-xs font-bold&quot;&gt;+ Add Subject&lt;/button&gt;
          &lt;button id=&quot;btn-add-chapter&quot; class=&quot;glass-pill px-3.5 py-2 rounded-2xl text-xs font-bold&quot;&gt;+ Add Chapter&lt;/button&gt;
          &lt;button id=&quot;btn-batches-jump&quot; class=&quot;glass-pill px-3.5 py-2 rounded-2xl text-xs font-bold&quot;&gt;🗂️ Batches&lt;/button&gt;
          &lt;button id=&quot;btn-analytics-jump&quot; class=&quot;glass-pill px-3.5 py-2 rounded-2xl text-xs font-bold&quot;&gt;📈 Analytics&lt;/button&gt;
        &lt;/div&gt;

        &lt;!-- Subject Tabs + Status Filter --&gt;
        &lt;div class=&quot;flex flex-wrap items-center justify-between gap-2 border-b border-white/25 pb-2&quot;&gt;
          &lt;div class=&quot;flex items-center gap-4 overflow-x-auto&quot;&gt;
            ${ex.subjects.map(s =&gt; {
              const act = s.id === sub.id;
              return `&lt;button data-sub=&quot;${s.id}&quot; class=&quot;pb-1 text-sm font-bold shrink-0 border-b-2 ${act ? &#39;border-current&#39; : &#39;border-transparent opacity-65&#39;}&quot; style=&quot;${act ? `color:${state.theme.accent}` : &#39;&#39;}&quot;&gt;${esc(s.name)} (${s.chapters.length})&lt;/button&gt;`;
            }).join(&#39;&#39;)}
          &lt;/div&gt;
          &lt;select id=&quot;sel-status-filter&quot; class=&quot;glass-pill px-2.5 py-1 rounded-xl text-xs font-semibold outline-none&quot;&gt;
            &lt;option value=&quot;all&quot; ${state.statusFilter===&#39;all&#39;?&#39;selected&#39;:&#39;&#39;}&gt;All Statuses&lt;/option&gt;
            &lt;option value=&quot;not_started&quot; ${state.statusFilter===&#39;not_started&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Not Started&lt;/option&gt;
            &lt;option value=&quot;in_progress&quot; ${state.statusFilter===&#39;in_progress&#39;?&#39;selected&#39;:&#39;&#39;}&gt;In Progress&lt;/option&gt;
            &lt;option value=&quot;completed&quot; ${state.statusFilter===&#39;completed&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Completed&lt;/option&gt;
            &lt;option value=&quot;revision_required&quot; ${state.statusFilter===&#39;revision_required&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Revision Required&lt;/option&gt;
          &lt;/select&gt;
        &lt;/div&gt;

        &lt;!-- Chapters List --&gt;
        &lt;div class=&quot;space-y-3&quot;&gt;
          ${filtered.map(ch =&gt; {
            const count = Object.values(ch.resources).filter(Boolean).length;
            const exp = state.expandedChapterId === ch.id;
            return `
              &lt;div class=&quot;glass-card rounded-3xl p-4 space-y-3&quot;&gt;
                &lt;div class=&quot;flex items-start justify-between gap-2&quot;&gt;
                  &lt;div class=&quot;min-w-0&quot;&gt;
                    &lt;div class=&quot;font-bold text-base leading-snug&quot;&gt;${esc(ch.name)}&lt;/div&gt;
                    &lt;div class=&quot;flex flex-wrap items-center gap-2 mt-1 text-[11px] opacity-85&quot;&gt;
                      &lt;select data-ch-status=&quot;${ch.id}&quot; class=&quot;px-2 py-0.5 rounded-full bg-white/60 dark:bg-slate-800 font-semibold outline-none&quot;&gt;
                        &lt;option value=&quot;not_started&quot; ${ch.status===&#39;not_started&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Not Started&lt;/option&gt;
                        &lt;option value=&quot;in_progress&quot; ${ch.status===&#39;in_progress&#39;?&#39;selected&#39;:&#39;&#39;}&gt;In Progress&lt;/option&gt;
                        &lt;option value=&quot;completed&quot; ${ch.status===&#39;completed&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Completed&lt;/option&gt;
                        &lt;option value=&quot;revision_required&quot; ${ch.status===&#39;revision_required&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Revision Required&lt;/option&gt;
                      &lt;/select&gt;
                      &lt;span&gt;Rev: ${ch.revisionCount}&lt;/span&gt;
                      ${ch.priority === &#39;high&#39; ? &#39;&lt;span class=&quot;px-1.5 py-0.5 rounded bg-rose-500/20 text-rose-500 font-bold&quot;&gt;High Priority&lt;/span&gt;&#39; : &#39;&#39;}
                    &lt;/div&gt;
                  &lt;/div&gt;
                  &lt;span class=&quot;px-2.5 py-1 rounded-full text-xs font-bold bg-white/75 dark:bg-slate-800 shrink-0&quot;&gt;${count}/4&lt;/span&gt;
                &lt;/div&gt;

                &lt;!-- 4 Resource Toggle Buttons --&gt;
                &lt;div class=&quot;grid grid-cols-4 gap-2&quot;&gt;
                  ${[[&#39;pw&#39;,&#39;PW&#39;],[&#39;rwa&#39;,&#39;RWA&#39;],[&#39;youtube&#39;,&#39;YouTube&#39;],[&#39;tests&#39;,&#39;Tests&#39;]].map(([k,lbl]) =&gt; {
                    const on = ch.resources[k];
                    return `&lt;button data-res=&quot;${ch.id}|${k}&quot; class=&quot;py-2 rounded-xl text-xs font-bold border transition ${on ? &#39;text-white border-transparent shadow&#39; : &#39;bg-white/50 dark:bg-slate-800/50 border-white/40 dark:border-slate-700&#39;}&quot; style=&quot;${on ? `background:${state.theme.accent}` : &#39;&#39;}&quot;&gt;${lbl}&lt;/button&gt;`;
                  }).join(&#39;&#39;)}
                &lt;/div&gt;

                &lt;div class=&quot;flex items-center justify-between text-xs pt-0.5&quot;&gt;
                  &lt;div class=&quot;flex items-center gap-3&quot;&gt;
                    &lt;button data-del-ch=&quot;${ch.id}&quot; class=&quot;opacity-75 hover:text-rose-500 font-semibold&quot;&gt;🗑️ Remove chapter&lt;/button&gt;
                    &lt;button data-rev-ch=&quot;${ch.id}&quot; class=&quot;font-bold&quot; style=&quot;color:${state.theme.accent}&quot;&gt;+1 Revision&lt;/button&gt;
                  &lt;/div&gt;
                  &lt;button data-exp-ch=&quot;${ch.id}&quot; class=&quot;font-semibold opacity-80 hover:opacity-100&quot;&gt;${exp ? &#39;Hide Details ▲&#39; : &#39;Notes &amp; Priority ▼&#39;}&lt;/button&gt;
                &lt;/div&gt;

                ${exp ? `
                  &lt;div class=&quot;pt-2.5 border-t border-white/25 space-y-2 text-xs&quot;&gt;
                    &lt;div class=&quot;grid grid-cols-2 gap-2&quot;&gt;
                      &lt;select data-prio-ch=&quot;${ch.id}&quot; class=&quot;px-2.5 py-1.5 rounded-xl bg-white/75 dark:bg-slate-800 outline-none&quot;&gt;
                        &lt;option value=&quot;low&quot; ${ch.priority===&#39;low&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Priority: Low&lt;/option&gt;
                        &lt;option value=&quot;medium&quot; ${ch.priority===&#39;medium&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Priority: Medium&lt;/option&gt;
                        &lt;option value=&quot;high&quot; ${ch.priority===&#39;high&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Priority: High&lt;/option&gt;
                      &lt;/select&gt;
                      &lt;select data-diff-ch=&quot;${ch.id}&quot; class=&quot;px-2.5 py-1.5 rounded-xl bg-white/75 dark:bg-slate-800 outline-none&quot;&gt;
                        &lt;option value=&quot;easy&quot; ${ch.difficulty===&#39;easy&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Difficulty: Easy&lt;/option&gt;
                        &lt;option value=&quot;medium&quot; ${ch.difficulty===&#39;medium&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Difficulty: Medium&lt;/option&gt;
                        &lt;option value=&quot;hard&quot; ${ch.difficulty===&#39;hard&#39;?&#39;selected&#39;:&#39;&#39;}&gt;Difficulty: Hard&lt;/option&gt;
                      &lt;/select&gt;
                    &lt;/div&gt;
                    &lt;textarea data-notes-ch=&quot;${ch.id}&quot; rows=&quot;2&quot; placeholder=&quot;Add notes, formulas, weak points...&quot; class=&quot;w-full px-3 py-2 rounded-xl bg-white/75 dark:bg-slate-800 outline-none&quot;&gt;${esc(ch.notes)}&lt;/textarea&gt;
                  </div>
                ` : ''}
              </div>`;
          }).join('')}
        </div>
      </div>`;

    // Bindings
    container.querySelectorAll('[data-exam]').forEach(b => b.onclick = () => {
      state.activeExamId = b.dataset.exam;
      state.activeSubjectId = getActiveExam().subjects[0].id;
      saveState(); render();
    });
    container.querySelectorAll('[data-sub]').forEach(b => b.onclick = () => {
      state.activeSubjectId = b.dataset.sub;
      saveState(); render();
    });
    container.querySelector('#sel-status-filter').onchange = (e) => {
      state.statusFilter = e.target.value; render();
    };
    container.querySelector('#btn-batches-jump').onclick = () => { state.tab = 'batches'; render(); };
    container.querySelector('#btn-analytics-jump').onclick = () => { state.tab = 'analytics'; render(); };

    container.querySelector('#btn-add-exam').onclick = () => openModal('Add Custom Exam', `
      <input name="code" required placeholder="Code (e.g. AFCAT)" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
      <input name="name" required placeholder="Full Exam Name" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
    `, (fd) => {
      const id = 'ex-' + Date.now();
      const subId = 'sub-' + Date.now();
      state.exams.push({
        id, code: String(fd.get('code')).toUpperCase().trim(), name: String(fd.get('name')).trim(),
        verificationNote: 'Custom student exam',
        subjects: [{ id: subId, name: 'General', chapters: [] }]
      });
      state.activeExamId = id; state.activeSubjectId = subId;
      saveState(); toast('Added custom exam'); render();
    });

    container.querySelector('#btn-add-subject').onclick = () => openModal('Add Subject', `
      <input name="name" required placeholder="Subject Name" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
    `, (fd) => {
      const sId = 'sub-' + Date.now();
      ex.subjects.push({ id: sId, name: String(fd.get('name')).trim(), chapters: [] });
      state.activeSubjectId = sId;
      saveState(); toast('Added subject'); render();
    });

    container.querySelector('#btn-add-chapter').onclick = () => openModal('Add Chapter', `
      <input name="name" required placeholder="Chapter Name" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
    `, (fd) => {
      sub.chapters.push(...makeChapters('custom-' + Date.now(), [String(fd.get('name')).trim()]));
      saveState(); toast('Added chapter'); render();
    });

    container.querySelectorAll('[data-res]').forEach(b => b.onclick = () => {
      const [cid, key] = b.dataset.res.split('|');
      const ch = sub.chapters.find(c => c.id === cid);
      if (!ch) return;
      ch.resources[key] = !ch.resources[key];
      const vals = Object.values(ch.resources);
      if (vals.every(Boolean)) ch.status = 'completed';
      else if (vals.some(Boolean) && ch.status === 'not_started') ch.status = 'in_progress';
      saveState(); render();
    });

    container.querySelectorAll('[data-ch-status]').forEach(sel => sel.onchange = () => {
      const ch = sub.chapters.find(c => c.id === sel.dataset.chStatus);
      if (ch) { ch.status = sel.value; saveState(); render(); }
    });

    container.querySelectorAll('[data-rev-ch]').forEach(b => b.onclick = () => {
      const ch = sub.chapters.find(c => c.id === b.dataset.revCh);
      if (ch) { ch.revisionCount++; ch.lastRevisedAt = new Date().toISOString().slice(0,10); saveState(); toast('Revision logged'); render(); }
    });

    container.querySelectorAll('[data-del-ch]').forEach(b => b.onclick = () => {
      const ch = sub.chapters.find(c => c.id === b.dataset.delCh);
      if (!ch) return;
      openModal('Remove Chapter?', `<p class="text-xs opacity-80">Remove "${esc(ch.name)}" from your personal syllabus?</p>`, () => {
        sub.chapters = sub.chapters.filter(c => c.id !== ch.id);
        saveState(); toast('Chapter removed'); render();
      });
    });

    container.querySelectorAll('[data-exp-ch]').forEach(b => b.onclick = () => {
      state.expandedChapterId = state.expandedChapterId === b.dataset.expCh ? null : b.dataset.expCh;
      render();
    });

    container.querySelectorAll('[data-prio-ch]').forEach(s => s.onchange = () => {
      const ch = sub.chapters.find(c => c.id === s.dataset.prioCh);
      if (ch) { ch.priority = s.value; saveState(); render(); }
    });
    container.querySelectorAll('[data-diff-ch]').forEach(s => s.onchange = () => {
      const ch = sub.chapters.find(c => c.id === s.dataset.diffCh);
      if (ch) { ch.difficulty = s.value; saveState(); render(); }
    });
    container.querySelectorAll('[data-notes-ch]').forEach(t => t.oninput = () => {
      const ch = sub.chapters.find(c => c.id === t.dataset.notesCh);
      if (ch) { ch.notes = t.value; saveState(); }
    });
  }

  function renderDashboard(container) {
    const allChapters = state.exams.flatMap(e => e.subjects.flatMap(s => s.chapters));
    const overall = chapterStats(allChapters);
    const ex = getActiveExam();
    const exStats = chapterStats(ex.subjects.flatMap(s => s.chapters));
    const today = new Date().toISOString().slice(0,10);
    const todayMins = state.sessions.filter(s => s.date === today).reduce((a,b)=>a+b.mins, 0);

    container.innerHTML = `
      <div class="space-y-4">
        <div class="glass-card rounded-3xl p-5 space-y-3">
          <div class="flex items-center justify-between">
            <div>
              <div class="text-xs font-bold uppercase opacity-75">Overall Syllabus Completion</div>
              <div class="text-xl font-extrabold">${ex.code} (${exStats.pct}%) • All Exams (${overall.pct}%)</div>
            </div>
            <div class="text-3xl font-black">${overall.pct}%</div>
          </div>
          <div class="h-3 rounded-full bg-slate-900/15 dark:bg-white/15 overflow-hidden">
            <div class="h-full rounded-full" style="width:${overall.pct}%;background:${state.theme.accent}"></div>
          </div>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-xs pt-1">
            <div class="p-2.5 rounded-2xl bg-white/45 dark:bg-slate-800/50">Completed: <b>${overall.completed}</b></div>
            <div class="p-2.5 rounded-2xl bg-white/45 dark:bg-slate-800/50">In Progress: <b>${overall.inProgress}</b></div>
            <div class="p-2.5 rounded-2xl bg-white/45 dark:bg-slate-800/50">Rev. Needed: <b>${overall.revReq}</b></div>
            <div class="p-2.5 rounded-2xl bg-white/45 dark:bg-slate-800/50">Today Study: <b>${todayMins}m</b></div>
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div class="glass-card rounded-3xl p-4 space-y-2.5">
            <div class="font-bold text-sm">Exam-wise Progress</div>
            ${state.exams.map(e => {
              const s = chapterStats(e.subjects.flatMap(sub => sub.chapters));
              return `
                <div class="space-y-1 text-xs">
                  <div class="flex justify-between font-semibold"><span>${esc(e.code)}</span><span>${s.completed}/${s.total} (${s.pct}%)</span></div>
                  <div class="h-2 rounded-full bg-slate-900/10 dark:bg-white/10 overflow-hidden">
                    <div class="h-full rounded-full" style="width:${s.pct}%;background:${state.theme.accent}"></div>
                  </div>
                </div>`;
            }).join('')}
          </div>

          <div class="glass-card rounded-3xl p-4 space-y-2.5">
            <div class="font-bold text-sm">Recent Mock Tests (${state.attempts.length})</div>
            ${state.attempts.length === 0
              ? '<p class="text-xs opacity-75 py-4 text-center">No mock tests logged yet. Open Mock Tests to record your test scores.</p>'
              : state.attempts.slice(0,4).map(a => `
                <div class="p-2.5 rounded-2xl bg-white/45 dark:bg-slate-800/55 flex justify-between text-xs">
                  <div><b>${esc(a.title)}</b><div class="opacity-75">${esc(a.exam)} • Acc ${a.acc}%</div></div>
                  <div class="font-black">${a.score}/${a.max} (${a.pct}%)</div>
                </div>`).join('')}
          </div>
        </div>
      </div>`;
  }

  function renderBatches(container) {
    container.innerHTML = `
      <div class="space-y-4">
        <form id="batch-form" class="glass-card rounded-3xl p-4 flex flex-wrap gap-2">
          <input name="name" required placeholder="New Personal Batch Name..." class="flex-1 min-w-[160px] px-3 py-2 rounded-xl bg-white/75 dark:bg-slate-800 text-sm outline-none" />
          <button type="submit" class="px-4 py-2 rounded-xl text-xs font-bold text-white" style="background:${state.theme.accent}">+ Create Batch</button>
        </form>
        <div class="space-y-2">
          <div class="font-bold text-sm px-1">My Batches (${state.batches.length})</div>
          ${state.batches.length === 0 ? '<div class="glass-card rounded-3xl p-5 text-xs text-center opacity-75">No personal batches yet. Create one above or copy a starter preset below.</div>' : state.batches.map(b => `
            &lt;div class=&quot;glass-card rounded-2xl p-4 flex items-center justify-between text-sm&quot;&gt;
              &lt;div&gt;&lt;div class=&quot;font-bold&quot;&gt;${esc(b.name)}&lt;/div&gt;&lt;div class=&quot;text-xs opacity-75&quot;&gt;${esc(b.desc || 'Personal study batch')}&lt;/div&gt;&lt;/div&gt;
              &lt;button data-del-batch=&quot;${b.id}&quot; class=&quot;text-xs text-rose-500 font-bold&quot;&gt;Delete&lt;/button&gt;
            &lt;/div&gt;`).join('')}
        </div>
        <div class="space-y-2">
          <div class="font-bold text-sm px-1">Starter Preset Batch Catalog</div>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            ${PRESET_BATCHES.map(p => `
              &lt;div class=&quot;glass-card rounded-3xl p-4 flex flex-col justify-between gap-3&quot;&gt;
                &lt;div&gt;
                  &lt;span class=&quot;text-[10px] font-bold px-2 py-0.5 rounded-full bg-amber-500/20 text-amber-800 dark:text-amber-200&quot;&gt;${p.exam} • Starter&lt;/span&gt;
                  &lt;div class=&quot;font-bold text-sm mt-1&quot;&gt;${esc(p.name)}&lt;/div&gt;
                  &lt;p class=&quot;text-xs opacity-75 mt-0.5&quot;&gt;${esc(p.desc)}&lt;/p&gt;
                &lt;/div&gt;
                &lt;button data-copy-preset=&quot;${p.id}&quot; class=&quot;w-full py-2 rounded-xl text-xs font-bold text-white&quot; style=&quot;background:${state.theme.accent}&quot;&gt;Copy to My Batches&lt;/button&gt;
              &lt;/div&gt;`).join('')}
          </div>
        </div>
      </div>`;

    container.querySelector('#batch-form').onsubmit = (e) => {
      e.preventDefault();
      const fd = new FormData(e.target);
      state.batches.unshift({ id: 'b-' + Date.now(), name: String(fd.get('name')).trim(), desc: 'Custom batch' });
      saveState(); toast('Batch created'); render();
    };
    container.querySelectorAll('[data-copy-preset]').forEach(b => b.onclick = () => {
      const p = PRESET_BATCHES.find(x => x.id === b.dataset.copyPreset);
      if (p) { state.batches.unshift({ id: 'b-' + Date.now(), name: p.name + ' (My Copy)', desc: p.desc }); saveState(); toast('Copied preset batch'); render(); }
    });
    container.querySelectorAll('[data-del-batch]').forEach(b => b.onclick = () => {
      state.batches = state.batches.filter(x => x.id !== b.dataset.delBatch);
      saveState(); toast('Batch deleted'); render();
    });
  }

  function renderMockTests(container) {
    const filter = state.mockExamFilter || 'ALL';
    const filtered = filter === 'ALL' ? state.attempts : state.attempts.filter(a => a.exam === filter);
    const totalTests = filtered.length;
    const avgPct = totalTests ? Math.round(filtered.reduce((s, a) => s + (a.pct || 0), 0) / totalTests) : 0;
    const bestPct = totalTests ? Math.max(...filtered.map(a => a.pct || 0)) : 0;
    const avgAcc = totalTests ? Math.round(filtered.reduce((s, a) => s + (a.acc || 0), 0) / totalTests) : 0;

    container.innerHTML = `
      <div class="space-y-4">
        <!-- Hero Mock Performance Card (Syllabus Style) -->
        <div class="glass-card rounded-3xl p-5 space-y-2.5">
          <div class="flex items-center justify-between gap-2">
            <div>
              <div class="text-lg sm:text-xl font-extrabold">Mock Test Data Tracker</div>
              <div class="text-[11px] opacity-80">Record & track your mock test scores, accuracy, and weak topics like Syllabus</div>
            </div>
            <div class="text-3xl font-black">${avgPct}%</div>
          </div>
          <div class="h-3 rounded-full bg-slate-900/15 dark:bg-white/15 overflow-hidden">
            <div class="h-full rounded-full transition-all duration-300" style="width:${Math.max(0, Math.min(100, avgPct))}%;background:${state.theme.accent}"></div>
          </div>
          <div class="text-[11px] opacity-80">Average Score (${filter === 'ALL' ? 'All Exams' : filter}) • Avg Accuracy: ${avgAcc}%</div>
        </div>

        <!-- 3 Stat Cards -->
        <div class="grid grid-cols-3 gap-2.5">
          <div class="glass-card rounded-2xl p-3 flex items-center gap-2 bg-orange-500/15 border-orange-400/50">
            <div class="w-8 h-8 rounded-xl bg-orange-500 text-white flex items-center justify-center shrink-0">📝</div>
            <div><div class="text-lg font-black leading-none">${totalTests}</div><div class="text-[11px] font-semibold opacity-80">Tests</div></div>
          </div>
          <div class="glass-card rounded-2xl p-3 flex items-center gap-2">
            <div class="w-8 h-8 rounded-xl bg-emerald-600 text-white flex items-center justify-center shrink-0">🏆</div>
            <div><div class="text-lg font-black leading-none">${bestPct}%</div><div class="text-[11px] font-semibold opacity-80">Best</div></div>
          </div>
          <div class="glass-card rounded-2xl p-3 flex items-center gap-2 bg-emerald-500/15 border-emerald-400/50">
            <div class="w-8 h-8 rounded-xl bg-emerald-500 text-white flex items-center justify-center shrink-0">🎯</div>
            <div><div class="text-lg font-black leading-none">${avgAcc}%</div><div class="text-[11px] font-semibold opacity-80">Accuracy</div></div>
          </div>
        </div>

        <!-- Exam Filter Pills + Add Mock Record Button -->
        <div class="flex flex-wrap items-center justify-between gap-2">
          <div class="flex items-center gap-2 overflow-x-auto pb-1">
            <button data-mfilter="ALL" class="px-4 py-1.5 rounded-full text-xs font-bold shrink-0 ${filter==='ALL'?'text-white shadow':'glass-pill'}" style="${filter==='ALL'?`background:${state.theme.accent}`:''}">ALL</button>
            ${state.exams.map(e => `
              <button data-mfilter="${esc(e.code)}" class="px-4 py-1.5 rounded-full text-xs font-bold shrink-0 ${filter===e.code?'text-white shadow':'glass-pill'}" style="${filter===e.code?`background:${state.theme.accent}`:''}">${esc(e.code)}</button>
            `).join('')}
          </div>
          <button id="btn-add-mock-record" class="px-4 py-2 rounded-2xl text-xs font-bold text-white shadow" style="background:${state.theme.accent}">+ Add Mock Test Data</button>
        </div>

        <!-- Mock Test Records List (Syllabus Card Style) -->
        <div class="space-y-3">
          ${filtered.length === 0 ? `
            <div class="glass-card rounded-3xl p-6 text-center space-y-2">
              <div class="text-sm font-bold">No mock test records yet</div>
              <p class="text-xs opacity-75">Tap "+ Add Mock Test Data" to log scores from PW, RWA, Testbook, YouTube, or Offline tests.</p>
            </div>
          ` : filtered.map(a => `
            <div class="glass-card rounded-3xl p-4 space-y-2.5">
              <div class="flex items-start justify-between gap-2">
                <div class="min-w-0">
                  <div class="font-bold text-base leading-snug truncate">${esc(a.title)}</div>
                  <div class="flex flex-wrap items-center gap-2 mt-1 text-[11px] opacity-80">
                    <span class="px-2 py-0.5 rounded-full font-bold text-white" style="background:${state.theme.accent}">${esc(a.exam)}</span>
                    <span class="px-2 py-0.5 rounded-full bg-white/60 dark:bg-slate-800 font-semibold">${esc(a.source || 'Mock')}</span>
                    <span>📅 ${esc(a.date || '')}</span>
                  </div>
                </div>
                <div class="text-right shrink-0">
                  <div class="text-lg font-black leading-none">${a.score}/${a.max}</div>
                  <div class="text-xs font-bold mt-0.5" style="color:${state.theme.accent}">${a.pct}%</div>
                </div>
              </div>

              <div class="grid grid-cols-4 gap-2 text-center text-xs">
                <div class="py-1.5 rounded-xl bg-emerald-500/15 font-bold">✓ ${a.correct}</div>
                <div class="py-1.5 rounded-xl bg-rose-500/15 font-bold">✗ ${a.wrong}</div>
                <div class="py-1.5 rounded-xl bg-white/45 dark:bg-slate-800/55 font-bold">− ${a.unattempted || 0}</div>
                <div class="py-1.5 rounded-xl bg-sky-500/15 font-bold">🎯 ${a.acc}%</div>
              </div>

              ${a.weak ? `<div class="text-xs opacity-85"><span class="font-bold">Weak Topics / Notes:</span> ${esc(a.weak)}</div>` : ''}

              <div class="flex items-center justify-between pt-1 text-xs">
                <button data-del-mock="${a.id}" class="opacity-75 hover:text-rose-500 font-semibold">🗑️ Remove record</button>
                <button data-edit-mock="${a.id}" class="font-bold" style="color:${state.theme.accent}">✏️ Edit score</button>
              </div>
            </div>
          `).join('')}
        </div>
      </div>`;

    container.querySelectorAll('[data-mfilter]').forEach(b => b.onclick = () => {
      state.mockExamFilter = b.dataset.mfilter;
      saveState(); render();
    });

    const openMockFormModal = (existing) => {
      openModal(existing ? 'Edit Mock Test Record' : 'Add Mock Test Data', `
        <input name="title" required value="${esc(existing ? existing.title : '')}" placeholder="Test Name (e.g. RWA Full Mock #3)" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
        <div class="grid grid-cols-2 gap-2">
          <select name="exam" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none">
            ${state.exams.map(e => `<option value="${esc(e.code)}" ${(existing ? existing.exam : getActiveExam().code)===e.code?'selected':''}>${esc(e.code)}</option>`).join('')}
          </select>
          <select name="source" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none">
            ${MOCK_SOURCES.map(s => `<option value="${s}" ${(existing ? existing.source : 'PW')===s?'selected':''}>${s}</option>`).join('')}
          </select>
        </div>
        <div class="grid grid-cols-3 gap-2">
          <input name="score" type="number" step="0.25" required value="${existing ? existing.score : ''}" placeholder="Marks Got" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
          <input name="max" type="number" step="0.25" required value="${existing ? existing.max : 50}" placeholder="Total Marks" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
          <input name="date" type="date" value="${esc(existing ? existing.date : new Date().toISOString().slice(0,10))}" class="px-2 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-xs outline-none" />
        </div>
        <div class="grid grid-cols-3 gap-2">
          <input name="correct" type="number" min="0" value="${existing ? existing.correct : 0}" placeholder="Correct" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
          <input name="wrong" type="number" min="0" value="${existing ? existing.wrong : 0}" placeholder="Wrong" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
          <input name="unattempted" type="number" min="0" value="${existing ? (existing.unattempted || 0) : 0}" placeholder="Skipped" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
        </div>
        <input name="weak" value="${esc(existing ? (existing.weak || '') : '')}" placeholder="Weak topics / notes (e.g. Optics, Preposition)" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-sm outline-none" />
      `, (fd) => {
        const score = Number(fd.get('score') || 0);
        const max = Math.max(1, Number(fd.get('max') || 50));
        const correct = Math.max(0, Number(fd.get('correct') || 0));
        const wrong = Math.max(0, Number(fd.get('wrong') || 0));
        const unattempted = Math.max(0, Number(fd.get('unattempted') || 0));
        const att = correct + wrong;
        const record = {
          id: existing ? existing.id : 'att-' + Date.now(),
          title: String(fd.get('title')).trim(),
          exam: String(fd.get('exam')),
          source: String(fd.get('source')),
          date: String(fd.get('date') || new Date().toISOString().slice(0,10)),
          score,
          max,
          pct: Math.round((score / max) * 100),
          correct,
          wrong,
          unattempted,
          acc: att ? Math.round((correct / att) * 100) : 0,
          weak: String(fd.get('weak') || '').trim()
        };
        if (existing) {
          state.attempts = state.attempts.map(x => x.id === existing.id ? record : x);
          toast('Mock test record updated');
        } else {
          state.attempts.unshift(record);
          toast('Mock test record saved');
        }
        saveState(); render();
      });
    };

    container.querySelector('#btn-add-mock-record').onclick = () => openMockFormModal(null);
    container.querySelectorAll('[data-edit-mock]').forEach(b => b.onclick = () => {
      const rec = state.attempts.find(x => x.id === b.dataset.editMock);
      if (rec) openMockFormModal(rec);
    });
    container.querySelectorAll('[data-del-mock]').forEach(b => b.onclick = () => {
      const rec = state.attempts.find(x => x.id === b.dataset.delMock);
      if (!rec) return;
      openModal('Delete Mock Test Record?', `<p class="text-xs opacity-80">Delete "${esc(rec.title)}" from your mock test tracker?</p>`, () => {
        state.attempts = state.attempts.filter(x => x.id !== rec.id);
        saveState(); toast('Mock test record removed'); render();
      });
    });
  }

  let pomoTimer = null;
  function renderPlanner(container) {
    const mins = Math.floor(state.pomo.secLeft / 60), secs = state.pomo.secLeft % 60;
    container.innerHTML = `
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div class="glass-card rounded-3xl p-5 text-center space-y-3">
          <div class="font-extrabold text-base">Pomodoro Focus Timer</div>
          <div id="pomo-display" class="text-5xl font-black tabular-nums">${String(mins).padStart(2,'0')}:${String(secs).padStart(2,'0')}</div>
          <div class="flex justify-center gap-2">
            ${[15,25,45].map(m => `&lt;button data-pomo-set=&quot;${m}&quot; class=&quot;px-3 py-1 rounded-xl text-xs font-bold ${state.pomo.preset===m?&#39;text-white&#39;:&#39;glass-pill&#39;}&quot; style=&quot;${state.pomo.preset===m?`background:${state.theme.accent}`:&#39;&#39;}&quot;&gt;${m}m&lt;/button&gt;`).join('')}
          </div>
          <div class="flex justify-center gap-2">
            <button id="btn-pomo-toggle" class="px-5 py-2 rounded-xl text-xs font-bold text-white" style="background:${state.theme.accent}">${state.pomo.running ? 'Pause' : 'Start Focus'}</button>
            <button id="btn-pomo-log" class="glass-pill px-4 py-2 rounded-xl text-xs font-bold">Log ${state.pomo.preset}m Session</button>
          </div>
        </div>
        <div class="glass-card rounded-3xl p-5 space-y-3">
          <div class="font-extrabold text-base">Daily & Weekly Study Goals</div>
          <form id="goal-form" class="flex gap-2">
            <input name="title" required placeholder="Add goal (e.g. Revise Tense)" class="flex-1 px-3 py-2 rounded-xl bg-white/75 dark:bg-slate-800 text-xs outline-none" />
            <button type="submit" class="px-3.5 py-2 rounded-xl text-xs font-bold text-white" style="background:${state.theme.accent}">Add</button>
          </form>
          <div class="space-y-1.5">
            ${state.goals.length === 0 ? '<p class="text-xs opacity-75">No goals added yet.</p>' : state.goals.map(g => `
              &lt;button data-toggle-goal=&quot;${g.id}&quot; class=&quot;w-full text-left p-2.5 rounded-xl bg-white/45 dark:bg-slate-800/55 text-xs flex items-center gap-2&quot;&gt;
                &lt;span&gt;${g.done ? '✅' : '⬜'}&lt;/span&gt;&lt;span class=&quot;${g.done ? &#39;line-through opacity-60&#39; : &#39;font-semibold&#39;}&quot;&gt;${esc(g.title)}&lt;/span&gt;
              &lt;/button&gt;`).join('')}
          </div>
        </div>
      </div>`;

    container.querySelectorAll('[data-pomo-set]').forEach(b => b.onclick = () => {
      if (pomoTimer) clearInterval(pomoTimer);
      state.pomo = { preset: Number(b.dataset.pomoSet), secLeft: Number(b.dataset.pomoSet)*60, running: false };
      render();
    });
    container.querySelector('#btn-pomo-toggle').onclick = () => {
      state.pomo.running = !state.pomo.running;
      if (pomoTimer) clearInterval(pomoTimer);
      if (state.pomo.running) {
        pomoTimer = setInterval(() => {
          state.pomo.secLeft--;
          const d = document.getElementById('pomo-display');
          if (d) d.textContent = `${String(Math.floor(state.pomo.secLeft/60)).padStart(2,'0')}:${String(state.pomo.secLeft%60).padStart(2,'0')}`;
          if (state.pomo.secLeft <= 0) {
            clearInterval(pomoTimer);
            state.pomo.running = false;
            state.sessions.push({ date: new Date().toISOString().slice(0,10), mins: state.pomo.preset });
            saveState(); toast('Pomodoro completed & logged!'); render();
          }
        }, 1000);
      }
      render();
    };
    container.querySelector('#btn-pomo-log').onclick = () => {
      state.sessions.push({ date: new Date().toISOString().slice(0,10), mins: state.pomo.preset });
      saveState(); toast(`Logged ${state.pomo.preset} min study session`); render();
    };
    container.querySelector('#goal-form').onsubmit = (e) => {
      e.preventDefault();
      const fd = new FormData(e.target);
      state.goals.unshift({ id: 'g-' + Date.now(), title: String(fd.get('title')).trim(), done: false });
      saveState(); render();
    };
    container.querySelectorAll('[data-toggle-goal]').forEach(b => b.onclick = () => {
      const g = state.goals.find(x => x.id === b.dataset.toggleGoal);
      if (g) { g.done = !g.done; saveState(); render(); }
    });
  }

  function renderAnalytics(container) {
    const allChapters = state.exams.flatMap(e => e.subjects.flatMap(s => s.chapters));
    const st = chapterStats(allChapters);
    const totalMins = state.sessions.reduce((a,b) => a + b.mins, 0);
    container.innerHTML = `
      <div class="glass-card rounded-3xl p-5 space-y-4">
        <div class="font-extrabold text-base">Analytics Overview</div>
        <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 text-center">
          <div class="p-3 rounded-2xl bg-white/45 dark:bg-slate-800/55"><div class="text-2xl font-black text-emerald-500">${st.completed}</div><div class="text-xs">Completed</div></div>
          <div class="p-3 rounded-2xl bg-white/45 dark:bg-slate-800/55"><div class="text-2xl font-black text-sky-500">${st.inProgress}</div><div class="text-xs">In Progress</div></div>
          <div class="p-3 rounded-2xl bg-white/45 dark:bg-slate-800/55"><div class="text-2xl font-black text-amber-500">${st.revReq}</div><div class="text-xs">Rev. Needed</div></div>
          <div class="p-3 rounded-2xl bg-white/45 dark:bg-slate-800/55"><div class="text-2xl font-black text-orange-500">${totalMins}m</div><div class="text-xs">Study Time</div></div>
        </div>
      </div>`;
  }

  function renderBabaAI(container) {
    container.innerHTML = `
      <div class="space-y-3 flex flex-col h-[calc(100vh-11.5rem)] min-h-[420px]">
        <div class="glass-card rounded-3xl p-3.5 flex items-center justify-between gap-2">
          <div>
            <div class="font-extrabold text-sm">🤖 Baba AI Study Assistant</div>
            <div class="text-[11px] opacity-75">Preview simulator (Live Gemini runs via /api/baba-ai on Vercel)</div>
          </div>
          <select id="baba-lang" class="glass-pill px-2.5 py-1 rounded-xl text-xs font-bold outline-none">
            <option value="hinglish" ${state.theme.babaLang==='hinglish'?'selected':''}>Hinglish</option>
            <option value="hindi" ${state.theme.babaLang==='hindi'?'selected':''}>हिंदी</option>
            <option value="english" ${state.theme.babaLang==='english'?'selected':''}>English</option>
          </select>
        </div>
        <div class="glass-card rounded-3xl p-4 flex-1 overflow-y-auto space-y-2.5">
          ${state.babaMessages.map(m => `
            &lt;div class=&quot;flex ${m.role===&#39;user&#39;?&#39;justify-end&#39;:&#39;justify-start&#39;}&quot;&gt;
              &lt;div class=&quot;max-w-[85%] rounded-2xl px-3.5 py-2.5 text-sm ${m.role===&#39;user&#39;?&#39;text-white&#39;:&#39;bg-white/75 dark:bg-slate-800/85&#39;}&quot; style=&quot;${m.role===&#39;user&#39;?`background:${state.theme.accent}`:&#39;&#39;}&quot;&gt;${esc(m.text)}&lt;/div&gt;
            &lt;/div&gt;`).join('')}
        </div>
        <form id="baba-form" class="glass-card rounded-3xl p-2 flex gap-2">
          <input name="msg" required placeholder="Ask Baba AI (e.g. 'My progress' or '7-day study plan')..." class="flex-1 bg-transparent px-3 py-2 text-sm outline-none" />
          <button type="submit" class="px-4 py-2 rounded-2xl text-xs font-bold text-white" style="background:${state.theme.accent}">Send</button>
        </form>
      </div>`;

    container.querySelector('#baba-lang').onchange = (e) => {
      state.theme.babaLang = e.target.value; saveState();
    };
    container.querySelector('#baba-form').onsubmit = (e) => {
      e.preventDefault();
      const text = new FormData(e.target).get('msg').toString().trim();
      if (!text) return;
      state.babaMessages.push({ role: 'user', text });
      const ex = getActiveExam();
      const st = chapterStats(ex.subjects.flatMap(s => s.chapters));
      const lang = state.theme.babaLang;
      let reply = '';
      if (lang === 'hindi') {
        reply = `जय हिन्द! अभी आपकी ${ex.code} तैयारी ${st.pct}% (${st.completed}/${st.total} अध्याय) पर है। लाइव जेमिनी उत्तरों के लिए Vercel पर GEMINI_API_KEY सेट करें।`;
      } else if (lang === 'english') {
        reply = `Jai Hind! Your current ${ex.code} progress is ${st.pct}% (${st.completed}/${st.total} chapters completed). Deploy to Vercel with GEMINI_API_KEY to activate live Gemini answers and automated chapter actions.`;
      } else {
        reply = `Jai Hind! Abhi aapki ${ex.code} progress ${st.pct}% (${st.completed}/${st.total} chapters) hai. Roz 2 Pomodoro sessions + 1 revision target rakhein! Live Gemini AI replies ke liye Vercel par GEMINI_API_KEY add karein.`;
      }
      state.babaMessages.push({ role: 'assistant', text: reply });
      saveState(); render();
    };
  }

  function renderSettings(container) {
    container.innerHTML = `
      <div class="space-y-4">
        <div class="glass-card rounded-3xl p-5 space-y-4">
          <div class="flex items-center justify-between">
            <div class="font-extrabold text-base">Theme, Accent & Background</div>
            <button id="btn-mode-toggle" class="glass-pill px-3.5 py-1.5 rounded-xl text-xs font-bold">${state.theme.mode==='dark'?'☀️ Switch to Light':'🌙 Switch to Dark'}</button>
          </div>
          <div>
            <div class="text-xs font-bold mb-2">Accent Color</div>
            <div class="flex flex-wrap gap-2">
              ${ACCENTS.map(a => `&lt;button data-acc=&quot;${a.hex}&quot; class=&quot;px-3 py-1.5 rounded-full text-xs font-bold text-white ${state.theme.accent===a.hex?&#39;ring-2 ring-white&#39;:&#39;&#39;}&quot; style=&quot;background:${a.hex}&quot;&gt;${a.name}&lt;/button&gt;`).join('')}
            </div>
          </div>
          <div>
            <div class="text-xs font-bold mb-2">Preset Backgrounds</div>
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2">
              ${PRESET_BACKGROUNDS.map(b => `&lt;button data-bg=&quot;${b.id}&quot; class=&quot;h-14 rounded-2xl p-2 text-left text-[11px] font-bold text-white shadow flex items-end border-2 ${!state.theme.customBg &amp;&amp; state.theme.bgId===b.id?&#39;border-white&#39;:&#39;border-transparent&#39;}&quot; style=&quot;background-image:${b.css}&quot;&gt;${b.name}&lt;/button&gt;`).join('')}
            </div>
          </div>
          <div class="flex flex-wrap items-center gap-2">
            <label class="px-4 py-2 rounded-xl text-xs font-bold text-white cursor-pointer" style="background:${state.theme.accent}">
              📷 Choose Gallery Image
              <input id="inp-gallery" type="file" accept="image/*" class="hidden" />
            </label>
            ${state.theme.customBg ? '<button id="btn-clear-bg" class="glass-pill px-3 py-2 rounded-xl text-xs font-bold">Remove Custom Image</button>' : ''}
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 text-xs">
            <label>Blur (${state.theme.blur}px)<input id="rng-blur" type="range" min="0" max="16" value="${state.theme.blur}" class="w-full mt-1" /></label>
            <label>Overlay (${Math.round(state.theme.overlay*100)}%)<input id="rng-ov" type="range" min="0.1" max="0.85" step="0.05" value="${state.theme.overlay}" class="w-full mt-1" /></label>
            <label>Position
              <select id="sel-pos" class="w-full mt-1 px-2.5 py-1.5 rounded-xl bg-white/75 dark:bg-slate-800">
                <option value="center" ${state.theme.pos==='center'?'selected':''}>Center</option>
                <option value="top" ${state.theme.pos==='top'?'selected':''}>Top</option>
                <option value="bottom" ${state.theme.pos==='bottom'?'selected':''}>Bottom</option>
              </select>
            </label>
          </div>
        </div>
      </div>`;

    container.querySelector('#btn-mode-toggle').onclick = () => {
      state.theme.mode = state.theme.mode === 'dark' ? 'light' : 'dark';
      saveState(); render();
    };
    container.querySelectorAll('[data-acc]').forEach(b => b.onclick = () => {
      state.theme.accent = b.dataset.acc; saveState(); render();
    });
    container.querySelectorAll('[data-bg]').forEach(b => b.onclick = () => {
      state.theme.bgId = b.dataset.bg; state.theme.customBg = ''; saveState(); render();
    });
    container.querySelector('#inp-gallery').onchange = (e) => {
      const f = e.target.files && e.target.files[0];
      if (!f) return;
      const r = new FileReader();
      r.onload = () => { state.theme.customBg = String(r.result); saveState(); toast('Background updated!'); render(); };
      r.readAsDataURL(f);
    };
    const clearBtn = container.querySelector('#btn-clear-bg');
    if (clearBtn) clearBtn.onclick = () => { state.theme.customBg = ''; saveState(); render(); };
    container.querySelector('#rng-blur').oninput = (e) => { state.theme.blur = Number(e.target.value); applyTheme(); saveState(); };
    container.querySelector('#rng-ov').oninput = (e) => { state.theme.overlay = Number(e.target.value); applyTheme(); saveState(); };
    container.querySelector('#sel-pos').onchange = (e) => { state.theme.pos = e.target.value; applyTheme(); saveState(); };
  }

  function render() {
    applyTheme();
    renderNav();
    const view = document.getElementById('main-view');
    if (state.tab === 'syllabus') renderSyllabus(view);
    else if (state.tab === 'dashboard') renderDashboard(view);
    else if (state.tab === 'batches') renderBatches(view);
    else if (state.tab === 'mock-tests') renderMockTests(view);
    else if (state.tab === 'planner') renderPlanner(view);
    else if (state.tab === 'analytics') renderAnalytics(view);
    else if (state.tab === 'baba-ai') renderBabaAI(view);
    else renderSettings(view);
  }

  document.getElementById('btn-quick-theme').onclick = () => {
    state.theme.mode = state.theme.mode === 'dark' ? 'light' : 'dark';
    saveState(); render();
  };

  render();
})();
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
