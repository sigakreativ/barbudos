<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Barbudos Club - Barbearia Premium</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: Arial, sans-serif;
            background-color: #000;
            color: #fff;
        }
        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>
    <!-- Tela de Login -->
    <div id="loginScreen" class="min-h-screen bg-black flex items-center justify-center p-6">
        <div class="w-full max-w-md">
            <!-- Logo -->
            <div class="mb-16 text-center">
                <h1 class="text-6xl font-black text-white tracking-wider mb-2">BARBUDOS</h1>
                <h2 class="text-4xl font-light text-yellow-500 tracking-widest">CLUB</h2>
            </div>

            <!-- Bem-vindo -->
            <h3 class="text-white text-3xl font-light text-center mb-12 tracking-widest">BEM-VINDO</h3>

            <!-- Formulário -->
            <div class="space-y-6 mb-8">
                <input
                    type="text"
                    id="loginName"
                    placeholder="Nome Completo"
                    class="w-full bg-white text-gray-800 rounded-full px-6 py-4 focus:outline-none focus:ring-2 focus:ring-yellow-500 transition placeholder-gray-400"
                />
                <input
                    type="tel"
                    id="loginPhone"
                    placeholder="Whatsapp"
                    class="w-full bg-white text-gray-800 rounded-full px-6 py-4 focus:outline-none focus:ring-2 focus:ring-yellow-500 transition placeholder-gray-400"
                />
            </div>

            <!-- Botões -->
            <div class="space-y-4">
                <button
                    onclick="handleLogin()"
                    class="w-full bg-yellow-500 text-black font-light text-lg py-4 rounded-full hover:bg-yellow-400 transition tracking-widest"
                >
                    ENTRAR
                </button>
                <button class="w-full bg-transparent text-white font-light text-lg py-4 rounded-full border-2 border-white hover:bg-white hover:text-black transition tracking-widest">
                    CADASTRAR
                </button>
            </div>
        </div>
    </div>

    <!-- Tela Principal -->
    <div id="mainScreen" class="hidden min-h-screen bg-black pb-20">
        <!-- Content -->
        <div class="p-4 pt-6">
            <!-- Tela Home -->
            <div id="homeScreen">
                <!-- Header com saldo -->
                <div class="bg-gray-900 rounded-2xl p-6 border border-yellow-500 border-opacity-20 mb-6">
                    <div class="flex items-center justify-between mb-4">
                        <div>
                            <p class="text-yellow-500 text-sm mb-1">Bem-vindo</p>
                            <h2 class="text-white text-2xl font-bold" id="welcomeName">Cliente</h2>
                        </div>
                        <button class="text-yellow-500">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                            </svg>
                        </button>
                    </div>
                    <div class="bg-black rounded-xl p-4 flex items-center justify-between border border-yellow-500 border-opacity-20">
                        <div>
                            <p class="text-gray-400 text-xs mb-1">Saldo Carteira</p>
                            <p class="text-yellow-500 text-2xl font-bold" id="walletBalance">R$ 0,00</p>
                        </div>
                        <button class="bg-yellow-500 text-black px-4 py-2 rounded-lg text-sm font-bold hover:bg-yellow-400 transition">
                            RECARREGAR
                        </button>
                    </div>
                </div>

                <!-- Tabs -->
                <div class="flex gap-3 mb-6">
                    <button class="bg-yellow-500 text-black px-6 py-2 rounded-full font-bold text-sm">SERVIÇOS</button>
                    <button class="bg-gray-900 text-white px-6 py-2 rounded-full font-semibold text-sm border border-yellow-500 border-opacity-20">BARBEIROS</button>
                    <button class="bg-gray-900 text-white px-6 py-2 rounded-full font-semibold text-sm border border-yellow-500 border-opacity-20">PROMOÇÕES</button>
                </div>

                <!-- Lista de Serviços -->
                <div id="servicesList" class="space-y-3"></div>
            </div>

            <!-- Tela de Agendamento -->
            <div id="bookingScreen" class="hidden"></div>

            <!-- Tela de Fidelidade -->
            <div id="loyaltyScreen" class="hidden">
                <div class="flex items-center justify-between mb-6">
                    <h2 class="text-2xl font-bold text-white">Fidelidade</h2>
                </div>

                <div class="bg-yellow-500 rounded-2xl p-6 mb-6">
                    <div class="flex items-center justify-between">
                        <div>
                            <p class="text-black text-sm font-semibold mb-1">Seus Pontos</p>
                            <p class="text-black text-5xl font-bold" id="loyaltyPoints">0</p>
                        </div>
                        <svg class="w-20 h-20 text-black opacity-20" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z"></path>
                        </svg>
                    </div>
                    <div class="mt-4 bg-black bg-opacity-20 rounded-lg p-3">
                        <p class="text-black text-sm" id="loyaltyMessage">Faltam 10 pontos para ganhar um corte grátis!</p>
                    </div>
                </div>

                <button id="redeemButton" class="hidden w-full bg-yellow-500 text-black py-4 rounded-lg font-bold text-lg hover:bg-yellow-400 transition mb-6" onclick="redeemReward()">
                    Resgatar Corte Grátis
                </button>

                <div class="bg-gray-900 rounded-xl p-6 border border-yellow-500 border-opacity-20">
                    <h3 class="font-bold text-white mb-3">Como funciona?</h3>
                    <ul class="space-y-2 text-gray-300">
                        <li>✓ Ganhe 1 ponto a cada serviço realizado</li>
                        <li>✓ Acumule 10 pontos</li>
                        <li>✓ Troque por 1 corte grátis</li>
                        <li>✓ Sem prazo de validade</li>
                    </ul>
                </div>
            </div>

            <!-- Tela de Perfil -->
            <div id="profileScreen" class="hidden">
                <div class="flex items-center justify-between mb-6">
                    <h2 class="text-2xl font-bold text-white">Meu Perfil</h2>
                </div>
                
                <div class="bg-gray-900 rounded-xl p-6 mb-6 border border-yellow-500 border-opacity-20">
                    <div class="flex items-center gap-4 mb-4">
                        <div class="w-20 h-20 bg-yellow-500 rounded-full flex items-center justify-center text-4xl">👤</div>
                        <div>
                            <p class="text-white font-bold text-xl" id="profileName">Cliente</p>
                            <p class="text-gray-400" id="profilePhone">Não informado</p>
                        </div>
                    </div>
                </div>

                <div class="space-y-4">
                    <div class="bg-gray-900 rounded-xl p-4 flex items-center justify-between border border-yellow-500 border-opacity-20">
                        <div class="flex items-center gap-3">
                            <svg class="w-6 h-6 text-yellow-500" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z"></path>
                            </svg>
                            <span class="text-white">Pontos de Fidelidade</span>
                        </div>
                        <span class="text-yellow-500 font-bold" id="profilePoints">0</span>
                    </div>

                    <div class="bg-gray-900 rounded-xl p-4 flex items-center justify-between border border-yellow-500 border-opacity-20">
                        <div class="flex items-center gap-3">
                            <svg class="w-6 h-6 text-yellow-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.121 14.121L19 19m-7-7l7-7m-7 7l-2.879 2.879M12 12L9.121 9.121m0 5.758a3 3 0 10-4.243 4.243 3 3 0 004.243-4.243zm0-5.758a3 3 0 10-4.243-4.243 3 3 0 004.243 4.243z"></path>
                            </svg>
                            <span class="text-white">Serviços Realizados</span>
                        </div>
                        <span class="text-yellow-500 font-bold" id="profileServices">0</span>
                    </div>

                    <div class="bg-gray-900 rounded-xl p-4 flex items-center justify-between border border-yellow-500 border-opacity-20">
                        <div class="flex items-center gap-3">
                            <svg class="w-6 h-6 text-yellow-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                            <span class="text-white">Saldo Carteira</span>
                        </div>
                        <span class="text-yellow-500 font-bold" id="profileWallet">R$ 0,00</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Bottom Navigation -->
        <div class="fixed bottom-0 left-0 right-0 bg-gray-900 border-t border-yellow-500 border-opacity-30 flex justify-around p-3">
            <button onclick="showScreen('home')" id="navHome" class="flex flex-col items-center gap-1 text-yellow-500">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                </svg>
                <span class="text-xs">Home</span>
            </button>
            
            <button onclick="showScreen('booking')" id="navBooking" class="flex flex-col items-center gap-1 text-gray-400">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                </svg>
                <span class="text-xs">Agendar</span>
            </button>
            
            <button onclick="showScreen('loyalty')" id="navLoyalty" class="flex flex-col items-center gap-1 text-gray-400">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z"></path>
                </svg>
                <span class="text-xs">Fidelidade</span>
            </button>
            
            <button onclick="showScreen('profile')" id="navProfile" class="flex flex-col items-center gap-1 text-gray-400">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                </svg>
                <span class="text-xs">Perfil</span>
            </button>
        </div>
    </div>

    <script>
        // Estado da aplicação
        let appState = {
            userName: '',
            userPhone: '',
            walletBalance: 0,
            loyaltyPoints: 0,
            bookingHistory: [],
            selectedService: null,
            selectedBarber: null,
            selectedDate: '',
            selectedTime: ''
        };

        // Dados
        const services = [
            { id: 1, name: 'Corte Masculino', price: 45, duration: 40, description: 'Corte completo com finalização', icon: '✂️' },
            { id: 2, name: 'Barba', price: 35, duration: 30, description: 'Aparar e modelar barba', icon: '🪒' },
            { id: 3, name: 'Sobrancelha', price: 15, duration: 15, description: 'Design e limpeza', icon: '✨' },
            { id: 4, name: 'Combo Corte + Barba', price: 70, duration: 60, description: 'Pacote completo', icon: '💈' },
            { id: 5, name: 'Hidratação', price: 25, duration: 20, description: 'Tratamento capilar', icon: '💧' }
        ];

        const barber = {
            id: 1,
            name: 'Yuri Barboza',
            photo: '👨🏻',
            specialties: 'Especialista em cortes modernos, barba e degradê',
            experience: '10 anos',
            rating: 5.0
        };

        const availableTimes = ['09:00', '11:30', '13:00', '13:30', '15:00', '16:00', '18:30', '20:00', '20:30'];

        // Funções
        function handleLogin() {
            const name = document.getElementById('loginName').value;
            const phone = document.getElementById('loginPhone').value;
            
            if (name && phone) {
                appState.userName = name;
                appState.userPhone = phone;
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('mainScreen').classList.remove('hidden');
                updateUI();
                renderServices();
            }
        }

        function updateUI() {
            document.getElementById('welcomeName').textContent = appState.userName.split(' ')[0] + '!';
            document.getElementById('walletBalance').textContent = 'R$ ' + appState.walletBalance.toFixed(2);
            document.getElementById('loyaltyPoints').textContent = appState.loyaltyPoints;
            document.getElementById('profileName').textContent = appState.userName;
            document.getElementById('profilePhone').textContent = appState.userPhone;
            document.getElementById('profilePoints').textContent = appState.loyaltyPoints;
            document.getElementById('profileServices').textContent = appState.bookingHistory.length;
            document.getElementById('profileWallet').textContent = 'R$ ' + appState.walletBalance.toFixed(2);
            
            const remaining = Math.max(0, 10 - appState.loyaltyPoints);
            document.getElementById('loyaltyMessage').textContent = 
                remaining > 0 ? `Faltam ${remaining} pontos para ganhar um corte grátis!` : 'Você pode resgatar um corte grátis!';
            
            if (appState.loyaltyPoints >= 10) {
                document.getElementById('redeemButton').classList.remove('hidden');
            } else {
                document.getElementById('redeemButton').classList.add('hidden');
            }
        }

        function renderServices() {
            const container = document.getElementById('servicesList');
            container.innerHTML = services.map(service => `
                <div onclick="selectService(${service.id})" class="bg-gray-900 rounded-xl p-4 flex items-center justify-between hover:bg-gray-800 transition cursor-pointer border border-yellow-500 border-opacity-20">
                    <div class="flex items-center gap-4">
                        <div class="bg-yellow-500 bg-opacity-20 w-12 h-12 rounded-lg flex items-center justify-center text-2xl border border-yellow-500 border-opacity-30">
                            ${service.icon}
                        </div>
                        <div>
                            <h3 class="text-white font-bold">${service.name}</h3>
                            <p class="text-gray-400 text-sm">${service.description}</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-3">
                        <span class="text-yellow-500 font-bold text-lg">R$ ${service.price}</span>
                        <button class="bg-yellow-500 hover:bg-yellow-400 w-8 h-8 rounded-full flex items-center justify-center transition">
                            <svg class="w-5 h-5 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
                            </svg>
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function selectService(serviceId) {
            appState.selectedService = services.find(s => s.id === serviceId);
            appState.selectedBarber = barber;
            showBookingScreen();
        }

        function showBookingScreen() {
            const container = document.getElementById('bookingScreen');
            container.innerHTML = `
                <div class="flex items-center justify-between mb-6">
                    <h2 class="text-2xl font-bold text-white">Agendar Horário</h2>
                </div>

                <div class="bg-gray-900 rounded-xl p-4 mb-6 border border-yellow-500 border-opacity-20">
                    <div class="flex items-center gap-4">
                        <div class="text-5xl">${barber.photo}</div>
                        <div class="flex-1">
                            <h3 class="font-bold text-white text-lg">${barber.name}</h3>
                            <p class="text-gray-400 text-sm">${barber.specialties}</p>
                            <div class="flex items-center gap-2 mt-1">
                                <span class="text-yellow-500">⭐</span>
                                <span class="text-yellow-500 text-sm">${barber.rating}</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="bg-gray-900 rounded-xl p-4 mb-6 border border-yellow-500 border-opacity-20">
                    <h3 class="font-bold text-white mb-2">Serviço Selecionado</h3>
                    <div class="flex justify-between items-center">
                        <div>
                            <p class="text-white">${appState.selectedService.name}</p>
                            <p class="text-gray-400 text-sm">${appState.selectedService.duration} minutos</p>
                        </div>
                        <p class="text-yellow-500 font-bold text-xl">R$ ${appState.selectedService.price}</p>
                    </div>
                </div>

                <div class="mb-6">
                    <label class="block text-white mb-2 font-semibold">Data</label>
                    <input type="date" id="bookingDate" class="w-full bg-gray-900 text-white p-3 rounded-lg border border-yellow-500 border-opacity-20" min="${new Date().toISOString().split('T')[0]}" onchange="updateTimeSlots()">
                </div>

                <div id="timeSlotsContainer" class="hidden mb-6">
                    <label class="block text-white mb-2 font-semibold">Horário</label>
                    <div class="grid grid-cols-3 gap-3" id="timeSlots"></div>
                </div>

                <button onclick="confirmBooking()" id="confirmButton" class="hidden w-full bg-yellow-500 text-black py-4 rounded-lg font-bold text-lg hover:bg-yellow-400 transition">
                    Confirmar via WhatsApp
                </button>
            `;
            showScreen('booking');
        }

        function updateTimeSlots() {
            const date = document.getElementById('bookingDate').value;
            if (date) {
                appState.selectedDate = date;
                const container = document.getElementById('timeSlotsContainer');
                const slotsContainer = document.getElementById('timeSlots');
                container.classList.remove('hidden');
                
                slotsContainer.innerHTML = availableTimes.map(time => `
                    <button onclick="selectTime('${time}')" class="time-slot py-3 rounded-lg font-semibold transition bg-gray-900 text-white hover:bg-gray-800 border border-yellow-500 border-opacity-20" data-time="${time}">
                        ${time}
                    </button>
                `).join('');
            }
        }

        function selectTime(time) {
            appState.selectedTime = time;
            document.querySelectorAll('.time-slot').forEach(btn => {
                if (btn.dataset.time === time) {
                    btn.className = 'time-slot py-3 rounded-lg font-semibold transition bg-yellow-500 text-black';
                } else {
                    btn.className = 'time-slot py-3 rounded-lg font-semibold transition bg-gray-900 text-white hover:bg-gray-800 border border-yellow-500 border-opacity-20';
                }
            });
            document.getElementById('confirmButton').classList.remove('hidden');
        }

        function confirmBooking() {
            const booking = {
                id: Date.now(),
                barber: appState.selectedBarber,
                service: appState.selectedService,
                date: appState.selectedDate,
                time: appState.selectedTime,
                status: 'confirmado'
            };
            
            appState.bookingHistory.push(booking);
            appState.loyaltyPoints++;
            
            const phone = '5522999030277';
            const message = encodeURIComponent(
                `Olá! Gostaria de confirmar meu agendamento.\n\n` +
                `Nome: ${appState.userName}\n` +
                `Serviço: ${appState.selectedService.name}\n` +
                `Barbeiro: ${appState.selectedBarber.name}\n` +
                `Data: ${new Date(appState.selectedDate + 'T00:00:00').toLocaleDateString('pt-BR')}\n` +
                `Horário: ${appState.selectedTime}\n` +
                `Telefone: ${appState.userPhone}`
            );
            
            window.open(`https://wa.me/${phone}?text=${message}`, '_blank');
            
            appState.selectedService = null;
            appState.selectedBarber = null;
            appState.selectedDate = '';
            appState.selectedTime = '';
            
            updateUI();
            showScreen('home');
        }

        function redeemReward() {
            if (appState.loyaltyPoints >= 10) {
                appState.loyaltyPoints -= 10;
                const phone = '5522999030277';
                const message = encodeURIComponent(
                    `Olá! Gostaria de resgatar meu corte grátis!\n\nNome: ${appState.userName}\nTelefone: ${appState.userPhone}`
                );
                window.open(`https://wa.me/${phone}?text=${message}`, '_blank');
                updateUI();
            }
        }

        function showScreen(screen) {
            const screens = ['homeScreen', 'bookingScreen', 'loyaltyScreen', 'profileScreen'];
            screens.forEach(s => document.getElementById(s).classList.add('hidden'));
            document.getElementById(screen + 'Screen').classList.remove('hidden');
            
            const navButtons = ['navHome', 'navBooking', 'navLoyalty', 'navProfile'];
            navButtons.forEach(btn => {
                const element = document.getElementById(btn);
                element.classList.remove('text-yellow-500');
                element.classList.add('text-gray-400');
            });
            
            const activeNav = 'nav' + screen.charAt(0).toUpperCase() + screen.slice(1);
            const activeElement = document.getElementById(activeNav);
            if (activeElement) {
                activeElement.classList.remove('text-gray-400');
                activeElement.classList.add('text-yellow-500');
            }
        }
    </script>
</body>
</html>
