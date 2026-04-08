/sf6-vtuber-site/
  ├─ <!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SF6 VTuberまとめ</title>
<style>
body { font-family: Arial, sans-serif; background:#f5f5f5; margin:0; padding:20px; }
h1 { text-align:center; }
.controls { text-align:center; margin-bottom:20px; }
.controls button, .controls select { margin:0 5px; padding:5px 10px; cursor:pointer; }
.grid { display:grid; grid-template-columns:repeat(auto-fill, minmax(220px,1fr)); gap:20px; }
.vtuber-card { background:white; padding:15px; border-radius:8px; text-align:center; box-shadow:0 2px 6px rgba(0,0,0,0.1);}
.vtuber-card img { border-radius:50%; }
.vtuber-card .vtuber-icon { width:100px; height:100px; margin-bottom:10px; }
.vtuber-card .character-icon { width:50px; height:50px; margin:5px; border-radius:5px; }
.vtuber-card h3 { margin:10px 0 5px; }
.vtuber-card p { margin:3px 0; }
.vtuber-card a { display:inline-block; margin-top:5px; text-decoration:none; color:#0077ff; font-size:14px; }
.character-list { display:flex; justify-content:center; flex-wrap:wrap; margin-top:5px; }
.rank { font-weight:bold; margin-top:5px; }
</style>
</head>
<body>

<h1>SF6 VTuberまとめ</h1>

<div class="controls">
  <button onclick="filterCards('all')">全て</button>
  <button onclick="filterCards('hololive')">ホロライブ</button>
  <button onclick="filterCards('nijisanji')">にじさんじ</button>
  <select id="sortSelect" onchange="sortCards(this.value)">
    <option value="none">並び替え: なし</option>
    <option value="maxMR">最高MR順</option>
    <option value="currentRank">現在ランク順</option>
  </select>
</div>

<div class="grid" id="vtuberGrid"></div>

<script>
// ランク数値化マッピング
const rankValue = {
  "Bronze": 1,
  "Silver": 2,
  "Gold": 3,
  "Platinum": 4,
  "Diamond": 5,
  "Ultra Diamond": 6,
  "Master": 7,
  "Grand Master": 8
};

let vtubers = [];

// GitHub Pagesでも動作するよう相対パスでJSON読み込み
fetch('vtubers.json')
  .then(res => res.json())
  .then(data => {
    vtubers = data;
    renderCards(vtubers);
  });

// カード生成
function renderCards(data) {
  const grid = document.getElementById('vtuberGrid');
  grid.innerHTML = '';
  data.forEach(v => {
    const card = document.createElement('div');
    card.className = 'vtuber-card';
    card.dataset.affiliation = v.affiliation;

    const charIcons = v.characters.map(c => `<img class="character-icon" src="images/${c}" alt="キャラクター">`).join('');

    card.innerHTML = `
      <img class="vtuber-icon" src="images/${v.icon}" alt="${v.name}">
      <h3>${v.name}</h3>
      <p>所属: ${v.affiliation}</p>
      <div class="character-list">${charIcons}</div>
      <p class="rank">現在ランク: ${v.currentRank}</p>
      <p class="rank">最高MR: ${v.maxMR}</p>
      <a href="${v.youtube}" target="_blank">YouTube</a><br>
      <a href="${v.twitter}" target="_blank">Twitter</a>
    `;
    grid.appendChild(card);
  });
}

// フィルタ
function filterCards(affiliation) {
  const filtered = affiliation === 'all' ? vtubers : vtubers.filter(v => v.affiliation === affiliation);
  renderCards(filtered);
}

// 並び替え
function sortCards(criteria) {
  const sorted = [...vtubers];
  if(criteria === 'maxMR') sorted.sort((a,b) => b.maxMR - a.maxMR);
  if(criteria === 'currentRank') sorted.sort((a,b) => (rankValue[b.currentRank]||0) - (rankValue[a.currentRank]||0));
  renderCards(sorted);
}
</script>

</body>
</html>
  ├─ kuzuha
  ├─ https://yt3.googleusercontent.com/ytc/AIdro_kOiA-_aFW-Qz7jxl0wCPDRAKIYL7wDIgs9-iKo7NjztcA=s900-c-k-c0x00ffffff-no-rj
  └─ https://www.streetfighter.com/6/assets/images/character/gouki_akuma/gouki_akuma.png
