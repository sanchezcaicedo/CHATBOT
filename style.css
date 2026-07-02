<!DOCTYPE html>
<html lang="es" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>SocialPulse AI - Social Media Command Center</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fdf4ff',
                            100: '#f3e8ff',
                            200: '#e9d5ff',
                            500: '#d946ef', /* Magenta/Fuchsia social vibe */
                            600: '#c084fc',
                            700: '#a855f7',
                            900: '#581c87',
                        }
                    }
                }
            }
        }
    </script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: #4b5563;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #6b7280;
        }
        /* Optimizaciones de scroll táctil */
        #messages-box, #ideas-grid, #editor-panel, #preview-panel {
            overflow-y: auto !important;
            touch-action: pan-y;
            -webkit-overflow-scrolling: touch;
            overscroll-behavior-y: contain;
        }
    </style>
    <script>
        // Declaramos las funciones clave en el head para prevenir cualquier "ReferenceError" al hacer click temprano
        let activeApiKey = "";
        let selectedAgentId = 'copywriter';
        let currentTab = 'editor';
        let previewPlatform = 'instagram';
        let ideasDatabase = [
            { id: 'idea-1', title: 'Tono de Voz de Marca', content: 'Somos una marca de tecnología moderna, cercana, entusiasta y sumamente didáctica. Evitamos el lenguaje corporativo aburrido; preferimos usar analogías cotidianas y frescas.' },
            { id: 'idea-2', title: 'Hashtags Frecuentes', content: '#Tecnologia #SocialMediaMarketing #InteligenciaArtificial #Productividad #Innovacion #NegociosDigitales' },
            { id: 'idea-3', title: 'Pilar de Contenido: Tips de Enfoque', content: 'Todos los martes publicamos un tip práctico de productividad que tome menos de 2 minutos aplicar para mejorar el balance vida-trabajo.' }
        ];

        let chatHistories = {
            copywriter: [{ sender: 'assistant', text: '## ¡Hola! Soy tu **Copywriter Viral**.\n\nEstoy listo para ayudarte a redactar los copys más atractivos para Instagram, TikTok y Threads. \n\nEscribe el tema que quieres desarrollar o pídeme ideas de contenido creativas para tu marca.' }],
            linkedin: [{ sender: 'assistant', text: '## Portal de Autoridad Profesional\n\nBienvenido, líder. Soy tu **Estratega de LinkedIn y X**. \n\nDiseñemos publicaciones de alto valor técnico, opiniones disruptivas de mercado o hilos detallados para elevar tu marca personal y conversiones profesionales. ¿Qué tema abordamos hoy?' }],
            traffic: [{ sender: 'assistant', text: '## Laboratorio de Conversiones & Ads\n\nHola. Soy tu **Estratega de Ads**. \n\nEstructuraremos ganchos de conversión, ángulos de venta directos y copys de alto impacto para tus anuncios pagados. ¿Qué producto u oferta queremos escalar hoy?' }]
        };
    </script>
