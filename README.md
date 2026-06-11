<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Tài Xỉu - Bet888</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎲 TÀI XỈU GAME 🎲</h1>
            <div class="score-board">
                <div class="score-item">
                    <span class="label">Điểm:</span>
                    <span class="value" id="score">0</span>
                </div>
                <div class="score-item">
                    <span class="label">Cược Hiện Tại:</span>
                    <span class="value" id="current-bet">0</span>
                </div>
            </div>
        </div>

        <div class="betting-section">
            <h2>Đặt Cược</h2>
            <div class="bet-amount">
                <label for="bet-input">Nhập số điểm cược:</label>
                <input type="number" id="bet-input" min="10" max="1000" value="100" placeholder="Nhập số điểm">
            </div>

            <div class="bet-buttons">
                <button class="bet-btn tai-btn" onclick="setBet('tai')">💰 TÀI</button>
                <button class="bet-btn xiu-btn" onclick="setBet('xiu')">💰 XỈU</button>
            </div>

            <p class="bet-status" id="bet-status">Hãy đặt cược để bắt đầu</p>
        </div>

        <div class="dice-section">
            <h2>Xúc Xắc</h2>
            <div class="dices" id="dices">
                <div class="dice" id="dice1">
                    <div class="dot"></div>
                </div>
                <div class="dice" id="dice2">
                    <div class="dot"></div>
                </div>
                <div class="dice" id="dice3">
                    <div class="dot"></div>
                </div>
            </div>

            <div class="total-section">
                <h3>Tổng Cộng: <span id="total">0</span></h3>
                <p id="result-text"></p>
            </div>

            <button class="roll-btn" id="roll-btn" onclick="rollDice()">🎲 ROLL XÚC XẮC</button>
        </div>

        <div class="history-section">
            <h2>Lịch Sử Cược</h2>
            <div class="history" id="history">
                <p class="empty-history">Chưa có cược nào</p>
            </div>
        </div>

        <div class="rules-section">
            <h2>📋 Luật Chơi</h2>
            <ul>
                <li>Roll 3 xúc xắc (mỗi xúc xắc từ 1-6 điểm)</li>
                <li><strong>TÀI:</strong> Tổng điểm ≥ 11 (thắng 1.9x cược)</li>
                <li><strong>XỈU:</strong> Tổng điểm ≤ 10 (thắng 1.9x cược)</li>
                <li>Nếu thua, mất toàn bộ số cược</li>
            </ul>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.container {
    background: white;
    border-radius: 20px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    max-width: 600px;
    width: 100%;
    padding: 40px;
    animation: slideIn 0.5s ease-out;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* Header */
.header {
    text-align: center;
    margin-bottom: 30px;
    border-bottom: 3px solid #667eea;
    padding-bottom: 20px;
}

.header h1 {
    color: #667eea;
    font-size: 2.5em;
    margin-bottom: 15px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.score-board {
    display: flex;
    justify-content: space-around;
    gap: 20px;
    flex-wrap: wrap;
}

.score-item {
    display: flex;
    align-items: center;
    gap: 10px;
}

.score-item .label {
    color: #666;
    font-weight: 600;
}

.score-item .value {
    color: #667eea;
    font-size: 1.5em;
    font-weight: bold;
    min-width: 80px;
}

/* Betting Section */
.betting-section {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 30px;
}

.betting-section h2 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.3em;
}

.bet-amount {
    margin-bottom: 15px;
}

.bet-amount label {
    display: block;
    color: #666;
    margin-bottom: 8px;
    font-weight: 600;
}

.bet-amount input {
    width: 100%;
    padding: 10px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 1em;
    transition: border-color 0.3s;
}

.bet-amount input:focus {
    outline: none;
    border-color: #667eea;
}

.bet-buttons {
    display: flex;
    gap: 15px;
    margin-bottom: 15px;
}

.bet-btn {
    flex: 1;
    padding: 12px;
    border: 2px solid #ddd;
    border-radius: 8px;
    font-size: 1.1em;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s;
    background: white;
}

.bet-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.tai-btn {
    border-color: #ff6b6b;
    color: #ff6b6b;
}

.tai-btn.active {
    background: #ff6b6b;
    color: white;
}

.xiu-btn {
    border-color: #4ecdc4;
    color: #4ecdc4;
}

.xiu-btn.active {
    background: #4ecdc4;
    color: white;
}

.bet-status {
    text-align: center;
    color: #666;
    font-weight: 600;
}

/* Dice Section */
.dice-section {
    text-align: center;
    margin-bottom: 30px;
}

.dice-section h2 {
    color: #333;
    margin-bottom: 20px;
    font-size: 1.3em;
}

.dices {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-bottom: 20px;
    min-height: 120px;
    align-items: center;
}

.dice {
    width: 100px;
    height: 100px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 8px;
    padding: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    transition: transform 0.1s;
}

.dice.rolling {
    animation: diceRoll 0.6s ease-out;
}

@keyframes diceRoll {
    0% {
        transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
    }
    50% {
        transform: rotateX(180deg) rotateY(180deg) rotateZ(180deg);
    }
    100% {
        transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
    }
}

.dot {
    width: 12px;
    height: 12px;
    background: white;
    border-radius: 50%;
}

.total-section {
    margin: 20px 0;
}

.total-section h3 {
    color: #667eea;
    font-size: 1.8em;
    margin-bottom: 10px;
}

#result-text {
    font-size: 1.1em;
    font-weight: bold;
    min-height: 25px;
}

