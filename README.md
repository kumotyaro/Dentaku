# Dentaku
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <title>旗コスト時間計算機</title>
  <style>
    body {
      font-family: sans-serif;
      padding: 30px;
      max-width: 600px;
      margin: auto;
      background-color: #fff9db;
      font-size: 18px;
    }
    h2 {
      text-align: center;
      margin-bottom: 30px;
      font-size: 26px;
    }
    .row {
      display: flex;
      align-items: center;
      margin-bottom: 25px;
    }
    .label {
      width: 70px;
      font-weight: bold;
      font-size: 20px;
      margin-right: 10px;
    }
    .gain-box {
      width: 140px;
      height: 48px;
      background-color: #eee;
      text-align: center;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 6px;
      font-size: 16px;
      margin-right: 10px;
      flex-shrink: 0;
    }
    input[type=number] {
      flex: 1;
      padding: 12px;
      font-size: 18px;
      border: 2px solid #ccc;
      border-radius: 6px;
      text-align: right;
    }
    input::placeholder {
      text-align: right;
      color: #aaa;
    }
    button {
      margin-top: 30px;
      padding: 14px;
      width: 100%;
      font-size: 20px;
      background-color: #f4a261;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background-color: #e07b3f;
    }
    .result {
      margin-top: 30px;
      font-weight: bold;
      white-space: pre-line;
      font-size: 20px;
    }
    .positive { color: green; }
    .negative { color: red; }
  </style>
</head>
<body>

<h2>旗コスト時間計算機</h2>

<!-- 木材 -->
<div class="row">
  <div class="label">木材</div>
  <div class="gain-box">151,800 /時</div>
  <input type="number" id="cost_wood" placeholder="旗コスト量（木材）" />
</div>

<!-- 食糧 -->
<div class="row">
  <div class="label">食糧</div>
  <div class="gain-box">151,800 /時</div>
  <input type="number" id="cost_food" placeholder="旗コスト量（食糧）" />
</div>

<!-- 石材 -->
<div class="row">
  <div class="label">石材</div>
  <div class="gain-box">101,200 /時</div>
  <input type="number" id="cost_stone" placeholder="旗コスト量（石材）" />
</div>

<!-- 鉄鉱 -->
<div class="row">
  <div class="label">鉄鉱</div>
  <div class="gain-box">55,200 /時</div>
  <input type="number" id="cost_iron" placeholder="旗コスト量（鉄鉱）" />
</div>

<button onclick="calculate()">計算</button>

<div id="result" class="result"></div>

<script>
// 入手量（毎時）を新しい数値に更新
const gains = {
  wood: 151800,
  food: 151800,
  stone: 101200,
  iron: 55200,
};

function calculate() {
  const get = id => {
    const val = document.getElementById(id).value;
    return val ? Number(val) : null;
  };

  const costs = {
    wood: get('cost_wood'),
    food: get('cost_food'),
    stone: get('cost_stone'),
    iron: get('cost_iron'),
  };

  let output = '';
  for (const key of ['wood', 'food', 'stone', 'iron']) {
    const label = toLabel(key);
    const cost = costs[key];
    const gainPerMin = gains[key] / 60;

    if (cost === null || isNaN(cost) || cost <= 0) {
      output += `${label}: 入力なし\n`;
      continue;
    }

    const minutes = Math.ceil(cost / gainPerMin);
    output += `${label}: 約 ${minutes} 分かかります\n`;
  }

  document.getElementById('result').innerHTML = output.replace(/\n/g, '<br>');
}

function toLabel(key) {
  return { wood: '木材', food: '食糧', stone: '石材', iron: '鉄鉱' }[key];
}
</script>

</body>
</html>