</head>
<body class="bg-slate-950 text-slate-100 h-screen w-screen flex flex-col font-sans overflow-hidden fixed inset-0">

    <!-- CABECERA -->
    <header class="border-b border-slate-800 bg-slate-900/50 px-6 py-4 flex items-center justify-between shrink-0 z-10">
        <div class="flex items-center gap-3">
            <div class="bg-gradient-to-tr from-fuchsia-500 to-violet-600 p-2.5 rounded-xl text-white shadow-lg shadow-fuchsia-500/25">
                <i data-lucide="sparkles" class="w-6 h-6"></i>
            </div>
            <div>
                <h1 class="text-base sm:text-lg font-black bg-gradient-to-r from-fuchsia-400 via-purple-400 to-cyan-400 bg-clip-text text-transparent leading-none">
                    SocialPulse AI
                </h1>
                <p class="text-[10px] sm:text-xs text-slate-400 mt-1">Copiloto Inteligente de Contenido y Estrategia Social</p>
            </div>
        </div>
        <div class="flex items-center gap-2 bg-fuchsia-500/10 border border-fuchsia-500/20 px-3 py-1.5 rounded-full">
            <span class="w-2 h-2 rounded-full bg-fuchsia-500 animate-pulse"></span>
            <span class="text-[10px] text-fuchsia-400 font-bold uppercase tracking-wider">Workspace Activo</span>
        </div>
    </header>

    <!-- NAVEGACIÓN TÁCTIL PARA MÓVILES -->
    <div class="md:hidden flex border-b border-slate-800 bg-slate-900/30 p-2 justify-around shrink-0 z-10">
        <button id="mobile-tab-editor" class="flex flex-col items-center gap-1 py-1 px-3 text-xs font-semibold text-fuchsia-400">
            <i data-lucide="layout" class="w-5 h-5"></i>
            <span>Editor</span>
        </button>
        <button id="mobile-tab-chat" class="flex flex-col items-center gap-1 py-1 px-3 text-xs font-semibold text-slate-400">
            <i data-lucide="message-square" class="w-5 h-5"></i>
            <span>Copiloto</span>
        </button>
        <button id="mobile-tab-ideas" class="flex flex-col items-center gap-1 py-1 px-3 text-xs font-semibold text-slate-400">
            <i data-lucide="folder-heart" class="w-5 h-5"></i>
            <span>Ideas</span>
        </button>
    </div>

    <!-- CONTENEDOR CENTRAL -->
    <div class="flex flex-1 overflow-hidden relative w-full h-full">
        
        <!-- SIDEBAR DE SELECCIÓN DE AGENTES (Escritorio) -->
        <aside class="w-64 border-r border-slate-800 bg-slate-900/30 flex flex-col justify-between shrink-0 hidden md:flex">
            <div class="p-4 space-y-6">
                <div>
                    <span class="text-[10px] font-bold tracking-wider text-slate-500 uppercase px-2">Herramientas</span>
                    <nav class="mt-2 space-y-1">
                        <button id="side-tab-editor" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm font-medium bg-fuchsia-600/10 text-fuchsia-400 border border-fuchsia-500/20">
                            <i data-lucide="layout" class="w-4 h-4"></i>
                            Editor & Previsualizador
                        </button>
                        <button id="side-tab-chat" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm font-medium text-slate-400 hover:bg-slate-800/50">
                            <i data-lucide="message-square" class="w-4 h-4"></i>
                            Chat Asistente IA
                        </button>
                        <button id="side-tab-ideas" class="w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm font-medium text-slate-400 hover:bg-slate-800/50">
                            <i data-lucide="folder-heart" class="w-4 h-4"></i>
                            Banco de Ideas (RAG)
                            <span id="idea-count-badge" class="ml-auto bg-slate-800 text-slate-300 text-xs px-2 py-0.5 rounded-full">3</span>
                        </button>
                    </nav>
                </div>

                <div class="pt-4 border-t border-slate-800">
                    <span class="text-[10px] font-bold tracking-wider text-slate-500 uppercase px-2">Especialista Activo</span>
                    <div class="mt-3 space-y-2" id="agent-selector-container">
                        <!-- Cargados por JS -->
                    </div>
                </div>
            </div>

            <div class="p-4 border-t border-slate-800 bg-slate-950/40 text-[11px] text-slate-400 space-y-2">
                <div class="flex items-center justify-between text-[11px] font-medium text-slate-300">
                    <span>Inyección RAG:</span>
                    <span class="text-fuchsia-400 flex items-center gap-1"><i data-lucide="check-circle" class="w-3 h-3"></i> Auto-Conectado</span>
                </div>
                <p class="leading-relaxed">Tus ideas guardadas enriquecen el contexto del chat para crear contenido coherente con tu marca de manera automatizada.</p>
            </div>
        </aside>

        <!-- SECCIÓN 1: EDITOR DE PUBLICACIONES Y PREVIEW (Panel Central/Izquierdo) -->
        <section class="flex-1 border-r border-slate-850 bg-slate-950 flex flex-col lg:flex-row shrink-0 h-full overflow-hidden" id="tab-content-editor">
            
            <!-- Entrada y Herramientas Rápidas -->
            <div class="flex-1 p-4 sm:p-6 flex flex-col h-1/2 lg:h-full overflow-y-auto space-y-4 border-b lg:border-b-0 lg:border-r border-slate-850" id="editor-panel">
                <div class="flex items-center justify-between">
                    <h2 class="text-sm font-extrabold uppercase tracking-wider text-slate-300 flex items-center gap-2">
                        <i data-lucide="edit-3" class="w-4 h-4 text-fuchsia-500"></i> Borrador de Contenido
                    </h2>
                    <span class="text-xs text-slate-500" id="char-counter">0 caracteres</span>
                </div>

                <textarea 
                    id="post-draft" 
                    placeholder="Escribe el borrador de tu publicación aquí o pídele a la IA en la pestaña de chat que redacte uno..." 
                    class="w-full flex-1 min-h-[140px] bg-slate-900/60 border border-slate-800 focus:border-fuchsia-500 focus:ring-2 focus:ring-fuchsia-500/20 rounded-2xl p-4 text-sm text-slate-200 placeholder-slate-500 focus:outline-none resize-none transition-all"
                ></textarea>

                <!-- Botones de Acción de IA de un Solo Clic -->
                <div class="space-y-2.5">
                    <span class="text-[10px] font-bold text-slate-500 uppercase tracking-wider block">Superpoderes de un toque (IA)</span>
                    <div class="grid grid-cols-2 gap-2">
                        <button id="btn-enhance-rewrite" class="bg-slate-900 border border-slate-800 hover:border-fuchsia-500/50 hover:bg-slate-850 text-slate-200 p-2.5 rounded-xl text-xs font-semibold flex items-center gap-2 transition-all">
                            <i data-lucide="wand-2" class="w-3.5 h-3.5 text-fuchsia-400"></i> Hacer Persuasivo
                        </button>
                        <button id="btn-enhance-hashtags" class="bg-slate-900 border border-slate-800 hover:border-fuchsia-500/50 hover:bg-slate-850 text-slate-200 p-2.5 rounded-xl text-xs font-semibold flex items-center gap-2 transition-all">
                            <i data-lucide="hash" class="w-3.5 h-3.5 text-cyan-400"></i> Crear Hashtags
                        </button>
                        <button id="btn-enhance-hook" class="bg-slate-900 border border-slate-800 hover:border-fuchsia-500/50 hover:bg-slate-850 text-slate-200 p-2.5 rounded-xl text-xs font-semibold flex items-center gap-2 transition-all">
                            <i data-lucide="zap" class="w-3.5 h-3.5 text-amber-400"></i> Generar Gancho Viral
                        </button>
                        <button id="btn-save-draft" class="bg-slate-900 border border-slate-800 hover:border-fuchsia-500/50 hover:bg-slate-850 text-slate-200 p-2.5 rounded-xl text-xs font-semibold flex items-center gap-2 transition-all">
                            <i data-lucide="folder-plus" class="w-3.5 h-3.5 text-emerald-400"></i> Guardar en Banco
                        </button>
                    </div>
                </div>
            </div>

            <!-- Previsualizador de Redes Sociales -->
            <div class="flex-1 p-4 sm:p-6 bg-slate-900/10 flex flex-col h-1/2 lg:h-full overflow-y-auto space-y-4" id="preview-panel">
                <div class="flex items-center justify-between shrink-0">
                    <h2 class="text-sm font-extrabold uppercase tracking-wider text-slate-300 flex items-center gap-2">
                        <i data-lucide="eye" class="w-4 h-4 text-fuchsia-500"></i> Previsualizador Social
                    </h2>
                    
                    <!-- Selector de Plataformas -->
                    <div class="flex bg-slate-900 p-1 rounded-lg border border-slate-800">
                        <button id="platform-btn-instagram" class="p-1.5 rounded-md text-fuchsia-450 bg-slate-800" title="Instagram">
                            <i data-lucide="instagram" class="w-4 h-4"></i>
                        </button>
                        <button id="platform-btn-twitter" class="p-1.5 rounded-md text-slate-400 hover:text-slate-200" title="X / Twitter">
                            <i data-lucide="twitter" class="w-4 h-4"></i>
                        </button>
                        <button id="platform-btn-linkedin" class="p-1.5 rounded-md text-slate-400 hover:text-slate-200" title="LinkedIn">
                            <i data-lucide="linkedin" class="w-4 h-4"></i>
                        </button>
                    </div>
                </div>

                <!-- Tarjeta de Vista Previa Dinámica -->
                <div id="social-preview-card" class="bg-slate-900 border border-slate-800 rounded-2xl p-4 space-y-3 shadow-xl max-w-sm mx-auto w-full transition-all duration-300">
                    <!-- El preview se renderiza dinámicamente según la plataforma activa -->
                </div>
            </div>

        </section>

        <!-- SECCIÓN 2: CHAT ASISTENTE (Copiloto) -->
        <section class="w-full md:w-[350px] lg:w-96 flex flex-col h-full overflow-hidden bg-slate-950 relative hidden md:flex" id="tab-content-chat">
            <div class="px-6 py-4.5 border-b border-slate-850 bg-slate-900/20 flex items-center justify-between shrink-0">
                <div class="flex items-center gap-2.5 min-w-0">
                    <div class="w-2.5 h-2.5 rounded-full bg-fuchsia-500 shrink-0" id="agent-indicator"></div>
                    <span class="font-extrabold text-xs uppercase tracking-wider text-slate-200 truncate" id="chat-agent-title">Copywriter Viral</span>
                </div>
                <button id="btn-clear-chat" class="text-[10px] text-slate-400 hover:text-rose-400 transition-colors uppercase font-bold flex items-center gap-1 shrink-0">
                    <i data-lucide="trash-2" class="w-3.5 h-3.5"></i> Borrar
                </button>
            </div>

            <!-- Ventana de Mensajes del Chat -->
            <div id="messages-box" class="flex-1 p-4 space-y-4 overflow-y-auto pb-36">
                <!-- Globos de conversación -->
            </div>

            <!-- Entrada del Chat -->
            <div class="absolute bottom-0 inset-x-0 p-4 bg-slate-950/95 border-t border-slate-850 backdrop-blur-md z-25 shrink-0">
                <!-- Indicador RAG en la barra de chat -->
                <div id="rag-chat-bar" class="hidden mb-2 px-3 py-1.5 rounded-lg bg-fuchsia-500/10 border border-fuchsia-500/20 text-[11px] text-fuchsia-400 flex items-center gap-1.5">
                    <i data-lucide="database" class="w-3.5 h-3.5"></i>
                    <span>Contexto de marca conectado: <strong id="rag-badge-count">0</strong> ideas inyectadas.</span>
                </div>

                <form id="chat-form" class="flex gap-2 relative items-end">
                    <textarea 
                        id="user-input" 
                        rows="1"
                        placeholder="Pregúntame o pídeme un post..." 
                        class="flex-1 bg-slate-900 border border-slate-850 rounded-xl px-4 py-3 focus:outline-none focus:ring-2 focus:ring-fuchsia-500/20 text-sm text-slate-100 placeholder-slate-500 resize-none max-h-24 min-h-[46px]"
                    ></textarea>
                    
                    <button type="submit" class="bg-fuchsia-600 hover:bg-fuchsia-500 text-white rounded-xl w-12 h-11 flex items-center justify-center transition-colors shadow-lg shadow-fuchsia-500/10 shrink-0">
                        <i data-lucide="send" class="w-5 h-5"></i>
                    </button>
                </form>
            </div>
        </section>

        <!-- SECCIÓN 3: BANCO DE IDEAS / CONOCIMIENTO (RAG) -->
        <section class="w-full flex-1 bg-slate-950 flex flex-col shrink-0 h-full overflow-hidden hidden" id="tab-content-ideas">
            <div class="p-6 space-y-6 flex-1 overflow-y-auto pb-24" id="ideas-grid-panel">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-4 border-b border-slate-800">
                    <div>
                        <h2 class="text-lg font-bold text-slate-100 flex items-center gap-2">
                            <i data-lucide="folder-heart" class="w-5 h-5 text-fuchsia-500"></i> Banco de Ideas y Pilares de Marca
                        </h2>
                        <p class="text-xs text-slate-400 mt-1">Guarda las pautas de tu marca, hashtags recurrentes o ideas rápidas. El Copiloto de IA las utilizará de forma inteligente.</p>
                    </div>
                    <button id="btn-new-idea" class="bg-fuchsia-600 hover:bg-fuchsia-500 text-white text-xs font-semibold px-4 py-2.5 rounded-lg flex items-center gap-2 transition-all self-start shadow-lg">
                        <i data-lucide="plus" class="w-4 h-4"></i> Crear Idea / Pilar
                    </button>
                </div>

                <!-- Cuadrícula de tarjetas de ideas -->
                <div id="ideas-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <!-- Cargadas dinámicamente -->
                </div>
            </div>
        </section>

    </div>

    <!-- MODAL PARA AGREGAR NUEVA IDEA -->
    <div id="idea-modal" class="hidden fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-md w-full flex flex-col overflow-hidden shadow-2xl">
            <div class="px-6 py-4 border-b border-slate-800 flex items-center justify-between">
                <h3 class="text-sm font-bold text-slate-100">Crear Nueva Idea / Pilar de Marca</h3>
                <button id="btn-close-idea-modal" class="text-slate-400 hover:text-slate-200">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            <form id="idea-form" class="p-6 space-y-4">
                <div>
                    <label class="block text-[10px] font-bold text-slate-400 uppercase tracking-wider mb-2">Título de la Idea / Pilar</label>
                    <input type="text" id="idea-title" required placeholder="Ej. Guía de Tonos, Hashtags de Tech, Pilares de Marketing..." class="w-full bg-slate-950 border border-slate-800 rounded-lg px-4 py-2.5 text-xs text-slate-100 focus:outline-none focus:ring-1 focus:ring-fuchsia-500">
                </div>
                <div>
                    <label class="block text-[10px] font-bold text-slate-400 uppercase tracking-wider mb-2">Detalles / Contexto</label>
                    <textarea id="idea-content" required rows="5" placeholder="Escribe aquí las pautas, el copy básico, los objetivos de esta idea o las directrices..." class="w-full bg-slate-950 border border-slate-800 rounded-lg px-4 py-2.5 text-xs text-slate-100 resize-none focus:outline-none focus:ring-1 focus:ring-fuchsia-500"></textarea>
                </div>
                <div class="flex justify-end gap-3 pt-2">
                    <button type="button" id="btn-cancel-idea" class="px-4 py-2 rounded-lg text-xs font-semibold text-slate-400 hover:bg-slate-800">Cancelar</button>
                    <button type="submit" class="bg-fuchsia-600 hover:bg-fuchsia-500 text-white px-5 py-2 rounded-lg text-xs font-semibold shadow-lg">Guardar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- TOASTS DE ACCIÓN -->
    <div id="toast" class="fixed bottom-24 right-6 transform translate-y-20 opacity-0 bg-rose-950 border border-rose-800 px-4 py-3 rounded-xl shadow-2xl flex items-center gap-2.5 text-rose-200 text-xs font-semibold transition-all duration-300 z-50">
        <i data-lucide="alert-circle" class="w-5 h-5 text-rose-400 shrink-0"></i>
        <span id="toast-message"></span>
    </div>

    <div id="success-toast" class="fixed bottom-24 right-6 transform translate-y-20 opacity-0 bg-emerald-950 border border-emerald-800 px-4 py-3 rounded-xl shadow-2xl flex items-center gap-2.5 text-emerald-200 text-xs font-semibold transition-all duration-300 z-50">
        <i data-lucide="check" class="w-5 h-5 text-emerald-400 shrink-0"></i>
        <span id="success-toast-message"></span>
    </div>

    <!-- LÓGICA DE JAVASCRIPT DE CONTROL SEGURO -->
    <script>
        const AGENTS = [
            {
                id: 'copywriter',
                name: 'Copywriter Viral',
                icon: 'instagram',
                desc: 'Instagram & TikTok. Ganchos emocionales, carruseles y copys directos al grano.',
                systemPrompt: 'Eres un Copywriter de Redes Sociales de élite especializado en Instagram y TikTok. Tus respuestas deben ser detalladas y creativas. Cuando el usuario te pida redactar un post o dar ideas, estructura tu respuesta con: \n\n1. ## Ganchos de Impacto (Provee 3 opciones de títulos irresistibles de 3 segundos)\n2. ## Propuesta de Estructura de Copiloto (El copy definitivo adaptado a Instagram/TikTok con emojis estratégicos y espaciado limpio)\n3. ## Lista de Hashtags Virales (Recomienda hashtags de nicho, medianos y macro).'
            },
            {
                id: 'linkedin',
                name: 'Estratega de LinkedIn & X',
                icon: 'linkedin',
                desc: 'LinkedIn & X (Twitter). Hilos de autoridad, ganchos profesionales y marca personal.',
                systemPrompt: 'Eres un estratega de marca personal en LinkedIn y X. Ayudas al usuario a redactar hilos, opiniones de valor técnico y publicaciones de liderazgo intelectual. Estructura tus respuestas con:\n\n1. ## Análisis de Autoridad (Por qué este tema aporta valor a su red profesional)\n2. ## Redacción del Post o Hilo (Párrafos cortos, directos, con saltos de línea estratégicos, sin exceso de emojis)\n3. ## Pregunta de Enganche (Una llamada a la acción potente para generar debate sano en los comentarios).'
            },
            {
                id: 'traffic',
                name: 'Estratega de Ads',
                icon: 'trending-up',
                desc: 'Estructuración de ofertas, copies para anuncios pagados y disparadores psicológicos.',
                systemPrompt: 'Eres un Media Buyer y Estratega de Tráfico Pago de nivel senior en Facebook Ads y TikTok Ads. Tu enfoque es maximizar el ROAS mediante anuncios persuasivos. Estructura tus respuestas con:\n\n1. ## Ángulo de Venta (Disparador psicológico a usar: Urgencia, Prueba Social, Oferta Irresistible)\n2. ## Copy de Anuncio / Script de Video (El texto persuasivo adaptado al formato publicitario)\n3. ## Sugerencia de Gancho Visual y Segmentación.'
            }
        ];

        const messagesBox = document.getElementById('messages-box');
        const userInput = document.getElementById('user-input');
        const chatForm = document.getElementById('chat-form');
        const postDraft = document.getElementById('post-draft');

        // Registro de manejadores de forma limpia para evitar "ReferenceError" de carga móvil
        window.addEventListener('DOMContentLoaded', () => {
            renderAgentsList();
            renderIdeasGrid();
            renderChatHistory();
            updatePreview();
            updateRagIndicator();
            lucide.createIcons();

            // Sincronizar borrador
            if(postDraft) {
                postDraft.addEventListener('input', () => {
                    updatePreview();
                    document.getElementById('char-counter').innerText = `${postDraft.value.length} caracteres`;
                });
            }

            // Pestañas móviles
            document.getElementById('mobile-tab-editor')?.addEventListener('click', () => switchTab('editor'));
            document.getElementById('mobile-tab-chat')?.addEventListener('click', () => switchTab('chat'));
            document.getElementById('mobile-tab-ideas')?.addEventListener('click', () => switchTab('ideas'));

            // Pestañas escritorio sidebar
            document.getElementById('side-tab-editor')?.addEventListener('click', () => switchTab('editor'));
            document.getElementById('side-tab-chat')?.addEventListener('click', () => switchTab('chat'));
            document.getElementById('side-tab-ideas')?.addEventListener('click', () => switchTab('ideas'));

            // Botones de optimización con IA rápida
            document.getElementById('btn-enhance-rewrite')?.addEventListener('click', () => aiEnhanceDraft('rewrite'));
            document.getElementById('btn-enhance-hashtags')?.addEventListener('click', () => aiEnhanceDraft('hashtags'));
            document.getElementById('btn-enhance-hook')?.addEventListener('click', () => aiEnhanceDraft('hook'));
            document.getElementById('btn-save-draft')?.addEventListener('click', () => saveDraftAsIdea());

            // Selector de plataformas
            document.getElementById('platform-btn-instagram')?.addEventListener('click', () => setPreviewPlatform('instagram'));
            document.getElementById('platform-btn-twitter')?.addEventListener('click', () => setPreviewPlatform('twitter'));
            document.getElementById('platform-btn-linkedin')?.addEventListener('click', () => setPreviewPlatform('linkedin'));

            // Otros controles
            document.getElementById('btn-clear-chat')?.addEventListener('click', () => clearChat());
            document.getElementById('btn-new-idea')?.addEventListener('click', () => openNewIdeaModal());
            document.getElementById('btn-close-idea-modal')?.addEventListener('click', () => closeIdeaModal());
            document.getElementById('btn-cancel-idea')?.addEventListener('click', () => closeIdeaModal());

            // Formulario de Idea
            document.getElementById('idea-form')?.addEventListener('submit', (e) => handleIdeaSubmit(e));

            // Asegurar comportamiento del Enter en el chat
            if (userInput) {
                userInput.addEventListener('keydown', (e) => {
                    if (e.key === 'Enter' && !e.shiftKey) {
                        e.preventDefault();
                        chatForm.requestSubmit();
                    }
                });
                userInput.addEventListener('input', () => {
                    userInput.style.height = 'auto';
                    userInput.style.height = (userInput.scrollHeight > 96 ? 96 : userInput.scrollHeight) + 'px';
                });
            }
        });

        // NAVEGACIÓN Y TABS
        function switchTab(tabId) {
            currentTab = tabId;

            document.getElementById('tab-content-editor').classList.add('hidden');
            document.getElementById('tab-content-chat').classList.add('hidden');
            document.getElementById('tab-content-ideas').classList.add('hidden');

            ['editor', 'chat', 'ideas'].forEach(t => {
                const mobBtn = document.getElementById(`mobile-tab-${t}`);
                if (mobBtn) mobBtn.className = "flex flex-col items-center gap-1 py-1 px-3 text-xs font-semibold text-slate-400";
                
                const sideBtn = document.getElementById(`side-tab-${t}`);
                if (sideBtn) sideBtn.className = "w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm font-medium text-slate-400 hover:bg-slate-800/50";
            });

            if (tabId === 'editor') {
                document.getElementById('tab-content-editor').classList.remove('hidden');
            } else if (tabId === 'chat') {
                document.getElementById('tab-content-chat').classList.remove('hidden', 'md:hidden');
                scrollToBottom();
            } else if (tabId === 'ideas') {
                document.getElementById('tab-content-ideas').classList.remove('hidden');
            }

            const activeMobBtn = document.getElementById(`mobile-tab-${tabId}`);
            if (activeMobBtn) activeMobBtn.className = "flex flex-col items-center gap-1 py-1 px-3 text-xs font-semibold text-fuchsia-400";

            const activeSideBtn = document.getElementById(`side-tab-${tabId}`);
            if (activeSideBtn) activeSideBtn.className = "w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-sm font-medium bg-fuchsia-600/10 text-fuchsia-400 border border-fuchsia-500/20";
        }

        // CONTROL DE AGENTES
        function renderAgentsList() {
            const container = document.getElementById('agent-selector-container');
            if (!container) return;
            container.innerHTML = '';

            AGENTS.forEach(agent => {
                const isActive = agent.id === selectedAgentId;
                const activeClasses = 'bg-fuchsia-600/10 text-fuchsia-400 border border-fuchsia-500/20';
                const inactiveClasses = 'text-slate-400 hover:bg-slate-800/30 border border-transparent';

                const btn = document.createElement('button');
                btn.className = `w-full text-left p-2.5 rounded-lg flex gap-3 transition-all duration-200 ${isActive ? activeClasses : inactiveClasses}`;
                btn.onclick = () => selectAgent(agent.id);
                btn.innerHTML = `
                    <div class="p-1.5 rounded-md ${isActive ? 'bg-fuchsia-500/20 text-fuchsia-400' : 'bg-slate-800 text-slate-400'} shrink-0">
                        <i data-lucide="${agent.icon}" class="w-4 h-4"></i>
                    </div>
                    <div class="min-w-0 flex-1">
                        <div class="text-xs font-bold leading-none mb-1 flex items-center justify-between">
                            <span>${agent.name}</span>
                        </div>
                    </div>
                `;
                container.appendChild(btn);
            });
            lucide.createIcons();
        }

        function selectAgent(agentId) {
            selectedAgentId = agentId;
            renderAgentsList();
            const activeAgent = AGENTS.find(a => a.id === agentId);
            document.getElementById('chat-agent-title').innerText = activeAgent.name;
            renderChatHistory();
            showSuccessToast(`Perfil: ${activeAgent.name}`);
        }

        // PREVISUALIZADOR DE REDES SOCIALES
        function setPreviewPlatform(platform) {
            previewPlatform = platform;
            
            ['instagram', 'twitter', 'linkedin'].forEach(p => {
                const btn = document.getElementById(`platform-btn-${p}`);
                if (btn) btn.className = "p-1.5 rounded-md text-slate-400 hover:text-slate-200";
            });

            const activeBtn = document.getElementById(`platform-btn-${platform}`);
            if (activeBtn) activeBtn.className = "p-1.5 rounded-md text-fuchsia-400 bg-slate-800";

            updatePreview();
        }

        function updatePreview() {
            const previewCard = document.getElementById('social-preview-card');
            if (!previewCard) return;

            const textVal = postDraft.value.trim() || "Este es un borrador del texto de tu publicación. Comienza a escribir en el editor de la izquierda para ver cómo se verá...";
            
            if (previewPlatform === 'instagram') {
                previewCard.innerHTML = `
                    <div class="flex items-center justify-between pb-2 border-b border-slate-800/60">
                        <div class="flex items-center gap-2">
                            <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-yellow-500 via-red-500 to-purple-500 flex items-center justify-center p-0.5 shrink-0">
                                <div class="w-full h-full bg-slate-900 rounded-full flex items-center justify-center text-[10px] font-bold">SP</div>
                            </div>
                            <span class="text-xs font-bold text-slate-200">socialpulse_ai</span>
                        </div>
                        <i data-lucide="more-horizontal" class="w-4 h-4 text-slate-500"></i>
                    </div>
                    <div class="bg-slate-950 aspect-video rounded-xl flex items-center justify-center border border-slate-800 text-slate-600 relative overflow-hidden">
                        <i data-lucide="image" class="w-8 h-8 absolute"></i>
                    </div>
                    <div class="space-y-1.5">
                        <div class="flex gap-3 text-slate-300">
                            <i data-lucide="heart" class="w-4 h-4 hover:text-rose-500 transition-colors cursor-pointer"></i>
                            <i data-lucide="message-circle" class="w-4 h-4 hover:text-cyan-400 transition-colors cursor-pointer"></i>
                            <i data-lucide="send" class="w-4 h-4 hover:text-brand-500 transition-colors cursor-pointer"></i>
                        </div>
                        <p class="text-xs text-slate-300 leading-relaxed whitespace-pre-wrap"><span class="font-bold text-slate-100">socialpulse_ai</span> ${textVal}</p>
                    </div>
                `;
            } else if (previewPlatform === 'twitter') {
                previewCard.innerHTML = `
                    <div class="flex gap-3 items-start">
                        <div class="w-9 h-9 rounded-full bg-slate-800 border border-slate-700 flex items-center justify-center text-xs font-black shrink-0 text-slate-300">SP</div>
                        <div class="min-w-0 flex-1 space-y-1">
                            <div class="flex items-center gap-1.5 text-xs">
                                <span class="font-bold text-slate-100 truncate">SocialPulse Copilot</span>
                                <span class="text-slate-500 truncate">@socialpulse_ai</span>
                                <span class="text-slate-500 shrink-0">• 1m</span>
                            </div>
                            <p class="text-xs text-slate-200 leading-relaxed whitespace-pre-wrap break-words">${textVal}</p>
                            <div class="flex justify-between text-slate-500 pt-1">
                                <span class="flex items-center gap-1 hover:text-cyan-400 transition-colors cursor-pointer text-[10px]"><i data-lucide="message-square" class="w-3.5 h-3.5"></i> 0</span>
                                <span class="flex items-center gap-1 hover:text-emerald-400 transition-colors cursor-pointer text-[10px]"><i data-lucide="repeat" class="w-3.5 h-3.5"></i> 0</span>
                                <span class="flex items-center gap-1 hover:text-rose-400 transition-colors cursor-pointer text-[10px]"><i data-lucide="heart" class="w-3.5 h-3.5"></i> 0</span>
                            </div>
                        </div>
                    </div>
                `;
            } else if (previewPlatform === 'linkedin') {
                previewCard.innerHTML = `
                    <div class="space-y-3">
                        <div class="flex items-center gap-2">
                            <div class="w-9 h-9 rounded bg-brand-900 flex items-center justify-center text-xs font-black shrink-0 text-fuchsia-300">SP</div>
                            <div>
                                <h4 class="text-xs font-black text-slate-200">SocialPulse AI</h4>
                                <p class="text-[9px] text-slate-500">10,240 seguidores • Promocionado</p>
                            </div>
                        </div>
                        <p class="text-xs text-slate-200 leading-relaxed whitespace-pre-wrap">${textVal}</p>
                        <div class="border-t border-slate-800/80 pt-2 flex justify-around text-slate-400 text-[10px] font-bold">
                            <span class="flex items-center gap-1 hover:text-brand-400 cursor-pointer"><i data-lucide="thumbs-up" class="w-3.5 h-3.5"></i> Recomendar</span>
                            <span class="flex items-center gap-1 hover:text-brand-400 cursor-pointer"><i data-lucide="message-square" class="w-3.5 h-3.5"></i> Comentar</span>
                            <span class="flex items-center gap-1 hover:text-brand-400 cursor-pointer"><i data-lucide="share-2" class="w-3.5 h-3.5"></i> Compartir</span>
                        </div>
                    </div>
                `;
            }
            lucide.createIcons();
        }

        // INTEGRACIÓN JAVASCRIPT COPILOTO IA
        function renderChatHistory() {
            messagesBox.innerHTML = '';
            chatHistories[selectedAgentId].forEach(msg => {
                appendMessageToUI(msg.sender, msg.text);
            });
            scrollToBottom();
        }

        function appendMessageToUI(sender, text) {
            const wrapper = document.createElement('div');
            wrapper.className = `flex gap-3 max-w-[95%] sm:max-w-[85%] ${sender === 'user' ? 'self-end ml-auto flex-row-reverse' : 'self-start'}`;
            
            const isUser = sender === 'user';
            const bgClass = isUser ? 'bg-fuchsia-600 text-white' : 'bg-slate-900 border border-slate-800 text-slate-200';
            const avatarHtml = isUser 
                ? `<div class="w-8 h-8 rounded-full bg-fuchsia-900 border border-fuchsia-500/30 flex items-center justify-center text-xs font-bold shrink-0">YO</div>`
                : `<div class="w-8 h-8 rounded-full bg-slate-800 border border-slate-700 flex items-center justify-center text-xs font-bold shrink-0 text-slate-300">AI</div>`;

            wrapper.innerHTML = `
                ${avatarHtml}
                <div class="rounded-2xl px-4 py-2.5 text-xs leading-relaxed whitespace-pre-wrap ${bgClass} shadow-md break-words w-full">
                    ${parseMarkdown(text)}
                </div>
            `;
            messagesBox.appendChild(wrapper);
        }

        function parseMarkdown(text) {
            if (!text) return '';
            let safeText = text.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
            
            safeText = safeText.replace(/```(\w*)\n([\s\S]*?)```/g, '<pre class="bg-slate-950 text-slate-300 p-3 rounded-lg border border-slate-800 text-[10px] font-mono my-2 overflow-x-auto"><code class="block whitespace-pre">$2</code></pre>');
            safeText = safeText.replace(/`([^`\n]+)`/g, '<code class="bg-slate-950 px-1.5 py-0.5 rounded text-rose-400 font-mono text-[10px]">$1</code>');
            safeText = safeText.replace(/^## (.*$)/gim, '<h3 class="text-xs font-black text-slate-100 border-b border-slate-800 pb-1 mt-3 mb-1.5 flex items-center gap-1.5"><span class="w-1.5 h-3 bg-fuchsia-500 rounded-sm"></span>$1</h3>');
            safeText = safeText.replace(/\*\*([^*]+)\*\*/g, '<strong class="font-bold text-white">$1</strong>');
            safeText = safeText.replace(/^\s*[\*\-]\s+(.+)$/gm, '<li class="ml-4 list-disc my-1 text-slate-300">$1</li>');

            return safeText;
        }

        // ENVIAR MENSAJES AL ASISTENTE CHAT
        chatForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const text = userInput.value.trim();
            if (!text) return;

            userInput.value = '';
            userInput.style.height = 'auto';

            chatHistories[selectedAgentId].push({ sender: 'user', text });
            appendMessageToUI('user', text);
            scrollToBottom();

            const loadingBubble = document.createElement('div');
            loadingBubble.id = 'typing-indicator';
            loadingBubble.className = 'flex gap-3 max-w-[85%] self-start';
            loadingBubble.innerHTML = `
                <div class="w-8 h-8 rounded-full bg-slate-800 border border-slate-700 flex items-center justify-center text-xs font-bold shrink-0">AI</div>
                <div class="bg-slate-900 border border-slate-800 text-slate-400 rounded-2xl px-4 py-3 text-xs flex items-center gap-1">
                    <span class="w-1.5 h-1.5 bg-fuchsia-500 rounded-full animate-bounce"></span>
                    <span class="w-1.5 h-1.5 bg-fuchsia-500 rounded-full animate-bounce" style="animation-delay: 150ms"></span>
                    <span class="w-1.5 h-1.5 bg-fuchsia-500 rounded-full animate-bounce" style="animation-delay: 300ms"></span>
                </div>
            `;
            messagesBox.appendChild(loadingBubble);
            scrollToBottom();

            try {
                const aiResponse = await callGeminiAPI(text);
                document.getElementById('typing-indicator')?.remove();

                chatHistories[selectedAgentId].push({ sender: 'assistant', text: aiResponse });
                appendMessageToUI('assistant', aiResponse);
                scrollToBottom();
            } catch (error) {
                document.getElementById('typing-indicator')?.remove();
                showToast("Fallo de conexión.");
                appendMessageToUI('assistant', '⚠️ Error de comunicación. Inténtalo de nuevo.');
                scrollToBottom();
            }
        });

        // OPTIMIZACIONES CON IA DE UN CLIC
        async function aiEnhanceDraft(actionType) {
            const currentDraft = postDraft.value.trim();
            if (!currentDraft) {
                showToast("Escribe primero un borrador o idea en la caja de texto para poder optimizarlo con IA.");
                return;
            }

            let enhancementPrompt = "";
            if (actionType === 'rewrite') {
                enhancementPrompt = `Optimiza el siguiente borrador de red de social para que sea sumamente persuasivo, tenga una estructura de lectura limpia con párrafos separados, emojis pertinentes y un llamado a la acción claro al final. Entrega únicamente la publicación redactada final sin texto explicativo adicional. \n\nBorrador original:\n"${currentDraft}"`;
            } else if (actionType === 'hashtags') {
                enhancementPrompt = `Analiza el borrador provisto y genera un listado de entre 10 y 15 hashtags organizados en categorías (nicho, general, virales). Entrega únicamente el bloque final de hashtags recomendados listos para pegar. \n\nBorrador original:\n"${currentDraft}"`;
            } else if (actionType === 'hook') {
                enhancementPrompt = `Genera un listado de 5 opciones de ganchos (títulos o frases iniciales de 3 segundos) sumamente virales e impactantes para abrir el siguiente post de redes sociales. \n\nBorrador original:\n"${currentDraft}"`;
            }

            showSuccessToast("La IA está optimizando tu borrador...");

            try {
                const response = await callGeminiAPI(enhancementPrompt);
                
                if (actionType === 'rewrite') {
                    postDraft.value = response;
                    updatePreview();
                    showSuccessToast("Borrador optimizado correctamente.");
                } else {
                    postDraft.value = postDraft.value + "\n\n" + response;
                    updatePreview();
                    showSuccessToast("Agregado al borrador.");
                }

            } catch (error) {
                showToast("Fallo al contactar el motor de IA.");
            }
        }

        // GUARDAR BORRADOR EN EL BANCO DE IDEAS
        function saveDraftAsIdea() {
            const currentDraft = postDraft.value.trim();
            if (!currentDraft) {
                showToast("La caja de borrador está vacía.");
                return;
            }

            const title = "Borrador guardado " + new Date().toLocaleDateString();
            ideasDatabase.push({
                id: 'idea-' + Date.now(),
                title: title,
                content: currentDraft
            });

            renderIdeasGrid();
            updateRagIndicator();
            showSuccessToast("Guardado en el Banco de Ideas.");
        }

        // COMUNICACIÓN CON LA API DE GEMINI 2.5 FLASH
        async function callGeminiAPI(userPrompt) {
            const currentAgent = AGENTS.find(a => a.id === selectedAgentId);
            let dynamicSystemPrompt = currentAgent.systemPrompt;
            
            // Inyectar base de conocimientos (RAG)
            if (ideasDatabase.length > 0) {
                dynamicSystemPrompt += `\n\n[CONTEXTO DE PILARES E IDEAS DE MARCA DEL USUARIO - RAG]
                Puedes utilizar los siguientes pilares guardados para adaptar el tono o usar detalles concretos de la marca del usuario en tu respuesta:`;
                
                ideasDatabase.forEach((idea, idx) => {
                    dynamicSystemPrompt += `\nIdea/Pilar ${idx + 1}: ${idea.title}\n${idea.content}`;
                });
            }

            const payload = {
                contents: [{ parts: [{ text: userPrompt }] }],
                systemInstruction: { parts: [{ text: dynamicSystemPrompt }] }
            };

            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(payload)
            });

            if (!response.ok) throw new Error("API Error");
            const result = await response.json();
            return result.candidates?.[0]?.content?.parts?.[0]?.text || "No se obtuvo respuesta.";
        }

        // BANCO DE IDEAS (DATABASE LOCAL)
        function renderIdeasGrid() {
            const grid = document.getElementById('ideas-grid');
            if(!grid) return;
            grid.innerHTML = '';
            document.getElementById('idea-count-badge').innerText = ideasDatabase.length;

            if (ideasDatabase.length === 0) {
                grid.innerHTML = `<div class="col-span-full text-center text-slate-500 text-xs py-8">Tu banco de ideas está vacío actualmente.</div>`;
                return;
            }

            ideasDatabase.forEach(idea => {
                const card = document.createElement('div');
                card.className = "bg-slate-900/40 border border-slate-800 rounded-xl p-4 flex flex-col justify-between hover:border-fuchsia-500/30 transition-all";
                card.innerHTML = `
                    <div>
                        <h4 class="text-xs font-bold text-slate-200 line-clamp-1">${idea.title}</h4>
                        <p class="text-[11px] text-slate-400 mt-1 line-clamp-3 leading-relaxed whitespace-pre-wrap">${idea.content}</p>
                    </div>
                    <div class="flex justify-end gap-2 mt-3 pt-2 border-t border-slate-800/60">
                        <button onclick="deleteIdea('${idea.id}')" class="text-rose-400 text-[10px] font-semibold hover:underline">Eliminar</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function deleteIdea(id) {
            ideasDatabase = ideasDatabase.filter(idea => idea.id !== id);
            renderIdeasGrid();
            updateRagIndicator();
            showSuccessToast("Eliminado del banco.");
        }

        // MODAL DE CREACIÓN DE IDEAS
        function openNewIdeaModal() {
            document.getElementById('idea-modal').classList.remove('hidden');
        }
        function closeIdeaModal() {
            document.getElementById('idea-modal').classList.add('hidden');
        }

        function handleIdeaSubmit(e) {
            e.preventDefault();
            const title = document.getElementById('idea-title').value.trim();
            const content = document.getElementById('idea-content').value.trim();

            if (!title || !content) return;

            ideasDatabase.push({
                id: 'idea-' + Date.now(),
                title,
                content
            });

            closeIdeaModal();
            renderIdeasGrid();
            updateRagIndicator();
            
            document.getElementById('idea-title').value = "";
            document.getElementById('idea-content').value = "";
            showSuccessToast("Nueva idea agregada al banco.");
        }

        function updateRagIndicator() {
            const count = ideasDatabase.length;
            document.getElementById('rag-badge-count').innerText = count;
            if (count > 0) {
                document.getElementById('rag-chat-bar').classList.remove('hidden');
            } else {
                document.getElementById('rag-chat-bar').classList.add('hidden');
            }
        }

        // UTILERÍAS
        function clearChat() {
            const activeAgent = AGENTS.find(a => a.id === selectedAgentId);
            chatHistories[selectedAgentId] = [{ sender: 'assistant', text: `Chat re-inicializado. Hola de nuevo, soy tu **${activeAgent.name}**.` }];
            renderChatHistory();
        }

        function scrollToBottom() {
            if (!messagesBox) return;
            messagesBox.scrollTop = messagesBox.scrollHeight;
            setTimeout(() => {
                messagesBox.scrollTo({
                    top: messagesBox.scrollHeight,
                    behavior: 'smooth'
                });
            }, 80);
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = msg;
            toast.style.transform = 'translateY(0)';
            toast.style.opacity = '1';
            setTimeout(() => {
                toast.style.transform = 'translateY(20px)';
                toast.style.opacity = '0';
            }, 3000);
        }

        function showSuccessToast(msg) {
            const toast = document.getElementById('success-toast');
            document.getElementById('success-toast-message').innerText = msg;
            toast.style.transform = 'translateY(0)';
            toast.style.opacity = '1';
            setTimeout(() => {
                toast.style.transform = 'translateY(20px)';
                toast.style.opacity = '0';
            }, 2500);
        }
    </script>
</body>
</html>