<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>罩顾健康 - 医院口罩公益服务</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:"Microsoft YaHei",sans-serif}
body{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);min-height:100vh;padding:20px}
.container{max-width:600px;margin:0 auto;background:white;border-radius:20px;padding:30px;box-shadow:0 10px 30px rgba(0,0,0,0.1)}
.header{text-align:center;margin-bottom:30px}
.logo{font-size:28px;font-weight:bold;color:#667eea;margin-bottom:10px}
.subtitle{color:#666;font-size:16px}
.choice-section{display:flex;gap:20px;margin-bottom:30px}
.choice-btn{flex:1;padding:25px 20px;border-radius:15px;border:none;font-size:18px;font-weight:bold;cursor:pointer;transition:all 0.3s ease;display:flex;flex-direction:column;align-items:center;gap:10px}
.buy-btn{background:linear-gradient(135deg,#4facfe 0%,#00f2fe 100%);color:white}
.donate-btn{background:linear-gradient(135deg,#fa709a 0%,#fee140 100%);color:white}
.choice-btn:hover{transform:translateY(-5px);box-shadow:0 8px 20px rgba(0,0,0,0.15)}
.icon{font-size:30px}
.payment-section{display:none;text-align:center;margin-bottom:30px}
.payment-title{font-size:22px;font-weight:bold;margin-bottom:20px;color:#333}
.price{font-size:36px;font-weight:bold;color:#667eea;margin-bottom:20px}
.pay-btn{background:#28a745;color:white;border:none;padding:15px 40px;border-radius:50px;font-size:18px;font-weight:bold;cursor:pointer;transition:all 0.3s ease}
.pay-btn:hover{background:#218838;transform:scale(1.05)}
.back-btn{background:#6c757d;color:white;border:none;padding:10px 20px;border-radius:50px;font-size:14px;cursor:pointer;margin-top:15px}
.success-section{display:none;text-align:center;margin-top:30px}
.success-icon{font-size:60px;color:#28a745;margin-bottom:20px}
.success-message{font-size:20px;font-weight:bold;color:#333;margin-bottom:15px;line-height:1.6}
.knowledge-section{margin-top:30px;padding:20px;background:#f8f9fa;border-radius:15px;text-align:left}
.knowledge-title{font-size:18px;font-weight:bold;color:#667eea;margin-bottom:15px;text-align:center}
.knowledge-item{margin-bottom:10px;color:#555;line-height:1.5}

/* 互动答题样式 */
.quiz-box{margin-top:20px;padding:15px;background:#eef5ff;border-radius:12px}
.quiz-title{font-weight:bold;margin-bottom:8px;color:#333}
.quick-answer-btn{
    background:#667eea;
    color:white;
    border:none;
    padding:6px 12px;
    border-radius:6px;
    font-size:14px;
    cursor:pointer;
    margin-left:10px;
    vertical-align:middle;
}
.option{
    padding:10px 12px;
    margin:8px 0;
    border-radius:8px;
    background:white;
    border:1px solid #ddd;
    cursor:pointer;
    position:relative;
    transition: all 0.5s ease;
}
.option.selected{background:#cfe2ff;border-color:#667eea}
/* 轻微偏移，只区分方向，不消失 */
.option.to-left{transform:translateX(-10%);}
.option.to-right{transform:translateX(10%);}
.quiz-btn-group{margin:12px 0}
.quiz-btn{background:#667eea;color:white;border:none;padding:10px 16px;border-radius:8px;cursor:pointer}
.answer-box{margin-top:10px;padding:10px;background:#fff3cd;border-radius:8px;font-size:14px}
.counter{margin-top:15px;font-size:15px;color:#333;text-align:center}

/* 翻页动画 */
.flip {
  display:inline-block;
  animation: flipNumber 0.6s ease;
}
@keyframes flipNumber {
  0% { transform: rotateX(0deg); opacity:0.5; }
  50% { transform: rotateX(180deg); opacity:0.8; }
  100% { transform: rotateX(360deg); opacity:1; }
}

.reset-btn{background:#667eea;color:white;border:none;padding:12px 30px;border-radius:50px;font-size:16px;cursor:pointer;margin-top:20px}
</style>
</head>
<body>
<div class="container">
    <div class="header">
        <div class="logo">罩顾健康</div>
        <div class="subtitle">医院口罩公益服务 · 守护你我健康</div>
    </div>

    <div id="choicePage">
        <div class="choice-section">
            <button class="choice-btn buy-btn">
                <div class="icon">😷</div>
                <div>购买口罩</div>
                <div style="font-size:14px">0.5元/个</div>
            </button>
            <button class="choice-btn donate-btn">
                <div class="icon">❤️</div>
                <div>捐赠口罩</div>
                <div style="font-size:14px">助力公益</div>
            </button>
        </div>
    </div>

    <div id="buyPage" class="payment-section">
        <div class="payment-title">购买口罩</div>
        <div class="price">¥0.50</div>
        <button class="pay-btn">确认支付</button>
        <br>
        <button class="back-btn">返回选择</button>
    </div>

    <div id="donatePage" class="payment-section">
        <div class="payment-title">捐赠口罩</div>
        <div class="price">爱心捐赠</div>
        <button class="pay-btn">确认捐赠</button>
        <br>
        <button class="back-btn">返回选择</button>
    </div>

    <div id="successPage" class="success-section">
        <div class="success-icon">✅</div>
        <div id="successMessage" class="success-message"></div>
        
        <div class="knowledge-section">
            <div class="knowledge-title">健康防护知识科普</div>
            <div class="knowledge-item">• 正确佩戴方法：覆盖口鼻下巴，压紧鼻夹，确保密合</div>
            <div class="knowledge-item">• 提醒家人（老人、儿童）共同佩戴，共筑健康防线</div>

            <!-- 互动答题 -->
            <div class="quiz-box">
                <div class="quiz-title">
                    您认为能通过戴口罩有效预防的传染病有：
                    <button class="quick-answer-btn" onclick="showAnswer()">直通答案</button>
                </div>
                
                <div class="option" onclick="toggleSelect(this,0)">流行性感冒</div>
                <div class="option" onclick="toggleSelect(this,1)">手足口病</div>
                <div class="option" onclick="toggleSelect(this,2)">水痘</div>
                <div class="option" onclick="toggleSelect(this,3)">麻疹</div>
                <div class="option" onclick="toggleSelect(this,4)">诺如病毒胃肠炎</div>
                <div class="option" onclick="toggleSelect(this,5)">流行性腮腺炎</div>
                <div class="option" onclick="toggleSelect(this,6)">肺炎</div>
                <div class="option" onclick="toggleSelect(this,7)">肺结核</div>
                <div class="option" onclick="toggleSelect(this,8)">流行性脑脊髓膜炎</div>
                
                <div class="quiz-btn-group">
                    <button class="quiz-btn" onclick="submitAnswer()">提交答案</button>
                </div>
                
                <div id="answerBox" class="answer-box" style="display:none"></div>
                <div class="counter">参与互动人数：<span id="count">0</span></div>
            </div>
        </div>
        
        <button class="reset-btn" onclick="resetPage()">返回首页</button>
    </div>
</div>

<script>
let buyCount = localStorage.getItem('maskBuyCount') || 0;
let playCount = parseInt(localStorage.getItem('quizPlayCount') || 0);
let answered = false;
const ans = [true,false,true,true,false,true,true,true,true];

window.onload = function(){
    document.getElementById('count').innerText = playCount;
    
    document.querySelector('.buy-btn').onclick = showBuy;
    document.querySelector('.donate-btn').onclick = showDonate;
    document.querySelectorAll('.back-btn')[0].onclick = backToChoice;
    document.querySelectorAll('.back-btn')[1].onclick = backToChoice;
    document.querySelector('.pay-btn').onclick = payBuy;
    document.querySelectorAll('.pay-btn')[1].onclick = payDonate;
}

function showBuy(){
    document.getElementById('choicePage').style.display='none'
    document.getElementById('buyPage').style.display='block'
    document.getElementById('donatePage').style.display='none'
    document.getElementById('successPage').style.display='none'
}

function showDonate(){
    document.getElementById('choicePage').style.display='none'
    document.getElementById('buyPage').style.display='none'
    document.getElementById('donatePage').style.display='block'
    document.getElementById('successPage').style.display='none'
}

function backToChoice(){
    document.getElementById('choicePage').style.display='block'
    document.getElementById('buyPage').style.display='none'
    document.getElementById('donatePage').style.display='none'
    document.getElementById('successPage').style.display='none'
}

function payBuy(){
    buyCount++;
    localStorage.setItem('maskBuyCount',buyCount);
    document.getElementById('successMessage').innerHTML="这是你第"+buyCount+"次在医院购买口罩，感谢你对健康卫生事业作出的贡献";
    showSuccess();
}

function payDonate(){
    document.getElementById('successMessage').innerHTML="每一份捐助，都会变成一只口罩、一道防线。感谢你，让保护得以传递";
    showSuccess();
}

function showSuccess(){
    document.getElementById('choicePage').style.display='none'
    document.getElementById('buyPage').style.display='none'
    document.getElementById('donatePage').style.display='none'
    document.getElementById('successPage').style.display='block'
}

function resetPage(){backToChoice()}

// 互动答题
function toggleSelect(el, idx){
    if(answered) return;
    el.classList.toggle('selected');
}

// 提交答案
function submitAnswer(){
    if(answered) return;
    splitAnswer();
    showAnswer();
}

// 直通答案
function showAnswer(){
    if(answered) return;
    document.getElementById('answerBox').style.display='block';
    document.getElementById('answerBox').innerText = '✅ 正确答案：流行性感冒、水痘、麻疹、流行性腮腺炎、肺炎、肺结核、流行性脑脊髓膜炎';
    answered = true;
    addCount(); // 统一只在这里+1
}

// 核心：正确轻微左移+✅，错误轻微右移+❌，用户选中保留蓝色，无红绿颜色
function splitAnswer(){
    if(answered) return;
    let all = document.querySelectorAll('.option');
    all.forEach((item,i)=>{
        // 先清空已有的符号，防止重复
        let text = item.innerText.trim().replace(/^(✅|❌)\s*/, '').replace(/\s*(✅|❌)$/, '');
        
        if(ans[i]){
            item.classList.add('to-left');
            item.innerText = "✅ " + text;
        }else{
            item.classList.add('to-right');
            item.innerText = text + " ❌";
        }
    });
}

// 人数+1 动画
function addCount(){
    playCount++;
    localStorage.setItem('quizPlayCount', playCount);
    
    let countEl = document.getElementById('count');
    countEl.classList.add('flip');
    setTimeout(() => {
        countEl.innerText = playCount;
        setTimeout(() => countEl.classList.remove('flip'), 100);
    }, 200);
}
</script>
</html>
