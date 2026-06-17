<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bloopy - Mystery Dumpling</title>
    <!-- Tailwind CSS para estilização rápida -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts para tipografia divertida -->
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;700&display=swap" rel="stylesheet">
    <!-- FontAwesome para ícones -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        bloopy: {
                            blue: '#48d1cc',    /* Azul principal da caixa */
                            purple: '#9370db',  /* Roxo do topo */
                            green: '#3cb371',   /* Verde do topo */
                            yellow: '#ffeb3b',  /* Amarelo vibrante */
                            pink: '#ffb6c1',    /* Rosa do dumpling base */
                            dark: '#2c3e50',    /* Cor de texto escura */
                            orange: '#ff9800'   /* Laranja para detalhes */
                        }
                    },
                    fontFamily: {
                        display: ['"Fredoka One"', 'cursive'],
                        body: ['"Nunito"', 'sans-serif'],
                    },
                    backgroundImage: {
                        'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
                        'gradient-bloop': 'linear-gradient(135deg, #48d1cc 0%, #9370db 100%)',
                    },
                    animation: {
                        'bounce-slow': 'bounce 3s infinite',
                        'wiggle': 'wiggle 2s ease-in-out infinite',
                        'float': 'float 4s ease-in-out infinite',
                    },
                    keyframes: {
                        wiggle: {
                            '0%, 100%': { transform: 'rotate(-3deg)' },
                            '50%': { transform: 'rotate(3deg)' },
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-15px)' },
                        }
                    }
                }
            }
        }
    </script>
    
    <style>
        /* Estilos adicionais e scrollbar customizada */
        body {
            background-color: #e0f7fa;
            background-image: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.4) 10%, transparent 10.1%),
                              radial-gradient(circle at 15% 15%, rgba(255, 255, 255, 0.3) 10%, transparent 10.1%),
                              radial-gradient(circle at 85% 85%, rgba(255, 255, 255, 0.3) 10%, transparent 10.1%);
            background-size: 60px 60px, 100px 100px, 80px 80px;
            background-attachment: fixed; /* Adicionado para não desconfigurar no scroll */
            overflow-x: hidden;
        }

        /* Ocultar barra de rolagem padrão para o carrossel, mas permitir rolagem */
        .hide-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .hide-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }

        .blob-shape {
            border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
            transition: all 0.5s ease;
        }
        
        .blob-shape:hover {
            border-radius: 50%;
            transform: scale(1.05);
        }

        .text-shadow-sm {
            text-shadow: 2px 2px 0px rgba(0,0,0,0.2);
        }
        .text-shadow-md {
            text-shadow: 3px 3px 0px rgba(0,0,0,0.2), -1px -1px 0px #fff;
        }
        .text-outline {
            -webkit-text-stroke: 2px white;
        }

        /* Estilo para vídeos curtos simulados */
        .tiktok-frame {
            border-radius: 1rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            position: relative;
            background: #000;
            aspect-ratio: 9/16;
            width: 280px;
            flex-shrink: 0;
            scroll-snap-align: center;
        }
        
        .carousel-container {
            scroll-snap-type: x mandatory;
            -webkit-overflow-scrolling: touch;
        }
    </style>
</head>

