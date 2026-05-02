<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MB_DETECTION_SYSTEM_V2</title>
    <style>
        body {
            background-color: #000;
            color: #0f0; /* 經典矩陣綠 */
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            text-shadow: 0 0 5px #0f0;
        }

        .terminal-box {
            border: 1px solid #0f0;
            padding: 30px;
            width: 85%;
            max-width: 600px;
            background: rgba(0, 20, 0, 0.9);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
            position: relative;
        }

        .header {
            border-bottom: 1px solid #0f0;
            margin-bottom: 20px;
            padding-bottom: 10px;
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
        }

        .system-title {
            font-weight: bold;
            letter-spacing: 2px;
        }

        .console-log {
            height: 100px;
            overflow-y: hidden;
            font-size: 0.8rem;
            color: #0a0;
            margin-bottom: 20px;
            line-height: 1.4;
        }

        .result-row {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
        }

        .number-box {
            font-size: 4rem;
            width: 100px;
            height: 120px;
            border: 1px dashed #0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
        }

        .number-box.locked {
            border-style: solid;
            background: rgba(0, 255, 0, 0.1);
            animation: pulse 0.5s ease-out;
        }

        @keyframes pulse {
            0% { transform: scale(1); box-shadow: 0 0 0px #0f0; }
            50% { transform: scale(1.1); box-shadow: 0 0 20px #0f0; }
            100% { transform: scale(1); box-shadow: 0 0 0px #0f0; }
        }

        .btn-container {
            text-align: right;
        }

        button {
            background: #0f0;
            color: #000;
            border: none;
            padding: 10px 25px;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }

        button:hover {
            background: #fff;
            box-shadow: 0 0 15px #fff;
        }

        button:disabled {
            background: #333;
            color: #666;
            cursor: not-allowed;
        }

        .glitch-text {
            animation: glitch 1s infinite;
        }

        @keyframes glitch {
            0% { opacity: 1; }
            50% { opacity: 0.7; transform: skewX(1deg); }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>

<div class="terminal-box">
    <div class="header">
        <span class="system-title">> MB自動偵測系統_V2.0</span>
        <span>STATUS: RUNNING</span>
    </div>

    <div class="console-log" id="console">
        [INFO] System initialized...<br>
        [INFO] Ready for data extraction...
    </div>

    <div class="result-row">
        <div class="number-box" id="n1">0</div>
        <div class="number-box" id="n2">0</div>
        <div class="number-box" id="n3">0</div>
    </div>

    <div class="btn-container">
        <button id="runBtn" onclick="executeSystem()">[ EXECUTE_SCAN ]</button>
    </div>
</div>

<script>
    const logs = [
        "[ACCESS] Connecting to core node...",
        "[DATA] Pulling random entropy seed...",
        "[CALC] Analyzing probability matrices...",
        "[WARN] Bypassing security layers...",
        "[INFO] Target sequences identified.",
        "[SUCCESS] Extraction complete."
    ];

    function addLog(text) {
        const consoleEl = document.getElementById('console');
        consoleEl.innerHTML += `<br>> ${text}`;
        consoleEl.scrollTop = consoleEl.scrollHeight;
    }

    async function executeSystem() {
        const btn = document.getElementById('runBtn');
        const boxes = [
            document.getElementById('n1'),
            document.getElementById('n2'),
            document.getElementById('n3')
        ];
        
        btn.disabled = true;
        document.getElementById('console').innerHTML = "[START] Initiating MB scan...";

        // 生成隨機數
        const pool = Array.from({length: 10}, (_, i) => i + 1);
        const results = [];
        for(let i=0; i<3; i++) {
            results.push(pool.splice(Math.floor(Math.random() * pool.length), 1)[0]);
        }
        results.sort((a,b) => a-b);

        // 模擬黑客日誌跑動
        for(let log of logs) {
            addLog(log);
            await new Promise(r => setTimeout(r, 400));
            
            // 隨機跳動盒子裡的數字
            boxes.forEach(box => {
                if(!box.classList.contains('locked')) {
                    box.innerText = Math.floor(Math.random() * 10) + 1;
                }
            });
        }

        // 逐一鎖定結果
        for(let i=0; i<3; i++) {
            await new Promise(r => setTimeout(r, 300));
            boxes[i].innerText = results[i];
            boxes[i].classList.add('locked');
        }

        btn.disabled = false;
        addLog("SYSTEM IDLE. Awaiting next command.");
    }
</script>

</body>
</html>
