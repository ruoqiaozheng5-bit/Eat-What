<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.5, user-scalable=yes">
  <title>🥗 智能每周菜单 · 家常菜版</title>
  <!-- Font Awesome 6 图标库 -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', 'SF Pro Display', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }

    body {
      background: linear-gradient(165deg, #f2f8f0 0%, #e7f0e9 100%);
      min-height: 100vh;
      padding: 1.5rem;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .menu-app {
      max-width: 1600px;
      width: 100%;
      background: rgba(255, 255, 255, 0.75);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border-radius: 3.5rem 3.5rem 2.5rem 2.5rem;
      box-shadow: 0 30px 60px -20px rgba(30, 70, 50, 0.4), inset 0 1px 2px #fff9;
      padding: 2.2rem 2rem 2.2rem;
      border: 1px solid rgba(180, 210, 180, 0.5);
    }

    /* 头部区域 */
    .app-header {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 1.5rem 1rem;
      margin-bottom: 2rem;
    }

    .title-section {
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }

    .title-section i {
      font-size: 2.5rem;
      color: #2b7342;
      filter: drop-shadow(0 4px 6px #b6d7c2);
    }

    h1 {
      font-size: 2rem;
      font-weight: 620;
      background: linear-gradient(130deg, #1f4d31, #3d8b5c);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      letter-spacing: -0.02em;
    }

    .config-panel {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 1rem 1.5rem;
      background: white;
      padding: 0.5rem 1.5rem 0.5rem 1.2rem;
      border-radius: 60px;
      box-shadow: 0 10px 20px -10px #2f5a4470;
      border: 1px solid #bfe0cd;
    }

    .people-counter {
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .people-counter label {
      font-weight: 550;
      color: #1f4d31;
      font-size: 1.1rem;
    }

    .people-counter input {
      width: 70px;
      padding: 0.5rem 0.5rem;
      border: 2px solid #cbe5d6;
      border-radius: 40px;
      text-align: center;
      font-weight: 600;
      font-size: 1.1rem;
      color: #1c4a2e;
      outline: none;
      background: #f6fef9;
    }

    .people-counter input:focus {
      border-color: #469d6e;
      box-shadow: 0 0 0 3px #c1efd4;
    }

    .week-nav {
      display: flex;
      align-items: center;
      background: #ffffffd0;
      border-radius: 60px;
      padding: 0.3rem;
      border: 1px solid #bcddcc;
    }

    .week-nav button {
      width: 2.8rem;
      height: 2.8rem;
      border: none;
      border-radius: 50%;
      background: transparent;
      font-size: 1.4rem;
      color: #286b41;
      cursor: pointer;
      transition: 0.15s;
    }

    .week-nav button:hover {
      background: #daf1e3;
    }

    .week-range {
      font-weight: 550;
      padding: 0 1.2rem;
      font-size: 1.1rem;
      color: #1b4b31;
    }

    .action-buttons {
      display: flex;
      gap: 0.8rem;
    }

    .btn {
      background: white;
      border: none;
      padding: 0.8rem 1.8rem;
      border-radius: 60px;
      font-weight: 600;
      font-size: 1rem;
      display: inline-flex;
      align-items: center;
      gap: 0.6rem;
      box-shadow: 0 8px 16px -10px #27633e;
      cursor: pointer;
      transition: 0.15s;
      border: 1px solid #b1d9c1;
      color: #1f5a37;
    }

    .btn i { color: #388e5c; }
    .btn:hover {
      background: #edfff5;
      border-color: #71b38c;
      transform: scale(1.02) translateY(-2px);
    }

    /* 菜单网格 */
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 1.2rem;
      margin: 2rem 0 1rem;
    }

    .day-card {
      background: white;
      border-radius: 28px;
      padding: 1.5rem 1rem 1.5rem;
      box-shadow: 0 20px 35px -16px #2d5b4270;
      border: 1px solid #e2f0e8;
      transition: 0.2s;
    }

    .day-card:hover {
      transform: translateY(-4px);
      border-color: #abd6be;
    }

    .card-header {
      border-bottom: 2px dashed #cbe3d6;
      padding-bottom: 0.7rem;
      margin-bottom: 1rem;
    }

    .day-name {
      font-size: 1.4rem;
      font-weight: 700;
      color: #1b5535;
      display: flex;
      align-items: center;
      gap: 0.4rem;
    }

    .day-date {
      font-size: 0.9rem;
      color: #678e7a;
    }

    /* 每顿饭区块 */
    .meal-block {
      margin-bottom: 1.2rem;
      border-bottom: 1px dashed #d4eadb;
      padding-bottom: 0.8rem;
    }

    .meal-title {
      font-weight: 600;
      font-size: 1rem;
      color: #54856b;
      letter-spacing: 0.3px;
      display: flex;
      align-items: center;
      gap: 0.3rem;
      margin-bottom: 0.5rem;
      border-left: 5px solid #b0dcc0;
      padding-left: 0.5rem;
    }

    .dish-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0.2rem 0.2rem 0.2rem 0.5rem;
      background: #f9fffc;
      border-radius: 30px;
      margin-bottom: 0.2rem;
      border: 1px solid #e2f0e6;
    }

    .dish-name {
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 0.3rem;
    }

    .dish-name i {
      font-size: 0.8rem;
    }

    .dish-cal {
      font-size: 0.7rem;
      color: #9b6f45;
      background: #fef4e8;
      padding: 0.1rem 0.5rem;
      border-radius: 20px;
      margin-left: 0.4rem;
      white-space: nowrap;
    }

    .meat-icon { color: #b95252 !important; }
    .veg-icon { color: #51a851 !important; }

    .swap-btn {
      background: transparent;
      border: none;
      width: 2rem;
      height: 2rem;
      border-radius: 50%;
      color: #4f8e6c;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.1s;
    }

    .swap-btn:hover {
      background: #def3e7;
      color: #25643b;
    }

    .staple-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-top: 0.3rem;
      padding: 0.2rem 0.2rem 0.2rem 0.5rem;
      background: #f1f9f3;
      border-radius: 30px;
      font-size: 0.9rem;
    }

    .staple-name i { color: #c09b4b; margin-right: 0.3rem; }

    .meal-total {
      font-size: 0.8rem;
      font-weight: 600;
      color: #467a5c;
      text-align: right;
      margin-top: 0.2rem;
      padding-right: 0.3rem;
    }

    .day-total {
      font-size: 0.9rem;
      font-weight: 700;
      color: #265f3b;
      border-top: 2px solid #bde0ce;
      padding-top: 0.5rem;
      margin-top: 0.3rem;
      text-align: center;
    }

    .add-dish-btn {
      width: 100%;
      margin-top: 0.6rem;
      background: #effcf5;
      border: 1px dashed #86ba9b;
      border-radius: 40px;
      padding: 0.4rem;
      color: #2d7a4f;
      font-weight: 500;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.4rem;
      cursor: pointer;
      transition: 0.15s;
      font-size: 0.85rem;
    }

    .add-dish-btn:hover {
      background: #daf5e6;
      border: 1px solid #5baa7c;
    }

    .footer-note {
      margin-top: 2rem;
      text-align: center;
      font-size: 0.9rem;
      color: #739e87;
      border-top: 1px dashed #c0ddce;
      padding-top: 1.5rem;
    }

    @media (max-width: 1100px) {
      .menu-grid { grid-template-columns: repeat(4, 1fr); }
    }
    @media (max-width: 800px) {
      .menu-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
<div class="menu-app">
  <div class="app-header">
    <div class="title-section">
      <i class="fas fa-seedling"></i>
      <h1>家常食单·每周计划</h1>
    </div>

    <div class="config-panel">
      <div class="people-counter">
        <label><i class="fas fa-users"></i> 人数</label>
        <input type="number" id="peopleInput" min="1" max="8" value="3" step="1">
      </div>
      <div class="week-nav">
        <button id="prevWeekBtn"><i class="fas fa-chevron-left"></i></button>
        <span class="week-range" id="weekRange"></span>
        <button id="nextWeekBtn"><i class="fas fa-chevron-right"></i></button>
      </div>
    </div>

    <div class="action-buttons">
      <button class="btn" id="randomAllBtn"><i class="fas fa-dice"></i> 全新菜单</button>
      <button class="btn" id="todayBtn"><i class="fas fa-calendar-check"></i> 本周</button>
    </div>
  </div>

  <div class="menu-grid" id="menuGrid"></div>

  <div class="footer-note">
    <span><i class="fas fa-utensils"></i> 早餐·午餐·晚餐  |  </span>
    <span><i class="fas fa-dragon"></i> 荤(含海鲜)  <i class="fas fa-leaf veg-icon"></i> 素  |  </span>
    <span><i class="fas fa-arrows-rotate"></i> 点击小图标换菜  |  </span>
    <span><i class="fas fa-plus-circle"></i> 加菜自动平衡营养</span>
  </div>
</div>

<script>
(function() {
  // ---------- 家常菜菜品库 ----------
  // 荤菜库 - 家常肉类菜肴 
  const meatDishes = [
    "🍅 番茄炒蛋", "🐔 宫保鸡丁", "🐷 鱼香肉丝", "🥩 红烧肉", "🐔 可乐鸡翅",
    "🐷 糖醋排骨", "🐟 红烧鲫鱼", "🐮 黑椒牛柳", "🐔 黄焖鸡", "🐷 回锅肉",
    "🥟 白菜猪肉炖粉条", "🐔 辣子鸡丁", "🐟 清蒸鲈鱼", "🐷 梅菜扣肉", "🐔 土豆炖鸡块",
    "🐷 蒜香排骨", "🐔 宫保虾球", "🐟 酸菜鱼", "🐮 水煮牛肉", "🐷 京酱肉丝",
    "🍖 红烧排骨", "🐔 葱油鸡", "🐟 剁椒鱼头", "🐮 孜然牛肉", "🐷 粉蒸肉",
    "🍗 照烧鸡腿", "🐟 干烧鱼", "🐔 麻油鸡", "🐷 东坡肉", "🦐 油焖大虾"
  ];

  // 素菜库 - 家常素菜 
  const vegDishes = [
    "🥔 酸辣土豆丝", "🍆 鱼香茄子", "🥬 蒜蓉炒时蔬", "🥒 拍黄瓜", "🍅 西红柿菜花",
    "🥦 清炒西兰花", "🥚 韭菜炒鸡蛋", "🥢 麻婆豆腐", "🍄 蚝油杏鲍菇", "🌽 松仁玉米",
    "🥗 大拌菜", "🥬 香菇油菜", "🍆 地三鲜", "🥔 干锅土豆片", "🥟 素炒豆芽",
    "🥕 胡萝卜炒蛋", "🥒 黄瓜炒鸡蛋", "🍅 番茄菜花", "🥬 醋溜白菜", "🥗 老虎菜",
    "🍲 家常豆腐", "🥢 干煸四季豆", "🥬 蒜蓉空心菜", "🌶️ 虎皮青椒", "🥚 香椿炒鸡蛋",
    "🍆 红烧茄子", "🥬 蚝油生菜", "🥗 果仁菠菜", "🥢 皮蛋豆腐", "🥬 上汤娃娃菜"
  ];

  // 早餐主食
  const breakfastStaple = [ 
    "🥣 燕麦粥", "🍳 煎蛋吐司", "🥟 蒸饺", "🍚 皮蛋瘦肉粥", "🥐 牛角包", 
    "🍠 烤红薯", "🌽 蒸玉米", "🍜 鸡汤面", "🥞 松饼", "🍘 饭团", 
    "🥟 小笼包", "🥟 锅贴", "🫓 葱油饼", "🥣 豆浆油条", "🍚 白粥" 
  ];
  
  const breakfastDrink = [ 
    "🥛 牛奶", "☕ 豆浆", "🍵 绿茶", "🧃 橙汁", "☕ 咖啡", 
    "🥛 酸奶", "🍶 米糊", "🥛 豆奶", "🧋 奶茶", "🍵 红茶" 
  ];
  
  const breakfastExtra = [ 
    "🍎 苹果", "🍌 香蕉", "🥚 水煮蛋", "🥗 蔬菜沙拉", "🧀 芝士片", 
    "🍊 橙子", "🍳 煎蛋", "🍓 草莓", "🥝 猕猴桃", "🍐 梨" 
  ];
  
  const stapleFoods = [ 
    "🍚 米饭", "🍜 面条", "🍲 粥", "🫓 饼", "🥟 饺子", 
    "🍞 包子", "🌮 卷饼", "🍛 杂粮饭", "🍝 意面", "🍚 糙米饭", 
    "🍜 米粉", "🍜 河粉", "🍚 炒饭", "🍜 炒面", "🥟 馄饨" 
  ];

  // ---------- 主料关键词（用于检测同餐冲突）----------
  const mainIngredientKeywords = [
    '蛋', '鸡', '鸭', '鹅', '牛', '羊', '猪', '鱼', '虾', '蟹', 
    '豆腐', '豆干', '土豆', '茄子', '豆角', '黄瓜', '番茄', '白菜', 
    '菜花', '西兰花', '蘑菇', '香菇', '木耳', '豆芽', '粉条', '萝卜', 
    '藕', '青椒', '辣椒', '南瓜', '冬瓜', '苦瓜', '丝瓜', '韭菜', 
    '芹菜', '菠菜', '空心菜', '生菜', '油麦菜', '娃娃菜', '杏鲍菇', '金针菇'
  ];

  // ---------- 辅助函数 ----------
  function hashCode(str) {
    let hash = 0;
    for (let i = 0; i < str.length; i++) {
      hash = ((hash << 5) - hash) + str.charCodeAt(i);
      hash |= 0;
    }
    return Math.abs(hash);
  }

  function getCalories(foodName, type) {
    const base = hashCode(foodName);
    switch (type) {
      case 'meat': return 350 + (base % 200);
      case 'veg': return 150 + (base % 200);
      case 'staple': return 200 + (base % 200);
      case 'breakfastStaple': return 200 + (base % 150);
      case 'breakfastDrink': return 50 + (base % 150);
      case 'breakfastExtra': return 80 + (base % 170);
      default: return 200;
    }
  }

  // 检查一道菜是否与已选菜品冲突（主料重复）
  function isConflicting(candidate, selectedNames) {
    // 完全相同的菜名当然冲突
    if (selectedNames.includes(candidate)) return true;
    
    // 提取候选菜中的关键词
    const candidateKeywords = mainIngredientKeywords.filter(keyword => candidate.includes(keyword));
    if (candidateKeywords.length === 0) return false; // 没有关键词，不检测
    
    // 检查已选菜品是否包含任何相同的关键词
    for (let selected of selectedNames) {
      for (let keyword of candidateKeywords) {
        if (selected.includes(keyword)) {
          return true;
        }
      }
    }
    return false;
  }

  // 从数组中随机取一项，并满足：不超过全局使用次数限制，且不与当前餐已选菜品冲突
  function pickDish(pool, usageCount, existingNames, maxCount = 2, maxAttempts = 100) {
    let attempts = 0;
    while (attempts < maxAttempts) {
      const candidate = pool[Math.floor(Math.random() * pool.length)];
      // 检查全局次数限制
      if (usageCount[candidate] && usageCount[candidate] >= maxCount) continue;
      // 检查餐内冲突
      if (isConflicting(candidate, existingNames)) continue;
      return candidate;
    }
    // 如果尝试多次找不到，放宽限制：忽略冲突，只检查全局次数
    attempts = 0;
    while (attempts < maxAttempts) {
      const candidate = pool[Math.floor(Math.random() * pool.length)];
      if (usageCount[candidate] && usageCount[candidate] >= maxCount) continue;
      return candidate;
    }
    // 如果还是找不到，返回随机（可能会超出次数限制，但概率极低）
    return pool[Math.floor(Math.random() * pool.length)];
  }

  function getMonday(date) {
    const d = new Date(date);
    const day = d.getDay();
    const diff = (day === 0) ? 6 : (day - 1);
    d.setDate(d.getDate() - diff);
    return d;
  }

  // ---------- 全局状态 ----------
  let people = 3;
  let displayMonday = getMonday(new Date());
  let weekMenu = [];

  const peopleInput = document.getElementById('peopleInput');
  const weekRangeEl = document.getElementById('weekRange');
  const menuGridEl = document.getElementById('menuGrid');
  const prevBtn = document.getElementById('prevWeekBtn');
  const nextBtn = document.getElementById('nextWeekBtn');
  const randomAllBtn = document.getElementById('randomAllBtn');
  const todayBtn = document.getElementById('todayBtn');

  function getDishCount() { return people + 1; }
  function targetMeatCount(totalDishes) { return Math.ceil(totalDishes / 2); }

  // 生成一周菜单
  function generateWeekMenu() {
    const dishCount = getDishCount();
    const targetMeat = targetMeatCount(dishCount);
    const targetVeg = dishCount - targetMeat;

    const meatUsage = {}, vegUsage = {};
    meatDishes.forEach(d => meatUsage[d] = 0);
    vegDishes.forEach(d => vegUsage[d] = 0);

    const week = [];
    for (let day = 0; day < 7; day++) {
      const breakfast = {
        staple: breakfastStaple[Math.floor(Math.random() * breakfastStaple.length)],
        drink: breakfastDrink[Math.floor(Math.random() * breakfastDrink.length)],
        extra: breakfastExtra[Math.floor(Math.random() * breakfastExtra.length)]
      };

      // 午餐菜品
      const lunchDishes = [];
      const lunchNames = []; // 用于冲突检测
      
      for (let i = 0; i < targetMeat; i++) {
        let candidate = pickDish(meatDishes, meatUsage, lunchNames, 2);
        meatUsage[candidate] = (meatUsage[candidate] || 0) + 1;
        lunchDishes.push({ name: candidate, type: 'meat' });
        lunchNames.push(candidate);
      }
      for (let i = 0; i < targetVeg; i++) {
        let candidate = pickDish(vegDishes, vegUsage, lunchNames, 2);
        vegUsage[candidate] = (vegUsage[candidate] || 0) + 1;
        lunchDishes.push({ name: candidate, type: 'veg' });
        lunchNames.push(candidate);
      }
      lunchDishes.sort(() => Math.random() - 0.5);
      const lunchStaple = stapleFoods[Math.floor(Math.random() * stapleFoods.length)];

      // 晚餐菜品
      const dinnerDishes = [];
      const dinnerNames = [];
      
      for (let i = 0; i < targetMeat; i++) {
        let candidate = pickDish(meatDishes, meatUsage, dinnerNames, 2);
        meatUsage[candidate] = (meatUsage[candidate] || 0) + 1;
        dinnerDishes.push({ name: candidate, type: 'meat' });
        dinnerNames.push(candidate);
      }
      for (let i = 0; i < targetVeg; i++) {
        let candidate = pickDish(vegDishes, vegUsage, dinnerNames, 2);
        vegUsage[candidate] = (vegUsage[candidate] || 0) + 1;
        dinnerDishes.push({ name: candidate, type: 'veg' });
        dinnerNames.push(candidate);
      }
      dinnerDishes.sort(() => Math.random() - 0.5);
      const dinnerStaple = stapleFoods[Math.floor(Math.random() * stapleFoods.length)];

      week.push({ breakfast, lunch: { dishes: lunchDishes, staple: lunchStaple }, dinner: { dishes: dinnerDishes, staple: dinnerStaple } });
    }
    return week;
  }

  function refreshWeek() { weekMenu = generateWeekMenu(); render(); }

  function sumMealCalories(meal) {
    let total = 0;
    if (meal.dishes) meal.dishes.forEach(d => total += getCalories(d.name, d.type));
    if (meal.staple) total += getCalories(meal.staple, 'staple');
    return total;
  }

  function sumBreakfastCalories(bf) {
    return getCalories(bf.staple, 'breakfastStaple') + getCalories(bf.drink, 'breakfastDrink') + getCalories(bf.extra, 'breakfastExtra');
  }

  // 渲染菜单
  function render() {
    const monday = new Date(displayMonday);
    const sunday = new Date(monday);
    sunday.setDate(monday.getDate() + 6);
    const y1 = monday.getFullYear(), m1 = monday.getMonth()+1, d1 = monday.getDate();
    const y2 = sunday.getFullYear(), m2 = sunday.getMonth()+1, d2 = sunday.getDate();
    let rangeText = (y1 === y2) ? `${y1}年 ${m1}月${d1}日 - ${m2}月${d2}日` : `${y1}年${m1}月${d1}日 - ${y2}年${m2}月${d2}日`;
    weekRangeEl.textContent = rangeText;

    const dayNames = ['周一', '周二', '周三', '周四', '周五', '周六', '周日'];
    let html = '';
    
    for (let i = 0; i < 7; i++) {
      const dayData = weekMenu[i];
      if (!dayData) continue;
      
      const currentDate = new Date(monday);
      currentDate.setDate(monday.getDate() + i);
      const dateLabel = `${currentDate.getMonth()+1}/${currentDate.getDate()}`;

      const bfCals = sumBreakfastCalories(dayData.breakfast);
      const lunchCals = sumMealCalories(dayData.lunch);
      const dinnerCals = sumMealCalories(dayData.dinner);
      const dayTotalCals = bfCals + lunchCals + dinnerCals;

      const bfPerPerson = Math.round(bfCals / people);
      const lunchPerPerson = Math.round(lunchCals / people);
      const dinnerPerPerson = Math.round(dinnerCals / people);
      const dayPerPerson = Math.round(dayTotalCals / people);

      const lunchDishesHtml = dayData.lunch.dishes.map((dish, idx) => `
        <div class="dish-item" data-day="${i}" data-meal="lunch" data-index="${idx}">
          <span class="dish-name"><i class="fas ${dish.type === 'meat' ? 'fa-drumstick-bite meat-icon' : 'fa-leaf veg-icon'}"></i> ${dish.name} <span class="dish-cal">${getCalories(dish.name, dish.type)} kcal</span></span>
          <button class="swap-btn" data-swap="dish"><i class="fas fa-rotate-right"></i></button>
        </div>
      `).join('');
      
      const dinnerDishesHtml = dayData.dinner.dishes.map((dish, idx) => `
        <div class="dish-item" data-day="${i}" data-meal="dinner" data-index="${idx}">
          <span class="dish-name"><i class="fas ${dish.type === 'meat' ? 'fa-drumstick-bite meat-icon' : 'fa-leaf veg-icon'}"></i> ${dish.name} <span class="dish-cal">${getCalories(dish.name, dish.type)} kcal</span></span>
          <button class="swap-btn" data-swap="dish"><i class="fas fa-rotate-right"></i></button>
        </div>
      `).join('');

      html += `
        <div class="day-card">
          <div class="card-header">
            <span class="day-name"><i class="fas fa-calendar-alt"></i>${dayNames[i]}</span>
            <span class="day-date">${dateLabel}</span>
          </div>
          <!-- 早餐 -->
          <div class="meal-block">
            <div class="meal-title"><i class="fas fa-sun"></i> 早餐</div>
            <div class="breakfast-items">
              <div class="dish-item" data-day="${i}" data-meal="bf-staple">
                <span class="dish-name"><i class="fas fa-bread-slice"></i> ${dayData.breakfast.staple} <span class="dish-cal">${getCalories(dayData.breakfast.staple, 'breakfastStaple')} kcal</span></span>
                <button class="swap-btn" data-swap="bfStaple"><i class="fas fa-rotate-right"></i></button>
              </div>
              <div class="dish-item" data-day="${i}" data-meal="bf-drink">
                <span class="dish-name"><i class="fas fa-mug-hot"></i> ${dayData.breakfast.drink} <span class="dish-cal">${getCalories(dayData.breakfast.drink, 'breakfastDrink')} kcal</span></span>
                <button class="swap-btn" data-swap="bfDrink"><i class="fas fa-rotate-right"></i></button>
              </div>
              <div class="dish-item" data-day="${i}" data-meal="bf-extra">
                <span class="dish-name"><i class="fas fa-apple-alt"></i> ${dayData.breakfast.extra} <span class="dish-cal">${getCalories(dayData.breakfast.extra, 'breakfastExtra')} kcal</span></span>
                <button class="swap-btn" data-swap="bfExtra"><i class="fas fa-rotate-right"></i></button>
              </div>
            </div>
            <div class="meal-total">早餐人均: ${bfPerPerson} kcal</div>
          </div>
          <!-- 午餐 -->
          <div class="meal-block">
            <div class="meal-title"><i class="fas fa-cloud-sun"></i> 午餐 · ${dayData.lunch.dishes.length}道</div>
            ${lunchDishesHtml}
            <div class="staple-row" data-day="${i}" data-meal="lunch-staple">
              <span class="staple-name"><i class="fas fa-utensil-spoon"></i> 主食: ${dayData.lunch.staple} <span class="dish-cal">${getCalories(dayData.lunch.staple, 'staple')} kcal</span></span>
              <button class="swap-btn" data-swap="lunchStaple"><i class="fas fa-rotate-right"></i></button>
            </div>
            <div class="meal-total">午餐人均: ${lunchPerPerson} kcal</div>
            <div class="add-dish-btn" data-day="${i}" data-meal="lunch"><i class="fas fa-plus-circle"></i> 加一道菜</div>
          </div>
          <!-- 晚餐 -->
          <div class="meal-block">
            <div class="meal-title"><i class="fas fa-moon"></i> 晚餐 · ${dayData.dinner.dishes.length}道</div>
            ${dinnerDishesHtml}
            <div class="staple-row" data-day="${i}" data-meal="dinner-staple">
              <span class="staple-name"><i class="fas fa-utensil-spoon"></i> 主食: ${dayData.dinner.staple} <span class="dish-cal">${getCalories(dayData.dinner.staple, 'staple')} kcal</span></span>
              <button class="swap-btn" data-swap="dinnerStaple"><i class="fas fa-rotate-right"></i></button>
            </div>
            <div class="meal-total">晚餐人均: ${dinnerPerPerson} kcal</div>
            <div class="add-dish-btn" data-day="${i}" data-meal="dinner"><i class="fas fa-plus-circle"></i> 加一道菜</div>
          </div>
          <div class="day-total">📊 日人均总计: ${dayPerPerson} kcal</div>
        </div>
      `;
    }
    menuGridEl.innerHTML = html;
  }

  // 换菜逻辑（带冲突检测）
  function handleSwap(day, meal, indexOrType) {
    const dayData = weekMenu[day];
    
    // 重新构建 usage 统计（简化，直接使用全局统计，为了保持一致性，我们重新统计当前所有菜品使用次数）
    const meatUsage = {}, vegUsage = {};
    meatDishes.forEach(d => meatUsage[d] = 0);
    vegDishes.forEach(d => vegUsage[d] = 0);
    
    weekMenu.forEach(d => {
      d.lunch.dishes.forEach(dd => {
        if (dd.type === 'meat') meatUsage[dd.name] = (meatUsage[dd.name] || 0) + 1;
        else vegUsage[dd.name] = (vegUsage[dd.name] || 0) + 1;
      });
      d.dinner.dishes.forEach(dd => {
        if (dd.type === 'meat') meatUsage[dd.name] = (meatUsage[dd.name] || 0) + 1;
        else vegUsage[dd.name] = (vegUsage[dd.name] || 0) + 1;
      });
    });

    if (meal === 'bfStaple') {
      dayData.breakfast.staple = breakfastStaple[Math.floor(Math.random() * breakfastStaple.length)];
    } else if (meal === 'bfDrink') {
      dayData.breakfast.drink = breakfastDrink[Math.floor(Math.random() * breakfastDrink.length)];
    } else if (meal === 'bfExtra') {
      dayData.breakfast.extra = breakfastExtra[Math.floor(Math.random() * breakfastExtra.length)];
    } else if (meal === 'lunchStaple') {
      dayData.lunch.staple = stapleFoods[Math.floor(Math.random() * stapleFoods.length)];
    } else if (meal === 'dinnerStaple') {
      dayData.dinner.staple = stapleFoods[Math.floor(Math.random() * stapleFoods.length)];
    } else if (meal === 'lunch' && typeof indexOrType === 'number') {
      const dish = dayData.lunch.dishes[indexOrType];
      // 获取该餐已选的其他菜品名（排除自己）
      const otherNames = dayData.lunch.dishes.map((d, idx) => idx === indexOrType ? null : d.name).filter(Boolean);
      // 减少原菜品的计数
      if (dish.type === 'meat') meatUsage[dish.name]--;
      else vegUsage[dish.name]--;
      
      const usage = dish.type === 'meat' ? meatUsage : vegUsage;
      const pool = dish.type === 'meat' ? meatDishes : vegDishes;
      
      // 选择新菜，考虑冲突和次数
      const newName = (() => {
        let attempts = 0;
        while (attempts < 100) {
          const candidate = pool[Math.floor(Math.random() * pool.length)];
          if (usage[candidate] && usage[candidate] >= 2) continue; // 全局次数限制
          if (isConflicting(candidate, otherNames)) continue;
          return candidate;
        }
        // 降级：忽略冲突，只检查次数
        attempts = 0;
        while (attempts < 100) {
          const candidate = pool[Math.floor(Math.random() * pool.length)];
          if (usage[candidate] && usage[candidate] >= 2) continue;
          return candidate;
        }
        return pool[Math.floor(Math.random() * pool.length)];
      })();
      
      if (dish.type === 'meat') meatUsage[newName] = (meatUsage[newName] || 0) + 1;
      else vegUsage[newName] = (vegUsage[newName] || 0) + 1;
      
      dish.name = newName;
    } else if (meal === 'dinner' && typeof indexOrType === 'number') {
      const dish = dayData.dinner.dishes[indexOrType];
      const otherNames = dayData.dinner.dishes.map((d, idx) => idx === indexOrType ? null : d.name).filter(Boolean);
      if (dish.type === 'meat') meatUsage[dish.name]--;
      else vegUsage[dish.name]--;
      
      const usage = dish.type === 'meat' ? meatUsage : vegUsage;
      const pool = dish.type === 'meat' ? meatDishes : vegDishes;
      
      const newName = (() => {
        let attempts = 0;
        while (attempts < 100) {
          const candidate = pool[Math.floor(Math.random() * pool.length)];
          if (usage[candidate] && usage[candidate] >= 2) continue;
          if (isConflicting(candidate, otherNames)) continue;
          return candidate;
        }
        attempts = 0;
        while (attempts < 100) {
          const candidate = pool[Math.floor(Math.random() * pool.length)];
          if (usage[candidate] && usage[candidate] >= 2) continue;
          return candidate;
        }
        return pool[Math.floor(Math.random() * pool.length)];
      })();
      
      if (dish.type === 'meat') meatUsage[newName] = (meatUsage[newName] || 0) + 1;
      else vegUsage[newName] = (vegUsage[newName] || 0) + 1;
      
      dish.name = newName;
    }
    render();
  }

  function addDish(day, mealType) {
    const dayData = weekMenu[day];
    const targetMeal = mealType === 'lunch' ? dayData.lunch : dayData.dinner;
    const dishCount = targetMeal.dishes.length + 1;
    const targetMeat = targetMeatCount(dishCount);
    const currentMeat = targetMeal.dishes.filter(d => d.type === 'meat').length;
    
    let newType = 'veg';
    if (currentMeat < targetMeat) newType = 'meat';
    else if (currentMeat > targetMeat) newType = 'veg';
    else newType = Math.random() < 0.5 ? 'meat' : 'veg';

    // 统计当前全局使用次数
    const meatUsage = {}, vegUsage = {};
    meatDishes.forEach(d => meatUsage[d] = 0);
    vegDishes.forEach(d => vegUsage[d] = 0);
    
    weekMenu.forEach(d => {
      d.lunch.dishes.forEach(dd => {
        if (dd.type === 'meat') meatUsage[dd.name] = (meatUsage[dd.name] || 0) + 1;
        else vegUsage[dd.name] = (vegUsage[dd.name] || 0) + 1;
      });
      d.dinner.dishes.forEach(dd => {
        if (dd.type === 'meat') meatUsage[dd.name] = (meatUsage[dd.name] || 0) + 1;
        else vegUsage[dd.name] = (vegUsage[dd.name] || 0) + 1;
      });
    });

    const pool = newType === 'meat' ? meatDishes : vegDishes;
    const usage = newType === 'meat' ? meatUsage : vegUsage;
    const otherNames = targetMeal.dishes.map(d => d.name);
    
    const newName = (() => {
      let attempts = 0;
      while (attempts < 100) {
        const candidate = pool[Math.floor(Math.random() * pool.length)];
        if (usage[candidate] && usage[candidate] >= 2) continue;
        if (isConflicting(candidate, otherNames)) continue;
        return candidate;
      }
      attempts = 0;
      while (attempts < 100) {
        const candidate = pool[Math.floor(Math.random() * pool.length)];
        if (usage[candidate] && usage[candidate] >= 2) continue;
        return candidate;
      }
      return pool[Math.floor(Math.random() * pool.length)];
    })();
    
    targetMeal.dishes.push({ name: newName, type: newType });
    render();
  }

  // 事件绑定
  menuGridEl.addEventListener('click', (e) => {
    const swapBtn = e.target.closest('.swap-btn');
    const addBtn = e.target.closest('.add-dish-btn');
    
    if (swapBtn) {
      const dishItem = swapBtn.closest('[data-day]');
      if (!dishItem) return;
      const day = parseInt(dishItem.dataset.day);
      const meal = dishItem.dataset.meal;
      if (meal === 'lunch' || meal === 'dinner') {
        const index = dishItem.dataset.index;
        if (index !== undefined) handleSwap(day, meal, parseInt(index));
      } else {
        handleSwap(day, meal);
      }
    } else if (addBtn) {
      const day = parseInt(addBtn.dataset.day);
      const meal = addBtn.dataset.meal;
      addDish(day, meal);
    }
  });

  peopleInput.addEventListener('input', (e) => {
    let val = parseInt(e.target.value);
    if (isNaN(val) || val < 1) val = 1;
    if (val > 8) val = 8;
    people = val;
    peopleInput.value = val;
    refreshWeek();
  });

  prevBtn.addEventListener('click', () => {
    displayMonday.setDate(displayMonday.getDate() - 7);
    refreshWeek();
  });
  
  nextBtn.addEventListener('click', () => {
    displayMonday.setDate(displayMonday.getDate() + 7);
    refreshWeek();
  });
  
  todayBtn.addEventListener('click', () => {
    displayMonday = getMonday(new Date());
    refreshWeek();
  });
  
  randomAllBtn.addEventListener('click', () => refreshWeek());

  // 初始化
  weekMenu = generateWeekMenu();
  render();
})();
</script>
</body>
</html>