.result-win {
    color: #51cf66;
}

.result-lose {
    color: #ff6b6b;
}

.roll-btn {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border: none;
    padding: 15px 40px;
    font-size: 1.2em;
    font-weight: bold;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s;
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.roll-btn:hover:not(:disabled) {
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(102, 126, 234, 0.6);
}

.roll-btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

/* History Section */
.history-section {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 20px;
}

.history-section h2 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.3em;
}

.history {
    max-height: 200px;
    overflow-y: auto;
}

.history-item {
    background: white;
    padding: 10px;
    margin-bottom: 8px;
    border-radius: 8px;
    border-left: 4px solid #667eea;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.history-item.win {
    border-left-color: #51cf66;
}

.history-item.lose {
    border-left-color: #ff6b6b;
}

.history-item .result {
    font-weight: bold;
    font-size: 0.9em;
}

.history-item .amount {
    color: #666;
}

.empty-history {
    color: #999;
    text-align: center;
    padding: 20px;
}

/* Rules Section */
.rules-section {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 15px;
}

.rules-section h2 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.3em;
}

.rules-section ul {
    list-style: none;
    color: #666;
}

.rules-section li {
    padding: 8px 0;
    border-bottom: 1px solid #ddd;
    line-height: 1.6;
}

.rules-section li:last-child {
    border-bottom: none;
}

/* Responsive */
@media (max-width: 600px) {
    .container {
        padding: 20px;
    }

    .header h1 {
        font-size: 1.8em;
    }

    .dices {
        flex-wrap: wrap;
    }

    .dice {
        width: 80px;
        height: 80px;
    }

    .score-board {
        flex-direction: column;
    }

    .bet-buttons {
        flex-direction: column;
    }
}
let currentBet = 0;
let betType = null;
let score = 0;
let history = [];
let isRolling = false;

const diceElements = [document.getElementById('dice1'), document.getElementById('dice2'), document.getElementById('dice3')];
const rollBtn = document.getElementById('roll-btn');
const betStatusEl = document.getElementById('bet-status');
const scoreEl = document.getElementById('score');
const currentBetEl = document.getElementById('current-bet');
const totalEl = document.getElementById('total');
const resultTextEl = document.getElementById('result-text');
const historyEl = document.getElementById('history');

// Thiết lập cược
function setBet(type) {
    const betAmount = parseInt(document.getElementById('bet-input').value);
    
    if (betAmount < 10 || betAmount > 1000) {
        alert('Cược phải từ 10 đến 1000 điểm!');
        return;
    }

    if (score < betAmount) {
        alert('Bạn không đủ điểm để cược!');
        return;
    }

    // Xóa active class từ tất cả nút
    document.querySelectorAll('.bet-btn').forEach(btn => btn.classList.remove('active'));
    
    // Thêm active class vào nút được chọn
    if (type === 'tai') {
        document.querySelector('.tai-btn').classList.add('active');
    } else {
        document.querySelector('.xiu-btn').classList.add('active');
    }

    currentBet = betAmount;
    betType = type;
    currentBetEl.textContent = currentBet;
    betStatusEl.textContent = `Đã đặt cược ${currentBet} điểm cho ${type.toUpperCase()}`;
    rollBtn.disabled = false;
}

