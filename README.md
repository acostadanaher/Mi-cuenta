<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VerPromos.com - Cuotas sin interés, Descuentos y Beneficios</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f5f0ff',
                            100: '#ede2fe',
                            500: '#7c3aed',
                            600: '#6d28d9',
                            700: '#5b21b6',
                            900: '#4c1d95',
                        },
                        orangePromo: '#ff6b00',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .transition-all-300 { transition: all 0.3s ease-in-out; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans antialiased min-h-screen flex flex-col justify-between selection:bg-purple-500 selection:text-white">

    <!-- HEADER SUPERIOR -->
    <header class="sticky top-0 z-50 bg-white shadow-sm border-b border-slate-100 transition-all duration-300">
        <!-- Barra Principal con Layout Exacto -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
            <div class="flex items-center justify-between h-16 sm:h-20">
                
                <!-- Izquierda: Menú Hamburguesa (3 rayitos) y Selector de Provincia -->
                <div class="flex items-center space-x-3">
                    <button onclick="toggleSideMenu()" class="p-2.5 text-slate-700 hover:text-purple-600 hover:bg-purple-50 rounded-xl transition focus:outline-none" aria-label="Menú">
                        <i class="fa-solid fa-bars text-xl"></i>
                    </button>
                    
                    <!-- Selector de Provincia por defecto Capital Federal y PBA -->
                    <div class="hidden sm:flex items-center bg-slate-100 hover:bg-slate-200 rounded-xl px-3 py-1.5 transition text-xs font-semibold text-slate-700">
                        <i class="fa-solid fa-location-dot text-purple-600 mr-2"></i>
                        <select id="provinceSelect" onchange="changeProvince(this.value)" class="bg-transparent border-none focus:outline-none cursor-pointer">
                            <option value="Capital Federal" selected>Capital Federal</option>
                            <option value="Provincia de Buenos Aires">Provincia de Buenos Aires</option>
                            <option value="Córdoba">Córdoba</option>
                            <option value="Santa Fe">Santa Fe</option>
                            <option value="Mendoza">Mendoza</option>
                        </select>
                    </div>
                </div>

                <!-- Centro: Logo profesional VerPromos -->
                <div class="flex items-center space-x-2.5 cursor-pointer absolute left-1/2 transform -translate-x-1/2" onclick="resetSearchAndFilter()">
                    <div class="bg-gradient-to-tr from-purple-600 via-purple-700 to-indigo-600 text-white w-10 h-10 rounded-2xl shadow-md flex items-center justify-center transform hover:rotate-6 transition">
                        <i class="fa-solid fa-tags text-lg"></i>
                    </div>
                    <div class="text-center sm:text-left">
                        <span class="text-xl sm:text-2xl font-black bg-gradient-to-r from-purple-700 to-indigo-700 bg-clip-text text-transparent tracking-tight">VerPromos</span>
                        <span class="text-[10px] hidden sm:block font-bold text-purple-500 uppercase tracking-widest leading-none">Beneficios & Cuotas</span>
                    </div>
                </div>

                <!-- Derecha: Icono de Usuario (Miembros) y Lupa de Buscador -->
                <div class="flex items-center space-x-1 sm:space-x-2">
                    <button onclick="openAuthModal()" class="p-2.5 text-slate-700 hover:text-purple-600 hover:bg-purple-50 rounded-xl transition relative group" aria-label="Miembro">
                        <i class="fa-regular fa-user text-xl"></i>
                        <span id="userIndicator" class="absolute top-2 right-2 w-2 h-2 bg-emerald-500 rounded-full ring-2 ring-white hidden"></span>
                    </button>
                    <button onclick="toggleSearchOverlay()" class="p-2.5 text-slate-700 hover:text-purple-600 hover:bg-purple-50 rounded-xl transition" aria-label="Buscar">
                        <i class="fa-solid fa-magnifying-glass text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- BUSCADOR DESPLEGABLE SOBRE TODO EL MENÚ (Con efecto deslizante y botón X) -->
        <div id="searchOverlayBar" class="absolute inset-x-0 top-0 bg-white shadow-xl border-b border-purple-100 p-4 transform -translate-y-full opacity-0 pointer-events-none transition-all duration-300 z-50">
            <div class="max-w-4xl mx-auto flex items-center space-x-3">
                <div class="relative flex-1">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-4 pointer-events-none text-purple-600">
                        <i class="fa-solid fa-magnifying-glass text-lg"></i>
                    </span>
                    <input type="text" id="liveSearchInput" placeholder="Buscá supermercados, cine, espectáculos, viajes, marcas..." 
                        class="w-full pl-12 pr-10 py-3.5 bg-purple-50/50 border-2 border-purple-200 rounded-2xl text-sm font-medium focus:outline-none focus:border-purple-600 transition shadow-inner">
                    <button onclick="clearSearchInput()" class="absolute inset-y-0 right-0 pr-3.5 flex items-center text-slate-400 hover:text-slate-700">
                        <i class="fa-solid fa-xmark text-lg"></i>
                    </button>
                </div>
                <button onclick="toggleSearchOverlay()" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold px-5 py-3.5 rounded-2xl text-sm transition">
                    Cerrar
                </button>
            </div>
        </div>

        <!-- BARRA DE CATEGORÍAS ICONOGRÁFICAS (Scroll Horizontal, Táctil & Botones) -->
        <div class="bg-white border-t border-slate-100 shadow-xs">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative group">
                <!-- Botón scroll izquierdo desktop -->
                <button onclick="scrollCategories(-200)" class="absolute left-1 top-1/2 -translate-y-1/2 z-10 bg-white/90 shadow-md border border-slate-200 w-8 h-8 rounded-full hidden md:flex items-center justify-center text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-chevron-left text-xs"></i>
                </button>
                
                <div id="categoryContainer" class="flex items-center space-x-6 sm:space-x-8 py-3.5 overflow-x-auto no-scrollbar scroll-smooth cursor-grab active:cursor-grabbing">
                    <button onclick="filterCategory('all')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none active" data-category="all">
                        <div class="w-12 h-12 rounded-2xl bg-purple-600 text-white flex items-center justify-center transition shadow-md mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-fire text-lg"></i>
                        </div>
                        <span class="text-xs font-bold text-purple-700 whitespace-nowrap">Todas</span>
                    </button>
                    <button onclick="filterCategory('super')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="super">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-cart-shopping text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Supermercados</span>
                    </button>
                    <button onclick="filterCategory('cine')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="cine">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-film text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Cine</span>
                    </button>
                    <button onclick="filterCategory('espectaculos')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="espectaculos">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-masks-theater text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Espectáculos</span>
                    </button>
                    <button onclick="filterCategory('electro')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="electro">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-bolt text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Cuotas Tecno</span>
                    </button>
                    <button onclick="filterCategory('viajes')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="viajes">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-plane text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Viajes</span>
                    </button>
                    <button onclick="filterCategory('indumentaria')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="indumentaria">
                        <div class="w-12 h-12 rounded-2xl bg-slate-100 group-hover:bg-purple-600 text-slate-600 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-shirt text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-slate-700 group-hover:text-purple-700 whitespace-nowrap">Moda</span>
                    </button>
                    <button onclick="filterCategory('sorteos')" class="category-btn flex flex-col items-center min-w-[75px] group focus:outline-none" data-category="sorteos">
                        <div class="w-12 h-12 rounded-2xl bg-amber-100 group-hover:bg-purple-600 text-amber-700 group-hover:text-white flex items-center justify-center transition shadow-sm mb-1.5 transform group-hover:scale-105">
                            <i class="fa-solid fa-gift text-lg"></i>
                        </div>
                        <span class="text-xs font-semibold text-amber-800 group-hover:text-purple-700 whitespace-nowrap">Sorteos</span>
                    </button>
                </div>

                <!-- Botón scroll derecho desktop -->
                <button onclick="scrollCategories(200)" class="absolute right-1 top-1/2 -translate-y-1/2 z-10 bg-white/90 shadow-md border border-slate-200 w-8 h-8 rounded-full hidden md:flex items-center justify-center text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- MENÚ LATERAL DESLIZABLE (SIDEBAR CON CATEGORÍAS) -->
    <div id="sideMenuBackdrop" onclick="toggleSideMenu()" class="fixed inset-0 bg-slate-900/50 backdrop-blur-xs z-50 opacity-0 pointer-events-none transition-opacity duration-300"></div>
    <div id="sideMenu" class="fixed top-0 left-0 bottom-0 w-80 bg-white z-50 shadow-2xl transform -translate-x-full transition-transform duration-300 flex flex-col justify-between overflow-y-auto">
        <div>
            <!-- Header del Menú -->
            <div class="p-6 bg-gradient-to-tr from-purple-900 to-indigo-900 text-white flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="bg-white/10 p-2.5 rounded-xl">
                        <i class="fa-solid fa-tags text-xl"></i>
                    </div>
                    <div>
                        <h3 class="font-black text-lg">VerPromos.com</h3>
                        <p class="text-xs text-purple-200">Panel de Miembros</p>
                    </div>
                </div>
                <button onclick="toggleSideMenu()" class="text-purple-200 hover:text-white p-2">
                    <i class="fa-solid fa-xmark text-xl"></i>
                </button>
            </div>

            <!-- Panel de Cuentas Precargadas / Caché Activa -->
            <div class="p-5 bg-purple-50/70 border-b border-purple-100">
                <div class="flex items-center justify-between mb-2">
                    <h4 class="text-xs font-extrabold text-purple-900 uppercase tracking-wider flex items-center space-x-1.5">
                        <i class="fa-solid fa-user-check text-purple-600"></i>
                        <span>Cuentas Registradas (Demo)</span>
                    </h4>
                </div>
                <div class="space-y-2">
                    <button onclick="loadPresetUser('mauricio')" class="w-full text-left bg-white hover:bg-purple-100 p-2.5 rounded-xl border border-purple-200 transition shadow-xs">
                        <p class="text-xs font-bold text-purple-900">Mauricio Acosta Danaher</p>
                        <p class="text-[10px] text-slate-500">DNI: 37170491 | Mercado Pago</p>
                    </button>
                    <button onclick="loadPresetUser('maria')" class="w-full text-left bg-white hover:bg-purple-100 p-2.5 rounded-xl border border-purple-200 transition shadow-xs">
                        <p class="text-xs font-bold text-purple-900">María Lucía Carpio Peralta</p>
                        <p class="text-[10px] text-slate-500">DNI: 93.976.879 | Capital Federal</p>
                    </button>
                </div>
            </div>

            <!-- Opciones de Navegación del Menú -->
            <div class="p-4 space-y-1">
                <p class="px-3 text-[11px] font-bold text-slate-400 uppercase tracking-wider mb-2">Categorías Principales</p>
                <a href="#section-super" onclick="toggleSideMenu(); filterCategory('super');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-cart-shopping w-5 text-purple-600"></i>
                    <span>Supermercados & Alimentos</span>
                </a>
                <a href="#section-cine" onclick="toggleSideMenu(); filterCategory('cine');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-film w-5 text-purple-600"></i>
                    <span>Cine & Entradas</span>
                </a>
                <a href="#section-espectaculos" onclick="toggleSideMenu(); filterCategory('espectaculos');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-masks-theater w-5 text-purple-600"></i>
                    <span>Espectáculos & Teatro</span>
                </a>
                <a href="#section-electro" onclick="toggleSideMenu(); filterCategory('electro');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-bolt w-5 text-purple-600"></i>
                    <span>Cuotas Tecno & Electro</span>
                </a>
                <a href="#section-viajes" onclick="toggleSideMenu(); filterCategory('viajes');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-slate-700 hover:bg-purple-50 hover:text-purple-700 transition">
                    <i class="fa-solid fa-plane w-5 text-purple-600"></i>
                    <span>Viajes y Turismo</span>
                </a>
                <a href="#section-sorteos" onclick="toggleSideMenu(); filterCategory('sorteos');" class="flex items-center space-x-3 px-3 py-2.5 rounded-xl text-sm font-semibold text-amber-700 hover:bg-amber-50 transition">
                    <i class="fa-solid fa-gift w-5 text-amber-600"></i>
                    <span>Sorteos Cinemark VIP</span>
                </a>
            </div>
        </div>

        <div class="p-5 border-t border-slate-100 bg-slate-50 text-center">
            <button onclick="openAuthModal(); toggleSideMenu();" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-bold py-2.5 rounded-xl text-sm shadow-md transition">
                Iniciar Sesión / Miembro
            </button>
            <p class="text-[11px] text-slate-400 mt-3">&copy; 2026 VerPromos.com</p>
        </div>
    </div>

    <!-- CONTENIDO PRINCIPAL -->
    <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-8 space-y-12 w-full">

        <!-- CONTENEDOR DE RESULTADOS DE BÚSQUEDA DINÁMICA (Aparece al buscar y oculta el carrusel) -->
        <div id="searchResultsContainer" class="hidden space-y-6 bg-purple-50/50 p-6 rounded-3xl border-2 border-purple-200">
            <div class="flex items-center justify-between">
                <div>
                    <h2 class="text-2xl font-black text-purple-900 tracking-tight">Resultados de Búsqueda</h2>
                    <p class="text-xs text-purple-600 font-medium">Coincidencias encontradas en tiempo real</p>
                </div>
                <button onclick="resetSearchAndFilter()" class="bg-white hover:bg-purple-100 text-purple-700 font-bold px-4 py-2 rounded-xl text-xs shadow-xs transition">
                    Ver todas las promos
                </button>
            </div>
            <div id="searchResultsGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Inyectado dinámicamente -->
            </div>
        </div>

        <!-- CARRUSEL SUPERIOR DESLIZABLE (Adaptado móvil compacto, touch swipe y botones laterales) -->
        <section id="topCarouselSection" class="relative bg-gradient-to-r from-purple-900 via-purple-800 to-indigo-900 rounded-3xl overflow-hidden shadow-xl text-white">
            <div class="absolute -right-16 -bottom-16 w-96 h-96 bg-purple-600/30 rounded-full blur-3xl pointer-events-none"></div>
            
            <!-- Contenedor Slides con Scroll Horizontal y Touch Swipe -->
            <div id="carouselTrack" class="flex overflow-x-auto no-scrollbar snap-x snap-mandatory scroll-smooth cursor-grab active:cursor-grabbing">
                
                <!-- Slide 1: Canal de WhatsApp -->
                <div class="min-w-full snap-center grid grid-cols-1 lg:grid-cols-12 items-center p-5 sm:p-8 lg:p-10 gap-6">
                    <div class="lg:col-span-7 space-y-3 z-10">
                        <span class="inline-flex items-center space-x-2 bg-emerald-500/20 text-emerald-300 px-3 py-1 rounded-full text-[11px] font-bold uppercase tracking-wider border border-emerald-500/30">
                            <i class="fa-brands fa-whatsapp text-sm"></i>
                            <span>Canal Oficial WhatsApp</span>
                        </span>
                        <h1 class="text-xl sm:text-2xl lg:text-3xl font-black tracking-tight leading-tight">
                            Enterate de las promos antes que nadie
                        </h1>
                        <p class="text-purple-200 text-xs sm:text-sm max-w-lg leading-relaxed">
                            Sumate a nuestro canal y recibí beneficios exclusivos, reintegros sorpresas y cuotas sin interés al instante.
                        </p>
                        <div class="pt-1 flex flex-wrap gap-3 items-center">
                            <button onclick="openWhatsAppModal()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-bold px-5 py-2.5 rounded-xl shadow-lg transition transform hover:-translate-y-0.5 flex items-center space-x-2 text-sm">
                                <i class="fa-brands fa-whatsapp text-lg"></i>
                                <span>Unirme al canal gratis</span>
                            </button>
                        </div>
                    </div>
                    <div class="lg:col-span-5 flex justify-center z-10">
                        <div class="relative w-56 sm:w-64 bg-slate-900 border-4 border-slate-700 rounded-[2rem] p-2 shadow-2xl">
                            <div class="bg-slate-950 rounded-[1.5rem] p-3 text-white space-y-2">
                                <div class="flex items-center justify-between border-b border-slate-800 pb-2">
                                    <div class="flex items-center space-x-2">
                                        <div class="w-6 h-6 rounded-full bg-emerald-600 flex items-center justify-center text-white font-bold text-[10px]">VP</div>
                                        <div>
                                            <p class="text-[10px] font-bold">VerPromos Oficial</p>
                                            <p class="text-[8px] text-emerald-400">142.5K seguidores</p>
                                        </div>
                                    </div>
                                </div>
                                <div class="bg-slate-900 rounded-xl p-2 space-y-1 border border-slate-800">
                                    <span class="bg-orangePromo text-white text-[8px] px-1.5 py-0.5 rounded font-bold uppercase">Exclusivo</span>
                                    <p class="text-[10px] font-semibold leading-snug">🔥 ¡Hasta 35% OFF en Coto y Jumbo este finde!</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Slide 2: Sorteo Cinemark Miembros -->
                <div class="min-w-full snap-center grid grid-cols-1 lg:grid-cols-12 items-center p-5 sm:p-8 lg:p-10 gap-6 bg-gradient-to-r from-indigo-900 via-purple-900 to-slate-900">
                    <div class="lg:col-span-7 space-y-3 z-10">
                        <span class="inline-flex items-center space-x-2 bg-amber-500/20 text-amber-300 px-3 py-1 rounded-full text-[11px] font-bold uppercase tracking-wider border border-amber-500/30">
                            <i class="fa-solid fa-gift text-sm"></i>
                            <span>Sorteo Exclusivo Miembros</span>
                        </span>
                        <h2 class="text-xl sm:text-2xl lg:text-3xl font-black tracking-tight leading-tight">
                            Ganá 1 Entrada para Cinemark Hoy
                        </h2>
                        <p class="text-purple-200 text-xs sm:text-sm max-w-lg leading-relaxed">
                            Participá con tu cuenta registrada en VerPromos y disfrutá del mejor cine gratis.
                        </p>
                        <div class="pt-1">
                            <button onclick="openGiveawayModal()" class="bg-amber-500 hover:bg-amber-600 text-slate-950 font-black px-5 py-2.5 rounded-xl shadow-lg transition transform hover:-translate-y-0.5 flex items-center space-x-2 text-sm">
                                <i class="fa-solid fa-ticket text-lg"></i>
                                <span>Participar en el Sorteo</span>
                            </button>
                        </div>
                    </div>
                    <div class="lg:col-span-5 flex justify-center z-10">
                        <div class="bg-white/10 backdrop-blur-md border border-white/20 p-5 rounded-3xl text-center shadow-2xl max-w-xs">
                            <i class="fa-solid fa-film text-4xl text-amber-400 mb-2"></i>
                            <h3 class="font-extrabold text-base text-white">Cinemark Hoyts</h3>
                            <p class="text-xs text-purple-200 mt-1">Sorteo semanal exclusivo para miembros.</p>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Botones de desplazamiento lateral y Puntos indicadores -->
            <div class="flex items-center justify-between px-6 pb-4 pt-2">
                <button onclick="moveCarousel(-1)" class="w-8 h-8 rounded-full bg-white/20 hover:bg-white/40 flex items-center justify-center text-white transition text-xs">
                    <i class="fa-solid fa-chevron-left"></i>
                </button>
                <div class="flex space-x-2" id="carouselDots">
                    <span class="w-6 h-1.5 bg-white rounded-full transition-all cursor-pointer" onclick="goToSlide(0)"></span>
                    <span class="w-2 h-1.5 bg-white/50 rounded-full transition-all cursor-pointer" onclick="goToSlide(1)"></span>
                </div>
                <button onclick="moveCarousel(1)" class="w-8 h-8 rounded-full bg-white/20 hover:bg-white/40 flex items-center justify-center text-white transition text-xs">
                    <i class="fa-solid fa-chevron-right"></i>
                </button>
            </div>
        </section>

        <!-- SECCIÓN 1: SUPERMERCADOS -->
        <section id="section-super" class="promo-section space-y-5">
            <div class="flex items-center justify-between">
                <div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight">Para tarjetear la compra del super</h2>
                    <p class="text-xs sm:text-sm text-slate-500 mt-0.5">Ahorrá en tus compras diarias con los mejores descuentos.</p>
                </div>
                <button onclick="showMoreCategory('super')" class="text-purple-600 hover:text-purple-800 font-bold text-sm flex items-center space-x-1 transition">
                    <span>Ver más</span>
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </button>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Coto -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-red-50 text-red-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Plan Turbo</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-emerald-700 tracking-tighter bg-emerald-50 px-3 py-1.5 rounded-lg border border-emerald-100">Coto Digital</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 25% off y 18 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Días seleccionados en Coto.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Débito</span>
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Coto Digital', 'Hasta 25% off y 18 cuotas sin interés', 'Aprovechá todos los beneficios exclusivos pagando con tus medios habilitados.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Vea -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-red-50 text-red-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Plan Turbo</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-red-600 tracking-tighter bg-red-50 px-3 py-1.5 rounded-lg border border-red-100">Vea Supermercados</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 25% off y 12 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Días seleccionados en Vea.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Débito</span>
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Vea Supermercados', 'Hasta 25% off y 12 cuotas sin interés', 'Válido en hipermercados Vea de todo el país.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Jumbo -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-red-50 text-red-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Plan Turbo</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-emerald-600 tracking-tighter bg-emerald-50 px-3 py-1.5 rounded-lg border border-emerald-100">JUMBO</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 25% off y 12 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Días seleccionados en Jumbo.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Débito</span>
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('JUMBO', 'Hasta 25% off y 12 cuotas sin interés', 'Aprovechá en Jumbo app y tiendas físicas.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Disco -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-red-50 text-red-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Plan Turbo</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-red-500 tracking-tighter bg-red-50 px-3 py-1.5 rounded-lg border border-red-100">DISCO</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 25% off y 12 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Días seleccionados en Disco.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Débito</span>
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('DISCO', 'Hasta 25% off y 12 cuotas sin interés', 'Descuento aplicado en línea de cajas.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 2: CINE Y ESPECTÁCULOS -->
        <section id="section-cine" class="promo-section space-y-5">
            <div class="flex items-center justify-between">
                <div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight">Cine y Espectáculos</h2>
                    <p class="text-xs sm:text-sm text-slate-500 mt-0.5">Beneficios exclusivos en entradas, obras de teatro y recitales.</p>
                </div>
                <button onclick="showMoreCategory('cine')" class="text-purple-600 hover:text-purple-800 font-bold text-sm flex items-center space-x-1 transition">
                    <span>Ver más</span>
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </button>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Cinemark Hoyts -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-amber-50 text-amber-700 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">2x1 Entradas</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-amber-600 tracking-tight bg-amber-50 px-3 py-1.5 rounded-lg border border-amber-100">CINEMARK HOYTS</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">2x1 todos los días en salas 2D y 3D</h3>
                        <p class="text-xs text-slate-500 mt-1">Exclusivo pagando con Mercado Pago y tarjetas asociadas.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Mercado Pago</span>
                        </div>
                        <button onclick="openPromoDetail('Cinemark Hoyts', '2x1 todos los días en salas 2D y 3D', 'Válido para compras online o boletería presencial en Capital Federal y GBA.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Showcase Cinemas -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-blue-700 tracking-tight bg-blue-50 px-3 py-1.5 rounded-lg border border-blue-100">SHOWCASE</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">50% OFF en la segunda entrada</h3>
                        <p class="text-xs text-slate-500 mt-1">Funciones de lunes a jueves.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Showcase Cinemas', '50% OFF en la segunda entrada', 'Promoción válida en complejos Showcase de Belgrano, Norte y Haedo.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Teatro Gran Rex -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-purple-800 tracking-tight bg-purple-50 px-3 py-1.5 rounded-lg border border-purple-100">TEATRO GRAN REX</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 6 cuotas sin interés en espectáculos</h3>
                        <p class="text-xs text-slate-500 mt-1">Obras teatrales y recitales seleccionados.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Teatro Gran Rex', 'Hasta 6 cuotas sin interés en espectáculos', 'Abonando con tarjetas habilitadas en boletería o Ticketek.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Ticketek Shows -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-indigo-700 tracking-tight bg-indigo-50 px-3 py-1.5 rounded-lg border border-indigo-100">TICKETEK</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">15% de reintegro en preventas</h3>
                        <p class="text-xs text-slate-500 mt-1">Con dinero en cuenta y Mercado Pago.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-indigo-100 text-indigo-700 px-2 py-0.5 rounded">Mercado Pago</span>
                        </div>
                        <button onclick="openPromoDetail('Ticketek', '15% de reintegro en preventas', 'Tope de reintegro $15.000 por usuario.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 3: TECNO Y ELECTRO -->
        <section id="section-electro" class="promo-section space-y-5">
            <div class="flex items-center justify-between">
                <div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight">Cuotas en tecno y electro</h2>
                    <p class="text-xs sm:text-sm text-slate-500 mt-0.5">Renová tus dispositivos con financiación imperdible.</p>
                </div>
                <button onclick="showMoreCategory('electro')" class="text-purple-600 hover:text-purple-800 font-bold text-sm flex items-center space-x-1 transition">
                    <span>Ver más</span>
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </button>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Cetrogar -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-blue-50 text-blue-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Especial</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-blue-800 tracking-tight bg-blue-50 px-3 py-1.5 rounded-lg border border-blue-100">CETROGAR</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 14 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Todos los días en Cetrogar.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('CETROGAR', 'Hasta 14 cuotas sin interés', 'Válido para compras online y sucursales.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Frávega -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-sky-600 tracking-tight bg-sky-50 px-3 py-1.5 rounded-lg border border-sky-100">FRÁVEGA</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 14 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Todos los días en Frávega.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('FRÁVEGA', 'Hasta 14 cuotas sin interés', 'Electro, línea blanca y tecnología.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Samsung -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-indigo-900 tracking-tight bg-indigo-50 px-3 py-1.5 rounded-lg border border-indigo-100">SAMSUNG</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 14 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Todos los días en Samsung Store.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('SAMSUNG', 'Hasta 14 cuotas sin interés', 'Promoción en smartphones y tablets seleccionadas.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Megatone -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-red-600 tracking-tight bg-red-50 px-3 py-1.5 rounded-lg border border-red-100">MEGATONE</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 14 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Todos los días en Megatone.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('MEGATONE', 'Hasta 14 cuotas sin interés', 'Aplicable a todo el catálogo online.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 4: VIAJES Y TURISMO -->
        <section id="section-viajes" class="promo-section space-y-5">
            <div class="flex items-center justify-between">
                <div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight">Cuotas y descuentos en viajes</h2>
                    <p class="text-xs sm:text-sm text-slate-500 mt-0.5">Planificá tus próximas vacaciones al mejor precio.</p>
                </div>
                <button onclick="showMoreCategory('viajes')" class="text-purple-600 hover:text-purple-800 font-bold text-sm flex items-center space-x-1 transition">
                    <span>Ver más</span>
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </button>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Viajes VerPromos -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative">
                    <div class="absolute top-3 right-3 bg-red-50 text-red-600 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">Plan Turbo</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-indigo-700 tracking-tight bg-indigo-50 px-3 py-1.5 rounded-lg border border-indigo-100">VIAJES VERPROMOS</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 35% off y 12 cuotas sin interés</h3>
                        <p class="text-xs text-slate-500 mt-1">Vuelos y hoteles seleccionados.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-purple-100 text-purple-700 px-2 py-0.5 rounded">Débito</span>
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Viajes VerPromos', 'Hasta 35% off y 12 cuotas sin interés', 'Destinos nacionales e internacionales habilitados.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Aerolíneas -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-sky-700 tracking-tight bg-sky-50 px-3 py-1.5 rounded-lg border border-sky-100">AEROLÍNEAS</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">6 cuotas sin interés en vuelos de cabotaje</h3>
                        <p class="text-xs text-slate-500 mt-1">Todos los destinos de Argentina.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Aerolíneas', '6 cuotas sin interés', 'Válido para volar por todo el país.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Hoteles & Resorts -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-blue-900 tracking-tight bg-blue-50 px-3 py-1.5 rounded-lg border border-blue-100">HOTELES & RESORTS</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">20% de reintegro en alojamientos</h3>
                        <p class="text-xs text-slate-500 mt-1">Pagando con tu dinero en cuenta.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-indigo-100 text-indigo-700 px-2 py-0.5 rounded">Dinero en cuenta</span>
                        </div>
                        <button onclick="openPromoDetail('Hoteles & Resorts', '20% de reintegro', 'Tope de reintegro $30.000 por usuario.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>

                <!-- Buquebus -->
                <div class="bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group">
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-teal-800 tracking-tight bg-teal-50 px-3 py-1.5 rounded-lg border border-teal-100">BUQUEBUS</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base sm:text-lg group-hover:text-purple-600 transition leading-snug">Hasta 9 cuotas sin interés a Uruguay</h3>
                        <p class="text-xs text-slate-500 mt-1">Pasajes y excursiones.</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <div class="flex items-center space-x-2 text-[11px] font-semibold text-slate-600">
                            <span class="bg-amber-100 text-amber-800 px-2 py-0.5 rounded">Crédito</span>
                        </div>
                        <button onclick="openPromoDetail('Buquebus', 'Hasta 9 cuotas sin interés', 'Rutas Buenos Aires - Montevideo / Colonia.')" class="w-full bg-purple-50 hover:bg-purple-600 text-purple-700 hover:text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 5: SORTEOS EXCLUSIVOS (CINEMARK) -->
        <section id="section-sorteos" class="promo-section space-y-5 bg-gradient-to-tr from-amber-500/10 via-purple-500/5 to-transparent p-6 sm:p-8 rounded-3xl border border-amber-500/20">
            <div class="flex items-center justify-between">
                <div>
                    <span class="bg-amber-500 text-slate-950 text-[10px] font-extrabold px-3 py-1 rounded-full uppercase tracking-wider">Comunidad VIP</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-slate-900 tracking-tight mt-1">Sorteos Exclusivos para Miembros</h2>
                    <p class="text-xs sm:text-sm text-slate-600 mt-0.5">Participá en nuestros sorteos semanales con tu cuenta de VerPromos.</p>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Tarjeta Sorteo Cinemark (Requisito: 1 entrada para Cinemark) -->
                <div class="bg-white rounded-2xl p-6 shadow-md border border-amber-200 flex flex-col justify-between relative overflow-hidden">
                    <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-amber-400/10 rounded-full blur-2xl"></div>
                    <div>
                        <div class="flex items-center space-x-3 mb-4">
                            <div class="w-12 h-12 rounded-2xl bg-amber-100 text-amber-700 flex items-center justify-center text-xl font-bold shadow-xs">
                                <i class="fa-solid fa-ticket"></i>
                            </div>
                            <div>
                                <span class="text-xs font-bold text-amber-600 uppercase">Sorteo Activo</span>
                                <h3 class="text-xl font-black text-slate-900">1 Entrada para Cinemark</h3>
                            </div>
                        </div>
                        <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">
                            Exclusivo miembros registrados. Sorteamos 1 entrada para Cinemark. Ingresá tus datos para participar al instante.
                        </p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 flex items-center justify-between">
                        <span class="text-xs font-bold text-slate-500"><i class="fa-regular fa-clock mr-1"></i> Finaliza en 2 días</span>
                        <button onclick="openGiveawayModal()" class="bg-amber-500 hover:bg-amber-600 text-slate-950 font-extrabold px-5 py-2.5 rounded-xl text-xs shadow-md transition transform hover:scale-105">
                            Participar Ahora
                        </button>
                    </div>
                </div>

                <!-- Tarjeta Sorteo Supermercado -->
                <div class="bg-white rounded-2xl p-6 shadow-md border border-purple-200 flex flex-col justify-between relative overflow-hidden">
                    <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-purple-400/10 rounded-full blur-2xl"></div>
                    <div>
                        <div class="flex items-center space-x-3 mb-4">
                            <div class="w-12 h-12 rounded-2xl bg-purple-100 text-purple-700 flex items-center justify-center text-xl font-bold shadow-xs">
                                <i class="fa-solid fa-cart-shopping"></i>
                            </div>
                            <div>
                                <span class="text-xs font-bold text-purple-600 uppercase">Sorteo Activo</span>
                                <h3 class="text-xl font-black text-slate-900">Orden de Compra $50.000</h3>
                            </div>
                        </div>
                        <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">
                            Sorteamos órdenes de compra semanales para canjear en Coto, Jumbo o Carrefour. ¡No te lo pierdas!
                        </p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 flex items-center justify-between">
                        <span class="text-xs font-bold text-slate-500"><i class="fa-regular fa-clock mr-1"></i> Finaliza en 4 días</span>
                        <button onclick="openGiveawayModal()" class="bg-purple-600 hover:bg-purple-700 text-white font-extrabold px-5 py-2.5 rounded-xl text-xs shadow-md transition transform hover:scale-105">
                            Participar Ahora
                        </button>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-slate-900 text-slate-400 mt-20 border-t border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
                <div class="space-y-4">
                    <div class="flex items-center space-x-3">
                        <div class="bg-purple-600 text-white p-2 rounded-xl flex items-center justify-center">
                            <i class="fa-solid fa-tags text-lg"></i>
                        </div>
                        <span class="text-xl font-extrabold text-white">VerPromos.com</span>
                    </div>
                    <p class="text-xs text-slate-400 leading-relaxed">
                        El portal líder en recopilación de descuentos, cuotas sin interés y beneficios en Argentina con sistema inteligente y cuentas verificadas.
                    </p>
                </div>
                <div>
                    <h4 class="text-white font-bold text-xs uppercase tracking-wider mb-4">Categorías</h4>
                    <ul class="space-y-2 text-xs">
                        <li><a href="#section-super" class="hover:text-white transition">Supermercados</a></li>
                        <li><a href="#section-cine" class="hover:text-white transition">Cine & Espectáculos</a></li>
                        <li><a href="#section-electro" class="hover:text-white transition">Cuotas Tecno y Electro</a></li>
                        <li><a href="#section-sorteos" class="hover:text-white transition">Sorteos Miembros</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-white font-bold text-xs uppercase tracking-wider mb-4">Comunidad</h4>
                    <ul class="space-y-2 text-xs">
                        <li><a href="#" onclick="openWhatsAppModal(); return false;" class="hover:text-white transition flex items-center space-x-2"><i class="fa-brands fa-whatsapp text-emerald-400"></i> <span>Canal de WhatsApp</span></a></li>
                        <li><a href="#" onclick="openAuthModal(); return false;" class="hover:text-white transition">Área de Miembros</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-white font-bold text-xs uppercase tracking-wider mb-4">Legal</h4>
                    <p class="text-[11px] text-slate-500 leading-relaxed">
                        VerPromos.com recopila información pública de promociones bancarias y comercios. Sujeto a términos y condiciones de cada entidad.
                    </p>
                </div>
            </div>
            <div class="pt-8 border-t border-slate-800 flex flex-col sm:flex-row items-center justify-between text-xs text-slate-500">
                <p>&copy; 2026 VerPromos.com - Todos los derechos reservados.</p>
                <div class="flex space-x-6 mt-4 sm:mt-0">
                    <a href="#" class="hover:text-slate-400">Términos y Condiciones</a>
                    <a href="#" class="hover:text-slate-400">Política de Privacidad</a>
                </div>
            </div>
        </div>
    </footer>

    <!-- MODAL DE DETALLE DE BENEFICIO (Ventana emergente al hacer clic) -->
    <div id="promoModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white rounded-3xl max-w-lg w-full p-6 sm:p-8 shadow-2xl transform scale-95 transition-transform duration-300 relative" id="promoModalContent">
            <button onclick="closePromoModal()" class="absolute top-5 right-5 text-slate-400 hover:text-slate-700 bg-slate-100 hover:bg-slate-200 w-9 h-9 rounded-full flex items-center justify-center transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="space-y-4">
                <span id="modalBrand" class="bg-purple-100 text-purple-700 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wide">Comercio</span>
                <h3 id="modalTitle" class="text-2xl font-black text-slate-900 leading-tight">Título de la Promoción</h3>
                <p id="modalDesc" class="text-slate-600 text-xs sm:text-sm leading-relaxed">Descripción detallada del beneficio, topes de reintegro y condiciones generales.</p>
                
                <div class="bg-purple-50 border border-purple-100 rounded-2xl p-4 space-y-2">
                    <h4 class="text-xs font-bold text-purple-900 uppercase tracking-wider flex items-center space-x-1.5">
                        <i class="fa-solid fa-circle-info text-purple-600"></i>
                        <span>Medios de Pago Habilitados</span>
                    </h4>
                    <p id="modalPaymentInfo" class="text-xs text-purple-700">Tarjetas de Débito, Crédito Visa/Mastercard y Mercado Pago.</p>
                </div>

                <div class="pt-4 flex items-center space-x-3">
                    <button onclick="closePromoModal()" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold py-3 rounded-xl text-sm transition">
                        Cerrar
                    </button>
                    <button onclick="simulateRedeem()" class="flex-1 bg-purple-600 hover:bg-purple-700 text-white font-bold py-3 rounded-xl text-sm shadow-md transition flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-share-nodes"></i>
                        <span>Compartir Promo</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL DE SORTEO / ENTRADA CINEMARK -->
    <div id="giveawayModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl transform scale-95 transition-transform duration-300 relative">
            <button onclick="closeGiveawayModal()" class="absolute top-5 right-5 text-slate-400 hover:text-slate-700 bg-slate-100 hover:bg-slate-200 w-9 h-9 rounded-full flex items-center justify-center transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="text-center mb-6">
                <div class="w-16 h-16 bg-amber-100 text-amber-600 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl shadow-inner">
                    <i class="fa-solid fa-ticket"></i>
                </div>
                <h3 class="text-2xl font-black text-slate-900">Sorteo 1 Entrada Cinemark</h3>
                <p class="text-xs text-slate-600 mt-1">Exclusivo miembros. Completá tus datos para participar enviando nombre, apellido y correo electrónico.</p>
            </div>
            
            <form onsubmit="submitGiveaway(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Nombre</label>
                    <input type="text" id="giveawayName" required placeholder="Tu nombre" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Apellido</label>
                    <input type="text" id="giveawayLastName" required placeholder="Tu apellido" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-amber-500">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Correo Electrónico</label>
                    <input type="email" id="giveawayEmail" required placeholder="tu@correo.com" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-amber-500">
                </div>
                <button type="submit" class="w-full bg-amber-500 hover:bg-amber-600 text-slate-950 font-black py-3.5 rounded-xl shadow-lg transition text-center mt-2">
                    Enviar e Inscribirme al Sorteo
                </button>
            </form>
        </div>
    </div>

    <!-- MODAL DE USUARIO / AUTENTICACIÓN & PERFILES -->
    <div id="authModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl transform scale-95 transition-transform duration-300 relative">
            <button onclick="closeAuthModal()" class="absolute top-5 right-5 text-slate-400 hover:text-slate-700 bg-slate-100 hover:bg-slate-200 w-9 h-9 rounded-full flex items-center justify-center transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="text-center mb-6">
                <div class="w-16 h-16 bg-purple-100 text-purple-600 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl shadow-inner">
                    <i class="fa-solid fa-user-shield"></i>
                </div>
                <h3 class="text-2xl font-black text-slate-900">Área de Miembros</h3>
                <p class="text-xs text-slate-600 mt-1">Seleccioná una cuenta pre-registrada o ingresá tus credenciales.</p>
            </div>

            <!-- Botones de Acceso Rápido con las Cuentas Solicitadas -->
            <div class="grid grid-cols-2 gap-2 mb-6">
                <button onclick="loadPresetUser('mauricio')" class="bg-purple-50 hover:bg-purple-100 border border-purple-200 p-2.5 rounded-xl text-left transition">
                    <p class="text-[11px] font-bold text-purple-900">Mauricio Acosta</p>
                    <p class="text-[9px] text-slate-500">Mercado Pago</p>
                </button>
                <button onclick="loadPresetUser('maria')" class="bg-purple-50 hover:bg-purple-100 border border-purple-200 p-2.5 rounded-xl text-left transition">
                    <p class="text-[11px] font-bold text-purple-900">María Lucía</p>
                    <p class="text-[9px] text-slate-500">Capital Federal</p>
                </button>
            </div>
            
            <form onsubmit="saveAuthCache(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Nombre y Apellido</label>
                    <input type="text" id="authInputName" required placeholder="Ej. Mauricio Acosta Danaher" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-purple-500">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">DNI</label>
                    <input type="text" id="authInputDni" required placeholder="Ej. 37170491" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-purple-500">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Correo Electrónico</label>
                    <input type="email" id="authInputEmail" required placeholder="mauricioacostacom@gmail.com" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-purple-500">
                </div>
                <div>
                    <label class="block text-xs font-bold text-slate-700 mb-1">Contraseña</label>
                    <input type="password" id="authInputPass" required placeholder="••••••••" class="w-full px-4 py-3 bg-slate-100 border-none rounded-xl text-sm focus:ring-2 focus:ring-purple-500">
                </div>
                <button type="submit" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-black py-3.5 rounded-xl shadow-lg transition text-center mt-2">
                    Acceder como Miembro
                </button>
            </form>
        </div>
    </div>

    <!-- MODAL DE WHATSAPP -->
    <div id="whatsappModal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-xs flex items-center justify-center p-4 opacity-0 pointer-events-none transition-opacity duration-300">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 shadow-2xl transform scale-95 transition-transform duration-300 relative text-center">
            <button onclick="closeWhatsAppModal()" class="absolute top-5 right-5 text-slate-400 hover:text-slate-700 bg-slate-100 hover:bg-slate-200 w-9 h-9 rounded-full flex items-center justify-center transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <div class="w-16 h-16 bg-emerald-100 text-emerald-600 rounded-full flex items-center justify-center mx-auto mb-4 text-3xl shadow-inner">
                <i class="fa-brands fa-whatsapp"></i>
            </div>
            <h3 class="text-2xl font-extrabold text-slate-900 mb-2">Unite al Canal de WhatsApp</h3>
            <p class="text-xs sm:text-sm text-slate-600 mb-6">Recibí alertas instantáneas de descuentos relámpago y cuotas sin interés directo en tu celular.</p>
            
            <a href="https://whatsapp.com" target="_blank" onclick="closeWhatsAppModal()" class="block w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-3.5 rounded-xl shadow-lg transition text-center mb-3">
                Unirme Ahora
            </a>
            <button onclick="closeWhatsAppModal()" class="text-xs text-slate-500 hover:text-slate-700 font-medium">
                Quizás más tarde
            </button>
        </div>
    </div>

    <!-- TOAST DE NOTIFICACIÓN -->
    <div id="toastNotification" class="fixed bottom-5 right-5 z-50 bg-slate-900 text-white px-5 py-3.5 rounded-2xl shadow-2xl flex items-center space-x-3 transform translate-y-24 opacity-0 transition-all duration-300">
        <div class="bg-emerald-500 text-white w-6 h-6 rounded-full flex items-center justify-center text-xs">
            <i class="fa-solid fa-check"></i>
        </div>
        <div>
            <p class="text-xs font-bold" id="toastTitle">¡Acción exitosa!</p>
            <p class="text-[11px] text-slate-300" id="toastDesc">Operación completada correctamente.</p>
        </div>
    </div>

    <!-- SCRIPTS DE FUNCIONALIDAD COMPLETA -->
    <script>
        // --- 1. BASE DE DATOS DE PROMOS PARA BÚSQUEDA Y FILTRADO ---
        const promoDatabase = [
            { category: 'super', brand: 'Coto Digital', title: 'Hasta 25% off y 18 cuotas sin interés', desc: 'Aprovechá todos los beneficios exclusivos pagando con tus medios habilitados en Coto.', tag: 'Plan Turbo', payment: 'Débito, Crédito y Mercado Pago' },
            { category: 'super', brand: 'Vea Supermercados', title: 'Hasta 25% off y 12 cuotas sin interés', desc: 'Válido en hipermercados Vea de todo el país en días seleccionados.', tag: 'Plan Turbo', payment: 'Tarjetas Débito y Crédito' },
            { category: 'super', brand: 'JUMBO', title: 'Hasta 25% off y 12 cuotas sin interés', desc: 'Aprovechá en Jumbo app y tiendas físicas con tarjetas habilitadas.', tag: 'Plan Turbo', payment: 'Débito y Crédito' },
            { category: 'super', brand: 'DISCO', title: 'Hasta 25% off y 12 cuotas sin interés', desc: 'Descuento aplicado en línea de cajas en supermercados Disco.', tag: 'Plan Turbo', payment: 'Débito y Crédito' },
            { category: 'cine', brand: 'CINEMARK HOYTS', title: '2x1 todos los días en salas 2D y 3D', desc: 'Exclusivo pagando con Mercado Pago y tarjetas asociadas en Capital Federal y GBA.', tag: '2x1 Entradas', payment: 'Mercado Pago y Tarjetas' },
            { category: 'cine', brand: 'SHOWCASE', title: '50% OFF en la segunda entrada', desc: 'Funciones de lunes a jueves en complejos Showcase.', tag: 'Cine', payment: 'Tarjetas de Crédito' },
            { category: 'espectaculos', brand: 'TEATRO GRAN REX', title: 'Hasta 6 cuotas sin interés en espectáculos', desc: 'Obras teatrales y recitales seleccionados en cartelera.', tag: 'Espectáculos', payment: 'Tarjetas de Crédito' },
            { category: 'espectaculos', brand: 'TICKETEK', title: '15% de reintegro en preventas', desc: 'Con dinero en cuenta y Mercado Pago. Tope $15.000.', tag: 'Reintegro', payment: 'Mercado Pago' },
            { category: 'electro', brand: 'CETROGAR', title: 'Hasta 14 cuotas sin interés', desc: 'Válido para compras online y sucursales en tecnología y electro.', tag: 'Especial', payment: 'Tarjetas de Crédito' },
            { category: 'electro', brand: 'FRÁVEGA', title: 'Hasta 14 cuotas sin interés', desc: 'Electro, línea blanca y tecnología todos los días.', tag: 'Financiación', payment: 'Tarjetas de Crédito' },
            { category: 'electro', brand: 'SAMSUNG', title: 'Hasta 14 cuotas sin interés', desc: 'Promoción en smartphones, smart TVs y tablets seleccionadas.', tag: 'Tecnología', payment: 'Tarjetas de Crédito' },
            { category: 'electro', brand: 'MEGATONE', title: 'Hasta 14 cuotas sin interés', desc: 'Aplicable a todo el catálogo online de electrodomésticos.', tag: 'Financiación', payment: 'Tarjetas de Crédito' },
            { category: 'viajes', brand: 'VIAJES VERPROMOS', title: 'Hasta 35% off y 12 cuotas sin interés', desc: 'Destinos nacionales e internacionales habilitados en paquetes.', tag: 'Plan Turbo', payment: 'Débito y Crédito' },
            { category: 'viajes', brand: 'AEROLÍNEAS', title: '6 cuotas sin interés en vuelos de cabotaje', desc: 'Válido para volar por todo el país durante la temporada.', tag: 'Vuelos', payment: 'Tarjetas de Crédito' },
            { category: 'viajes', brand: 'HOTELES & RESORTS', title: '20% de reintegro en alojamientos', desc: 'Pagando con tu dinero en cuenta. Tope $30.000.', tag: 'Reintegro', payment: 'Dinero en cuenta' },
            { category: 'viajes', brand: 'BUQUEBUS', title: 'Hasta 9 cuotas sin interés a Uruguay', desc: 'Pasajes y excursiones en rutas Buenos Aires - Montevideo / Colonia.', tag: 'Turismo', payment: 'Tarjetas de Crédito' },
            { category: 'sorteos', brand: 'CINEMARK', title: 'Sorteo 1 Entrada para Cinemark', desc: 'Entrada doble exclusiva para miembros registrados en VerPromos.', tag: 'Sorteo VIP', payment: 'Exclusivo Miembros' }
        ];

        // --- 2. GESTIÓN DE CUENTAS PRECARGADAS ---
        const presetUsers = {
            mauricio: {
                name: 'Mauricio Acosta Danaher',
                dni: '37170491',
                email: 'mauricioacostacom@gmail.com',
                payment: 'Mercado Pago',
                due: '20 de diciembre de 2026',
                status: 'Cuenta al día habilitada',
                province: 'Capital Federal',
                interests: ['Cine', 'Espectáculos', 'Supermercados']
            },
            maria: {
                name: 'María Lucía Carpio Peralta',
                dni: '93.976.879',
                email: 'marialucia20@gmail.com',
                payment: 'Mercado Pago / Tarjeta',
                due: '15 de diciembre de 2026',
                status: 'Cuenta al día habilitada',
                province: 'Capital Federal',
                interests: ['Cine', 'Espectáculos', 'Supermercados']
            }
        };

        window.addEventListener('DOMContentLoaded', () => {
            // Por defecto cargar a Mauricio Acosta o verificar caché
            const cached = localStorage.getItem('verpromos_active_user');
            if (!cached) {
                localStorage.setItem('verpromos_active_user', JSON.stringify(presetUsers.mauricio));
            }
            loadUserCache();
        });

        function loadPresetUser(key) {
            const user = presetUsers[key];
            if (user) {
                localStorage.setItem('verpromos_active_user', JSON.stringify(user));
                document.getElementById('provinceSelect').value = user.province;
                loadUserCache();
                closeAuthModal();
                showToast("¡Sesión iniciada!", `Bienvenido/a ${user.name} (${user.province}).`);
            }
        }

        function saveAuthCache(e) {
            e.preventDefault();
            const name = document.getElementById('authInputName').value;
            const dni = document.getElementById('authInputDni').value;
            const email = document.getElementById('authInputEmail').value;
            const province = document.getElementById('provinceSelect').value;

            const userData = { name, dni, email, province, status: 'Cuenta activa', interests: ['Cine', 'Supermercados'] };
            localStorage.setItem('verpromos_active_user', JSON.stringify(userData));

            loadUserCache();
            closeAuthModal();
            showToast("¡Cuenta registrada!", `Hola ${name}, tus datos están guardados.`);
        }

        function loadUserCache() {
            const cached = localStorage.getItem('verpromos_active_user');
            if (cached) {
                try {
                    const data = JSON.parse(cached);
                    document.getElementById('userIndicator').classList.remove('hidden');
                    if(data.province) {
                        document.getElementById('provinceSelect').value = data.province;
                    }
                } catch(err) {
                    console.error("Error reading cache", err);
                }
            }
        }

        // --- 3. BUSCADOR INTERACTIVO Y DESPLEGABLE SOBRE EL MENÚ ---
        const liveSearchInput = document.getElementById('liveSearchInput');
        const searchOverlayBar = document.getElementById('searchOverlayBar');
        const searchResultsContainer = document.getElementById('searchResultsContainer');
        const searchResultsGrid = document.getElementById('searchResultsGrid');
        const topCarouselSection = document.getElementById('topCarouselSection');

        function toggleSearchOverlay() {
            const isOpen = searchOverlayBar.classList.contains('translate-y-0');
            if (isOpen) {
                searchOverlayBar.classList.remove('translate-y-0', 'opacity-100');
                searchOverlayBar.classList.add('-translate-y-full', 'opacity-0', 'pointer-events-none');
            } else {
                searchOverlayBar.classList.remove('-translate-y-full', 'opacity-0', 'pointer-events-none');
                searchOverlayBar.classList.add('translate-y-0', 'opacity-100');
                setTimeout(() => liveSearchInput.focus(), 100);
            }
        }

        function clearSearchInput() {
            liveSearchInput.value = '';
            searchResultsContainer.classList.add('hidden');
            topCarouselSection.style.display = 'block';
            document.querySelectorAll('.promo-section').forEach(sec => sec.style.display = 'block');
        }

        if (liveSearchInput) {
            liveSearchInput.addEventListener('input', function(e) {
                const query = e.target.value.toLowerCase().trim();
                
                if (query.length > 0) {
                    // Ocultar carrusel superior y mostrar solo resultados de búsqueda justo debajo
                    topCarouselSection.style.display = 'none';
                    document.querySelectorAll('.promo-section').forEach(sec => sec.style.display = 'none');
                    searchResultsContainer.classList.remove('hidden');

                    const filtered = promoDatabase.filter(p => 
                        p.brand.toLowerCase().includes(query) || 
                        p.title.toLowerCase().includes(query) || 
                        p.desc.toLowerCase().includes(query) ||
                        p.category.toLowerCase().includes(query)
                    );

                    renderSearchResults(filtered);
                } else {
                    searchResultsContainer.classList.add('hidden');
                    topCarouselSection.style.display = 'block';
                    document.querySelectorAll('.promo-section').forEach(sec => sec.style.display = 'block');
                }
            });
        }

        function renderSearchResults(results) {
            searchResultsGrid.innerHTML = '';
            if (results.length === 0) {
                searchResultsGrid.innerHTML = `<div class="col-span-full py-8 text-center text-slate-500 font-medium">No se encontraron promociones para tu búsqueda. Probá con otra palabra.</div>`;
                return;
            }

            results.forEach(promo => {
                const card = document.createElement('div');
                card.className = "bg-white rounded-2xl p-5 shadow-sm hover:shadow-xl border border-slate-100 transition duration-300 flex flex-col justify-between group relative";
                card.innerHTML = `
                    <div class="absolute top-3 right-3 bg-purple-50 text-purple-700 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase tracking-wider">${promo.tag}</div>
                    <div>
                        <div class="h-12 flex items-center mb-4">
                            <span class="text-lg font-black text-purple-900 tracking-tighter bg-purple-50 px-3 py-1.5 rounded-lg border border-purple-100">${promo.brand}</span>
                        </div>
                        <h3 class="font-bold text-slate-800 text-base group-hover:text-purple-600 transition leading-snug">${promo.title}</h3>
                        <p class="text-xs text-slate-500 mt-1">${promo.desc}</p>
                    </div>
                    <div class="mt-6 pt-4 border-t border-slate-100 space-y-3">
                        <button onclick="openPromoDetail('${promo.brand}', '${promo.title}', '${promo.desc}', '${promo.payment}')" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-bold py-2.5 rounded-xl text-sm transition text-center shadow-xs">
                            Ver beneficio
                        </button>
                    </div>
                `;
                searchResultsGrid.appendChild(card);
            });
        }

        function resetSearchAndFilter() {
            liveSearchInput.value = '';
            searchResultsContainer.classList.add('hidden');
            topCarouselSection.style.display = 'block';
            document.querySelectorAll('.promo-section').forEach(sec => sec.style.display = 'block');
            filterCategory('all');
            if(searchOverlayBar.classList.contains('translate-y-0')) toggleSearchOverlay();
        }

        // --- 4. FILTRADO DE CATEGORÍAS Y "VER MÁS" ---
        function filterCategory(category) {
            document.querySelectorAll('.category-btn').forEach(btn => {
                const div = btn.querySelector('div');
                const span = btn.querySelector('span');
                if (btn.getAttribute('data-category') === category) {
                    div.classList.remove('bg-slate-100', 'text-slate-600', 'bg-amber-100', 'text-amber-700');
                    div.classList.add('bg-purple-600', 'text-white');
                    span.classList.remove('text-slate-700', 'text-amber-800');
                    span.classList.add('text-purple-700', 'font-bold');
                } else {
                    div.classList.remove('bg-purple-600', 'text-white');
                    if(btn.getAttribute('data-category') === 'sorteos') {
                        div.classList.add('bg-amber-100', 'text-amber-700');
                    } else {
                        div.classList.add('bg-slate-100', 'text-slate-600');
                    }
                    span.classList.remove('text-purple-700', 'font-bold');
                    span.classList.add('text-slate-700');
                }
            });

            const sections = {
                'super': document.getElementById('section-super'),
                'cine': document.getElementById('section-cine'),
                'espectaculos': document.getElementById('section-cine'), // Agrupado visualmente
                'electro': document.getElementById('section-electro'),
                'viajes': document.getElementById('section-viajes'),
                'sorteos': document.getElementById('section-sorteos')
            };

            if (category === 'all') {
                Object.values(sections).forEach(sec => { if(sec) sec.style.display = 'block'; });
            } else {
                Object.keys(sections).forEach(key => {
                    if(sections[key]) {
                        if (category === 'cine' || category === 'espectaculos') {
                            sections['cine'].style.display = 'block';
                            if(key !== 'cine') sections[key].style.display = 'none';
                        } else {
                            sections[key].style.display = (key === category) ? 'block' : 'none';
                        }
                    }
                });
            }
            if(searchResultsContainer) searchResultsContainer.classList.add('hidden');
            topCarouselSection.style.display = 'block';
        }

        function showMoreCategory(catName) {
            filterCategory(catName);
            showToast("Categoría expandida", `Mostrando todos los beneficios y cuotas de ${catName}.`);
        }

        // --- 5. CARRUSEL SUPERIOR ADAPTABLE (SLIDES Y TOUCH SWIPE) ---
        let currentSlide = 0;
        const totalSlides = 2;

        function moveCarousel(direction) {
            currentSlide = (currentSlide + direction + totalSlides) % totalSlides;
            updateCarouselPosition();
        }

        function goToSlide(index) {
            currentSlide = index;
            updateCarouselPosition();
        }

        function updateCarouselPosition() {
            const track = document.getElementById('carouselTrack');
            track.scrollTo({ left: track.clientWidth * currentSlide, behavior: 'smooth' });
        }

        // --- 6. MENÚ LATERAL TOGGLE ---
        function toggleSideMenu() {
            const menu = document.getElementById('sideMenu');
            const backdrop = document.getElementById('sideMenuBackdrop');
            const isOpen = menu.classList.contains('translate-x-0');

            if (isOpen) {
                menu.classList.remove('translate-x-0');
                menu.classList.add('-translate-x-full');
                backdrop.classList.remove('opacity-100', 'pointer-events-auto');
                backdrop.classList.add('opacity-0', 'pointer-events-none');
            } else {
                menu.classList.remove('-translate-x-full');
                menu.classList.add('translate-x-0');
                backdrop.classList.remove('opacity-0', 'pointer-events-none');
                backdrop.classList.add('opacity-100', 'pointer-events-auto');
            }
        }

        // --- 7. SELECTOR DE PROVINCIA ---
        function changeProvince(province) {
            showToast("Provincia actualizada", `Viendo promociones exclusivas para ${province}.`);
            const cached = localStorage.getItem('verpromos_active_user');
            if (cached) {
                try {
                    let data = JSON.parse(cached);
                    data.province = province;
                    localStorage.setItem('verpromos_active_user', JSON.stringify(data));
                } catch(e){}
            }
        }

        // --- 8. MODALES Y DETALLES DE BENEFICIOS ---
        function openPromoDetail(brand, title, desc, payment = 'Tarjetas de Débito, Crédito y Mercado Pago') {
            document.getElementById('modalBrand').innerText = brand;
            document.getElementById('modalTitle').innerText = title;
            document.getElementById('modalDesc').innerText = desc;
            document.getElementById('modalPaymentInfo').innerText = payment;

            const modal = document.getElementById('promoModal');
            const content = document.getElementById('promoModalContent');
            modal.classList.remove('opacity-0', 'pointer-events-none');
            content.classList.remove('scale-95');
            content.classList.add('scale-100');
        }

        function closePromoModal() {
            const modal = document.getElementById('promoModal');
            const content = document.getElementById('promoModalContent');
            modal.classList.add('opacity-0', 'pointer-events-none');
            content.classList.remove('scale-100');
            content.classList.add('scale-95');
        }

        function openGiveawayModal() {
            const modal = document.getElementById('giveawayModal');
            modal.classList.remove('opacity-0', 'pointer-events-none');
            // Autocompletar con usuario actual en sesión si existe
            const cached = localStorage.getItem('verpromos_active_user');
            if(cached) {
                try {
                    const data = JSON.parse(cached);
                    const parts = data.name.split(' ');
                    document.getElementById('giveawayName').value = parts[0] || '';
                    document.getElementById('giveawayLastName').value = parts.slice(1).join(' ') || '';
                    document.getElementById('giveawayEmail').value = data.email || '';
                } catch(e){}
            }
        }

        function closeGiveawayModal() {
            document.getElementById('giveawayModal').classList.add('opacity-0', 'pointer-events-none');
        }

        function submitGiveaway(e) {
            e.preventDefault();
            const name = document.getElementById('giveawayName').value;
            closeGiveawayModal();
            showToast("¡Inscripción exitosa!", `¡Felicitaciones ${name}! Ya estás participando por la entrada a Cinemark.`);
        }

        function openAuthModal() {
            document.getElementById('authModal').classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeAuthModal() {
            document.getElementById('authModal').classList.add('opacity-0', 'pointer-events-none');
        }

        function openWhatsAppModal() {
            document.getElementById('whatsappModal').classList.remove('opacity-0', 'pointer-events-none');
        }

        function closeWhatsAppModal() {
            document.getElementById('whatsappModal').classList.add('opacity-0', 'pointer-events-none');
        }

        function simulateRedeem() {
            closePromoModal();
            const dummy = document.createElement('textarea');
            document.body.appendChild(dummy);
            dummy.value = window.location.href;
            document.execCommand('copy');
            document.body.removeChild(dummy);
            showToast("¡Enlace copiado!", "Compartí este beneficio con tus amigos.");
        }

        function showToast(title, desc) {
            const toast = document.getElementById('toastNotification');
            document.getElementById('toastTitle').innerText = title;
            document.getElementById('toastDesc').innerText = desc;
            
            toast.classList.remove('translate-y-24', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3500);
        }

        function scrollCategories(offset) {
            const container = document.getElementById('categoryContainer');
            container.scrollBy({ left: offset, behavior: 'smooth' });
        }
    </script>

</body>
</html>
