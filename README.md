<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>AI Color Trading Predictor</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #0f172a;
        color: white;
        text-align: center;
        padding: 20px;
    }

    h1 {
        color: #38bdf8;
    }

    .container {
        max-width: 500px;
        margin: auto;
        background: #1e293b;
        padding: 20px;
        border-radius: 15px;
        box-shadow: 0 0 15px rgba(0,0,0,0.5);
    }

    button {
        padding: 10px 20px;
        margin: 5px;
        border: none;
        border-radius: 10px;
        font-size: 16px;
        cursor: pointer;
        transition: 0.3s;
    }

    .big {
        background: #22c55e;
    }

    .small {
        background: #ef4444;
    }

    .analyze {
        background: #3b82f6;
        width: 100%;
        margin-top: 10px;
    }

    button:hover {
        opacity: 0.8;
    }

    #history {
        margin: 15px 0;
        font-size: 18px;
    }

    .result-box {
        margin-top: 15px;
        padding: 15px;
        background: #334155;
        border-radius: 10px;
    }
</style>
</head>
<body>

<div class="container">
    <h1>AI Trading Predictor</h1>

    <p>Enter Last 10 Results:</p>

    <button class="big" onclick="addResult('B')">BIG</button>
    <button class="small" onclick="addResult('S')">SMALL</button>

    <div id="history">History: </div>

    <button class="analyze" onclick="analyze()">Analyze</button>

    <div class="result-box">
        <p id="prediction">Prediction: -</p>
        <p id="confidence">Confidence: -</p>
        <p id="advice">Advice: -</p>
        <p id="numbers">Suggested Numbers: -</p>
    </div>
</div>

<script>
let history = [];

function addResult(val) {
    if (history.length >= 10) {
        history.shift(); // remove oldest
    }
    history.push(val);
    document.getElementById("history").innerText = "History: " + history.join(" ");
}

function analyze() {
    if (history.length < 5) {
        alert("Enter at least 5 results!");
        return;
    }

    let bigCount = history.filter(x => x === 'B').length;
    let smallCount = history.filter(x => x === 'S').length;

    let prediction, confidence, advice, nums;

    // Pattern logic
    if (bigCount > smallCount) {
        prediction = "SMALL";
        confidence = 60 + Math.floor(Math.random() * 30);
    } else if (smallCount > bigCount) {
        prediction = "BIG";
        confidence = 60 + Math.floor(Math.random() * 30);
    } else {
        prediction = Math.random() > 0.5 ? "BIG" : "SMALL";
        confidence = 50 + Math.floor(Math.random() * 20);
    }

    // Skip logic
    if (confidence < 65) {
        advice = "SKIP ⚠️";
    } else {
        advice = "BET ✅";
    }

    // Number suggestion
    function getRandom(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    if (prediction === "BIG") {
        nums = getRandom(5,9) + " , " + getRandom(5,9);
    } else {
        nums = getRandom(0,4) + " , " + getRandom(0,4);
    }

    document.getElementById("prediction").innerText = "Prediction: " + prediction;
    document.getElementById("confidence").innerText = "Confidence: " + confidence + "%";
    document.getElementById("advice").innerText = "Advice: " + advice;
    document.getElementById("numbers").innerText = "Suggested Numbers: " + nums;
}
</script>

</body>
</html>
