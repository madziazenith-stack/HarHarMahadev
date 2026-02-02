<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mahashivratri Virtual Puja</title>
    <style>
        body {
            background-color: #0f0f0f;
            color: #f39c12;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            margin: 0;
            font-family: 'Times New Roman', serif;
            overflow: hidden;
        }
        h1 { text-shadow: 0 0 15px #f39c12; margin: 5px; }
        
        /* Altar Setup */
        .altar {
            position: relative;
            width: 350px;
            height: 450px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;
        }

        .shivling-img { width: 220px; z-index: 5; margin-bottom: 20px; }

        /* The Lota (Pot) */
        #lota {
            position: absolute;
            top: 40px;
            width: 80px;
            z-index: 10;
            transition: transform 0.5s ease-in-out;
            transform-origin: top right;
        }
        .tilt-lota { transform: rotate(-45deg); }

        /* Liquids and Symbols */
        .stream {
            position: absolute;
            top: 100px;
            width: 8px;
            height: 0;
            z-index: 4;
            transition: height 0.4s ease-in;
            border-radius: 4px;
        }
        .water { background: rgba(173, 216, 230, 0.8); box-shadow: 0 0 10px #add8e6; }
        .milk { background: rgba(255, 255, 255, 0.95); box-shadow: 0 0 10px #fff; }

        /* Om and Flowers Animation */
        .om-symbol {
            position: absolute;
            font-size: 40px;
            color: #f39c12;
            font-weight: bold;
            opacity: 0;
            z-index: 15;
            animation: riseFade 2s ease-out forwards;
        }
        @keyframes riseFade {
            0% { transform: translateY(0); opacity: 0; }
            50% { opacity: 1; }
            100% { transform: translateY(-150px); opacity: 0; }
        }

        .offering-item {
            position: absolute;
            font-size: 25px;
            z-index: 6;
            animation: fallRotate 3s ease-in forwards;
        }
        @keyframes fallRotate {
            0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(300px) rotate(360deg); opacity: 0; }
        }

        /* Controls */
        .controls { margin-top: 20px; display: grid; grid-template-columns: 1fr 1fr; gap: 10px; z-index: 20; }
        .puja-btn {
            background: #d35400; color: white; border: none; padding: 12px;
            border-radius: 8px; cursor: pointer; font-size: 1rem; transition: 0.3s;
        }
        .puja-btn:hover { background: #e67e22; transform: translateY(-2px); }
    </style>
</head>
<body>

    <h1>Om Namah Shivaya</h1>
    <p>May Lord Shiva bless you</p>

    <div class="altar">
        <img src="lota.png" id="lota" alt="Lota">
        <div id="liquidStream" class="stream"></div>
        <div id="omContainer"></div>
        <img src="shivling.png" class="shivling-img" alt="Shivling">
    </div>

    <div class="controls">
        <button class="puja-btn" onclick="offerLiquid('water')">Offer Water</button>
        <button class="puja-btn" onclick="offerLiquid('milk')">Offer Milk</button>
        <button class="puja-btn" onclick="offerItem('🌸')">Offer Flowers</button>
        <button class="puja-btn" onclick="offerItem('🌿')">Offer Bel Leaves</button>
    </div>

    <script>
        function showOm() {
            const container = document.getElementById('omContainer');
            const om = document.createElement('div');
            om.className = 'om-symbol';
            om.innerHTML = 'ॐ';
            om.style.left = (Math.random() * 100 - 50) + 'px'; // Random slight shift
            container.appendChild(om);
            setTimeout(() => om.remove(), 2000);
        }

        function offerLiquid(type) {
            const lota = document.getElementById('lota');
            const stream = document.getElementById('liquidStream');
            
            // Tilt the Lota
            lota.classList.add('tilt-lota');
            showOm();

            // Start Pouring
            setTimeout(() => {
                stream.className = 'stream ' + type;
                stream.style.height = '280px';
            }, 300);

            // Stop Pouring
            setTimeout(() => {
                stream.style.height = '0';
                lota.classList.remove('tilt-lota');
            }, 2000);
        }

        function offerItem(emoji) {
            showOm();
            for(let i=0; i<8; i++) {
                setTimeout(() => {
                    const item = document.createElement('div');
                    item.className = 'offering-item';
                    item.innerHTML = emoji;
                    item.style.left = (Math.random() * 200 + 75) + 'px';
                    document.querySelector('.altar').appendChild(item);
                    setTimeout(() => item.remove(), 3000);
                }, i * 150);
            }
        }
    </script>
</body>
</html>


