<!DOCTYPE html>
<html>
<head>
<title>BTC AI Realtime</title>
<script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
<style>
body{background:#0a0a0a;color:#fff;font-family:sans-serif;margin:0;padding:20px}
#chart{height:400px}
#ai{background:#1a1a1a;padding:20px;border-radius:10px;margin-top:20px;text-align:center}
#score{font-size:48px;font-weight:bold}
.buy{color:#00ff88} .sell{color:#ff3366}
</style>
</head>
<body>
<h2>BTCUSDT REALTIME + AI</h2>
<div id="chart"></div>
<div id="ai">
  <div>AI SCORE</div>
  <div id="score">Loading...</div>
  <div id="signal">Menghubungkan ke Binance...</div>
</div>

<script>
const chart = LightweightCharts.createChart(document.getElementById('chart'), {
  layout:{bgColor:'#0a0a0a',textColor:'#DDD'},
  grid:{vertLines:{color:'#222'},horzLines:{color:'#222'}}
});
const candle = chart.addCandlestickSeries();

let klines = [];
const ws = new WebSocket('wss://stream.binance.com:9443/ws/btcusdt@kline_1m');
ws.onmessage = (e)=>{
  const k = JSON.parse(e.data).k;
  const data = {time:k.t/1000,open:+k.o,high:+k.h,low:+k.l,close:+k.c};
  candle.update(data);
  klines.push(data);
  if(klines.length>100) klines.shift();
  runAI();
}

function runAI(){
  if(klines.length<20) return;
  const closes = klines.map(k=>k.close);
  const rsi = 50 + Math.random()*30 - 15; // simulasi dulu biar cepet muncul
  const score = rsi > 60 ? 70 : rsi < 40 ? -70 : 0;
  document.getElementById('score').innerText = score;
  document.getElementById('score').className = score>0?'buy':'sell';
  document.getElementById('signal').innerText = score>50?'STRONG BUY':score>0?'BUY':score<-50?'STRONG SELL':'WAIT';
}
</script>
</body>
</html>
