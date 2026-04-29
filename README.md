# index.html.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#01696f" />
  <link rel="manifest" href="./manifest.webmanifest">
  <link rel="icon" href="./assets/icon-192.png" sizes="192x192">
  <link rel="apple-touch-icon" href="./assets/icon-192.png">
  <title>Student Income Calculator</title>
  <style>
    body{font-family:Arial,sans-serif;margin:0;background:#171614;color:#e3e0da;padding:20px}
    .card{max-width:800px;margin:auto;background:#1c1b19;border:1px solid #393836;border-radius:16px;padding:20px}
    h1{margin-top:0;font-size:24px}
    .row{margin:15px 0}
    label{display:block;font-weight:700;margin-bottom:5px}
    input[type=range]{width:100%}
    .box{background:#201f1d;border-radius:12px;padding:15px;margin-top:15px}
    .big{font-size:32px;font-weight:800;color:#4f98a3}
    button{border:0;border-radius:20px;padding:10px 20px;font-weight:700;margin-top:10px}
    .primary{background:#01696f;color:white}
  </style>
</head>
<body>
  <div class="card">
    <h1>Income Calculator</h1>
    <div class="row"><label>Trading</label><input id="trade" type="range" min="0" max="50000" value="15000"></div>
    <div class="row"><label>Freelance</label><input id="freelance" type="range" min="0" max="60000" value="20000"></div>
    <div class="row"><label>Dropshipping</label><input id="dropship" type="range" min="0" max="80000" value="25000"></div>
    <div class="box">
        <div style="color:#a6a39c">Total Monthly Income</div>
        <div class="big" id="total">₹60,000</div>
    </div>
    <button class="primary" id="installBtn" hidden>Install as App</button>
  </div>
  <script>
    const el = id => document.getElementById(id);
    function update(){
      const t=+el('trade').value, f=+el('freelance').value, d=+el('dropship').value;
      el('total').textContent = '₹' + (t+f+d).toLocaleString('en-IN');
    }
    ['trade','freelance','dropship'].forEach(i => el(i).addEventListener('input', update));
    update();
    let deferredPrompt;
    window.addEventListener('beforeinstallprompt', e => { e.preventDefault(); deferredPrompt=e; el('installBtn').hidden=false; });
    el('installBtn').onclick = () => { deferredPrompt.prompt(); el('installBtn').hidden=true; };
    if('serviceWorker' in navigator) navigator.serviceWorker.register('./sw.js');
  </script>
</body>
</html>
