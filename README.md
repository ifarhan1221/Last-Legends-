<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PUBG Tournaments Registrations </title>
<style>
    *{margin:0;padding:0;box-sizing:border-box;}
    body{font-family:Arial,sans-serif;min-height:100vh;background:#0a0a0a;}
    .bg{position:fixed;top:0;left:0;width:100%;height:100%;background:url('https://wallpapercave.com/wp/wp8350342.jpg') center/cover;z-index:-2;}
    .bg::after{content:'';position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.75);}
    .container{position:relative;z-index:1;max-width:600px;margin:0 auto;padding:20px;min-height:100vh;display:flex;align-items:center;}
    .card{background:rgba(0,0,0,0.9);border-radius:20px;padding:30px;border:2px solid #ff6600;width:100%;}
    h1{text-align:center;color:#ff6600;font-size:1.6em;margin-bottom:10px;text-shadow:0 0 10px #ff6600;}
    .sub{text-align:center;color:#ffcc00;margin-bottom:20px;font-size:1em;}
    .prize{text-align:center;padding:12px;background:rgba(255,102,0,0.2);border-radius:10px;margin-bottom:25px;border:1px solid #ff6600;}
    .prize h3{color:#ffcc00;}
    .prize p{color:#ff6600;font-weight:bold;}
    input{width:100%;padding:12px;margin:8px 0;background:#222;border:2px solid #ff6600;border-radius:8px;color:#fff;}
    button{width:100%;padding:12px;margin-top:10px;background:#ff6600;border:none;border-radius:8px;color:#fff;font-weight:bold;cursor:pointer;}
    button:hover{background:#ff5500;}
    .logout-btn{background:#cc3333;}
    .message{padding:12px;border-radius:8px;margin-bottom:15px;text-align:center;display:none;}
    .success{background:rgba(0,255,0,0.2);border:1px solid #0f0;color:#0f0;}
    .error{background:rgba(255,0,0,0.2);border:1px solid #f00;color:#f88;}
    .info{background:rgba(255,102,0,0.2);border:1px solid #ff6600;color:#ffaa66;}
    .status-box{padding:15px;border-radius:10px;text-align:center;margin-top:15px;}
    .pending{background:rgba(255,102,0,0.3);border:1px solid #ff6600;color:#ffaa66;}
    .approved{background:rgba(0,255,0,0.3);border:1px solid #0f0;color:#8f8;}
    .tabs{display:flex;gap:10px;margin:20px 0;flex-wrap:wrap;}
    .tab{flex:1;padding:10px;background:#333;border:none;border-radius:8px;color:#ffcc00;cursor:pointer;}
    .tab.active{background:#ff6600;color:#fff;}
    .tab-content{display:none;}
    .tab-content.active{display:block;}
    table{width:100%;border-collapse:collapse;font-size:12px;}
    th,td{padding:8px;text-align:left;border-bottom:1px solid #ff6600;color:#fff;}
    th{background:rgba(255,102,0,0.3);}
    .action-btn{padding:4px 8px;margin:2px;background:#ff6600;border:none;border-radius:4px;color:#fff;cursor:pointer;}
    .danger{background:#cc3333;}
    .toggle-area{display:flex;justify-content:space-between;align-items:center;background:rgba(255,102,0,0.2);padding:10px;border-radius:8px;margin-bottom:15px;}
    .switch{position:relative;display:inline-block;width:50px;height:24px;}
    .switch input{opacity:0;width:0;height:0;}
    .slider{position:absolute;cursor:pointer;top:0;left:0;right:0;bottom:0;background:#ccc;border-radius:24px;}
    .slider:before{position:absolute;content:"";height:18px;width:18px;left:3px;bottom:3px;background:#fff;border-radius:50%;}
    input:checked + .slider{background:#ff6600;}
    input:checked + .slider:before{transform:translateX(26px);}
    .stats{background:rgba(255,102,0,0.2);padding:10px;border-radius:8px;margin-bottom:15px;text-align:center;color:#ffcc00;}
    .section-header{display:flex;justify-content:space-between;margin-bottom:10px;}
    .del-all{background:#cc3333;padding:5px 10px;border:none;border-radius:5px;color:#fff;cursor:pointer;font-size:11px;}
</style>
</head>
<body>
<div class="bg"></div>
<div class="container">

<div id="loginBox" class="card">
    <h1> 💀 Last Legends 💀 </h1>
    <div class="sub"> 🔥 PUBG Tournament Registrations 🔥 </div>
    <div class="prize"><h3>🏆 WINNER PRIZE 🏆</h3><p>Cash Prize + In-Game Rewards</p></div>
    <div id="loginMsg" class="message"></div>
    <input type="text" id="loginUser" placeholder="Username">
    <input type="password" id="loginPass" placeholder="Password">
    <button onclick="doLogin()">LOGIN / SIGNUP</button>
</div>

<div id="regBox" class="card" style="display:none">
    <h1>🔥 PUBG Tournaments 🔥</h1>
    <div class="sub">PUBG Tournaments Registrations</div>
    <div id="regMsg" class="message"></div>
    <div id="statusBox" class="status-box" style="display:none"></div>
    <div id="formBox">
        <input type="text" id="uid" placeholder="PUBG UID (11 digits)">
        <input type="text" id="pname" placeholder="Player Name">
        <input type="text" id="squad" placeholder="Squad Name">
        <input type="email" id="email" placeholder="Email">
        <input type="tel" id="phone" placeholder="Phone (03xxxxxxxxx)" maxlength="11">
        <button onclick="doRegister()">SUBMIT</button>
    </div>
    <button class="logout-btn" onclick="doLogout()">LOGOUT</button>
</div>

<div id="adminBox" class="card" style="display:none">
    <h1>🔥 PUBG Tournaments 🔥</h1>
    <div class="sub">PUBG Tournaments Registrations</div>
    <div class="toggle-area">
        <span>Registration:</span>
        <label class="switch"><input type="checkbox" id="regToggle" onchange="toggleReg()"><span class="slider"></span></label>
        <span id="regStat">Open</span>
    </div>
    <div class="stats" id="statsArea">Stats</div>
    <div class="tabs">
        <button class="tab active" onclick="showTab('open')">📋 Open</button>
        <button class="tab" onclick="showTab('accept')">✅ Accepted</button>
        <button class="tab" onclick="showTab('reject')">❌ Rejected</button>
        <button class="tab" onclick="showTab('close')">🔒 Closed Time</button>
    </div>
    
    <div id="openTab" class="tab-content active">
        <div class="section-header"><span>📋 Pending Requests</span><button class="del-all" onclick="delAll('open')">Delete All</button></div>
        <div style="overflow-x:auto">\t<table><thead><tr><th>#</th><th>Name</th><th>UID</th><th>Squad</th><th>Phone</th><th>Email</th><th>Action</th></tr></thead><tbody id="openList"></tbody></table></div>
    </div>
    <div id="acceptTab" class="tab-content">
        <div class="section-header"><span>✅ Accepted</span><button class="del-all" onclick="delAll('accept')">Delete All</button></div>
        <div style="overflow-x:auto"><table><thead><tr><th>#</th><th>Name</th><th>UID</th><th>Squad</th><th>Phone</th><th>Contact</th><th>Action</th></tr></thead><tbody id="acceptList"></tbody></table></div>
    </div>
    <div id="rejectTab" class="tab-content">
        <div class="section-header"><span>❌ Rejected</span><button class="del-all" onclick="delAll('reject')">Delete All</button></div>
        <div style="overflow-x:auto"><table><thead><tr><th>#</th><th>Name</th><th>UID</th><th>Squad</th><th>Phone</th><th>Reason</th><th>Action</th></tr></thead><tbody id="rejectList"></tbody></table></div>
    </div>
    <div id="closeTab" class="tab-content">
        <div class="section-header"><span>🔒 Closed Time Registrations</span><button class="del-all" onclick="delAll('close')">Delete All</button></div>
        <div style="overflow-x:auto"><table><thead><tr><th>#</th><th>Name</th><th>UID</th><th>Squad</th><th>Phone</th><th>Email</th><th>Action</th></tr></thead><tbody id="closeList"></tbody></table></div>
    </div>
    <button class="logout-btn" onclick="doLogout()" style="margin-top:20px">LOGOUT</button>
</div>

</div>

<script>
let users = [];
let openList = [];
let acceptList = [];
let rejectList = [];
let closeList = [];
let currentUser = null;
let regOpen = true;

function loadAll() {
    try {
        users = JSON.parse(localStorage.getItem('users') || '[]');
        openList = JSON.parse(localStorage.getItem('open') || '[]');
        acceptList = JSON.parse(localStorage.getItem('accept') || '[]');
        rejectList = JSON.parse(localStorage.getItem('reject') || '[]');
        closeList = JSON.parse(localStorage.getItem('close') || '[]');
        // Admin credentials changed to: iamfarhan / *ifarhanali#
        if(!users.find(u=>u.name==='iamfarhan')) {
            users.push({name:'iamfarhan', pass:'*ifarhanali#', admin:true});
            saveAll();
        }
    } catch(e) {}
}

function saveAll() {
    localStorage.setItem('users', JSON.stringify(users));
    localStorage.setItem('open', JSON.stringify(openList));
    localStorage.setItem('accept', JSON.stringify(acceptList));
    localStorage.setItem('reject', JSON.stringify(rejectList));
    localStorage.setItem('close', JSON.stringify(closeList));
}

function showMsg(id, txt, type) {
    let el = document.getElementById(id);
    if(!el) return;
    el.innerHTML = txt;
    if(type === 's') el.className = 'message success';
    else if(type === 'i') el.className = 'message info';
    else el.className = 'message error';
    el.style.display = 'block';
    setTimeout(()=>{el.style.display='none';},4000);
}

function doLogin() {
    let name = document.getElementById('loginUser').value.trim();
    let pass = document.getElementById('loginPass').value.trim();
    if(!name || !pass) { showMsg('loginMsg','Enter username/password','e'); return; }
    let user = users.find(u=>u.name===name && u.pass===pass);
    if(!user) {
        user = {name:name, pass:pass, admin:false};
        users.push(user);
        saveAll();
        showMsg('loginMsg','Account created!','s');
    }
    currentUser = user;
    if(user.admin) {
        document.getElementById('loginBox').style.display = 'none';
        document.getElementById('regBox').style.display = 'none';
        document.getElementById('adminBox').style.display = 'block';
        document.getElementById('regToggle').checked = regOpen;
        document.getElementById('regStat').innerText = regOpen ? 'Open' : 'Closed';
        loadAdmin();
    } else {
        document.getElementById('loginBox').style.display = 'none';
        document.getElementById('regBox').style.display = 'block';
        document.getElementById('adminBox').style.display = 'none';
        checkUserReg();
    }
}

function checkUserReg() {
    let found = openList.find(r=>r.userId===currentUser.name) ||
                acceptList.find(r=>r.userId===currentUser.name) ||
                rejectList.find(r=>r.userId===currentUser.name) ||
                closeList.find(r=>r.userId===currentUser.name);
    let formDiv = document.getElementById('formBox');
    let statusDiv = document.getElementById('statusBox');
    if(found) {
        formDiv.style.display = 'none';
        statusDiv.style.display = 'block';
        if(found.status === 'accept') statusDiv.innerHTML = '✅ ACCEPTED!<br>Admin will contact you on WhatsApp.';
        else if(found.status === 'reject') statusDiv.innerHTML = '❌ REJECTED<br>Contact admin.';
        else if(found.status === 'close') statusDiv.innerHTML = '🔒 Registrations are currently closed. Your request has been saved and will be reviewed when registration reopens.';
        else statusDiv.innerHTML = '⏳ PENDING<br>Admin will review.';
        statusDiv.className = 'status-box ' + (found.status==='accept'?'approved':'pending');
    } else {
        formDiv.style.display = 'block';
        statusDiv.style.display = 'none';
    }
}

function doRegister() {
    let uid = document.getElementById('uid').value.trim();
    let pname = document.getElementById('pname').value.trim();
    let squad = document.getElementById('squad').value.trim();
    let email = document.getElementById('email').value.trim();
    let phone = document.getElementById('phone').value.trim();
    
    if(!uid||!pname||!squad||!email||!phone) { showMsg('regMsg','All fields required','e'); return; }
    if(!/^\d{11}$/.test(uid)) { showMsg('regMsg','UID must be 11 digits','e'); return; }
    if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) { showMsg('regMsg','Valid email required','e'); return; }
    if(!/^03\d{9}$/.test(phone)) { showMsg('regMsg','Phone must start with 03 (11 digits)','e'); return; }
    
    let exists = openList.find(r=>r.userId===currentUser.name) ||
                 acceptList.find(r=>r.userId===currentUser.name) ||
                 rejectList.find(r=>r.userId===currentUser.name) ||
                 closeList.find(r=>r.userId===currentUser.name);
    if(exists) { showMsg('regMsg','Already submitted!','e'); return; }
    
    let newReg = {
        id: Date.now(),
        userId: currentUser.name,
        uid: uid,
        playerName: pname,
        squadName: squad,
        email: email,
        contact: phone,
        status: regOpen ? 'open' : 'close'
    };
    
    if(regOpen) {
        openList.push(newReg);
        showMsg('regMsg', '✅ Registration submitted successfully! Redirecting...', 's');
    } else {
        closeList.push(newReg);
        showMsg('regMsg', '🔒 Registrations are currently closed. Your request has been saved and will be reviewed when registration reopens.', 'i');
    }
    saveAll();
    
    document.getElementById('uid').value = '';
    document.getElementById('pname').value = '';
    document.getElementById('squad').value = '';
    document.getElementById('email').value = '';
    document.getElementById('phone').value = '';
    
    setTimeout(()=>{ doLogout(); }, 3000);
}

function loadAdmin() {
    document.getElementById('statsArea').innerHTML = `📊 Open:${openList.length} | Accepted:${acceptList.length} | Rejected:${rejectList.length} | Closed:${closeList.length}`;
    
    let openBody = document.getElementById('openList');
    openBody.innerHTML = '';
    for(let i=0; i<openList.length; i++) {
        let r = openList[i];
        openBody.innerHTML += `<tr><td>${i+1}</td><td>${r.playerName}</td><td>${r.uid}</td><td>${r.squadName}</td><td>${r.contact}</td><td>${r.email}</td>
        <td><button class="action-btn" onclick="moveItem(${r.id},'open','accept')">✅ Accept</button>
        <button class="action-btn" onclick="moveItem(${r.id},'open','reject')">❌ Reject</button>
        <button class="action-btn danger" onclick="delItem(${r.id},'open')">🗑 Del</button></td></tr>`;
    }
    
    let acceptBody = document.getElementById('acceptList');
    acceptBody.innerHTML = '';
    for(let i=0; i<acceptList.length; i++) {
        let r = acceptList[i];
        acceptBody.innerHTML += `<tr><td>${i+1}</td><td>${r.playerName}</td><td>${r.uid}</td><td>${r.squadName}</td><td>${r.contact}</td>
        <td><a href="https://wa.me/${r.contact}" target="_blank" style="color:#0f0;">📱 Contact</a></td>
        <td><button class="action-btn danger" onclick="delItem(${r.id},'accept')">🗑 Del</button></td></tr>`;
    }
    
    let rejectBody = document.getElementById('rejectList');
    rejectBody.innerHTML = '';
    for(let i=0; i<rejectList.length; i++) {
        let r = rejectList[i];
        rejectBody.innerHTML += `<tr><td>${i+1}</td><td>${r.playerName}</td><td>${r.uid}</td><td>${r.squadName}</td><td>${r.contact}</td>
        <td>Admin decision</td><td><button class="action-btn danger" onclick="delItem(${r.id},'reject')">🗑 Del</button></td></tr>`;
    }
    
    let closeBody = document.getElementById('closeList');
    closeBody.innerHTML = '';
    for(let i=0; i<closeList.length; i++) {
        let r = closeList[i];
        closeBody.innerHTML += `<tr><td>${i+1}</td><td>${r.playerName}</td><td>${r.uid}</td><td>${r.squadName}</td><td>${r.contact}</td><td>${r.email}</td>
        <td><button class="action-btn" onclick="moveItem(${r.id},'close','open')">📋 Move to Open</button>
        <button class="action-btn danger" onclick="delItem(${r.id},'close')">🗑 Del</button></td></tr>`;
    }
}

function moveItem(id, from, to) {
    let item = null;
    if(from === 'open') {
        item = openList.find(r=>r.id===id);
        openList = openList.filter(r=>r.id!==id);
    } else if(from === 'close') {
        item = closeList.find(r=>r.id===id);
        closeList = closeList.filter(r=>r.id!==id);
    }
    if(item) {
        if(to === 'accept') { item.status = 'accept'; acceptList.push(item); }
        else if(to === 'reject') { item.status = 'reject'; rejectList.push(item); }
        else if(to === 'open') { item.status = 'open'; openList.push(item); }
        saveAll();
        loadAdmin();
        showTab('open');
    }
}

function delItem(id, type) {
    if(!confirm('Delete this?')) return;
    if(type === 'open') openList = openList.filter(r=>r.id!==id);
    else if(type === 'accept') acceptList = acceptList.filter(r=>r.id!==id);
    else if(type === 'reject') rejectList = rejectList.filter(r=>r.id!==id);
    else if(type === 'close') closeList = closeList.filter(r=>r.id!==id);
    saveAll();
    loadAdmin();
}

function delAll(type) {
    if(!confirm(`Delete ALL ${type} registrations?`)) return;
    if(type === 'open') openList = [];
    else if(type === 'accept') acceptList = [];
    else if(type === 'reject') rejectList = [];
    else if(type === 'close') closeList = [];
    saveAll();
    loadAdmin();
}

function toggleReg() {
    regOpen = document.getElementById('regToggle').checked;
    document.getElementById('regStat').innerText = regOpen ? 'Open' : 'Closed';
}

function showTab(tab) {
    document.getElementById('openTab').classList.remove('active');
    document.getElementById('acceptTab').classList.remove('active');
    document.getElementById('rejectTab').classList.remove('active');
    document.getElementById('closeTab').classList.remove('active');
    let btns = document.querySelectorAll('.tab');
    btns.forEach(b=>b.classList.remove('active'));
    
    if(tab === 'open') { document.getElementById('openTab').classList.add('active'); btns[0].classList.add('active'); }
    else if(tab === 'accept') { document.getElementById('acceptTab').classList.add('active'); btns[1].classList.add('active'); }
    else if(tab === 'reject') { document.getElementById('rejectTab').classList.add('active'); btns[2].classList.add('active'); }
    else if(tab === 'close') { document.getElementById('closeTab').classList.add('active'); btns[3].classList.add('active'); }
}

function doLogout() {
    currentUser = null;
    document.getElementById('loginBox').style.display = 'block';
    document.getElementById('regBox').style.display = 'none';
    document.getElementById('adminBox').style.display = 'none';
    document.getElementById('loginUser').value = '';
    document.getElementById('loginPass').value = '';
}

loadAll();
</script>
</body>
</html>