// Hàm vẽ xúc xắc
function drawDice(diceElement, value) {
    diceElement.innerHTML = '';
    
    const dotPatterns = {
        1: [[5]],
        2: [[1, 9], [5], [9, 1]],
        3: [[1], [5], [9]],
        4: [[1, 3], [7, 9]],
        5: [[1, 3], [5], [7, 9]],
        6: [[1, 3], [4, 6], [7, 9]]
    };

    const pattern = dotPatterns[value];
    for (let row of pattern) {
        for (let position of row) {
            const dot = document.createElement('div');
            dot.className = 'dot';
            diceElement.appendChild(dot);
        }
    }
}

// Roll xúc xắc
function rollDice() {
    if (!betType || currentBet === 0) {
        alert('Hãy đặt cược trước!');
        return;
    }

    if (isRolling) return;
    
    isRolling = true;
    rollBtn.disabled = true;
    resultTextEl.textContent = '';

    // Hiệu ứng quay xúc xắc
    diceElements.forEach(dice => dice.classList.add('rolling'));

    let rollCount = 0;
    const maxRolls = 20;
    const rollInterval = setInterval(() => {
        const diceValues = [getRandomDice(), getRandomDice(), getRandomDice()];
        diceValues.forEach((value, index) => {
            drawDice(diceElements[index], value);
        });
        rollCount++;

        if (rollCount >= maxRolls) {
            clearInterval(rollInterval);
            // Xúc xắc cuối cùng
            const finalDiceValues = [getRandomDice(), getRandomDice(), getRandomDice()];
            finalDiceValues.forEach((value, index) => {
                drawDice(diceElements[index], value);
            });
            diceElements.forEach(dice => dice.classList.remove('rolling'));
            
            checkResult(finalDiceValues);
            isRolling = false;
        }
    }, 50);
}

function getRandomDice() {
    return Math.floor(Math.random() * 6) + 1;
}

// Kiểm tra kết quả
function checkResult(diceValues) {
    const total = diceValues.reduce((a, b) => a + b, 0);
    totalEl.textContent = total;

    let isWin = false;
    if (betType === 'tai' && total >= 11) {
        isWin = true;
    } else if (betType === 'xiu' && total <= 10) {
        isWin = true;
    }

    let winAmount = 0;
    if (isWin) {
        winAmount = Math.round(currentBet * 1.9);
        score += winAmount;
        resultTextEl.textContent = `🎉 THẮNG! +${winAmount} điểm`;
        resultTextEl.className = 'result-win';
    } else {
        score -= currentBet;
        resultTextEl.textContent = `😢 THUA! -${currentBet} điểm`;
        resultTextEl.className = 'result-lose';
        winAmount = -currentBet;
    }

    scoreEl.textContent = score;

    // Thêm vào lịch sử
    addHistory({
        type: betType.toUpperCase(),
        total: total,
        bet: currentBet,
        result: isWin ? 'WIN' : 'LOSE',
        amount: winAmount
    });

    // Reset
    currentBet = 0;
    betType = null;
    currentBetEl.textContent = '0';
    document.querySelectorAll('.bet-btn').forEach(btn => btn.classList.remove('active'));
    betStatusEl.textContent = 'Hãy đặt cược để bắt đầu';
    rollBtn.disabled = true;
}

// Thêm vào lịch sử
function addHistory(record) {
    history.unshift(record);
    if (history.length > 10) {
        history.pop();
    }

    updateHistoryDisplay();
}

function updateHistoryDisplay() {
    if (history.length === 0) {
        historyEl.innerHTML = '<p class="empty-history">Chưa có cược nào</p>';
        return;
    }

    historyEl.innerHTML = history.map((record, index) => {
        const resultClass = record.result === 'WIN' ? 'win' : 'lose';
        const icon = record.result === 'WIN' ? '✅' : '❌';
        return `
            <div class="history-item ${resultClass}">
                <div>
                    <span class="result">${icon} ${record.type} - Tổng: ${record.total}</span>
                    <span class="amount"> | Cược: ${record.bet}</span>
                </div>
                <div style="color: ${record.result === 'WIN' ? '#51cf66' : '#ff6b6b'}; font-weight: bold;">
                    ${record.amount > 0 ? '+' : ''}${record.amount}
                </div>
            </div>
        `;
    }).join('');
}

// Khởi tạo
window.addEventListener('load', () => {
    score = 1000; // Điểm ban đầu
    scoreEl.textContent = score;
    rollBtn.disabled = true;
});
