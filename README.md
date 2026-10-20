<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hiệu Ứng Lời Chúc 20/10 🌸</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Montserrat:wght@400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            height: 100vh;
            background: linear-gradient(135deg, #ff758c 0%, #ff7eb3 100%);
            overflow: hidden;
            font-family: 'Montserrat', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        /* Canvas để vẽ pháo hoa / hiệu ứng linh hoạt bằng JS */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        /* Hộp thiệp trung tâm */
        .card {
            background: rgba(255, 255, 255, 0.9);
            padding: 40px 30px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            text-align: center;
            z-index: 10;
            max-width: 450px;
            width: 90%;
            backdrop-filter: blur(10px);
            animation: zoomIn 1s ease-in-out;
        }

        @keyframes zoomIn {
            0% { transform: scale(0); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        h1 {
            font-family: 'Dancing Script', cursive;
            color: #d63384;
            font-size: 3.2rem;
            margin-bottom: 15px;
        }

        /* Hiệu ứng gõ chữ */
        .typing-text {
            color: #444;
            font-size: 1.1rem;
            line-height: 1.6;
            min-height: 80px;
            margin-bottom: 25px;
            font-weight: 600;
            border-right: 2px solid #d63384;
            white-space: pre-wrap;
            animation: blink 0.75s step-end infinite;
        }

        @keyframes blink {
            from, to { border-color: transparent }
            50% { border-color: #d63384; }
        }

        .btn {
            background: linear-gradient(45deg, #ff4d6d, #d63384);
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1rem;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 600;
            transition: 0.3s;
            box-shadow: 0 5px 15px rgba(255, 77, 109, 0.4);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(255, 77, 109, 0.6);
        }
    </style>
</head>
<body>

    <!-- Canvas cho JavaScript vẽ hiệu ứng hạt / trái tim -->
    <canvas id="effectCanvas"></canvas>

    <!-- Khung thiệp -->
    <div class="card">
        <h1>20/10 Rực Rỡ 🌸</h1>
        <div class="typing-text" id="typing"></div>
        <button class="btn" onclick="triggerFireworks()">Bắn Pháo Hoa Chúc Mừng 🎆</button>
    </div>

    <script>
        const canvas = document.getElementById('effectCanvas');
        const ctx = canvas.getContext('2d');

        // Tự động điều chỉnh kích thước canvas theo màn hình
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // --- 1. HIỆU ỨNG GÕ CHỮ (TYPING EFFECT) ---
        const message = "Chúc một nửa thế giới luôn luôn xinh đẹp, ngập tràn hạnh phúc, thành công trong cuộc sống và mãi là đóa hoa tỏa hương thơm ngát!";
        let index = 0;
        const speed = 50; // Tốc độ gõ chữ (ms)

        function typeWriter() {
            if (index < message.length) {
                document.getElementById("typing").innerHTML += message.charAt(index);
                index++;
                setTimeout(typeWriter, speed);
            }
        }
        // Bắt đầu chạy hiệu ứng gõ chữ sau 1 giây
        setTimeout(typeWriter, 1000);


        // --- 2. HIỆU ỨNG TRÁI TIM RƠI BẰNG JAVASCRIPT ---
        let particles = [];

        class Heart {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * -canvas.height;
                this.size = Math.random() * 10 + 8;
                this.speedY = Math.random() * 2 + 1;
                this.speedX = Math.random() * 2 - 1;
                this.opacity = Math.random() * 0.5 + 0.3;
                this.color = `rgba(255, ${Math.floor(Math.random() * 100 + 150)}, 180, ${this.opacity})`;
            }

            update() {
                this.y += this.speedY;
                this.x += this.speedX;
                if (this.y > canvas.height) {
                    this.y = -20;
                    this.x = Math.random() * canvas.width;
                }
            }

            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                let d = this.size;
                ctx.moveTo(this.x, this.y + d / 4);
                ctx.quadraticCurveTo(this.x, this.y, this.x + d / 4, this.y);
                ctx.quadraticCurveTo(this.x + d / 2, this.y, this.x + d / 2, this.y + d / 4);
                ctx.quadraticCurveTo(this.x + d / 2, this.y + d / 2, this.x, this.y + d * 0.75);
                ctx.quadraticCurveTo(this.x - d / 2, this.y + d / 2, this.x - d / 2, this.y + d / 4);
                ctx.quadraticCurveTo(this.x - d / 2, this.y, this.x - d / 4, this.y);
                ctx.quadraticCurveTo(this.x, this.y, this.x, this.y + d / 4);
                ctx.fill();
            }
        }

        // Khởi tạo 40 trái tim rơi nền
        for (let i = 0; i < 40; i++) {
            particles.push(new Heart());
        }


        // --- 3. HIỆU ỨNG PHÁO HOA KHI BẤM NÚT ---
        let fireworks = [];

        class FireworkParticle {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                const angle = Math.random() * Math.PI * 2;
                const speed = Math.random() * 6 + 2;
                this.vx = Math.cos(angle) * speed;
                this.vy = Math.sin(angle) * speed;
                this.alpha = 1;
                this.color = `hsl(${Math.random() * 60 + 330}, 100%, 70%)`; // Tông hồng/đỏ
                this.size = Math.random() * 4 + 2;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;
                this.vy += 0.05; // Trọng lực nhẹ
                this.alpha -= 0.015;
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.alpha;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }

        function triggerFireworks() {
            // Tạo 3 điểm nổ pháo hoa ngẫu nhiên trên màn hình
            for (let f = 0; f < 3; f++) {
                let fx = Math.random() * (canvas.width - 200) + 100;
                let fy = Math.random() * (canvas.height / 2);
                for (let i = 0; i < 50; i++) {
                    fireworks.push(new FireworkParticle(fx, fy));
                }
            }
        }


        // --- HÀM LOOP CHÍNH ĐỂ VẼ LIÊN TỤC ---
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Vẽ và cập nhật tim rơi
            particles.forEach(p => {
                p.update();
                p.draw();
            });

            // Vẽ và cập nhật pháo hoa
            fireworks.forEach((fw, index) => {
                fw.update();
                fw.draw();
                if (fw.alpha <= 0) {
                    fireworks.splice(index, 1);
                }
            });

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