<body class="font-body text-bloopy-dark antialiased">

    <!-- Navegação -->
    <nav class="fixed w-full z-50 transition-all duration-300 py-2" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <div class="flex-shrink-0 flex items-center">
                    <span class="font-display text-3xl text-white text-shadow-sm tracking-wider" style="-webkit-text-stroke: 1px #2c3e50;">Bloopy</span>
                </div>
                <div class="hidden md:flex space-x-8">
                    <a href="#home" class="text-white font-bold text-lg hover:text-bloopy-yellow transition-colors drop-shadow-md">Home</a>
                    <a href="#sobre" class="text-white font-bold text-lg hover:text-bloopy-yellow transition-colors drop-shadow-md">O que é?</a>
                    <a href="#colecione" class="text-white font-bold text-lg hover:text-bloopy-yellow transition-colors drop-shadow-md">Colecione</a>
                    <a href="#viral" class="text-white font-bold text-lg hover:text-bloopy-yellow transition-colors drop-shadow-md">Vídeos Virais</a>
                </div>
                <div class="hidden md:flex">
                    <a href="#comprar" class="bg-bloopy-yellow text-bloopy-dark font-display py-2 px-6 rounded-full hover:bg-white hover:text-bloopy-purple transition-all transform hover:scale-105 shadow-lg border-2 border-white">
                        Comprar Agora!
                    </a>
                </div>
                <!-- Mobile menu button -->
                <div class="md:hidden flex items-center">
                    <button id="mobile-menu-btn" class="text-white hover:text-bloopy-yellow focus:outline-none">
                        <i class="fas fa-bars text-2xl drop-shadow-md"></i>
                    </button>
                </div>
            </div>
        </div>
        <!-- Mobile Menu (hidden by default) -->
        <div id="mobile-menu" class="hidden md:hidden bg-bloopy-blue bg-opacity-95 shadow-lg">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3 text-center">
                <a href="#home" class="block px-3 py-2 text-white font-bold hover:bg-bloopy-purple rounded-md">Home</a>
                <a href="#sobre" class="block px-3 py-2 text-white font-bold hover:bg-bloopy-purple rounded-md">O que é?</a>
                <a href="#colecione" class="block px-3 py-2 text-white font-bold hover:bg-bloopy-purple rounded-md">Colecione</a>
                <a href="#viral" class="block px-3 py-2 text-white font-bold hover:bg-bloopy-purple rounded-md">Vídeos Virais</a>
                <a href="#comprar" class="block px-3 py-2 text-bloopy-yellow font-display text-xl hover:bg-bloopy-purple rounded-md">Comprar Agora!</a>
            </div>
        </div>
    </nav>

    <!-- Seção Hero: Fluxo ajustado para não transbordar -->
    <section id="home" class="relative pt-36 pb-48 md:pt-48 md:pb-64 overflow-hidden bg-bloopy-blue">
        <!-- Elementos de fundo decorativos inspirados na caixa -->
        <div class="absolute top-20 left-10 w-32 h-32 bg-bloopy-pink rounded-full mix-blend-multiply filter blur-xl opacity-70 animate-float"></div>
        <div class="absolute bottom-40 right-10 w-48 h-48 bg-bloopy-yellow rounded-full mix-blend-multiply filter blur-xl opacity-70 animate-float" style="animation-delay: 2s;"></div>
        <div class="absolute top-1/2 right-1/4 w-40 h-40 bg-bloopy-purple rounded-full mix-blend-multiply filter blur-xl opacity-70 animate-float" style="animation-delay: 1s;"></div>
        <div class="absolute bottom-20 left-1/4 w-24 h-24 bg-bloopy-green rounded-full mix-blend-multiply filter blur-xl opacity-70 animate-float" style="animation-delay: 3s;"></div>

        <!-- Container principal -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="flex flex-col lg:flex-row items-center justify-between gap-16">
                
                <!-- Texto Hero -->
                <div class="lg:w-1/2 text-center lg:text-left">
                    <div class="inline-block bg-bloopy-yellow text-bloopy-dark font-bold px-4 py-1 rounded-full mb-4 shadow-md transform -rotate-2">
                        <i class="fas fa-star text-orange-500 mr-2"></i>Fun Squishy!
                    </div>
                    <h1 class="font-display text-5xl md:text-7xl lg:text-8xl text-white text-shadow-md mb-2 tracking-wide text-outline">
                        MYSTERY
                    </h1>
                    <h1 class="font-display text-4xl md:text-6xl text-bloopy-yellow text-shadow-md mb-6 transform -rotate-3 inline-block">
                        DUMPLING
                    </h1>
                    
                    <p class="text-xl md:text-2xl text-white font-bold mb-8 drop-shadow-lg max-w-lg mx-auto lg:mx-0">
                        Qual será a sua cor?? Aperte, estique e descubra o squishy mais divertido do momento!
                    </p>
                    
                    <div class="flex flex-col sm:flex-row justify-center lg:justify-start space-y-4 sm:space-y-0 sm:space-x-4">
                        <a href="#comprar" class="bg-white text-bloopy-purple font-display text-xl py-4 px-8 rounded-full shadow-xl hover:scale-105 hover:bg-bloopy-yellow hover:text-bloopy-dark transition-all flex items-center justify-center group border-4 border-bloopy-purple">
                            <i class="fas fa-shopping-cart mr-2 group-hover:animate-bounce"></i> Garantir o Meu
                        </a>
                        <a href="#viral" class="bg-transparent border-4 border-white text-white font-display text-xl py-4 px-8 rounded-full shadow-lg hover:bg-white hover:text-bloopy-blue transition-all flex items-center justify-center">
                            <i class="fas fa-play mr-2"></i> Ver Vídeos
                        </a>
                    </div>
                    
                    <div class="mt-8 flex items-center justify-center lg:justify-start space-x-2">
                        <span class="bg-bloopy-green text-white font-bold px-3 py-1 rounded-full text-sm shadow-sm border-2 border-white">+3 ANOS</span>
                        <span class="text-white font-bold drop-shadow-md">Contém 12 Unidades na caixa</span>
                    </div>
                </div>

                <!-- Imagem/Gráfico Hero -->
                <div class="lg:w-1/2 relative flex justify-center mt-12 lg:mt-0">
                    <!-- Simulação do Dumpling Principal (baseado na caixa) -->
                    <div class="relative w-64 h-64 md:w-80 md:h-80 lg:w-[400px] lg:h-[400px] animate-wiggle z-20">
                        <!-- Imagem do personagem do repositório (com fundo removido via CSS mix-blend-multiply) -->
                        <img src="01.png" alt="Bloopy Mystery Dumpling" onerror="this.onerror=null; this.src='https://placehold.co/400x400/ffe4e1/ff9800?text=01.png+não+encontrada'" class="w-full h-full object-contain mix-blend-multiply z-20 relative">
                        
                        <!-- Ponto de interrogação flutuante -->
                        <div class="absolute -top-10 -right-5 font-display text-6xl text-white text-shadow-md animate-bounce-slow transform rotate-12 z-30">
                            ?!
                        </div>
                    </div>
                    
                    <!-- Dumplings menores ao redor -->
                    <div class="absolute bottom-10 -left-10 w-24 h-24 bg-bloopy-yellow rounded-full shadow-lg border-4 border-white animate-float z-10 flex items-center justify-center">
                         <div class="flex space-x-2 mb-2"><div class="w-2 h-2 bg-gray-800 rounded-full"></div><div class="w-2 h-2 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="absolute top-20 -right-10 w-20 h-20 bg-bloopy-green rounded-full shadow-lg border-4 border-white animate-float z-10 flex items-center justify-center" style="animation-delay: 1.5s;">
                         <div class="flex space-x-2 mb-2"><div class="w-2 h-2 bg-gray-800 rounded-full"></div><div class="w-2 h-2 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="absolute -bottom-5 right-10 w-28 h-28 bg-gradient-to-br from-blue-400 to-purple-500 rounded-full shadow-lg border-4 border-white animate-float z-30 flex items-center justify-center" style="animation-delay: 0.5s;">
                         <div class="flex space-x-3 mb-2"><div class="w-2.5 h-2.5 bg-white rounded-full"></div><div class="w-2.5 h-2.5 bg-white rounded-full"></div></div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Onda separadora na base com translate para alinhar perfeitamente -->
        <div class="absolute bottom-0 left-0 w-full leading-none z-20 transform translate-y-1">
            <svg viewBox="0 0 1200 120" preserveAspectRatio="none" class="w-full h-16 md:h-32 text-white fill-current block">
                <path d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V120H0V95.8C59.71,118.08,130.83,123.63,200.2,112.3Z" opacity=".25"></path>
                <path d="M0,0V46.29c47.79,22.2,103.59,32.15,158,28,70.36-5.37,136.33-33.31,206.8-37.5C438.64,32.43,512.34,53.67,583,72.05c69.27,18,138.3,24.88,209.4,13.08,36.15-6,69.85-17.84,104.45-29.34C989.49,25,1113-14.29,1200,52.47V0Z" opacity=".5"></path>
                <path d="M0,0V15.81C13,36.92,27.64,56.86,47.69,72.05,99.41,111.27,165,111,224.58,91.58c31.15-10.15,60.09-26.07,89.67-39.8,40.92-19,84.73-46,130.83-49.67,36.26-2.85,70.9,9.42,98.6,31.56,31.77,25.39,62.32,62,103.63,73,40.44,10.79,81.35-6.69,119.13-24.28s75.16-39,116.92-43.05c59.73-5.85,113.28,22.88,168.9,38.84,30.2,8.66,59,6.17,87.09-7.5,22.43-10.89,48-26.93,60.65-49.24V0Z"></path>
            </svg>
        </div>
    </section>

    <section id="sobre" class="py-20 bg-white">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="font-display text-4xl md:text-5xl text-bloopy-purple mb-4">Aperte e Surpreenda-se!</h2>
                <div class="w-24 h-2 bg-bloopy-yellow mx-auto rounded-full"></div>
            </div>

            <div class="grid md:grid-cols-3 gap-10">
                <!-- Card 1 -->
                <div class="bg-blue-50 rounded-3xl p-8 text-center shadow-lg transform transition duration-300 hover:-translate-y-2 border-4 border-bloopy-blue blob-shape">
                    <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-inner">
                        <i class="fas fa-question text-4xl text-bloopy-blue"></i>
                    </div>
                    <h3 class="font-display text-2xl mb-3 text-bloopy-dark">Cores Misteriosas</h3>
                    <p class="font-bold text-gray-600">Por fora parece um Dumpling fofinho de massa... mas qual será a cor dele por dentro? É uma surpresa!</p>
                </div>

                <!-- Card 2 -->
                <div class="bg-pink-50 rounded-3xl p-8 text-center shadow-lg transform transition duration-300 hover:-translate-y-2 border-4 border-bloopy-pink blob-shape" style="animation-delay: 0.2s;">
                    <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-inner">
                        <i class="fas fa-hand-rock text-4xl text-bloopy-pink"></i>
                    </div>
                    <h3 class="font-display text-2xl mb-3 text-bloopy-dark">Super Squishy</h3>
                    <p class="font-bold text-gray-600">Aperte muito! Ele é super macio, estica e volta ao normal. A sensação tátil é incrível e relaxante.</p>
                </div>

                <!-- Card 3 -->
                <div class="bg-yellow-50 rounded-3xl p-8 text-center shadow-lg transform transition duration-300 hover:-translate-y-2 border-4 border-bloopy-yellow blob-shape" style="animation-delay: 0.4s;">
                    <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-6 shadow-inner">
                        <i class="fas fa-users text-4xl text-bloopy-orange"></i>
                    </div>
                    <h3 class="font-display text-2xl mb-3 text-bloopy-dark">Colecione Todos</h3>
                    <p class="font-bold text-gray-600">São várias cores para descobrir! Troque com os amigos e tente achar o raro dumpling dourado!</p>
                </div>
            </div>
            
            <!-- Imagens explicativas baseadas na caixa (Aperte) -->
            <div class="mt-20 flex flex-col md:flex-row justify-center items-center gap-8 bg-gray-50 p-8 rounded-[3rem] shadow-inner">
                <div class="text-center md:text-left md:w-1/2">
                    <h3 class="font-display text-3xl text-bloopy-green mb-4">Como funciona?</h3>
                    <p class="text-lg font-bold text-gray-700 mb-4">A magia acontece quando você aperta! A capa externa macia revela a verdadeira cor do seu Dumpling.</p>
                    <ul class="space-y-3 font-bold text-gray-600">
                        <li class="flex items-center"><i class="fas fa-check-circle text-bloopy-green mr-2"></i> 1. Abra a caixinha surpresa</li>
                        <li class="flex items-center"><i class="fas fa-check-circle text-bloopy-green mr-2"></i> 2. Pegue seu Dumpling macio</li>
                        <li class="flex items-center"><i class="fas fa-check-circle text-bloopy-green mr-2"></i> 3. <strong>APERTE COM VONTADE!</strong></li>
                        <li class="flex items-center"><i class="fas fa-check-circle text-bloopy-green mr-2"></i> 4. Descubra a cor que vai estourar!</li>
                    </ul>
                </div>
                
                <!-- Simulação dos ícones "Aperte" da caixa -->
                <div class="flex gap-4">
                    <div class="relative w-32 h-32 bg-white rounded-full shadow-lg border-4 border-bloopy-yellow flex items-center justify-center">
                        <div class="text-center">
                            <i class="far fa-smile text-3xl text-pink-300 mb-1"></i>
                            <p class="text-xs font-bold">Antes</p>
                        </div>
                    </div>
                    <i class="fas fa-arrow-right text-3xl text-bloopy-blue self-center animate-pulse"></i>
                    <div class="relative w-32 h-32 bg-white rounded-full shadow-lg border-4 border-bloopy-yellow flex items-center justify-center overflow-hidden">
                        <!-- Simulação do aperto -->
                        <div class="absolute bg-purple-400 w-20 h-20 rounded-full scale-110"></div>
                        <div class="absolute top-0 bottom-0 left-2 w-4 bg-gray-200 opacity-50 transform -skew-x-12"></div>
                        <div class="absolute top-0 bottom-0 right-2 w-4 bg-gray-200 opacity-50 transform skew-x-12"></div>
                        <p class="text-xs font-bold z-10 text-white bg-black bg-opacity-30 px-2 rounded mt-10">Apertado!</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="viral" class="py-20 bg-gradient-to-b from-bloopy-purple to-bloopy-blue overflow-hidden relative">
        <!-- Background elements -->
        <div class="absolute top-0 left-0 w-full h-full overflow-hidden z-0 opacity-20 pointer-events-none">
            <i class="fas fa-heart text-white text-6xl absolute top-10 left-10 transform -rotate-12"></i>
            <i class="fas fa-share text-white text-4xl absolute bottom-20 left-1/4 transform rotate-12"></i>
            <i class="fas fa-play text-white text-8xl absolute top-1/4 right-10 transform rotate-45"></i>
            <i class="fas fa-fire text-white text-5xl absolute bottom-10 right-1/3"></i>
        </div>

        <div class="max-w-7xl mx-auto px-4 relative z-10">
            <div class="text-center mb-12">
                <div class="inline-block bg-black text-white font-bold px-4 py-1 rounded-full mb-4 shadow-lg flex items-center justify-center mx-auto w-max">
                    <i class="fab fa-tiktok mr-2 text-[#ff0050]"></i> #MysteryDumpling
                </div>
                <h2 class="font-display text-4xl md:text-6xl text-white text-shadow-md mb-4 text-outline">Febre na Internet!</h2>
                <p class="text-xl text-white font-bold drop-shadow-md">Veja as reações de quem apertou pela primeira vez!</p>
            </div>

            <!-- Container do Carrossel -->
            <div class="relative">
                <!-- Botões de navegação (Visíveis em telas maiores) -->
                <button id="prevBtn" class="hidden md:flex absolute left-[-20px] top-1/2 transform -translate-y-1/2 w-12 h-12 bg-white rounded-full items-center justify-center shadow-xl text-bloopy-dark z-20 hover:bg-bloopy-yellow transition-colors border-2 border-gray-200">
                    <i class="fas fa-chevron-left text-xl"></i>
                </button>
                <button id="nextBtn" class="hidden md:flex absolute right-[-20px] top-1/2 transform -translate-y-1/2 w-12 h-12 bg-white rounded-full items-center justify-center shadow-xl text-bloopy-dark z-20 hover:bg-bloopy-yellow transition-colors border-2 border-gray-200">
                    <i class="fas fa-chevron-right text-xl"></i>
                </button>

                <!-- Track do Carrossel (Scroll horizontal) -->
                <div id="carousel-track" class="carousel-container flex space-x-6 overflow-x-auto py-8 px-4 hide-scrollbar snap-x">
                    
                    <!-- Vídeo Fake 1 -->
                    <div class="tiktok-frame snap-center group">
                        <!-- Imagem placeholder representando o thumbnail do video -->
                        <img src="https://placehold.co/300x533/ffb6c1/ffffff?text=Unboxing+Bloopy!" alt="Video Thumbnail" class="w-full h-full object-cover">
                        <!-- Overlay da interface de short video -->
                        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black opacity-80"></div>
                        <!-- Play Button (Aparece no hover) -->
                        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-black bg-opacity-30">
                            <i class="fas fa-play-circle text-6xl text-white opacity-80"></i>
                        </div>
                        <!-- UI Elements -->
                        <div class="absolute bottom-4 left-4 right-12 text-white">
                            <p class="font-bold text-sm">@bloopyfan_oficial</p>
                            <p class="text-xs mt-1 font-bold">Qual cor vcs acham que é? 😱 <span class="text-bloopy-yellow">#bloopy #mysterydumpling</span></p>
                        </div>
                        <!-- Lateral Actions -->
                        <div class="absolute bottom-4 right-2 flex flex-col space-y-4 items-center">
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-heart text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">124K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-comment-dots text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">1.2K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-share text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">5K</span>
                            </div>
                        </div>
                    </div>

                    <!-- Vídeo Fake 2 -->
                    <div class="tiktok-frame snap-center group">
                        <img src="https://placehold.co/300x533/48d1cc/ffffff?text=Olha+essa+Cor!!" alt="Video Thumbnail" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black opacity-80"></div>
                        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-black bg-opacity-30">
                            <i class="fas fa-play-circle text-6xl text-white opacity-80"></i>
                        </div>
                        <div class="absolute bottom-4 left-4 right-12 text-white">
                            <p class="font-bold text-sm">@toyreviewer</p>
                            <p class="text-xs mt-1 font-bold">Melhor fidget toy de 2024! 😍 Satisfatório demais. <span class="text-bloopy-yellow">#fidget #asmr</span></p>
                        </div>
                        <div class="absolute bottom-4 right-2 flex flex-col space-y-4 items-center">
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-heart text-red-500 text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">342K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-comment-dots text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">4.5K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-share text-white text-xl"></i>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Vídeo Fake 3 -->
                    <div class="tiktok-frame snap-center group">
                        <img src="https://placehold.co/300x533/9370db/ffffff?text=ASMR+Squishy" alt="Video Thumbnail" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black opacity-80"></div>
                        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-black bg-opacity-30">
                            <i class="fas fa-play-circle text-6xl text-white opacity-80"></i>
                        </div>
                        <div class="absolute bottom-4 left-4 right-12 text-white">
                            <p class="font-bold text-sm">@relaxing_times</p>
                            <p class="text-xs mt-1 font-bold">Achei o ROXO MÍSTICO!! 🔮🔮🔮 <span class="text-bloopy-yellow">#bloopy #raro</span></p>
                        </div>
                        <div class="absolute bottom-4 right-2 flex flex-col space-y-4 items-center">
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-heart text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">89K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-comment-dots text-white text-xl"></i>
                                </div>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-share text-white text-xl"></i>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Vídeo Fake 4 -->
                    <div class="tiktok-frame snap-center group">
                        <img src="https://placehold.co/300x533/ffeb3b/2c3e50?text=Minha+Colecao" alt="Video Thumbnail" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black opacity-80"></div>
                        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-black bg-opacity-30">
                            <i class="fas fa-play-circle text-6xl text-white opacity-80"></i>
                        </div>
                        <div class="absolute bottom-4 left-4 right-12 text-white">
                            <p class="font-bold text-sm">@kids_fun_br</p>
                            <p class="text-xs mt-1 font-bold">Comprei a caixa inteira! Vamos abrir todos! 🎁 <span class="text-bloopy-yellow">#unboxing</span></p>
                        </div>
                        <div class="absolute bottom-4 right-2 flex flex-col space-y-4 items-center">
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-heart text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">512K</span>
                            </div>
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-comment-dots text-white text-xl"></i>
                                </div>
                            </div>
                        </div>
                    </div>

                     <!-- Vídeo Fake 5 -->
                     <div class="tiktok-frame snap-center group">
                        <img src="https://placehold.co/300x533/3cb371/ffffff?text=Brincando+com+Bloopy" alt="Video Thumbnail" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-transparent to-black opacity-80"></div>
                        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-black bg-opacity-30">
                            <i class="fas fa-play-circle text-6xl text-white opacity-80"></i>
                        </div>
                        <div class="absolute bottom-4 left-4 right-12 text-white">
                            <p class="font-bold text-sm">@brincadeiras_legais</p>
                            <p class="text-xs mt-1 font-bold">Olha como estica! Verde alienígena! 👽💚</p>
                        </div>
                        <div class="absolute bottom-4 right-2 flex flex-col space-y-4 items-center">
                            <div class="text-center">
                                <div class="w-10 h-10 bg-white bg-opacity-20 rounded-full flex items-center justify-center mb-1 backdrop-blur-sm">
                                    <i class="fas fa-heart text-white text-xl"></i>
                                </div>
                                <span class="text-white text-xs font-bold">67K</span>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
            
            <div class="text-center mt-10">
                <p class="text-white font-bold mb-4">Arraste para o lado para ver mais <i class="fas fa-arrows-alt-h mx-2"></i></p>
                <a href="#" class="inline-block border-2 border-white text-white font-display px-6 py-2 rounded-full hover:bg-white hover:text-bloopy-blue transition-colors">
                    Siga a gente no TikTok @bloopy_br
                </a>
            </div>
        </div>
    </section>

    <section id="colecione" class="py-20 bg-[#e0f7fa]">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center mb-16">
                <img src="https://placehold.co/200x80/transparent/2c3e50?text=Bloopy&font=Montserrat" class="mx-auto h-16 object-contain mb-2" alt="Bloopy Logo">
                <h2 class="font-display text-4xl md:text-5xl text-bloopy-dark mb-2">Colecione Todos!</h2>
                <p class="text-xl font-bold text-gray-600">Encontre o Dumpling Escondido!</p>
            </div>

            <!-- Grid de Cores Baseado na arte da caixa -->
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-6 relative">
                
                <!-- Enfeite de background -->
                <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full h-1/2 bg-white rounded-[3rem] shadow-sm z-0"></div>

                <!-- Cor 1 (Amarelo) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer">
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-bloopy-yellow shadow-lg flex items-center justify-center border-4 border-white transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-gray-800 rounded-full"></div><div class="w-3 h-3 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-white px-4 py-1 rounded-full shadow text-sm font-bold text-gray-700 opacity-0 group-hover:opacity-100 transition-opacity">Raio de Sol</div>
                </div>

                <!-- Cor 2 (Rosa/Vermelho) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer mt-8">
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-pink-400 shadow-lg flex items-center justify-center border-4 border-white transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-gray-800 rounded-full"></div><div class="w-3 h-3 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-white px-4 py-1 rounded-full shadow text-sm font-bold text-gray-700 opacity-0 group-hover:opacity-100 transition-opacity">Morango</div>
                </div>

                <!-- Cor 3 (Azul claro) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer">
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-blue-300 shadow-lg flex items-center justify-center border-4 border-white transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-gray-800 rounded-full"></div><div class="w-3 h-3 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-white px-4 py-1 rounded-full shadow text-sm font-bold text-gray-700 opacity-0 group-hover:opacity-100 transition-opacity">Céu Azul</div>
                </div>

                <!-- Cor 4 (Roxo) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer mt-8">
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-bloopy-purple shadow-lg flex items-center justify-center border-4 border-white transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-gray-800 rounded-full"></div><div class="w-3 h-3 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-white px-4 py-1 rounded-full shadow text-sm font-bold text-gray-700 opacity-0 group-hover:opacity-100 transition-opacity">Uva Doce</div>
                </div>

                <!-- Cor 5 (Multicolor/Raro) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer">
                    <div class="absolute -top-3 -right-3 text-2xl animate-bounce">✨</div>
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-gradient-to-tr from-pink-500 via-purple-500 to-blue-500 shadow-lg flex items-center justify-center border-4 border-bloopy-yellow transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-white rounded-full"></div><div class="w-3 h-3 bg-white rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-bloopy-yellow px-4 py-1 rounded-full shadow text-sm font-bold text-bloopy-dark opacity-0 group-hover:opacity-100 transition-opacity border border-white">Galáxia (RARO!)</div>
                </div>

                <!-- Cor 6 (Verde) -->
                <div class="relative z-10 flex flex-col items-center group cursor-pointer mt-8">
                    <div class="w-24 h-24 md:w-32 md:h-32 rounded-full bg-bloopy-green shadow-lg flex items-center justify-center border-4 border-white transform transition-transform group-hover:scale-110 group-hover:-translate-y-2">
                        <div class="flex space-x-2"><div class="w-3 h-3 bg-gray-800 rounded-full"></div><div class="w-3 h-3 bg-gray-800 rounded-full"></div></div>
                    </div>
                    <div class="mt-4 bg-white px-4 py-1 rounded-full shadow text-sm font-bold text-gray-700 opacity-0 group-hover:opacity-100 transition-opacity">Maçã Verde</div>
                </div>
            </div>

            <div class="mt-16 bg-white p-8 rounded-3xl shadow-md border-2 border-blue-100 flex flex-col md:flex-row items-center justify-between">
                <div class="flex items-center mb-6 md:mb-0">
                    <div class="bg-blue-100 p-4 rounded-full mr-4">
                        <i class="fas fa-box-open text-3xl text-bloopy-blue"></i>
                    </div>
                    <div>
                        <h4 class="font-display text-2xl text-bloopy-dark">A Caixa Display</h4>
                        <p class="font-bold text-gray-600">Contém 12 unidades sortidas.</p>
                    </div>
                </div>
                <a href="#comprar" class="bg-bloopy-green text-white font-display text-xl py-3 px-8 rounded-full shadow-lg hover:scale-105 hover:bg-green-500 transition-all text-center">
                    Comprar Caixa Fechada
                </a>
            </div>
        </div>
    </section>

    <!-- Seção de Compra / Call to Action Final -->
    <section id="comprar" class="py-24 bg-bloopy-yellow relative overflow-hidden">
        <!-- SVG Wave Top -->
        <div class="absolute top-0 w-full leading-none z-10 rotate-180">
            <svg viewBox="0 0 1200 120" preserveAspectRatio="none" class="w-full h-12 text-[#e0f7fa] fill-current">
                <path d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V120H0V95.8C59.71,118.08,130.83,123.63,200.2,112.3Z"></path>
            </svg>
        </div>

        <div class="max-w-4xl mx-auto px-4 relative z-20 text-center">
            <h2 class="font-display text-5xl md:text-6xl text-bloopy-dark mb-6 text-shadow-sm">Qual será a sua cor?</h2>
            <p class="text-2xl font-bold text-gray-800 mb-10">Não fique de fora dessa febre. Garanta o seu Mystery Dumpling hoje mesmo!</p>
            
            <div class="flex flex-col md:flex-row justify-center gap-6">
                <button onclick="showMessage('Adicionado ao carrinho!')" class="bg-bloopy-purple text-white font-display text-2xl py-4 px-10 rounded-full shadow-xl hover:scale-105 transition-transform border-4 border-white flex items-center justify-center">
                    <i class="fas fa-shopping-bag mr-3"></i> Comprar 1 Unidade
                </button>
                <button onclick="showMessage('Caixa (12 un) adicionada ao carrinho!')" class="bg-white text-bloopy-dark font-display text-2xl py-4 px-10 rounded-full shadow-xl hover:scale-105 transition-transform border-4 border-bloopy-purple flex items-center justify-center">
                    <i class="fas fa-box mr-3"></i> Levar a Caixa (12 un)
                </button>
            </div>
            <p class="mt-6 text-sm font-bold text-gray-700">*Indicado para crianças maiores de 3 anos (+3)</p>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-bloopy-dark text-white py-10">
        <div class="max-w-7xl mx-auto px-4 grid grid-cols-1 md:grid-cols-3 gap-8 text-center md:text-left">
            <div>
                <h3 class="font-display text-3xl mb-4 text-bloopy-yellow">Bloopy</h3>
                <p class="text-gray-400 font-bold mb-4">Fun Squishy. Fabricando sorrisos e diversão misteriosa.</p>
                <div class="flex space-x-4 justify-center md:justify-start">
                    <a href="#" class="w-10 h-10 rounded-full bg-gray-700 flex items-center justify-center hover:bg-bloopy-yellow hover:text-bloopy-dark transition-colors"><i class="fab fa-instagram"></i></a>
                    <a href="#" class="w-10 h-10 rounded-full bg-gray-700 flex items-center justify-center hover:bg-bloopy-yellow hover:text-bloopy-dark transition-colors"><i class="fab fa-tiktok"></i></a>
                    <a href="#" class="w-10 h-10 rounded-full bg-gray-700 flex items-center justify-center hover:bg-bloopy-yellow hover:text-bloopy-dark transition-colors"><i class="fab fa-youtube"></i></a>
                </div>
            </div>
            <div>
                <h4 class="font-bold text-xl mb-4 text-white">Links Rápidos</h4>
                <ul class="space-y-2 text-gray-400 font-bold">
                    <li><a href="#home" class="hover:text-bloopy-yellow">Home</a></li>
                    <li><a href="#sobre" class="hover:text-bloopy-yellow">Como Funciona</a></li>
                    <li><a href="#colecione" class="hover:text-bloopy-yellow">Coleção</a></li>
                    <li><a href="#" class="hover:text-bloopy-yellow">Atendimento ao Cliente</a></li>
                </ul>
            </div>
            <div>
                <h4 class="font-bold text-xl mb-4 text-white">Segurança</h4>
                <div class="flex items-center justify-center md:justify-start space-x-4 mb-4">
                    <div class="w-12 h-12 bg-white rounded flex items-center justify-center text-bloopy-dark font-bold border-2 border-red-500">
                        <span class="text-red-500 line-through mr-1 text-sm">0-3</span>
                    </div>
                    <p class="text-gray-400 text-sm font-bold text-left">
                        ATENÇÃO! Não recomendável para crianças menores de 3 anos por conter partes pequenas que podem ser engolidas.
                    </p>
                </div>
            </div>
        </div>
        <div class="text-center text-gray-500 text-sm mt-10 font-bold border-t border-gray-700 pt-6">
            &copy; 2024 Bloopy Fun Squishy. Todos os direitos reservados.
        </div>
    </footer>

    <!-- Caixa de Mensagem Customizada (Substitui alert) -->
    <div id="messageBox" class="fixed bottom-5 right-5 transform translate-y-20 opacity-0 bg-white border-l-4 border-bloopy-green rounded shadow-lg p-4 transition-all duration-300 z-50 flex items-center">
        <i class="fas fa-check-circle text-bloopy-green text-2xl mr-3"></i>
        <p id="messageText" class="font-bold text-gray-800"></p>
    </div>

    <!-- Scripts -->
    <script>
        // Função para mostrar mensagens (evitando alert)
        function showMessage(text) {
            const msgBox = document.getElementById('messageBox');
            const msgText = document.getElementById('messageText');
            
            msgText.innerText = text;
            
            // Show
            msgBox.classList.remove('translate-y-20', 'opacity-0');
            
            // Hide after 3 seconds
            setTimeout(() => {
                msgBox.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        // Lógica do Menu Mobile
        const btn = document.getElementById('mobile-menu-btn');
        const menu = document.getElementById('mobile-menu');

        btn.addEventListener('click', () => {
            menu.classList.toggle('hidden');
        });

        // Fechar menu mobile ao clicar num link
        const mobileLinks = menu.querySelectorAll('a');
        mobileLinks.forEach(link => {
            link.addEventListener('click', () => {
                menu.classList.add('hidden');
            });
        });

        // Efeito de Navbar ao rolar a página
        window.addEventListener('scroll', () => {
            const nav = document.getElementById('navbar');
            if (window.scrollY > 50) {
                nav.classList.add('bg-bloopy-blue', 'bg-opacity-95', 'shadow-md');
                nav.classList.remove('py-2');
            } else {
                nav.classList.remove('bg-bloopy-blue', 'bg-opacity-95', 'shadow-md');
                nav.classList.add('py-2');
            }
        });

        // Lógica do Carrossel de Vídeos
        const track = document.getElementById('carousel-track');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');

        if(track && prevBtn && nextBtn) {
            // Avança um card (largura do card + gap)
            const scrollAmount = 300 + 24; 

            nextBtn.addEventListener('click', () => {
                track.scrollBy({ left: scrollAmount, behavior: 'smooth' });
            });

            prevBtn.addEventListener('click', () => {
                track.scrollBy({ left: -scrollAmount, behavior: 'smooth' });
            });
        }
    </script>
</body>
</html>
