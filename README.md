<html lang="ro">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZAPPER ⚡</title>
<style>
  *{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif}
  body{background:#0f0f1a;color:white;min-height:100vh}
  header{text-align:center;padding:40px 20px 20px}
  header h1{font-size:55px;letter-spacing:2px}
  header h1 span{color:#a855f7}
  header p{color:#aaa;margin-top:10px;font-size:17px}
  .buttons{display:flex;flex-wrap:wrap;justify-content:center;gap:12px;padding:20px}
  .buttons button{background:#1e1e2e;border:2px solid #2d2d44;color:white;padding:16px 22px;border-radius:14px;font-size:16px;cursor:pointer}
  .buttons button:hover{background:#a855f7;border-color:#a855f7}
  .box{max-width:650px;margin:0 auto;padding:0 15px 40px}
  .zipu{background:#1a1a2e;border:1px solid #333;border-radius:20px;padding:20px}
  .zipu h2{font-size:20px;margin-bottom:5px}
  .zipu p{color:#bbb;font-size:14px;margin-bottom:15px}
  #chat{height:260px;overflow-y:auto;background:#0f0f1a;border-radius:12px;padding:12px;margin-bottom:12px;display:flex;flex-direction:column;gap:10px}
  .msg{padding:10px 14px;border-radius:12px;max-width:85%;font-size:14px;line-height:1.4}
  .ai{background:#2d2d44;align-self:flex-start}
  .me{background:#a855f7;align-self:flex-end}
  .row{display:flex;gap:8px}
  .row input{flex:1;padding:13px;border-radius:12px;border:none;outline:none;background:#0f0f1a;color:white;border:1px solid #333}
  .row button{background:#a855f7;border:none;color:white;padding:0 20px;border-radius:12px;font-weight:bold;cursor:pointer}
  #preview{margin-top:15px;background:white;color:black;border-radius:12px;padding:15px;display:none}
  #preview iframe{width:100%;height:220px;border:none;border-radius:8px;background:white}
  .small{text-align:center;color:#666;font-size:12px;padding-bottom:20px}
</style>
</head>
<body>

<header>
  <h1>⚡ ZAP<span>PER</span></h1>
  <p>Creeaza Website-uri, Jocuri si Apps cu AI. Fa-ti si Server.</p>
</header>

<div class="buttons">
  <button onclick="alege('Website 🌐')">🌐 Website</button>
  <button onclick="alege('Joc 🎮')">🎮 Joc</button>
  <button onclick="alege('App 📱')">📱 App</button>
  <button onclick="alege('Server 💬')">💬 Server</button>
</div>

<div class="box">
  <div class="zipu">
    <h2>🤖 ZIPU</h2>
    <p>Salut! Eu sunt Zipu. Ce vrei sa creezi azi? Scrie-mi mai jos.</p>
    <div id="chat">
      <div class="msg ai">Salut! ⚡ Eu sunt Zipu. Scrie-mi: "fa-mi un site cu pisici" sau "fa-mi un joc" si ti-l fac pe loc!</div>
    </div>
    <div class="row">
      <input id="input" placeholder="Scrie-i lui Zipu... ex: fa-mi un joc" onkeypress="if(event.key==='Enter') trimite()">
      <button onclick="trimite()">Trimite</button>
    </div>
    <div id="preview">
      <b>✨ Creatia ta:</b>
      <div id="previewContent" style="margin-top:10px"></div>
    </div>
  </div>
</div>
<p class="small">ZAPPER © 2026 - Made with Zipu</p>

<script>
let tip = "Website";
function alege(t){
  tip = t;
  adaugaMesaj("ai", "Super! Hai sa facem un " + t + ". Spune-mi cum vrei sa arate? Ex: 'cu pisici' sau 'cu masini'");
}
function adaugaMesaj(cine, text){
  let chat = document.getElementById("chat");
  let div = document.createElement("div");
  div.className = "msg " + cine;
  div.innerText = text;
  chat.appendChild(div);
  chat.scrollTop = chat.scrollHeight;
}
function trimite(){
  let inp = document.getElementById("input");
  let text = inp.value.trim();
  if(!text) return;
  adaugaMesaj("me", text);
  inp.value = "";
  setTimeout(()=>{ raspundeZipu(text.toLowerCase()); }, 600);
}
function raspundeZipu(t){
  let preview = document.getElementById("preview");
  let content = document.getElementById("previewContent");
  preview.style.display = "block";

  if(t.includes("joc") || t.includes("masin") || t.includes("click")){
    adaugaMesaj("ai", "Gata! 🎮 Ti-am facut un joc de click! Apasa pe buton cat poti de repede!");
    content.innerHTML = `<h2 style="text-align:center">🎮 Jocul tau de Click</h2><p style="text-align:center">Scor: <b id="scor">0</b></p><button onclick="document.getElementById('scor').innerText = parseInt(document.getElementById('scor').innerText)+1" style="display:block;margin:15px auto;padding:15px 30px;font-size:20px;background:#a855f7;color:white;border:none;border-radius:12px;cursor:pointer">APASA-MA! ⚡</button>`;
  } else if(t.includes("pisic")){
    adaugaMesaj("ai", "Gata! 🐱 Ti-am facut un site cu pisici!");
    content.innerHTML = `<h1 style="text-align:center">🐱 Site cu Pisici</h1><p style="text-align:center">Cele mai dragute pisici din lume!</p><p style="text-align:center;font-size:50px">🐱 🐈 😻 🐾</p><p style="text-align:center">Facut cu ZAPPER + ZIPU</p>`;
  } else if(t.includes("server")){
    adaugaMesaj("ai", "Gata! 💬 Ti-am facut serverul! Momentan e demo, in curand o sa fie chat real.");
    content.innerHTML = `<h2>💬 Serverul tau</h2><p>Bine ai venit in server!</p><div style="background:#eee;padding:10px;border-radius:8px"># general - Chat aici<br># jocuri - Vorbim despre jocuri</div>`;
  } else {
    adaugaMesaj("ai", "Gata! 🌐 Ti-am facut un website despre: " + t + ". Uite-l mai jos!");
    content.innerHTML = `<h1 style="text-align:center">⚡ ${t}</h1><p style="text-align:center">Acesta este website-ul tau creat cu ZAPPER.</p><p style="text-align:center"><button style="padding:10px 20px;background:#a855f7;color:white;border:none;border-radius:10px">Vezi mai mult</button></p><p style="text-align:center;color:#888">Facut cu Zipu 🤖</p>`;
  }
}
</script>
</body>
</html>
