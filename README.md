
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Digital Business Card - Syadad Nabil Mudzafar</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter & Plus Jakarta Sans -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        jakarta: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            gold: '#D4AF37',
                            silver: '#E5E7EB',
                            glass: 'rgba(255, 255, 255, 0.08)',
                            glassBorder: 'rgba(255, 255, 255, 0.18)',
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background: #030712;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        /* Latar Belakang Liquid yang Bergerak (Gaya Apple) */
        .ambient-bg {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            z-index: 0;
            overflow: hidden;
            pointer-events: none;
        }

        .blob {
            position: absolute;
            border-radius: 50%;
            filter: blur(100px);
            opacity: 0.35;
            mix-blend-mode: screen;
            animation: moveBlob 25s infinite alternate ease-in-out;
        }

        .blob-1 {
            width: 500px;
            height: 500px;
            background: radial-gradient(circle, #2563eb 0%, #1d4ed8 100%);
            top: -10%;
            left: -10%;
            animation-duration: 20s;
        }

        .blob-2 {
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, #0284c7 0%, #0369a1 100%);
            bottom: -15%;
            right: -10%;
            animation-duration: 28s;
            animation-delay: 2s;
        }

        .blob-3 {
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, #7d52a8 0%, #581c87 100%);
            top: 40%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation-duration: 25s;
            animation-delay: 5s;
        }

        @keyframes moveBlob {
            0% { transform: translate(0px, 0px) scale(1); }
            50% { transform: translate(100px, 80px) scale(1.1); }
            100% { transform: translate(-50px, -50px) scale(0.9); }
        }

        /* Efek Liquid Glass Premium */
        .liquid-glass {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.09) 0%, rgba(255, 255, 255, 0.03) 100%);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid rgba(255, 255, 255, 0.16);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4),
                        inset 0 1px 1px rgba(255, 255, 255, 0.2),
                        inset 0 10px 20px rgba(255, 255, 255, 0.05);
        }

        /* Mekanisme Balik 3D Terkunci (Sama Sekali Tidak Geser) */
        .card-container {
            perspective: 2000px;
            touch-action: manipulation;
            position: relative;
            z-index: 40;
            width: 100%;
            height: 260px; /* Kunci tinggi wadah agar elemen luar tidak terpengaruh */
        }

        .card-inner {
            position: absolute; /* Ubah ke absolut untuk penguncian posisi total */
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            transition: transform 0.6s cubic-bezier(0.19, 1, 0.22, 1);
            transform-style: preserve-3d;
            -webkit-transform-style: preserve-3d;
            will-change: transform;
        }

        /* Rotasi murni tepat di tempat */
        .card-inner.flipped {
            transform: rotateY(180deg) !important;
            -webkit-transform: rotateY(180deg) !important;
        }

        .card-front, .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
            border-radius: 1rem;
            box-sizing: border-box;
        }

        /* Pembagian kedalaman 3D agar tidak saling menembus saat rotasi */
        .card-front {
            z-index: 2;
            transform: rotateY(0deg);
            -webkit-transform: rotateY(0deg);
        }

        .card-back {
            z-index: 1;
            transform: rotateY(180deg);
            -webkit-transform: rotateY(180deg);
        }

        /* Pantulan kilau cahaya atas kartu */
        .glass-specular {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 50%;
            background: linear-gradient(to bottom, rgba(255,255,255,0.15) 0%, rgba(255,255,255,0) 100%);
            border-top-left-radius: inherit;
            border-top-right-radius: inherit;
            pointer-events: none;
        }

        /* Tombol dengan kilau transisi halus */
        .glass-btn {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.08) 0%, rgba(255, 255, 255, 0.02) 100%);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
            touch-action: manipulation;
        }

        .glass-btn::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent 45%, rgba(255, 255, 255, 0.1) 50%, transparent 55%);
            transform: rotate(45deg);
            transition: transform 0.5s ease;
            pointer-events: none;
        }

        .glass-btn:hover::after {
            transform: translate(50%, 50%) rotate(45deg);
        }

        .glass-btn:hover {
            border-color: rgba(255, 255, 255, 0.3);
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.15) 0%, rgba(255, 255, 255, 0.05) 100%);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.25);
        }
    </style>
