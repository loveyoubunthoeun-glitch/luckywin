<!DOCTYPE html>
<html lang="km">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ចុះឈ្មោះចូលរួមចាប់រង្វាន់</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        body {
            font-family: 'Inter', 'Kantumruy Pro', sans-serif;
            /* Background image styling */
            background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('lucky pic.jpg');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }
    </style>
</head>

<body class="flex items-center justify-center min-h-screen p-4">

    <div class="bg-white text-gray-900 rounded-2xl shadow-2xl p-6 sm:p-8 w-full max-w-md my-8">

        <h1 class="text-2xl sm:text-3xl font-extrabold text-center mb-4 bg-clip-text text-transparent bg-gradient-to-r from-blue-600 to-purple-500">
            ចុះឈ្មោះចូលរួម
        </h1>
        <p class="text-center text-gray-600 mb-6 text-sm">សូមបង់ប្រាក់តាមរយៈ ABA ឬ ACLEDA រួចបញ្ចូលឈ្មោះ។</p>

        <!-- Payment Options Container -->
        <div class="space-y-4 mb-6">

            <!-- 1. ABA BANK Section -->
            <div class="bg-[#005F92] rounded-xl p-5 text-white shadow-lg relative overflow-hidden">
                <div class="absolute -right-6 -top-6 w-24 h-24 bg-white opacity-10 rounded-full"></div>

                <div class="flex justify-between items-center mb-4">
                    <span class="font-bold text-lg tracking-wider">ABA BANK</span>
                    <span class="text-xs bg-white text-[#005F92] px-2 py-1 rounded font-bold">PAY</span>
                </div>

                <div class="flex justify-center mb-4">
                    <div class="bg-white p-2 rounded-lg shadow-md">
                        <img src="Qr AbA.jpg" alt="ABA QR Code" class="w-28 h-28 object-contain">
                    </div>
                </div>

                <div class="space-y-1 text-center">
                    <p class="text-xs opacity-80">Account Number</p>
                    <p class="text-xl font-mono font-bold tracking-widest select-all">004 255 933</p>
                </div>

                <div class="mt-3 pt-3 border-t border-white/20 text-center">
                    <p class="text-xs opacity-80">Account Name</p>
                    <p class="text-base font-semibold uppercase tracking-wide">LYSONGENG</p>
                </div>
            </div>

            <!-- 2. NEW: ACLEDA BANK Section -->
            <div class="bg-[#0E336A] rounded-xl p-5 text-white shadow-lg relative overflow-hidden border border-gray-200">
                <!-- Decorative circle -->
                <div class="absolute -left-6 -bottom-6 w-24 h-24 bg-white opacity-10 rounded-full"></div>

                <div class="flex justify-between items-center mb-4">
                    <span class="font-bold text-lg tracking-wider">ACLEDA</span>
                    <span class="text-xs bg-[#FDB913] text-[#0E336A] px-2 py-1 rounded font-bold">KHQR</span>
                </div>

                <!-- QR Code Section -->
                <div class="flex justify-center mb-4">
                    <div class="bg-white p-2 rounded-lg shadow-md">
                        <!-- Using the uploaded ACLEDA QR -->
                        <img src="Ac.jpg.jpg" alt="ACLEDA QR Code" class="w-28 h-28 object-contain">
                    </div>
                </div>

                <div class="space-y-1 text-center">
                    <p class="text-xs opacity-80">Phone/Account Number</p>
                    <p class="text-xl font-mono font-bold tracking-widest select-all">077 772 604</p>
                </div>

                <div class="mt-3 pt-3 border-t border-white/20 text-center">
                    <p class="text-xs opacity-80">Account Name</p>
                    <p class="text-base font-semibold uppercase tracking-wide">HOK SAN PANHA</p>
                </div>
            </div>

        </div>

        <!-- Name Input -->
        <div class="mb-4">
            <label for="nameInput" class="block text-sm font-medium text-gray-700 mb-2">បញ្ចូលឈ្មោះរបស់អ្នក</label>
            <input type="text" id="nameInput" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="ឧ. សុខ វណ្ណា">
        </div>

        <!-- Payment Confirmation Checkbox -->
        <div class="mb-6 flex items-start gap-3 p-3 bg-gray-50 rounded-lg border border-gray-200">
            <input type="checkbox" id="paymentCheck" class="w-5 h-5 mt-0.5 text-blue-600 rounded border-gray-300 focus:ring-blue-500 cursor-pointer">
            <label for="paymentCheck" class="text-sm text-gray-700 cursor-pointer select-none">
                ខ្ញុំបានធ្វើការផ្ទេរប្រាក់ទៅគណនី (ABA ឬ ACLEDA) ខាងលើរួចរាល់ហើយ។
            </label>
        </div>

        <!-- Submit Button -->
        <button id="submitButton" disabled class="w-full bg-gray-400 text-white p-3 rounded-lg text-lg font-bold transition duration-300 shadow-lg cursor-not-allowed">
            ចុះឈ្មោះ
        </button>

        <!-- Message Display -->
        <div id="messageDisplay" class="mt-4 text-center font-medium min-h-[24px]"></div>

    </div>

    <script>
        const nameInput = document.getElementById('nameInput');
        const submitButton = document.getElementById('submitButton');
        const messageDisplay = document.getElementById('messageDisplay');
        const paymentCheck = document.getElementById('paymentCheck');

        // This is the shared key between client and admin
        const PARTICIPANT_STORAGE_KEY = 'luckyDrawParticipants';

        // Telegram Bot Configuration
        const telegram_bot_id = "8273106488:AAHHTDMqoZemCK563T-YQMB4arMYl5Ntq-w";
        const chat_id = 1126254088;

        // Toggle button state based on checkbox
        paymentCheck.addEventListener('change', function() {
            if (this.checked) {
                submitButton.disabled = false;
                submitButton.classList.remove('bg-gray-400', 'cursor-not-allowed');
                submitButton.classList.add('bg-blue-600', 'hover:bg-blue-700');
            } else {
                submitButton.disabled = true;
                submitButton.classList.add('bg-gray-400', 'cursor-not-allowed');
                submitButton.classList.remove('bg-blue-600', 'hover:bg-blue-700');
            }
        });

        // Function to send a message to Telegram
        async function sendToTelegram(messageText) {
            const url = `https://api.telegram.org/bot${telegram_bot_id}/sendMessage`;
            const payload = {
                chat_id: chat_id,
                text: messageText,
                parse_mode: 'HTML'
            };

            try {
                const response = await fetch(url, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(payload)
                });
                await response.json();
            } catch (error) {
                console.error('Error sending to Telegram:', error);
            }
        }

        function registerName() {
            const name = nameInput.value.trim();

            if (!name) {
                messageDisplay.textContent = 'សូមបញ្ចូលឈ្មោះរបស់អ្នក!';
                messageDisplay.className = 'mt-4 text-center font-medium text-red-600';
                return;
            }

            if (!paymentCheck.checked) {
                messageDisplay.textContent = 'សូមបញ្ជាក់ថាអ្នកបានបង់ប្រាក់រួចរាល់!';
                messageDisplay.className = 'mt-4 text-center font-medium text-red-600';
                return;
            }

            try {
                let names = JSON.parse(localStorage.getItem(PARTICIPANT_STORAGE_KEY)) || [];

                const nameExists = names.some(existingName => existingName.toLowerCase() === name.toLowerCase());

                if (nameExists) {
                    messageDisplay.textContent = 'ឈ្មោះនេះបានចុះឈ្មោះរួចរាល់ហើយ។';
                    messageDisplay.className = 'mt-4 text-center font-medium text-yellow-600';
                } else {
                    names.push(name);
                    localStorage.setItem(PARTICIPANT_STORAGE_KEY, JSON.stringify(names));

                    messageDisplay.textContent = 'ការចុះឈ្មោះបានជោគជ័យ! សូមរង់ចាំការចាប់រង្វាន់។';
                    messageDisplay.className = 'mt-4 text-center font-medium text-green-600';

                    // Reset form
                    nameInput.value = '';
                    paymentCheck.checked = false;
                    submitButton.disabled = true;
                    submitButton.classList.add('bg-gray-400', 'cursor-not-allowed');
                    submitButton.classList.remove('bg-blue-600', 'hover:bg-blue-700');

                    // Send notification to Telegram with Payment Confirmation
                    // MODIFIED: Updated message to mention both banks
                    const telegramMessage = `💸 <b>ការចុះឈ្មោះថ្មី (New Payment)</b> 💸\n\n<b>ឈ្មោះ:</b> ${name}\n<b>ស្ថានភាព:</b> បានបញ្ជាក់ថាបានផ្ទេរប្រាក់\n<b>សូមពិនិត្យគណនី:</b>\n1. ABA (Lysongeng)\n2. ACLEDA (Hok San Panha)`;
                    sendToTelegram(telegramMessage);
                }
            } catch (e) {
                console.error("Error accessing localStorage", e);
                messageDisplay.textContent = 'មានបញ្ហាក្នុងការរក្សាទុកទិន្នន័យ។';
                messageDisplay.className = 'mt-4 text-center font-medium text-red-600';
            }

            setTimeout(() => {
                messageDisplay.textContent = '';
            }, 5000);
        }

        submitButton.addEventListener('click', registerName);
        nameInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && !submitButton.disabled) {
                registerName();
            }
        });
    </script>

</body>

</html>
