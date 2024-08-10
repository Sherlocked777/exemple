<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alert Message</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            background-color: black;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: Arial, sans-serif;
            position: relative;
        }

        .matrix {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            overflow: hidden;
            display: none;
        }

        .message-box {
            border: 2px solid red;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.8);
            color: #00FF00;
            font-size: 30px;
            text-align: center;
            white-space: nowrap;
            z-index: 1;
            position: relative;
            animation: flash 1.5s infinite;
        }

        @keyframes flash {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }

        #trigger {
            color: red;
            font-size: 24px;
            text-decoration: underline;
            z-index: 2;
            padding: 10px 20px;
            background-color: rgba(0, 0, 0, 0.8);
            transition: all 0.3s ease;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        #trigger:hover {
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <canvas class="matrix" id="matrix"></canvas>
    <a href="#" id="trigger">Click Here</a>
    <div class="message-box" id="message" style="display: none;">
        YOUR ACCOUNT IS HACKED...
    </div>

    <audio id="siren" src="path/to/your/musicfile.mp3"></audio>

    <script>
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        const chars = '12345';
        const fontSize = 14;
        let columns;
        let drops;

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            columns = Math.floor(canvas.width / fontSize);
            drops = Array(columns).fill(1);
        }

        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#00FF00';
            ctx.font = `${fontSize}px monospace`;

            for (let i = 0; i < drops.length; i++) {
                const x = i * fontSize;
                const y = drops[i] * fontSize;
                const text = chars.charAt(Math.floor(Math.random() * chars.length));
                ctx.fillText(text, x, y);

                if (y > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }

                drops[i]++;
            }
        }

        setInterval(drawMatrix, 100);
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        document.getElementById("trigger").addEventListener("click", function(event) {
            event.preventDefault();
            document.getElementById("trigger").style.display = "none";
            document.getElementById("matrix").style.display = "block";
            document.getElementById("message").style.display = "block";
            document.getElementById("siren").play();
        });
    </script>
</body>
</html>
