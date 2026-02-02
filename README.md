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
        h1 { text-shadow: 0 0 15px #f39c12; margin: 5px; z-index: 20; }
        
        .altar {
            position: relative;
            width: 100vw;
            height: 500px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .shivling-img { width: 220px; z-index: 5; margin-top: 50px; }

        #lota {
            position: absolute;
            top: 20px;
            left: 55%;
            width: 80px;
            z-index: 10;
            transition: transform 0.5s ease-in-out;
            transform-origin: top right;
        }
        .tilt-lota { transform: rotate(-45deg); }

        /* Aarti Thaali Styling */
        #thaali {
            position: absolute;
            bottom: 20px;
            width: 180px;
            z-index: 12;
            opacity: 0.8;
            display: none; /* Only shows during Aarti */
            animation: rotateAarti 5s linear infinite;
        }

        @keyframes rotateAarti {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .stream {
            position: absolute;
            top: 80px;
            left: 54.5%;
            width: 8px;
            height: 0;
            z-index: 4;
            transition: height 0.4s ease-in;
            border-radius: 4px;
        }
        .water { background: rgba(173, 216, 230, 0.8); box-shadow: 0 0 10px #add8e6; }
        .milk { background: rgba(255, 255, 255, 0.95); box-shadow: 0 0 10px #fff; }

        /* Rising Om Animation */
        .om-symbol {
            position: absolute;
            font-size: 30px;
            color: #f39c12;
            opacity: 0;
            z-index: 2;
            animation: riseFade 4s ease-out forwards;
        }
        @keyframes riseFade {
            0% { transform: translateY(100vh) scale(0.5); opacity: 0; }
            20% { opacity: 0.6; }
            100% { transform: translateY(-110vh) scale(1.5); opacity: 0; }
        }

        .offering-item {
            position: absolute;
            font-size: 25px;
            z-index: 6;
            animation: fallRotate 3s ease-in forwards;
        }
        @keyframes fallRotate {
            0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(400px) rotate(360deg); opacity: 0; }
        }

        .controls { margin-top: 20px; display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; z-index: 25; }
        .puja-btn {
            background: #d35400; color: white; border: none; padding: 12px;
            border-radius: 8px; cursor: pointer; font-size: 0.9rem; transition: 0.3s;
        }
        .puja-btn:hover { background: #e67e22; transform: translateY(-2px); }
        .active-aarti { background: #f39c12 !important; box-shadow: 0 0 15px #f39c12; }
    </style>
</head>
<body>

    <h1>Om Namah Shivaya</h1>
    <p>Virtual Mahashivratri Puja</p>

    <div class="altar" id="altar">
        <img src="lota.png" id="lota" alt="Lota">
        <div id="liquidStream" class="stream"></div>
        <img src="shivling.png" class="shivling-img" alt="Shivling">
        <img src="thaali.png" id="thaali" alt="Aarti Thaali">
    </div>

    <div class="controls">
        <button class="puja-btn" onclick="offerLiquid('water')">Water</button>
        <button class="puja-btn" onclick="offerLiquid('milk')">Milk</button>
        <button class="puja-btn" onclick="offerItem('🌸')">Flowers</button>
        <button class="puja-btn" onclick="offerItem('🌿')">Bel Leaves</button>
        <button class="puja-btn" id="aartiBtn" onclick="toggleAarti()">Aarti</button>
    </div>

    <script>
        // Function to create many rising Oms
        function emergeOms() {
            for(let i=0; i<5; i++) {
                setTimeout(() => {
                    const om = document.createElement('div');
                    om.className = 'om-symbol';
                    om.innerHTML = 'ॐ';
                    om.style.left = Math.random() * 100 + 'vw';
                    om.style.animationDuration = (Math.random() * 2 + 3) + 's';
                    document.body.appendChild(om);
                    setTimeout(() => om.remove(), 4000);
                }, i * 300);
            }
        }

        function offerLiquid(type) {
            const lota = document.getElementById('lota');
            const stream = document.getElementById('liquidStream');
            lota.classList.add('tilt-lota');
            emergeOms();

            setTimeout(() => {
                stream.className = 'stream ' + type;
                stream.style.height = '200px';
            }, 300);

            setTimeout(() => {
                stream.style.height = '0';
                lota.classList.remove('tilt-lota');
            }, 2000);
        }

        function offerItem(emoji) {
            emergeOms();
            for(let i=0; i<10; i++) {
                setTimeout(() => {
                    const item = document.createElement('div');
                    item.className = 'offering-item';
                    item.innerHTML = emoji;
                    item.style.left = (Math.random() * 60 + 20) + 'vw';
                    document.getElementById('altar').appendChild(item);
                    setTimeout(() => item.remove(), 3000);
                }, i * 150);
            }
        }

        function toggleAarti() {
            const thaali = document.getElementById('thaali');
            const btn = document.getElementById('aartiBtn');
            
            if (thaali.style.display === 'block') {
                thaali.style.display = 'none';
                btn.classList.remove('active-aarti');
                clearInterval(window.aartiInterval);
            } else {
                thaali.style.display = 'block';
                btn.classList.add('active-aactive-aarti');
                // Create Oms continuously during Aarti
                window.aartiInterval = setInterval(emergeOms, 1500);
            }
        }
    </script>
</body>
</html>

