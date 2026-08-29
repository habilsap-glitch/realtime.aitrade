<!DOCTYPE html>
<html>
<head>
<title>BTC AI ALERT</title>
<style>
body{background:#0D1117;color:#fff;font-family:Arial;padding:20px;text-align:center}
h1{color:#f2a900}
.box{background:#161b22;padding:30px;border-radius:15px;margin:20px auto;max-width:500px}
#score{font-size:80px;font-weight:bold}
.buy{color:#00ff88} .sell{color:#ff3366}
</style>
</head>
<body>
<h1>🚨 BTCUSDT AI ANALYSIS 🚨</h1>

<!-- CHART DARI TRADINGVIEW GRATIS -->
<div class="tradingview-widget-container">
<div id="tradingview_123"></div>
<script type="text/javascript" src="https://s3.tradingview.com/tv.js"></script>
<script>
new TradingView.widget({
  "container_id": "tradingview_123",
  "symbol": "BINANCE:BTCUSDT",
  "theme": "dark",
  "autosize": true,
  "interval": "1"
});
</script>
</div>

<!-- AI SCORE -->
<div class="box">
  <h2>AI SCORE</h2>
  <div id="score" class="buy">+72</div>
  <h3 id="signal">BUY</h3>
  <p id="reason">RSI Oversold + Support Kuat</p>
</div>

<script>
// AI SIMULASI BIAR LANGSUNG JALAN
setInterval(()=>{
  let score = Math.floor(Math.random()*200-100);
  document.getElementById('score').innerText = score>0?'+score:score;
  document.getElementById('score').className = score>0?'buy':'sell';
  document.getElementById('signal').innerText = score>50?'STRONG BUY':score>0?'BUY':score<-50?'STRONG SELL':score<0?'SELL':'WAIT';
  if(score>0) new Audio('https://www.soundjay.com/buttons/sounds/button-4.mp3').play();
  if(score<0) new Audio('https://www.soundjay.com/buttons/sounds/button-10.mp3').play();
},8000);
</script>
</body>
</html>
