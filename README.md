<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>北笙的小网页</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,sans-serif}
body{background:#f2f2f2;color:#333}
.page{display:none;padding:20px 0 100px;height:100vh;overflow:auto}
.page.active{display:block}
.main-content{text-align:center;padding:60px 20px}
.main-content h1{font-size:28px;margin-bottom:12px}
.main-content a{color:#0066ff;text-decoration:underline}
.description{font-size:16px;color:#666;margin-bottom:40px}
.buttons{display:flex;flex-direction:column;gap:16px;max-width:400px;margin:0 auto}
.buttons button{padding:18px 0;border:none;border-radius:12px;background:#4caf50;color:white;font-size:18px}
.footer{text-align:center;margin-top:60px;padding:20px;color:#666}
.footer a{color:#4caf50}
.scroll-container{padding:20px}
h1{text-align:center;margin-bottom:24px;font-size:24px}
.container{max-width:400px;margin:0 auto}
.input-section{margin-bottom:28px}
.input-section h3{font-size:16px;margin-bottom:10px;display:flex;justify-content:space-between;align-items:center}
.item-list{display:flex;flex-direction:column;gap:8px}
.item-row{display:flex;gap:8px}
.item-row input{flex:1;padding:10px;border:1px solid #ddd;border-radius:8px}
.item-row button{padding:0 12px;background:#ff4444;color:white;border:none;border-radius:8px}
.small{padding:6px 10px;font-size:12px;background:#0066ff;color:white;border:none;border-radius:6px}
.range-group{display:flex;flex-direction:column;gap:10px}
.range-row{display:flex;align-items:center;gap:10px}
.range-row label{width:80px}
.range-row input{flex:1;padding:8px;border:1px solid #ddd;border-radius:8px;width:100px}
.hint-text{font-size:12px;color:#666;margin-top:6px}
.toggle-section{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}
.switch{position:relative;width:40px;height:24px}
.switch input{opacity:0;width:0;height:0}
.slider{position:absolute;cursor:pointer;top:0;left:0;right:0;bottom:0;background:#ccc;border-radius:24px}
.slider:before{position:absolute;content:"";height:18px;width:18px;left:3px;bottom:3px;background:white;border-radius:50%}
input:checked+.slider{background:#4caf50}
input:checked+.slider:before{transform:translateX(16px)}
.sub-settings{margin-top:10px;padding-left:10px;border-left:2px solid #eee}
.result-container{background:white;padding:20px;border-radius:12px;min-height:120px;white-space:pre-line}
.action-buttons{position:fixed;bottom:20px;left:0;right:0;display:flex;gap:10px;padding:0 20px;max-width:400px;margin:0 auto}
.action-buttons button{flex:1;padding:16px 0;border:none;border-radius:12px;background:#4caf50;color:white;font-size:16px}
button.secondary{background:#888}
.game-info{display:flex;gap:10px;margin-bottom:20px}
.info-box{flex:1;background:white;padding:12px;border-radius:12px;text-align:center}
.tools-list{min-height:40px;padding-top:6px}
.back-btn{background:#888!important}
</style>
</head>
<body>
<div id="main-page" class="page active">
  <div class="main-content">
    <h1><a href="https://x.com/jin_chuan89117" target="_blank">北笙</a>的小网页</h1>
    <p class="description">点关注不迷路有问题可私信反馈</p>
    <div class="buttons">
      <button id="randomPreset">随机露出任务</button>
      <button id="customSP">自定义SP</button>
      <button id="movementGame">脱衣移动游戏</button>
    </div>
  </div>
  <div class="footer">
    <p>QQ 2014736291 <a href="https://t.me/+UXRLfaf1cyAyNjRl" target="_blank">点击转跳至TG频道</a></p>
  </div>
</div>

<div id="settings-page" class="page">
  <div class="scroll-container">
    <h1>自定义惩罚设置</h1>
    <div class="container">
      <div class="input-section">
        <h3>道具设置 <button class="small add-btn" id="addTool">+ 添加</button></h3>
        <div class="item-list" id="toolsList"></div>
      </div>
      <div class="input-section">
        <h3>部位设置 <button class="small add-btn" id="addBodyPart">+ 添加</button></h3>
        <div class="item-list" id="bodyPartsList"></div>
      </div>
      <div class="input-section">
        <h3>数量范围</h3>
        <div class="range-group">
          <div class="range-row"><label>最小值:</label> <input type="number" id="minCount" min="1" value="1"></div>
          <div class="range-row"><label>最大值:</label> <input type="number" id="maxCount" min="1" value="3"></div>
        </div>
      </div>
      <div class="input-section">
        <h3>强度范围 (1-10)</h3>
        <div class="range-group">
          <div class="range-row"><label>最小值:</label> <input type="number" id="minStrength" min="1" max="10" value="3"></div>
          <div class="range-row"><label>最大值:</label> <input type="number" id="maxStrength" min="1" max="10" value="8"></div>
        </div>
      </div>
      <div class="input-section">
        <h3>生成条数</h3>
        <input type="number" id="resultCount" min="1" value="5">
        <div id="maxPossible" class="hint-text"></div>
      </div>
    </div>
  </div>
  <div class="action-buttons">
    <button id="generatePresetResult">生成惩罚</button>
    <button class="back-btn" id="backFromSettings">返回</button>
  </div>
</div>

<div id="movement-settings" class="page">
  <div class="scroll-container">
    <h1>脱衣移动游戏设置</h1>
    <p class="description">点击下方按钮添加/删除，折叠后不执行该功能</p>
    <div class="container">
      <div class="input-section">
        <h3>衣物设置 <button class="small add-btn" id="addMovementTool">+ 添加</button></h3>
        <div class="item-list" id="movementToolsList"></div>
      </div>
      <div class="input-section">
        <div class="toggle-section">
          <h3><span>事件设置</span></h3>
          <button class="small add-btn" id="addAction">+ 添加</button>
        </div>
        <div class="item-list" id="actionsList"></div>
        <div id="actionSettings" class="sub-settings">
          <div class="input-section">
            <h3>事件触发设置</h3>
            <div class="range-group">
              <div class="range-row"><label>触发概率:</label> <input type="number" id="actionRate" min="0" max="100" value="30">%</div>
            </div>
          </div>
          <div class="input-section">
            <h3>事件执行时间</h3>
            <div class="range-group">
              <div class="range-row"><label>最短:</label> <input type="number" id="minActionTime" min="1" value="5">秒</div>
              <div class="range-row"><label>最长:</label> <input type="number" id="maxActionTime" min="1" value="15">秒</div>
            </div>
          </div>
        </div>
      </div>
      <div class="input-section">
        <div class="toggle-section">
          <h3><span>穿脱概率</span></h3>
        </div>
        <div id="probabilitySettings" class="sub-settings">
          <div class="range-group">
            <div class="range-row"><label>脱下概率:</label> <input type="number" id="dropRate" min="1" max="100" value="60">%</div>
            <div class="range-row"><label>穿戴概率:</label> <input type="number" id="pickupRate" min="1" max="100" value="40">%</div>
          </div>
        </div>
      </div>
      <div class="input-section">
        <h3>移动范围</h3>
        <div class="range-group">
          <div class="range-row"><label>最少步数:</label> <input type="number" id="minDistance" min="1" value="1">步</div>
          <div class="range-row"><label>最大步数:</label> <input type="number" id="maxDistance" min="1" value="5">步</div>
        </div>
      </div>
    </div>
  </div>
  <div class="action-buttons">
    <button id="startMovementGame">开始游戏</button>
    <button class="back-btn" id="backFromMovementSettings">返回</button>
  </div>
</div>

<div id="sp-result-page" class="page">
  <div class="scroll-container">
    <h1>惩罚结果</h1>
    <div class="result-container" id="spResult"></div>
  </div>
  <div class="action-buttons">
    <button id="regenerateSP">再次生成</button>
    <button class="back-btn" id="backFromSPResult">返回主页面</button>
  </div>
</div>

<div id="exposure-result-page" class="page">
  <div class="scroll-container">
    <h1>随机露出任务</h1>
    <div class="result-container" id="exposureResult"></div>
  </div>
  <div class="action-buttons">
    <button id="regenerateExposure">再次生成</button>
    <button class="back-btn" id="backFromExposureResult">返回主页面</button>
  </div>
</div>

<div id="movement-game" class="page">
  <div class="scroll-container">
    <h1>脱衣移动游戏</h1>
    <p class="description">非时间限制事件可忽略时间，没路可以适当拐弯</p>
    <div class="game-info">
      <div class="info-box"><h3>剩余</h3><div id="remainingTools" class="tools-list"></div></div>
      <div class="info-box"><h3>待拾</h3><div id="droppedTools" class="tools-list"></div></div>
    </div>
    <div class="result-container" id="gameOutput"></div>
  </div>
  <div class="action-buttons">
    <button id="nextStep">下一步</button>
    <button id="backFromGame" class="secondary">返回</button>
  </div>
</div>

<script>
// 页面切换
function showPage(id){document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));document.getElementById(id).classList.add('active')}
document.getElementById('customSP').onclick=()=>showPage('settings-page')
document.getElementById('randomPreset').onclick=()=>{genExposure();showPage('exposure-result-page')}
document.getElementById('movementGame').onclick=()=>showPage('movement-settings')
document.getElementById('backFromSettings').onclick=()=>showPage('main-page')
document.getElementById('backFromMovementSettings').onclick=()=>showPage('main-page')
document.getElementById('backFromSPResult').onclick=()=>showPage('main-page')
document.getElementById('backFromExposureResult').onclick=()=>showPage('main-page')
document.getElementById('backFromGame').onclick=()=>showPage('main-page')

// 添加项目
function makeItem(listId,placeholder){
  const list=document.getElementById(listId)
  const div=document.createElement('div')
  div.className='item-row'
  div.innerHTML=`<input placeholder="${placeholder}"><button class="del">删除</button>`
  div.querySelector('.del').onclick=()=>div.remove()
  list.appendChild(div)
}
document.getElementById('addTool').onclick=()=>makeItem('toolsList','例如：尺子')
document.getElementById('addBodyPart').onclick=()=>makeItem('bodyPartsList','例如：手心')
document.getElementById('addMovementTool').onclick=()=>makeItem('movementToolsList','例如：外套')
document.getElementById('addAction').onclick=()=>makeItem('actionsList','例如：原地跳')

// 获取列表值
function getList(listId){
  const arr=[]
  document.querySelectorAll(`#${listId} input`).forEach(i=>{if(i.value.trim())arr.push(i.value.trim())})
  return arr
}

// 随机数
function rnd(min,max){return Math.floor(Math.random()*(max-min+1))+min}

// 随机露出
function genExposure(){
  const tasks=[
    "在窗边站立1分钟",
    "开门外站30秒",
    "走廊快速走一圈",
    "楼下取快递不遮挡",
"坐火车卧铺，脱至全裸后，将外套盖在身上 ",
    "无内穿浅色衬衫，喝饮料时不小心撒到胸部",
    "脱剩一条内裤，用手挡住胸部跑回家",
    "塞入肛门拉珠，点外卖，让外面员帮忙扯出拉珠",
    "将假阳具放在公园长椅上自慰",
    "出门一小时后脱下内裤",
    "塞上跳蛋，人越多挡位调的越高",
    "佩戴远程遥控玩具，将遥控链接和插入的照片一起发送给主人",
    "在单元门口脱剩一条内裤，用手挡住胸部跑回家",
    "穿情趣制服将手铐在背后开门等待外将外卖放到手上",
    "无内带铃铛肛塞摇晃屁股",
    "无罩佩戴铃铛乳夹摇晃胸部",
    "去一次天体沙滩",
    "去便利店购物时用现金结账，将现金放在乳沟里",
    "脱至全裸后将衣物叠好放在背上爬行",
    "公共男厕内敞开隔间门蒙眼1分钟",
    "前往公共男厕撒尿",
    "餐厅吃饭时边自慰边吃饭",
    "在公共场所将短裙当裤子提起",
    "将自己裸照设为手机屏保",
    "佩戴铃铛肛塞出门",
    "在电梯内解开所有衣服扣子，不露点",
    "买一个假阳具，快递到快递柜时取出，就近将阳具塞入小穴带回",
    "将假阳具塞到穴内出门一天",
    "露出胸罩对路人挺胸展示胸部",
    "在户外有人场景，将衣领下拉至露点",
    "在单元门口脱剩一件内衣，用手挡住跑回家",
    "使用大头贴机露出胸部拍照",
    "穿裙子无内对路人摇晃屁股",
    "购买情趣内衣并拍照上传买家秀",
    "浅色外套深色内衣裤度过一天",
    "在拥挤的公交/地铁上站着用手自慰一站",
    "凌晨全裸出门倒垃圾",
    "在户外角落掀起衣服撒尿",
    "公厕隔间内脱光衣物，走出隔间自慰高潮后穿回衣物可选择凌晨",
    "夜间全裸上街允许出门穿一个外套但是要完整全裸走完3分钟",
    "在阳台全裸展示自己",
    "全天佩戴跳蛋抵档出门，高潮一次脱一件衣服控制权在主人手上可随时遥控",
    "乘坐公交车，坐在最后一排自慰",
    "将内衣内裤剪出洞让阴蒂乳头从洞中露出",
    "将纸巾沾湿后贴在乳房，和屁股上露出",
    "和主人猜拳脱衣",
    "对着路人展示胸部",
    "在户外长椅上露出小穴",
    "在男厕隔间内自慰",
    "佩戴跳蛋出门",
    "早起排尿后接下来一天禁止厕所排尿，没憋住尿到内裤上就脱下来",
    "无内穿短裙，在自动售货机前弯腰取出",
    "小区楼下趴下摇晃屁股狗叫两声",
    "将自慰后的内裤写下联系方式遗落在公共场所",
    "穿透视装，无内，乳头贴乳贴/创可贴",
    "在拥挤的公交/地铁上摸男人屁股/jj",
    "试衣间全裸自慰",
    "穿超短连衣裙（只遮一半屁股那种）前往便利店购物",
    "穿透视装，在傍晚天未全黑时脱下胸罩",
    "无内穿裙子去店里买鞋试鞋",
    "裸体敲邻居家门",
    "穿吊带连衣裙，出门后找个角落脱下内衣",
    "在人来人往的地方脱下内衣丢到地上",
    "将假阳具贴在邻居家门上自慰",
    "将假阳具贴楼梯间自慰到高潮",
    "在电梯内靠墙掀起裙子露出屁股",
    "多带一套衣服根朋友出门，趁着间隙时间换上",
    "在公共洗手间脱光换另一套出门",
    "将内裤塞入小穴一定要做好杀菌",
    "穿一件长外套，敞开衣服走过人行横道 凌晨",
    "被雨淋湿薄衣服，然后去买东西",
    "夜晚在路旁角落脱光，有路人经过悄悄跟在后面前进5米，然后快速返回  ",
    "穿短裙蹦极，里面配一条性感内裤/无内",
    "穿短裙带肛塞尾巴出门",
    "在临街酒店露出胸部探出窗外",
    "夜晚在路灯下脱光衣服拍照4张 ",
    "穿裙子在公园健身器材处压腿",
    "阳台站立2分钟"
  ]
  document.getElementById('exposureResult').textContent=tasks[rnd(0,tasks.length-1)]
}
document.getElementById('regenerateExposure').onclick=genExposure

// 生成SP
function genSP(){
  const tools=getList('toolsList')
  const parts=getList('bodyPartsList')
  const minC=Number(document.getElementById('minCount').value)||1
  const maxC=Number(document.getElementById('maxCount').value)||3
  const minS=Number(document.getElementById('minStrength').value)||1
  const maxS=Number(document.getElementById('maxStrength').value)||10
  const cnt=Number(document.getElementById('resultCount').value)||5
  if(tools.length===0||parts.length===0){document.getElementById('spResult').textContent='请先添加道具和部位';return}
  let out=''
  for(let i=0;i<cnt;i++){
    const t=tools[rnd(0,tools.length-1)]
    const p=parts[rnd(0,parts.length-1)]
    const n=rnd(minC,maxC)
    const s=rnd(minS,maxS)
    out+=`${i+1}. ${t}打${p} ${n}下，强度${s}\n`
  }
  document.getElementById('spResult').textContent=out
}
document.getElementById('generatePresetResult').onclick=genSP
document.getElementById('regenerateSP').onclick=genSP

// 游戏逻辑
let gameTools=[],dropped=[]
function startGame(){
  gameTools=getList('movementToolsList')
  dropped=[]
  refreshGameUI()
  document.getElementById('gameOutput').textContent='游戏开始！点击下一步'
  showPage('movement-game')
}
function refreshGameUI(){
  document.getElementById('remainingTools').textContent=gameTools.join('、')||'无'
  document.getElementById('droppedTools').textContent=dropped.join('、')||'无'
}
document.getElementById('startMovementGame').onclick=startGame
document.getElementById('nextStep').onclick=()=>{
  if(gameTools.length===0&&dropped.length===0){document.getElementById('gameOutput').textContent='已全部穿戴';return}
  const step=rnd(Number(document.getElementById('minDistance').value)||1,Number(document.getElementById('maxDistance').value)||1)
  let txt=`走${step}步\n`
  if(gameTools.length>0&&rnd(1,100)<=Number(document.getElementById('dropRate').value||60)){
    const idx=rnd(0,gameTools.length-1)
    const item=gameTools.splice(idx,1)[0]
    dropped.push(item)
    txt+=`脱下：${item}\n`
  }
  if(dropped.length>0&&rnd(1,100)<=Number(document.getElementById('pickupRate').value||40)){
    const idx=rnd(0,dropped.length-1)
    const item=dropped.splice(idx,1)[0]
    gameTools.push(item)
    txt+=`穿上：${item}\n`
  }
  if(rnd(1,100)<=Number(document.getElementById('actionRate').value||30)){
    const acts=getList('actionsList')
    if(acts.length>0)txt+=`事件：${acts[rnd(0,acts.length-1)]}\n时间：${rnd(Number(document.getElementById('minActionTime').value)||5,Number(document.getElementById('maxActionTime').value)||15)}秒`
  }
  document.getElementById('gameOutput').textContent=txt
  refreshGameUI()
}
</script>
</body>
</html>