</head>
<body class="text-white min-h-screen flex items-center justify-center p-4 md:p-8">

    <!-- Ambient Liquid Lighting -->
    <div class="ambient-bg">
        <div class="blob blob-1"></div>
        <div class="blob blob-2"></div>
        <div class="blob blob-3"></div>
    </div>

    <!-- Main Container -->
    <div class="relative z-10 w-full max-w-md mx-auto my-auto flex flex-col items-center">
        
        <!-- Header / Brand Logo -->
        <div class="w-full text-center mb-6">
            <span class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-white/5 border border-white/10 text-xs tracking-wider uppercase text-blue-300 backdrop-blur-md">
                <i class="fa-solid fa-id-card-clip text-[10px]"></i> Kartu Profil Digital
            </span>
        </div>

        <!-- 3D Flippable Card Section (Locked Position) -->
        <div class="card-container mb-8" id="cardContainer">
            <div class="card-inner" id="cardInner">
                
                <!-- KARTU SISI DEPAN -->
                <div class="card-front liquid-glass overflow-hidden p-6 flex flex-col justify-between relative">
                    <div class="glass-specular"></div>
                    
                    <!-- Top Ribbon -->
                    <div class="flex justify-between items-start">
                        <!-- Corporate Logo (img1.jpg dengan fallback cerdas) -->
                        <div class="flex items-center gap-3">
                            <div class="relative w-10 h-10 rounded-xl overflow-hidden bg-white/10 border border-white/20 flex items-center justify-center shadow-md" id="logoContainer">
                                <img src="img1.jpg" alt="Logo PT. Rifan Financindo" class="w-full h-full object-cover" onerror="handleImageError(this)">
                            </div>
                            <div class="text-left">
                                <p class="text-[9px] uppercase tracking-widest text-slate-400 font-semibold leading-none">MEMBER OF</p>
                                <h4 class="text-xs font-bold text-white tracking-wide leading-tight">PT. RIFAN FINANCINDO</h4>
                            </div>
                        </div>
                        
                        <!-- Verified Badge -->
                        <span class="text-[10px] px-2 py-1 rounded-md bg-white/5 border border-white/10 text-slate-300 flex items-center gap-1.5 backdrop-blur-sm">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span> TERVERIFIKASI
                        </span>
                    </div>

                    <!-- Name & Title -->
                    <div class="my-auto pt-4">
                        <h1 class="text-2xl font-bold tracking-tight font-jakarta bg-gradient-to-r from-white via-slate-100 to-slate-400 bg-clip-text text-transparent">
                            Syadad Nabil Mudzafar
                        </h1>
                        <p class="text-xs tracking-widest uppercase text-blue-300 font-semibold mt-1">
                            Bisnis Konsultan
                        </p>
                    </div>

                    <!-- Bottom Branding & Slogan -->
                    <div class="flex justify-between items-end border-t border-white/10 pt-3">
                        <div class="text-left">
                            <p class="text-[9px] text-slate-400 tracking-wider">SLOGAN PERUSAHAAN</p>
                            <p class="text-xs font-medium italic text-slate-200">"Strive for solid future."</p>
                        </div>
                        <!-- Flip Button Indicator -->
                        <div class="w-8 h-8 rounded-full bg-white/5 border border-white/10 flex items-center justify-center transition-colors">
                            <i class="fa-solid fa-rotate text-xs text-blue-300"></i>
                        </div>
                    </div>
                </div>

                <!-- KARTU SISI BELAKANG -->
                <div class="card-back liquid-glass overflow-hidden p-6 flex flex-col justify-between relative">
                    <div class="glass-specular"></div>

                    <!-- Header Back -->
                    <div class="flex justify-between items-center border-b border-white/10 pb-3">
                        <span class="text-xs font-semibold text-slate-300 flex items-center gap-2">
                            <i class="fa-solid fa-building text-blue-400"></i> Kantor Utama
                        </span>
                        <span class="text-[10px] text-slate-400 font-bold tracking-wider">RFB JAKARTA</span>
                    </div>

                    <!-- Alamat Content -->
                    <div class="text-left text-xs text-slate-300 my-auto py-2 space-y-1.5">
                        <p class="font-semibold text-white">AXA Tower Lt. 25</p>
                        <p class="text-[11px] leading-relaxed text-slate-400">
                            Jl. Prof. DR. Satrio Kav. 18, Lantai 30, 35, 23 & 25, Kuningan, Setiabudi, Jakarta Selatan, DKI Jakarta 12940
                        </p>
                        <p class="text-[10px] text-blue-300 flex items-center gap-1 mt-1">
                            <i class="fa-solid fa-network-wired"></i> Multi-lantai Operasional: 23, 25, 30, & 35
                        </p>
                    </div>

                    <!-- Action Back -->
                    <div class="flex justify-between items-center border-t border-white/10 pt-3">
                        <button id="copyAddressBtn" class="text-[11px] text-blue-300 hover:text-white flex items-center gap-1.5 transition-colors duration-200 bg-white/5 hover:bg-blue-500/20 px-2.5 py-1.5 rounded-lg border border-white/10">
                            <i class="fa-regular fa-copy" id="copyIcon"></i> <span id="copyText">Salin Alamat</span>
                        </button>
                        <div class="w-8 h-8 rounded-full bg-white/5 border border-white/10 flex items-center justify-center transition-colors">
                            <i class="fa-solid fa-rotate text-xs text-blue-300"></i>
                        </div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Tap Hint -->
        <p class="text-slate-400 text-xs mb-6 text-center animate-pulse z-10">
            <i class="fa-solid fa-hand-pointer mr-1"></i> Ketuk kartu untuk melihat alamat kantor
        </p>

        <!-- Social & Chat Buttons Grid -->
        <div class="w-full space-y-3 relative z-10">
            <h3 class="text-xs font-bold uppercase tracking-widest text-slate-400 text-left pl-1">Saluran Komunikasi Utama</h3>

            <!-- WhatsApp 1 -->
            <a href="https://wa.me/6285780085291?text=Halo%20Syadad%20Nabil%2C%20saya%20ingin%20berkonsultasi%20mengenai%20bisnis." 
               target="_blank" 
               class="glass-btn w-full px-5 py-4 rounded-xl flex items-center justify-between group">
                <div class="flex items-center gap-3.5">
                    <div class="w-10 h-10 rounded-lg bg-emerald-500/20 text-emerald-400 flex items-center justify-center border border-emerald-500/30 group-hover:bg-emerald-500 group-hover:text-white transition-all duration-300 shadow-md">
                        <i class="fa-brands fa-whatsapp text-xl"></i>
                    </div>
                    <div class="text-left">
                        <p class="text-xs text-slate-400 font-medium leading-none mb-1">WhatsApp Chat 1</p>
                        <p class="text-sm font-bold text-white tracking-wide">0857-8008-5291</p>
                    </div>
                </div>
                <div class="text-emerald-400 group-hover:translate-x-1 transition-transform duration-300">
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </div>
            </a>

            <!-- WhatsApp 2 -->
            <a href="https://wa.me/6285780085292?text=Halo%20Syadad%20Nabil%2C%20saya%20ingin%20berkonsultasi." 
               target="_blank" 
               class="glass-btn w-full px-5 py-4 rounded-xl flex items-center justify-between group">
                <div class="flex items-center gap-3.5">
                    <div class="w-10 h-10 rounded-lg bg-emerald-500/20 text-emerald-400 flex items-center justify-center border border-emerald-500/30 group-hover:bg-emerald-500 group-hover:text-white transition-all duration-300 shadow-md">
                        <i class="fa-brands fa-whatsapp text-xl"></i>
                    </div>
                    <div class="text-left">
                        <p class="text-xs text-slate-400 font-medium leading-none mb-1">WhatsApp Chat 2</p>
                        <p class="text-sm font-bold text-white tracking-wide">0857-8008-5292</p>
                    </div>
                </div>
                <div class="text-emerald-400 group-hover:translate-x-1 transition-transform duration-300">
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </div>
            </a>

            <!-- Telegram -->
            <a href="https://t.me/gus_adad" 
               target="_blank" 
               class="glass-btn w-full px-5 py-4 rounded-xl flex items-center justify-between group">
                <div class="flex items-center gap-3.5">
                    <div class="w-10 h-10 rounded-lg bg-sky-500/20 text-sky-400 flex items-center justify-center border border-sky-500/30 group-hover:bg-sky-500 group-hover:text-white transition-all duration-300 shadow-md">
                        <i class="fa-brands fa-telegram text-xl"></i>
                    </div>
                    <div class="text-left">
                        <p class="text-xs text-slate-400 font-medium leading-none mb-1">Telegram Messenger</p>
                        <p class="text-sm font-bold text-white tracking-wide">@gus_adad</p>
                    </div>
                </div>
                <div class="text-sky-400 group-hover:translate-x-1 transition-transform duration-300">
                    <i class="fa-solid fa-chevron-right text-xs"></i>
                </div>
            </a>

            <!-- Social Media Section -->
            <h3 class="text-xs font-bold uppercase tracking-widest text-slate-400 text-left pl-1 pt-3">Media Sosial & Portofolio</h3>

            <!-- Grid for Instagram & X -->
            <div class="grid grid-cols-2 gap-3 pb-6">
                <!-- Instagram -->
                <a href="https://www.instagram.com/gus_adad?igsh=MTRkajNvNmJvaGF6bw%3D%3D&utm_source=qr" 
                   target="_blank" 
                   class="glass-btn px-4 py-4 rounded-xl flex flex-col justify-between items-start group relative">
                    <div class="w-10 h-10 rounded-lg bg-pink-500/20 text-pink-400 flex items-center justify-center border border-pink-500/30 group-hover:bg-pink-500 group-hover:text-white transition-all duration-300 mb-3 shadow-md">
                        <i class="fa-brands fa-instagram text-lg"></i>
                    </div>
                    <div class="text-left">
                        <p class="text-[10px] text-slate-400 font-medium leading-none mb-1">Instagram</p>
                        <p class="text-xs font-bold text-white tracking-wide">@gus_adad</p>
                    </div>
                    <div class="absolute right-4 bottom-4 text-pink-400 group-hover:translate-x-1 transition-transform duration-300">
                        <i class="fa-solid fa-arrow-right text-[10px]"></i>
                    </div>
                </a>

                <!-- X (Twitter) -->
                <a href="https://x.com/gus_adadd?s=21" 
                   target="_blank" 
                   class="glass-btn px-4 py-4 rounded-xl flex flex-col justify-between items-start group relative">
                    <div class="w-10 h-10 rounded-lg bg-slate-300/20 text-white flex items-center justify-center border border-white/20 group-hover:bg-white group-hover:text-black transition-all duration-300 mb-3 shadow-md">
                        <i class="fa-brands fa-x-twitter text-lg"></i>
                    </div>
                    <div class="text-left">
                        <p class="text-[10px] text-slate-400 font-medium leading-none mb-1">X Platform</p>
                        <p class="text-xs font-bold text-white tracking-wide">@gus_adadd</p>
                    </div>
                    <div class="absolute right-4 bottom-4 text-slate-300 group-hover:translate-x-1 transition-transform duration-300">
                        <i class="fa-solid fa-arrow-right text-[10px]"></i>
                    </div>
                </a>
            </div>
        </div>

        <!-- Toast Notification Box -->
        <div id="toast" class="fixed bottom-6 left-1/2 transform -translate-x-1/2 scale-90 opacity-0 pointer-events-none transition-all duration-300 bg-emerald-500/90 text-white font-medium text-xs px-5 py-3 rounded-full shadow-xl flex items-center gap-2 backdrop-blur-md border border-emerald-400/30 z-50">
            <i class="fa-regular fa-circle-check text-sm"></i>
            <span>Alamat berhasil disalin ke papan klip!</span>
        </div>

        <!-- Footer -->
        <div class="mt-8 text-center text-[11px] text-slate-500 tracking-wider relative z-10">
            <p>© 2026 PT. Rifan Financindo Berjangka</p>
            <p class="mt-1">Designed with Apple Liquid Glass Style</p>
        </div>

    </div>

    <!-- Interactive Script logic -->
    <script>
        const cardContainer = document.getElementById('cardContainer');
        const cardInner = document.getElementById('cardInner');
        const copyBtn = document.getElementById('copyAddressBtn');

        // Penanganan Error Gambar Cadangan
        function handleImageError(img) {
            img.style.display = 'none'; // Sembunyikan tag img yang rusak
            const container = document.getElementById('logoContainer');
            // Ganti isi wadah dengan logo grafik default yang indah
            container.className = "w-10 h-10 rounded-xl bg-gradient-to-br from-blue-500 to-indigo-600 flex items-center justify-center shadow-md border border-white/10";
            container.innerHTML = '<i class="fa-solid fa-chart-line text-white text-lg"></i>';
        }

        // Fungsi pembalik kartu yang konsisten
        function toggleFlip() {
            cardInner.classList.toggle('flipped');
        }

        // Penanganan klik untuk desktop
        cardContainer.addEventListener('click', function(e) {
            if (e.target.closest('#copyAddressBtn')) return;
            toggleFlip();
        });

        // Penanganan sentuh untuk mobile (Mencegah pergeseran tata letak)
        let touchStartX = 0;
        let touchStartY = 0;
        
        cardContainer.addEventListener('touchstart', function(e) {
            touchStartX = e.touches[0].screenX;
            touchStartY = e.touches[0].screenY;
        }, { passive: true });

        cardContainer.addEventListener('touchend', function(e) {
            const touchEndX = e.changedTouches[0].screenX;
            const touchEndY = e.changedTouches[0].screenY;
            
            // Evaluasi apakah itu sentuhan murni atau gerakan geser scroll layar
            const isTap = Math.abs(touchEndX - touchStartX) < 10 && Math.abs(touchEndY - touchStartY) < 10;
            
            if (isTap) {
                if (e.target.closest('#copyAddressBtn')) return;
                toggleFlip();
                e.preventDefault();
            }
        }, { passive: false });

        // Menyalin alamat tanpa mengganggu letak elemen
        copyBtn.addEventListener('click', function(e) {
            e.stopPropagation();
            e.preventDefault();
            
            const addressText = "PT. Rifan Financindo Berjangka, AXA Tower Lt. 25, Jl. Prof. DR. Satrio Kav. 18, Lantai 30, 35, 23 dan 25, Kuningan, Setiabudi, Jakarta Selatan, DKI Jakarta 12940";
            
            // Solusi clipboard andal
            const tempInput = document.createElement("textarea");
            tempInput.value = addressText;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand("copy");
            document.body.removeChild(tempInput);

            const copyIcon = document.getElementById('copyIcon');
            const copyText = document.getElementById('copyText');
            
            copyIcon.className = "fa-solid fa-check text-emerald-400 animate-bounce";
            copyText.textContent = "Tersalin!";
            copyText.classList.add("text-emerald-400");

            const toast = document.getElementById('toast');
            toast.classList.remove('opacity-0', 'scale-90', 'pointer-events-none');
            toast.classList.add('opacity-100', 'scale-100');

            setTimeout(() => {
                copyIcon.className = "fa-regular fa-copy";
                copyText.textContent = "Salin Alamat";
                copyText.classList.remove("text-emerald-400");
                
                toast.classList.add('opacity-0', 'scale-90', 'pointer-events-none');
                toast.classList.remove('opacity-100', 'scale-100');
            }, 2500);
        });

        copyBtn.addEventListener('touchend', function(e) {
            e.stopPropagation();
        }, { passive: true });

        // Efek Paralaks 3D Gerakan Mouse (Hanya aktif di Desktop)
        cardContainer.addEventListener('mousemove', (e) => {
            if (window.innerWidth < 768) return;
            
            const rect = cardContainer.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            const xRotation = -((y - rect.height / 2) / rect.height) * 12;
            const yRotation = ((x - rect.width / 2) / rect.width) * 12;
            
            if(!cardInner.classList.contains('flipped')) {
                cardInner.style.transform = `rotateX(${xRotation}deg) rotateY(${yRotation}deg) scale3d(1.02, 1.02, 1.02)`;
            }
        });

        cardContainer.addEventListener('mouseleave', () => {
            if(!cardInner.classList.contains('flipped')) {
                cardInner.style.transform = `rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)`;
            } else {
                cardInner.style.transform = `rotateY(180deg)`;
            }
        });
    </script>
</body>
</html>

