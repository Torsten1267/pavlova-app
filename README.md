[index 8.html](https://github.com/user-attachments/files/26547031/index.8.html)
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Pavlova Bestell">
<meta name="theme-color" content="#c4bfb6">
<title>Pavlova – Lieferanten-Bestellung</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow:hidden;}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;color:#1a1a1a;font-size:15px;background:#fff;}
:root{
  --gruen:#1D9E75;--gruen-dk:#0F6E56;--gruen-hell:#E1F5EE;--gruen-tx:#0F6E56;
  --beige:#c4bfb6;--bg:#fff;--bg2:#f5f4f2;--bg3:#efefed;
  --tx:#1a1a1a;--tx2:#666;--tx3:#aaa;
  --rand:rgba(0,0,0,0.1);--rand2:rgba(0,0,0,0.18);
  --r:10px;--rl:14px;--rot:#E24B4A;
  --amber-bg:#FAEEDA;--amber-tx:#854F0B;
}
#app{display:flex;flex-direction:column;height:100%;max-width:600px;margin:0 auto;}
.kopfzeile{background:var(--bg);border-bottom:0.5px solid var(--rand);padding:10px 16px;padding-top:max(10px,env(safe-area-inset-top));display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.kopf-logo{width:38px;height:38px;flex-shrink:0;}
.kopf-titel{font-size:15px;font-weight:600;color:var(--tx);}
.kopf-sub{font-size:11px;color:var(--tx2);margin-top:1px;}
.nutzer-btn{display:flex;align-items:center;gap:6px;background:var(--bg2);border:0.5px solid var(--rand);border-radius:20px;padding:5px 10px;cursor:pointer;-webkit-appearance:none;}
.nutzer-av{width:24px;height:24px;border-radius:50%;background:#B5D4F4;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:#0C447C;flex-shrink:0;}
.nutzer-nm{font-size:12px;color:var(--tx);max-width:90px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.nav-leiste{display:flex;background:var(--bg);border-top:0.5px solid var(--rand);padding-bottom:max(8px,env(safe-area-inset-bottom));flex-shrink:0;}
.nav-btn{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;padding:8px 4px;border:none;background:transparent;color:var(--tx2);cursor:pointer;font-size:10px;position:relative;-webkit-appearance:none;}
.nav-btn.aktiv{color:var(--gruen);}
.nav-btn svg{width:22px;height:22px;stroke:currentColor;fill:none;stroke-width:1.8;}
.nav-badge{position:absolute;top:5px;right:calc(50% - 18px);background:var(--rot);color:#fff;font-size:9px;font-weight:700;border-radius:8px;padding:1px 5px;min-width:16px;text-align:center;display:none;}
.inhalt{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;}
.ansicht{display:none;padding:16px;padding-bottom:28px;}
.ansicht.aktiv{display:block;}
.pillen{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:14px;scrollbar-width:none;}
.pillen::-webkit-scrollbar{display:none;}
.pille{padding:7px 14px;border-radius:20px;border:0.5px solid var(--rand);font-size:13px;cursor:pointer;background:var(--bg);color:var(--tx2);white-space:nowrap;flex-shrink:0;-webkit-appearance:none;}
.pille.aktiv{border-color:var(--gruen);background:var(--gruen-hell);color:var(--gruen-tx);font-weight:600;}
.suche{position:relative;margin-bottom:12px;}
.suche input{width:100%;padding:9px 12px 9px 34px;border:0.5px solid var(--rand);border-radius:var(--r);font-size:14px;background:var(--bg2);color:var(--tx);-webkit-appearance:none;}
.suche input:focus{outline:none;border-color:var(--gruen);background:var(--bg);}
.such-icon{position:absolute;left:10px;top:50%;transform:translateY(-50%);width:16px;height:16px;stroke:var(--tx3);fill:none;stroke-width:1.5;}
.kategorien{display:flex;gap:6px;overflow-x:auto;padding-bottom:4px;margin-bottom:14px;scrollbar-width:none;}
.kategorien::-webkit-scrollbar{display:none;}
.kat-btn{padding:5px 12px;font-size:12px;border-radius:16px;border:0.5px solid var(--rand);background:transparent;color:var(--tx2);cursor:pointer;white-space:nowrap;flex-shrink:0;-webkit-appearance:none;}
.kat-btn.aktiv{background:var(--bg3);color:var(--tx);border-color:var(--rand2);font-weight:500;}
.produkt-zeile{display:flex;align-items:center;gap:10px;background:var(--bg);border:0.5px solid var(--rand);border-radius:var(--r);padding:11px 12px;margin-bottom:6px;}
.prod-info{flex:1;min-width:0;}
.prod-name{font-size:14px;font-weight:500;color:var(--tx);}
.prod-meta{font-size:11px;color:var(--tx2);margin-top:2px;}
.prod-hinweis{font-size:11px;color:var(--amber-tx);margin-top:2px;}
.menge-steuerung{display:flex;align-items:center;gap:8px;flex-shrink:0;}
.menge-btn{width:32px;height:32px;border-radius:50%;border:0.5px solid var(--rand2);background:var(--bg2);color:var(--tx);font-size:20px;cursor:pointer;display:flex;align-items:center;justify-content:center;-webkit-appearance:none;line-height:1;}
.menge-btn:active{background:var(--bg3);}
.menge-zahl{font-size:15px;font-weight:700;min-width:24px;text-align:center;color:var(--tx);}
.warenkorb-kopf{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;}
.lieferant-tag{font-size:12px;color:var(--tx2);background:var(--bg2);padding:3px 10px;border-radius:10px;}
.leer-hinweis{text-align:center;padding:3rem 0;color:var(--tx2);font-size:14px;}
.warenkorb-pos{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:0.5px solid var(--rand);}
.wk-info{flex:1;}
.wk-name{font-size:14px;color:var(--tx);}
.wk-detail{font-size:12px;color:var(--tx2);margin-top:1px;}
.wk-loeschen{width:28px;height:28px;border-radius:50%;border:none;background:var(--bg2);color:var(--tx2);cursor:pointer;font-size:18px;display:flex;align-items:center;justify-content:center;flex-shrink:0;-webkit-appearance:none;}
.wk-loeschen:active{background:#FCEBEB;color:var(--rot);}
.mail-zusammenfassung{background:var(--bg2);border-radius:var(--r);padding:12px;margin:14px 0;}
.mail-zeile{display:flex;gap:6px;font-size:12px;color:var(--tx2);margin-bottom:4px;}
.mail-zeile:last-child{margin-bottom:0;}
.mail-wert{color:var(--tx);font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.pdf-hinweis{background:var(--gruen-hell);border-radius:var(--r);padding:10px 12px;margin-bottom:12px;font-size:12px;color:var(--gruen-tx);line-height:1.5;}
.notiz{width:100%;padding:10px 12px;border:0.5px solid var(--rand);border-radius:var(--r);font-size:14px;background:var(--bg);color:var(--tx);resize:none;font-family:inherit;margin-bottom:10px;-webkit-appearance:none;}
.notiz:focus{outline:none;border-color:var(--gruen);}
.btn-grau{width:100%;padding:11px;border-radius:var(--r);border:0.5px solid var(--rand2);background:var(--bg2);color:var(--tx);font-size:14px;font-weight:500;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:6px;margin-bottom:10px;-webkit-appearance:none;}
.btn-grau:active{background:var(--bg3);}
.btn-gruen{width:100%;padding:14px;border-radius:var(--rl);border:none;background:var(--gruen);color:#fff;font-size:16px;font-weight:600;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;-webkit-appearance:none;}
.btn-gruen:active{background:var(--gruen-dk);}
.btn-gruen:disabled{background:var(--bg3);color:var(--tx2);cursor:default;}
.bestell-karte{background:var(--bg);border:0.5px solid var(--rand);border-radius:var(--rl);padding:14px;margin-bottom:10px;}
.bk-kopf{display:flex;align-items:center;gap:8px;margin-bottom:5px;flex-wrap:wrap;}
.bk-nr{font-size:13px;font-weight:600;color:var(--tx);}
.bk-tag{font-size:11px;padding:2px 8px;border-radius:8px;background:var(--bg2);color:var(--tx2);}
.status-pille{font-size:11px;padding:2px 8px;border-radius:8px;cursor:pointer;-webkit-appearance:none;border:none;}
.s-offen{background:var(--amber-bg);color:var(--amber-tx);}
.s-bestaetigt{background:var(--gruen-hell);color:var(--gruen-tx);}
.s-geliefert{background:var(--bg2);color:var(--tx2);}
.bk-info{font-size:12px;color:var(--tx2);margin-bottom:8px;}
.bk-aktionen{display:flex;gap:8px;flex-wrap:wrap;}
.aktion-btn{font-size:12px;padding:5px 12px;border-radius:var(--r);border:0.5px solid var(--rand2);background:transparent;color:var(--tx2);cursor:pointer;-webkit-appearance:none;}
.aktion-btn:active{background:var(--bg2);}
.einst-abschnitt{margin-bottom:22px;}
.einst-titel{font-size:13px;font-weight:600;color:var(--tx2);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:10px;}
.einst-karte{background:var(--bg);border:0.5px solid var(--rand);border-radius:var(--rl);overflow:hidden;margin-bottom:10px;}
.einst-zeile{display:flex;align-items:center;gap:10px;padding:12px 14px;border-bottom:0.5px solid var(--rand);}
.einst-zeile:last-child{border-bottom:none;}
.einst-info{flex:1;}
.einst-name{font-size:14px;color:var(--tx);}
.einst-sub{font-size:12px;color:var(--tx2);margin-top:1px;}
.loeschen-btn{width:28px;height:28px;border-radius:50%;border:0.5px solid var(--rand);background:var(--bg2);color:var(--tx2);cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;flex-shrink:0;-webkit-appearance:none;}
.loeschen-btn:active{color:var(--rot);border-color:var(--rot);}
.eingabe-bereich{padding:12px 14px;background:var(--bg2);display:flex;flex-direction:column;gap:8px;}
.eingabe-zeile{display:flex;gap:8px;}
.eingabe-bereich input,.mail-eingabe{flex:1;padding:8px 10px;border:0.5px solid var(--rand);border-radius:var(--r);font-size:13px;background:var(--bg);color:var(--tx);min-width:0;-webkit-appearance:none;}
.eingabe-bereich input:focus,.mail-eingabe:focus{outline:none;border-color:var(--gruen);}
.eingabe-bereich input[readonly],.mail-eingabe[readonly]{color:var(--tx2);background:var(--bg2);}
.hinzufuegen-btn{padding:9px 16px;border-radius:var(--r);border:none;background:var(--gruen);color:#fff;font-size:13px;font-weight:600;cursor:pointer;-webkit-appearance:none;}
.hinzufuegen-btn:active{background:var(--gruen-dk);}
.hinzufuegen-btn.sekundaer{background:var(--bg2);color:var(--tx);border:0.5px solid var(--rand2);}
.hinzufuegen-btn.sekundaer:active{background:var(--bg3);}
.lief-pillen{display:flex;gap:6px;overflow-x:auto;padding-bottom:6px;margin-bottom:10px;scrollbar-width:none;}
.lief-pillen::-webkit-scrollbar{display:none;}
.lief-pille{padding:5px 12px;font-size:12px;border-radius:16px;border:0.5px solid var(--rand);background:transparent;color:var(--tx2);cursor:pointer;white-space:nowrap;flex-shrink:0;-webkit-appearance:none;}
.lief-pille.aktiv{background:var(--gruen-hell);color:var(--gruen-tx);border-color:var(--gruen);font-weight:600;}
.server-karte{background:var(--bg);border:0.5px solid var(--rand);border-radius:var(--rl);padding:14px;margin-bottom:10px;}
.server-feld{margin-bottom:12px;}
.server-feld:last-child{margin-bottom:0;}
.server-label{font-size:12px;color:var(--tx2);font-weight:500;margin-bottom:5px;}
.status-punkt{width:10px;height:10px;border-radius:50%;background:var(--rot);flex-shrink:0;}
.overlay{position:fixed;inset:0;background:rgba(0,0,0,0.45);z-index:100;display:none;align-items:flex-end;}
.overlay.aktiv{display:flex;}
.blatt{background:var(--bg);border-radius:20px 20px 0 0;width:100%;max-width:600px;margin:0 auto;padding:20px 16px;padding-bottom:max(20px,env(safe-area-inset-bottom));max-height:70vh;overflow-y:auto;}
.blatt-titel{font-size:16px;font-weight:700;color:var(--tx);margin-bottom:14px;}
.blatt-zeile{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:0.5px solid var(--rand);cursor:pointer;}
.blatt-zeile:last-child{border-bottom:none;}
.blatt-haken{width:20px;height:20px;border-radius:50%;border:2px solid var(--rand2);flex-shrink:0;}
.blatt-zeile.aktiv .blatt-haken{background:var(--gruen);border-color:var(--gruen);}
.blatt-zeile.aktiv .blatt-name{color:var(--gruen);font-weight:600;}
.blatt-name{font-size:15px;color:var(--tx);}
.hinweis-box{background:var(--gruen-hell);color:var(--gruen-tx);font-size:11px;padding:3px 8px;border-radius:8px;margin-top:5px;display:inline-flex;}
.meldung{position:fixed;bottom:calc(62px + env(safe-area-inset-bottom) + 10px);left:50%;transform:translateX(-50%) translateY(16px);background:#085041;color:#fff;padding:10px 20px;border-radius:20px;font-size:13px;font-weight:500;opacity:0;transition:all 0.25s;z-index:999;white-space:nowrap;pointer-events:none;}
.meldung.aktiv{opacity:1;transform:translateX(-50%) translateY(0);}
</style>
</head>
<body>
<div id="app">

<div class="kopfzeile">
  <div style="display:flex;align-items:center;gap:10px;">
    <div class="kopf-logo"><svg id="icons_filled" data-name="icons filled" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 226.77 226.77">
  <defs>
    <style>
      .cls-1 {
        fill: #fff;
      }

      .cls-2 {
        fill: #c4bfb6;
      }
    </style>
  </defs>
  <g id="icon-filled-beige">
    <circle id="circle" class="cls-2" cx="113.39" cy="113.39" r="85.04"/>
    <path id="logomark" class="cls-1" d="m59.83,122.61c-.3.22-.6.46-.89.71l-.78.75-.69.79c-.34.39-.71.76-1.09,1.11-.07.07-.17.1-.26.1s-.19-.04-.27-.11c-.15-.14-.16-.37-.02-.52.33-.39.66-.81.97-1.24l.99-1.34.4-.45c.28-.3.57-.59.89-.87.32-.29.64-.57.96-.83l.52-.43c.5-.41,1.01-.82,1.5-1.27l.3-.27c.26-.23.52-.48.79-.7.21-.18.45-.35.71-.5.24-.14.48-.27.73-.36l.38-.14c.47-.13.92-.25,1.37-.37.43-.11.85-.22,1.28-.34,8.69-2.54,12.46-2.74,20.73-3.16,2.43-.2,4.67-.51,6.62-.91,2.47-.52,4.58-1.21,6.25-2.05.55-.28,1.08-.58,1.6-.88-.28.02-.58.02-.88-.02-.38-.04-.77-.13-1.02-.19l-.18-.06c-.32-.11-.59-.21-.83-.33l-.26-.14c-.23-.11-.47-.24-.69-.42-.58-.41-1.11-.91-1.55-1.5-.44-.57-.8-1.22-1.05-1.88-.22-.58-.35-1.19-.4-1.81-.05-.63-.02-1.28.09-1.92.14-.8.59-1.88,1.17-2.81.47-.74.99-1.34,1.52-1.74.62-.47,1.27-.66,1.88-.55.23.04.46.13.69.25-.16-.6-.28-1.2-.36-1.77-.08-.61-.12-1.21-.12-1.8v-.23c.06-1,.11-2.13.59-3.07,2.43-4.75,5.82-5.72,7.27-6.13l1.3-.37.93-.14c1.99-.13,5.04.2,7.71,1.55,2.17,1.09,3.72,2.68,4.49,4.59.11.27.19.56.25.84.06.3.08.59.08.88-.02,1.15-.5,2.12-.97,3.07-.56,1.13-1.09,2.19-.92,3.57.1.82.44,1.79,1,2.9.47.94,1.04,1.84,1.58,2.68.29.45.82.73,1.56.81.15.02.32.02.49.02.17-.01.34.12.38.3.04.18-.05.36-.22.43-.73.33-1.28.41-1.75.25l-.35-.21-.64-.61c-.82-.8-1.71-1.93-2.44-3.11-.71-1.16-1.23-2.28-1.48-3.24-.1-.4-.15-.81-.16-1.22,0-.43.04-.87.12-1.28.12-.6.37-1.21.61-1.79.59-1.41,1.09-2.61.17-3.94-.53-.76-1.31-1.51-2.27-2.17-.99-.68-2.16-1.27-3.28-1.65-1.36-.46-2.8-.65-4.16-.56-1.34.09-2.57.48-3.57,1.11-1.31.83-2.22,2.11-2.63,3.69-.43,1.6-.33,3.44.28,5.32.15.46,1.38,2.37,3.23,4.99.1.15.09.34-.03.48-.12.13-.32.16-.47.07-.9-.51-1.74-1.18-2.43-1.94-.85-.93-1.49-2.02-1.86-3.13-.2-.62-.3-.8-.33-.84,0,.05,0,.16.01.39.09.77.4,2.22.75,3.22.17.31.48.89.04,1.15-.38.2-1.05.06-2.12-.2-.56-.14-1.1-.26-1.46-.26h0c-.31,0-1.07.39-1.81,1.04-.64.56-1.07,1.15-1.11,1.53-.04.52-.03,1.03.05,1.53.07.49.21.95.4,1.36.44.98,1.36,1.9,2.51,2.55.66.37,1.37.61,2.05.71.71.1,1.36.03,1.89-.21.49-.22.88-.59,1.15-1.08.17-.3.26-.66.26-1.05,0-.38-.09-.78-.25-1.13-.22-.46-.57-.86-1.04-1.19-.48-.33-1.08-.59-1.78-.76-.27-.07-.55-.13-.84-.16-.29-.03-.55-.01-.8.04-.27.07-.52.2-.71.38-.11.1-.19.21-.26.34-.1.17-.31.24-.49.16-.18-.08-.27-.29-.2-.48.05-.13.11-.25.19-.38.24-.38.57-.68.97-.89,0,0,.08-.04.09-.04.2-.09.38-.17.56-.21l.68-.12c.25-.02.51-.01.78.02.26.03.53.09.79.17.61.19,1.17.46,1.69.8.51.35.97.77,1.36,1.25.54.69.87,1.52.92,2.34.05.8-.19,1.55-.66,2.11.53-.18,1.06-.3,1.59-.38.58-.09,1.18-.12,1.77-.08l.51.05c.19.02.37.04.55.07l.93.11c.49.04.94-.12,1.31-.46.37-.33.65-.86.81-1.47.05-.19.08-.39.11-.59.02-.2.16-.38.39-.34.2,0,.36.16.37.36.06.98-.09,1.88-.43,2.54-.1.18-.2.33-.31.46-.76.9-2.02.84-3.13.78-.34-.02-.67-.03-.98-.03-1.75.06-3.15.36-4.52.97-.83.37-1.69.9-2.46,1.36-.61.37-1.19.73-1.68.96l-.4.19c-1.42.68-2.64,1.26-6.88,2.24-1.84.42-3.6.72-5.25.87-1.83.17-3.63.24-5.36.3-2.67.09-5.2.18-7.75.64-3.71.66-10.05,2.3-12.35,4.06l-.31.24c-.56.42-1.12.79-1.65,1.15l-.56.38c-.34.23-.68.46-1,.7h0Zm33.25-2.92c6.66-.95,13.55-1.94,15.24-1.13,5.19,2.46,8.53,5.75,9.16,9.01.43,2.24-.38,4.49-2.41,6.69-.13.14-.14.36-.01.5.07.09.18.13.29.13.07,0,.14-.02.21-.06,1.77-1.15,2.85-2.63,3.19-4.4.41-2.09-.25-4.44-1.9-6.81-2.86-4.12-8.44-7.86-13.55-7.02l-2.87.49c-6.86,1.17-13.96,2.38-21.11,2.51-3.49.14-6.74.31-9.6.46l-2.6.13c-1.26.03-2.99.06-3.71,1.54-.12.25-.21.49-.28.72-.04.13-.09.26-.14.39-.1.25-.23.48-.37.72l-.25.41c-.39.65-.8,1.33-1.09,2.09-.33.95-.7,1.84-1.47,2.34-.17.11-.22.34-.12.51.1.17.32.24.5.15,1.05-.54,1.59-1.61,2.01-2.57.3-.63.71-1.22,1.12-1.79l.3-.43c.17-.25.35-.53.5-.85.07-.15.14-.3.2-.45.08-.18.15-.36.24-.52.44-.76,1.61-.7,2.55-.66h.18c2.44-.21,5.22-.33,8.16-.46,3.92-.17,7.98-.34,11.29-.76,2.04-.26,4.2-.57,6.35-.87h0Zm67.46-59.76c-.12-.16-.35-.2-.52-.09-1.5,1.01-3.03,1.2-4.51,1.4-2.11.27-4.11.53-5.42,3.14l-1.4,2.62-2.39,4.11c-.82,1.37-1.66,2.78-2.45,4.3l-.76,1.55-.68,1.6-1.08,3.19-1.05,2.99c-.18.47-.36.94-.56,1.41-.19.46-.39.9-.6,1.32l-.65,1.24-.71,1.14-.78,1-.86.9c-.45.42-.92.83-1.43,1.27-.36.31-.71.61-1.05.92-.34.31-.67.63-.97.96l-.63.74c-.13.16-.11.38.04.52.07.07.16.1.26.1s.19-.04.27-.11l.6-.55c.57-.5,1.21-.95,1.9-1.43l.28-.2c.49-.35,1.01-.71,1.53-1.12l1.02-.89.91-1.01.85-1.16.77-1.27c.24-.44.48-.89.71-1.36.23-.47.44-.94.65-1.43.21-.5.42-.99.61-1.48.2-.51.39-1.03.57-1.53l.83-2.32c.2-.52.39-.99.61-1.5l1.07-2.24c.6-1.15,1.24-2.29,1.87-3.39l1.31-2.33,1.46-2.81,1.3-2.77c.97-2.27,2.48-2.58,4.39-2.98,1.45-.3,3.09-.64,4.64-1.97.15-.13.18-.36.05-.52h0Zm-25.68,57.93l-.53.16c-.19.06-.31.26-.26.46,1.47,5.64,1.18,10.09-.88,13.6-3.7,6.29-12.67,8.59-21.34,10.82-6.97,1.79-13.55,3.48-17.71,7.09-6.27,5.52-11.54,15.02-9.5,22.51.07.24.26.39.49.39.05,0,.1,0,.15-.02.31-.09.57-.46.46-.85-1.88-6.89,3.34-15.71,9.2-20.51,5.49-4.46,10.98-5.68,16.78-6.98,2.92-.65,5.94-1.33,9.1-2.44,6.79-2.34,11.82-6.32,14.15-11.2,1.86-3.89,1.98-8.31.35-12.8-.07-.19-.28-.29-.47-.23h0Z"/>
  </g>
</svg></div>
    <div>
      <div class="kopf-titel">Lieferanten-Bestellung</div>
      <div class="kopf-sub">Pavlova Cafe Berlin</div>
    </div>
  </div>
  <button class="nutzer-btn" onclick="blattOeffnen()">
    <div class="nutzer-av" id="nutzerKuerzel">MK</div>
    <div class="nutzer-nm" id="nutzerName">Marco Koch</div>
  </button>
</div>

<div class="inhalt">

  <!-- BESTELLEN -->
  <div class="ansicht aktiv" id="ansicht-bestellen">
    <div style="font-size:12px;color:var(--tx2);font-weight:500;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px;">Lieferant auswählen</div>
    <div class="pillen" id="lieferantenPillen"></div>
    <div class="suche">
      <svg class="such-icon" viewBox="0 0 16 16"><circle cx="6.5" cy="6.5" r="4.5"/><path d="m10 10 3 3"/></svg>
      <input type="search" id="suchEingabe" placeholder="Artikel suchen..." oninput="produkteAnzeigen()">
    </div>
    <div class="kategorien" id="kategorienLeiste"></div>
    <div id="produktListe"></div>
  </div>

  <!-- WARENKORB -->
  <div class="ansicht" id="ansicht-warenkorb">
    <div class="warenkorb-kopf">
      <div style="font-size:13px;font-weight:600;color:var(--tx2);text-transform:uppercase;letter-spacing:0.5px;">Warenkorb</div>
      <div class="lieferant-tag" id="warenkorbLieferant">Dieter Fuhrmann</div>
    </div>
    <div id="warenkorbPositionen"></div>
    <div id="bestellFormular" style="display:none;">
      <div class="mail-zusammenfassung">
        <div class="mail-zeile"><span style="min-width:30px;">Von:</span><span class="mail-wert">Bestellung@pavlovacafe.de</span></div>
        <div class="mail-zeile"><span style="min-width:30px;">An:</span><span class="mail-wert" id="warenkorbEmpfaenger"></span></div>
        <div class="mail-zeile"><span style="min-width:30px;">CC:</span><span class="mail-wert">Bestellung@pavlovacafe.de</span></div>
      </div>
      <div class="pdf-hinweis">PDF-Bestellformular wird automatisch erstellt und als E-Mail-Anhang versendet.</div>
      <textarea class="notiz" id="bestellNotiz" rows="2" placeholder="Hinweis zur Bestellung (optional)..."></textarea>
      <button class="btn-grau" onclick="pdfVorschau()">
        <svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M9 1H4a1 1 0 00-1 1v12a1 1 0 001 1h8a1 1 0 001-1V5L9 1z"/><path d="M9 1v4h4"/></svg>
        PDF Vorschau speichern
      </button>
      <button class="btn-gruen" onclick="bestellungAbsenden()">
        <svg width="17" height="17" viewBox="0 0 16 16" fill="none" stroke="white" stroke-width="1.5"><path d="M14 2L1 7l5 2m8-7l-6 11-2-4m8-7L6 9"/></svg>
        Bestellung senden
      </button>
    </div>
    <div class="leer-hinweis" id="warenkorbLeer">Noch nichts im Warenkorb</div>
  </div>

  <!-- BESTELLUNGEN -->
  <div class="ansicht" id="ansicht-bestellungen">
    <div id="bestellungsListe"></div>
    <div class="leer-hinweis" id="keineBestellungen">Noch keine Bestellungen</div>
  </div>

  <!-- EINSTELLUNGEN -->
  <div class="ansicht" id="ansicht-einstellungen">

    <div class="einst-abschnitt">
      <div class="einst-titel">Server & E-Mail</div>

      <div class="einst-karte">
        <div class="einst-zeile">
          <div class="einst-info">
            <div class="einst-name">Server-Verbindung</div>
            <div class="einst-sub" id="serverStatusText">Nicht verbunden</div>
          </div>
          <div class="status-punkt" id="serverStatusPunkt"></div>
        </div>
      </div>

      <div class="server-karte">
        <div class="server-feld">
          <div class="server-label">Server-URL (Render.com)</div>
          <input class="mail-eingabe" id="serverAdresse" placeholder="https://pavlova-server.onrender.com" style="width:100%;margin-top:5px;">
          <div style="font-size:11px;color:var(--tx2);margin-top:5px;">Die URL aus dem Render-Dashboard eintragen</div>
        </div>
        <div style="display:flex;gap:8px;margin-top:10px;">
          <button class="hinzufuegen-btn" style="flex:1;" onclick="serverSpeichern()">Speichern</button>
          <button class="hinzufuegen-btn sekundaer" style="flex:1;" onclick="serverTesten()">Verbindung testen</button>
        </div>
      </div>

      <div class="einst-titel" style="margin-top:16px;">SMTP-Einstellungen</div>
      <div class="server-karte">
        <div class="server-feld">
          <div class="server-label">SMTP-Host (Postausgangsserver)</div>
          <input class="mail-eingabe" id="smtpHost" placeholder="mail.pavlovacafe.de" style="width:100%;margin-top:5px;">
        </div>
        <div class="server-feld">
          <div class="server-label">Port</div>
          <input class="mail-eingabe" id="smtpPort" type="number" placeholder="587" style="width:100%;margin-top:5px;">
        </div>
        <div class="server-feld">
          <div class="server-label">Benutzername (E-Mail Adresse)</div>
          <input class="mail-eingabe" id="smtpBenutzer" placeholder="Bestellung@pavlovacafe.de" style="width:100%;margin-top:5px;">
        </div>
        <div class="server-feld">
          <div class="server-label">Passwort</div>
          <input class="mail-eingabe" id="smtpPasswort" type="password" placeholder="E-Mail Passwort" style="width:100%;margin-top:5px;">
        </div>
        <div style="display:flex;gap:8px;margin-top:10px;">
          <button class="hinzufuegen-btn" style="flex:1;" onclick="smtpSpeichern()">Speichern</button>
          <button class="hinzufuegen-btn sekundaer" style="flex:1;" onclick="smtpTesten()">SMTP testen</button>
        </div>
      </div>

      <div class="server-karte">
        <div class="server-feld">
          <div class="server-label">Absender – fest hinterlegt</div>
          <input class="mail-eingabe" value="Bestellung@pavlovacafe.de" readonly style="width:100%;margin-top:5px;">
        </div>
        <div class="server-feld" style="margin-top:10px;margin-bottom:0;">
          <div class="server-label">CC – automatisch bei jeder Bestellung</div>
          <input class="mail-eingabe" value="Bestellung@pavlovacafe.de" readonly style="width:100%;margin-top:5px;">
        </div>
      </div>

      <div class="einst-titel" style="margin-top:16px;">Lieferanten verwalten</div>
      <div class="einst-karte" id="lieferantenEmailListe"></div>
      <div class="einst-karte">
        <div class="eingabe-bereich">
          <div class="eingabe-zeile">
            <input id="neuerLieferantName" placeholder="Lieferantenname *">
          </div>
          <div class="eingabe-zeile">
            <input id="neuerLieferantEmail" placeholder="E-Mail Adresse *" type="email">
          </div>
          <div class="eingabe-zeile">
            <input id="neuerLieferantKategorie" placeholder="Erste Kategorie (z.B. Fleisch)">
          </div>
          <button class="hinzufuegen-btn" onclick="lieferantHinzufuegen()">+ Lieferant anlegen</button>
        </div>
      </div>
    </div>

    <div class="einst-abschnitt">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;">
        <div class="einst-titel" style="margin-bottom:0;">Mitarbeiter</div>
        <button style="font-size:11px;padding:4px 10px;border-radius:8px;border:0.5px solid var(--rand2);background:transparent;color:var(--tx2);cursor:pointer;" onclick="mitarbeiterZuruecksetzen()">Zurücksetzen</button>
      </div>
      <div class="einst-karte" id="mitarbeiterListe"></div>
      <div class="einst-karte">
        <div class="eingabe-bereich">
          <div class="eingabe-zeile">
            <input id="neuerMitarbeiterName" placeholder="Name (z.B. Lisa Müller)">
            <input id="neuerMitarbeiterKuerzel" placeholder="Kürzel" style="max-width:70px;">
          </div>
          <button class="hinzufuegen-btn" onclick="mitarbeiterHinzufuegen()">+ Mitarbeiter hinzufügen</button>
        </div>
      </div>
    </div>

    <div class="einst-abschnitt">
      <div class="einst-titel">Produkte verwalten</div>
      <div class="lief-pillen" id="einstellungenLiefPillen"></div>
      <div class="einst-karte" id="einstellungenProduktListe"></div>
      <div class="einst-karte">
        <div class="eingabe-bereich">
          <input id="neuerArtikelName" placeholder="Artikelname *">
          <div class="eingabe-zeile">
            <input id="neuerArtikelEinheit" placeholder="Einheit *" style="max-width:90px;">
            <input id="neuerArtikelKategorie" placeholder="Kategorie">
            <input id="neuerArtikelNr" placeholder="Art.-Nr." style="max-width:80px;">
          </div>
          <input id="neuerArtikelHinweis" placeholder="Hinweis (optional)">
          <button class="hinzufuegen-btn" onclick="artikelHinzufuegen()">+ Artikel hinzufügen</button>
        </div>
      </div>
    </div>

  </div>
</div>

<div class="nav-leiste">
  <button class="nav-btn aktiv" id="nav-bestellen" onclick="ansichtWechseln('bestellen')">
    <svg viewBox="0 0 24 24"><path d="M6 2L3 6v14a2 2 0 002 2h14a2 2 0 002-2V6l-3-4z"/><line x1="3" y1="6" x2="21" y2="6"/><path d="M16 10a4 4 0 01-8 0"/></svg>
    Bestellen
  </button>
  <button class="nav-btn" id="nav-warenkorb" onclick="ansichtWechseln('warenkorb')">
    <svg viewBox="0 0 24 24"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 002 1.61h9.72a2 2 0 002-1.61L23 6H6"/></svg>
    Warenkorb
    <span class="nav-badge" id="warenkorbBadge"></span>
  </button>
  <button class="nav-btn" id="nav-bestellungen" onclick="ansichtWechseln('bestellungen')">
    <svg viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></svg>
    Bestellungen
    <span class="nav-badge" id="bestellungenBadge"></span>
  </button>
  <button class="nav-btn" id="nav-einstellungen" onclick="ansichtWechseln('einstellungen')">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>
    Einstellungen
  </button>
</div>

<div class="overlay" id="nutzerBlatt" onclick="if(event.target===this)blattSchliessen()">
  <div class="blatt">
    <div class="blatt-titel">Mitarbeiter wechseln</div>
    <div id="blattMitarbeiter"></div>
  </div>
</div>

<div class="meldung" id="meldung"></div>

<script>
const ABSENDER='Bestellung@pavlovacafe.de';
const CC='Bestellung@pavlovacafe.de';

const STANDARD_MITARBEITER=[{id:'MK',name:'Marco Koch'},{id:'AL',name:'Anna Lenz'},{id:'TH',name:'Thomas Huber'}];
let mitarbeiter=[...STANDARD_MITARBEITER];
let aktuellerNutzer=mitarbeiter[0];

const SUPPLIERS = {
  'Dieter Fuhrmann': {email:'bestellung@dieter-fuhrmann.de', cats:['Früchte','Beeren','Kräuter & Kresse','Gemüse','Milchprodukte'], products:[
    {id:1,nr:'',name:'Rhabarber',unit:'KG',cat:'Früchte',hint:''},{id:2,nr:'',name:'Erdbeeren',unit:'KG',cat:'Beeren',hint:''},{id:3,nr:'',name:'Himbeeren',unit:'Schalen',cat:'Beeren',hint:''},{id:4,nr:'',name:'Heidelbeeren',unit:'Schalen',cat:'Beeren',hint:'Wenn möglich kleine Beeren'},{id:5,nr:'',name:'Brombeeren',unit:'Schalen',cat:'Beeren',hint:''},{id:6,nr:'',name:'Passionsfrüchte / Maracuja',unit:'KG',cat:'Früchte',hint:''},{id:7,nr:'',name:'Mango vorgereift',unit:'STK',cat:'Früchte',hint:''},{id:8,nr:'',name:'Mango fest',unit:'STK',cat:'Früchte',hint:'Bitte feste Mangos!!!'},{id:9,nr:'',name:'Cranberry',unit:'Tüten',cat:'Früchte',hint:'Frische Ware'},{id:10,nr:'',name:'Kiwi lose',unit:'STK',cat:'Früchte',hint:''},{id:11,nr:'',name:'Avocado',unit:'STK',cat:'Früchte',hint:''},{id:12,nr:'',name:'Orangen',unit:'KG',cat:'Früchte',hint:''},{id:13,nr:'',name:'Limetten',unit:'STK',cat:'Früchte',hint:''},{id:14,nr:'',name:'Zitronen',unit:'STK',cat:'Früchte',hint:''},{id:15,nr:'',name:'Granatapfel',unit:'STK',cat:'Früchte',hint:''},{id:16,nr:'',name:'Äpfel',unit:'KG',cat:'Früchte',hint:'Preiswerte Äpfel'},{id:17,nr:'',name:'Ingwer',unit:'STK',cat:'Früchte',hint:''},{id:18,nr:'',name:'Minze',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:19,nr:'',name:'Rosmarin',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:20,nr:'',name:'Erbsenkresse (Affilakresse)',unit:'Schalen',cat:'Kräuter & Kresse',hint:'von Koppert Cress'},{id:21,nr:'',name:'Porreesprossen',unit:'Schalen',cat:'Kräuter & Kresse',hint:''},{id:22,nr:'',name:'Schnittlauch',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:23,nr:'',name:'Petersilie Krause',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:24,nr:'',name:'Dill',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:25,nr:'',name:'Basilikum',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:26,nr:'',name:'Rucola',unit:'Bund',cat:'Kräuter & Kresse',hint:''},{id:27,nr:'',name:'Kresse',unit:'Schalen',cat:'Kräuter & Kresse',hint:''},{id:28,nr:'',name:'Lollo Rosso',unit:'Kopf',cat:'Gemüse',hint:'Bitte frische Ware'},{id:29,nr:'',name:'Lollo Bianco',unit:'Kopf',cat:'Gemüse',hint:''},{id:30,nr:'',name:'Drillinge mit Schale vorgegart',unit:'STK',cat:'Gemüse',hint:''},{id:31,nr:'',name:'Kleine Strauchtomaten',unit:'KG',cat:'Gemüse',hint:''},{id:32,nr:'',name:'Schlagsahne Frankenland 33% 1L',unit:'STK',cat:'Milchprodukte',hint:'Mindestens 33% Fett'},{id:33,nr:'',name:'Frischmilch 3,5% 1L',unit:'STK',cat:'Milchprodukte',hint:'Pasteurisiert, keine H-Milch, Tetra 1L'},{id:34,nr:'',name:'Alpro Barista Hafermilch 1L',unit:'STK',cat:'Milchprodukte',hint:''},{id:35,nr:'',name:'Alpro Barista Mandelmilch 1L',unit:'STK',cat:'Milchprodukte',hint:''},{id:36,nr:'',name:'Alpro Sojamilch 1L',unit:'STK',cat:'Milchprodukte',hint:''},{id:37,nr:'',name:'Alpro Barista Kokosmilch 1L',unit:'STK',cat:'Milchprodukte',hint:''},{id:38,nr:'',name:'Milch Laktosefrei 1L',unit:'STK',cat:'Milchprodukte',hint:''},{id:39,nr:'',name:'Eier 10er Packung',unit:'STK',cat:'Milchprodukte',hint:''},{id:40,nr:'',name:'Körniger Frischkäse ca. 200g',unit:'Becher',cat:'Milchprodukte',hint:''},{id:41,nr:'',name:'Jogurt 1 kg',unit:'Becher',cat:'Milchprodukte',hint:''},{id:42,nr:'',name:'Butter 250g',unit:'STK',cat:'Milchprodukte',hint:''},{id:43,nr:'',name:'Crème Fraîche',unit:'Becher',cat:'Milchprodukte',hint:''},
  ]},
  'Preuss Getränke': {email:'Bestellung@getraenke-pm.de', cats:['Wasser & Mineralwasser','Säfte & Limonaden','Bier','Sonstiges'], products:[
    {id:201,nr:'13352',name:'Lammsbräu Edel Pils',unit:'Mw 20x0,33 (BIO)',cat:'Bier',hint:''},{id:202,nr:'28075',name:'Lammsbräu Edell Hell',unit:'Mw 10x0,33 (BIO)',cat:'Bier',hint:''},{id:203,nr:'461783',name:'Bauer R wie Rhabarber',unit:'Mw 24x0,33',cat:'Säfte & Limonaden',hint:''},{id:204,nr:'29106',name:'Now Bio Apfelschorle',unit:'Mw 10x0,50 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:205,nr:'29107',name:'Now Bio Mate Granate',unit:'Mw 10x0,50',cat:'Säfte & Limonaden',hint:''},{id:206,nr:'416220',name:'Now Black Cola',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:207,nr:'29105',name:'Now Cassis Lime',unit:'Mw 10x0,50 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:208,nr:'416223',name:'Now Fresh Lemon',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:209,nr:'1352',name:'Now Grape Fruit Mix',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:210,nr:'3095',name:'Now Holler Blüte',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:211,nr:'27830',name:'Now Limo Light Black Cola',unit:'10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:212,nr:'416226',name:'Now Orange Cola',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:213,nr:'416225',name:'Now Red Berry',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:214,nr:'416224',name:'Now Sunny Orange',unit:'Mw 10x0,33 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:215,nr:'1359',name:'Thomas Henry Spicy Ginger',unit:'Mw 24x0,20',cat:'Säfte & Limonaden',hint:''},{id:216,nr:'1357',name:'Thomas Henry Tonic Water',unit:'Mw 24x0,20',cat:'Säfte & Limonaden',hint:''},{id:217,nr:'461734',name:'Bauer Cranberry Fruit Drink',unit:'Mw 6x1,00',cat:'Säfte & Limonaden',hint:''},{id:218,nr:'461789',name:'Bauer Orangensaft',unit:'Mw 6x0,98 (BIO)',cat:'Säfte & Limonaden',hint:''},{id:219,nr:'461704',name:'Bauer Orangensaft',unit:'Mw 6x1,00',cat:'Säfte & Limonaden',hint:''},{id:220,nr:'413817',name:'Adello Medium PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:221,nr:'416505',name:'Adello Mineralwasser PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:222,nr:'13034',name:'Adello Naturell PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:223,nr:'3428',name:'BioKristall Medium',unit:'Mw 10x0,33 Gastro',cat:'Wasser & Mineralwasser',hint:''},{id:224,nr:'3429',name:'BioKristall Medium',unit:'Mw 6x0,75 (BIO)',cat:'Wasser & Mineralwasser',hint:''},{id:225,nr:'4128',name:'BioKristall Still',unit:'Mw 6x0,75 (BIO)',cat:'Wasser & Mineralwasser',hint:''},{id:226,nr:'416237',name:'BioKristall Still',unit:'Mw 10x0,33 Gastro',cat:'Wasser & Mineralwasser',hint:''},{id:227,nr:'416538',name:'BLW Medium PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:228,nr:'416541',name:'BLW Naturell PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:229,nr:'6112',name:'BLW Spritzig PET',unit:'Mw 12x1,00',cat:'Wasser & Mineralwasser',hint:''},{id:230,nr:'416522',name:'Bauer Glühwein Rot',unit:'Mw 6x1,00',cat:'Sonstiges',hint:''},
  ]},
  'Terra Naturkost': {email:'Verkauf@terra-natur.de', cats:['Backwaren'], products:[
    {id:301,nr:'',name:'Baguette',unit:'STK',cat:'Backwaren',hint:''},{id:302,nr:'',name:'Ciabatta',unit:'STK',cat:'Backwaren',hint:''},{id:303,nr:'',name:'Brötchen',unit:'10er',cat:'Backwaren',hint:''},
  ]},
  'Transgourmet': {email:'Alessandro.stettnisch@transgourmet.de', cats:['Fleisch'], products:[
    {id:401,nr:'',name:'Hähnchenfilet',unit:'KG',cat:'Fleisch',hint:''},{id:402,nr:'',name:'Rinderfilet',unit:'KG',cat:'Fleisch',hint:''},
  ]},
};

let warenkorb={}, aktuellerLieferant='Dieter Fuhrmann', aktuelleKategorie='Alle';
let bestellungen=[], einstellungenLieferant='Dieter Fuhrmann', naechsteId=5000;

// ── Speichern / Laden ────────────────────────────────────────────
function speichern(){
  try{
    localStorage.setItem('pv_mitarbeiter',JSON.stringify(mitarbeiter));
    localStorage.setItem('pv_nutzer_id',aktuellerNutzer.id);
    const sd={};
    Object.keys(SUPPLIERS).forEach(k=>{sd[k]={email:SUPPLIERS[k].email,products:SUPPLIERS[k].products,cats:SUPPLIERS[k].cats};});
    localStorage.setItem('pv_lieferanten',JSON.stringify(sd));
  }catch(e){}
}

function laden(){
  try{
    const m=localStorage.getItem('pv_mitarbeiter');
    if(m){const p=JSON.parse(m);if(p&&p.length)mitarbeiter=p;}
    const uid=localStorage.getItem('pv_nutzer_id');
    if(uid){const f=mitarbeiter.find(m=>m.id===uid);if(f)aktuellerNutzer=f;}
    const sd=localStorage.getItem('pv_lieferanten');
    if(sd){
      const p=JSON.parse(sd);
      Object.keys(p).forEach(k=>{
        if(SUPPLIERS[k]){
          // Bestehenden Lieferanten aktualisieren
          SUPPLIERS[k].products=p[k].products;
          SUPPLIERS[k].cats=p[k].cats;
          if(p[k].email)SUPPLIERS[k].email=p[k].email;
        } else {
          // Neuen gespeicherten Lieferanten wiederherstellen
          SUPPLIERS[k]={email:p[k].email||'',cats:p[k].cats||['Allgemein'],products:p[k].products||[]};
        }
      });
    }
    const su=localStorage.getItem('pv_server_url');
    if(su&&document.getElementById('serverAdresse'))document.getElementById('serverAdresse').value=su;
  }catch(e){}
}

// ── Hilfsfunktionen ──────────────────────────────────────────────
function esc(s){return s.replace(/'/g,"'");}

function meldungZeigen(text){
  const m=document.getElementById('meldung');
  m.textContent=text;m.classList.add('aktiv');
  setTimeout(()=>m.classList.remove('aktiv'),2600);
}

function ansichtWechseln(name){
  document.querySelectorAll('.ansicht').forEach(e=>e.classList.remove('aktiv'));
  document.querySelectorAll('.nav-btn').forEach(e=>e.classList.remove('aktiv'));
  document.getElementById('ansicht-'+name).classList.add('aktiv');
  document.getElementById('nav-'+name).classList.add('aktiv');
  if(name==='bestellungen')bestellungenAnzeigen();
  if(name==='warenkorb')warenkorbAnzeigen();
  if(name==='einstellungen'){
    mitarbeiterListeAnzeigen();
    einstellungenLieferantenPillen();
    einstellungenProdukteAnzeigen();
    lieferantenEmailsAnzeigen();
    const su=localStorage.getItem('pv_server_url');
    if(su){const el=document.getElementById('serverAdresse');if(el)el.value=su;}
    serverStatusPruefen();
  }
}

// ── Nutzer-Blatt ──────────────────────────────────────────────────
function blattOeffnen(){
  document.getElementById('blattMitarbeiter').innerHTML=mitarbeiter.map(m=>`
    <div class="blatt-zeile ${m.id===aktuellerNutzer.id?'aktiv':''}" onclick="nutzerWaehlen('${m.id}')">
      <div class="blatt-haken"></div>
      <div class="blatt-name">${m.name}</div>
    </div>`).join('');
  document.getElementById('nutzerBlatt').classList.add('aktiv');
}
function blattSchliessen(){document.getElementById('nutzerBlatt').classList.remove('aktiv');}
function nutzerWaehlen(id){
  aktuellerNutzer=mitarbeiter.find(m=>m.id===id)||mitarbeiter[0];
  document.getElementById('nutzerKuerzel').textContent=aktuellerNutzer.id;
  document.getElementById('nutzerName').textContent=aktuellerNutzer.name;
  localStorage.setItem('pv_nutzer_id',aktuellerNutzer.id);
  blattSchliessen();
}

// ── Lieferanten-Pillen ────────────────────────────────────────────
function lieferantenPillenErstellen(){
  document.getElementById('lieferantenPillen').innerHTML=Object.keys(SUPPLIERS).map((n,i)=>
    `<div class="pille ${i===0?'aktiv':''}" onclick="lieferantWaehlen(this,'${esc(n)}')">${n}</div>`
  ).join('');
}

function lieferantWaehlen(el,name){
  document.querySelectorAll('#lieferantenPillen .pille').forEach(p=>p.classList.remove('aktiv'));
  el.classList.add('aktiv');
  aktuellerLieferant=name;warenkorb={};aktuelleKategorie='Alle';
  document.getElementById('suchEingabe').value='';
  document.getElementById('warenkorbLieferant').textContent=name;
  document.getElementById('warenkorbEmpfaenger').textContent=SUPPLIERS[name].email;
  kategorienAnzeigen();produkteAnzeigen();badgeAktualisieren();
}

function kategorienAnzeigen(){
  const kats=['Alle',...SUPPLIERS[aktuellerLieferant].cats];
  document.getElementById('kategorienLeiste').innerHTML=kats.map(k=>
    `<button class="kat-btn ${k===aktuelleKategorie?'aktiv':''}" onclick="kategorieWaehlen(this,'${esc(k)}')">${k}</button>`
  ).join('');
}

function kategorieWaehlen(el,kat){
  document.querySelectorAll('.kat-btn').forEach(b=>b.classList.remove('aktiv'));
  el.classList.add('aktiv');aktuelleKategorie=kat;produkteAnzeigen();
}

function produkteAnzeigen(){
  const suche=document.getElementById('suchEingabe').value.toLowerCase();
  const prods=SUPPLIERS[aktuellerLieferant].products.filter(p=>
    (aktuelleKategorie==='Alle'||p.cat===aktuelleKategorie)&&
    (p.name.toLowerCase().includes(suche)||(p.nr&&p.nr.includes(suche)))
  );
  const zeigeNr=aktuellerLieferant.indexOf('Preuss')>=0;
  document.getElementById('produktListe').innerHTML=prods.length?prods.map(p=>{
    const m=warenkorb[p.id]||0;
    return`<div class="produkt-zeile">
      <div class="prod-info">
        <div class="prod-name">${p.name}</div>
        <div class="prod-meta">${p.unit}${zeigeNr&&p.nr?' · Nr.'+p.nr:''}</div>
        ${p.hint?`<div class="prod-hinweis">${p.hint}</div>`:''}
      </div>
      <div class="menge-steuerung">
        <button class="menge-btn" onclick="mengeAendern(${p.id},-1)">−</button>
        <span class="menge-zahl" id="m${p.id}">${m||''}</span>
        <button class="menge-btn" onclick="mengeAendern(${p.id},1)">+</button>
      </div>
    </div>`;
  }).join(''):'<div style="padding:2rem 0;text-align:center;color:var(--tx2);">Keine Artikel gefunden</div>';
}

function mengeAendern(id,d){
  const n=Math.max(0,(warenkorb[id]||0)+d);
  if(n===0)delete warenkorb[id];else warenkorb[id]=n;
  const el=document.getElementById('m'+id);if(el)el.textContent=n||'';
  badgeAktualisieren();
}

function badgeAktualisieren(){
  const z=Object.keys(warenkorb).length;
  const b=document.getElementById('warenkorbBadge');
  b.style.display=z?'block':'none';b.textContent=z;
}

function warenkorbAnzeigen(){
  const keys=Object.keys(warenkorb);
  const sup=SUPPLIERS[aktuellerLieferant];
  document.getElementById('warenkorbLieferant').textContent=aktuellerLieferant;
  document.getElementById('warenkorbEmpfaenger').textContent=sup.email;
  if(!keys.length){
    document.getElementById('warenkorbPositionen').innerHTML='';
    document.getElementById('warenkorbLeer').style.display='block';
    document.getElementById('bestellFormular').style.display='none';
    return;
  }
  document.getElementById('warenkorbLeer').style.display='none';
  document.getElementById('bestellFormular').style.display='block';
  document.getElementById('warenkorbPositionen').innerHTML=keys.map(id=>{
    const p=sup.products.find(x=>x.id==id);if(!p)return'';
    return`<div class="warenkorb-pos">
      <div class="wk-info">
        <div class="wk-name">${p.name}</div>
        <div class="wk-detail">${warenkorb[id]} × ${p.unit}</div>
      </div>
      <button class="wk-loeschen" onclick="positionLoeschen(${id})">×</button>
    </div>`;
  }).join('');
}

function positionLoeschen(id){
  delete warenkorb[id];
  const el=document.getElementById('m'+id);if(el)el.textContent='';
  badgeAktualisieren();warenkorbAnzeigen();
}

// ── PDF ───────────────────────────────────────────────────────────
function buildPDFContent(doc, o) {
  const W=210, ml=18, mr=18, cw=W-ml-mr;
  const beige=[196,191,182], dk=[50,50,50], mid=[120,120,120], lg=[235,233,230], grn=[29,158,117], amr=[180,120,30];
  doc.setFillColor(...beige); doc.rect(0,0,W,36,'F');
  doc.setFont('helvetica','bold'); doc.setFontSize(15); doc.setTextColor(...dk);
  doc.text('Pavlova Cafe Berlin', ml+6, 16);
  doc.setFont('helvetica','normal'); doc.setFontSize(8.5); doc.setTextColor(...mid);
  doc.text('Kurfuerstendamm 210  |  10719 Berlin  |  Tel: 030 85621805', ml+6, 22);
  doc.text('Bestellung@pavlovacafe.de', ml+6, 27);
  doc.setFillColor(255,255,255); doc.rect(0,36,W,14,'F');
  doc.setFont('helvetica','bold'); doc.setFontSize(12); doc.setTextColor(...dk);
  doc.text('BESTELLUNG  ' + o.id, ml, 47);
  doc.setDrawColor(...beige); doc.setLineWidth(0.5); doc.line(ml,51,W-mr,51);
  let y=60;
  const cols=[ml,ml+52,ml+104,ml+155];
  const labels=['LIEFERANT','BESTELLDATUM','ANLIEFERUNG','BESTELLER'];
  const vals=[o.supplier,o.date,o.delivDate||o.date,o.user];
  labels.forEach((l,i)=>{ doc.setFont('helvetica','normal'); doc.setFontSize(7.5); doc.setTextColor(...mid); doc.text(l,cols[i],y); doc.setFont('helvetica','bold'); doc.setFontSize(9.5); doc.setTextColor(...dk); doc.text((vals[i]||'').substring(0,22),cols[i],y+5); });
  const sup=SUPPLIERS[o.supplier];
  if(sup){ doc.setFont('helvetica','normal'); doc.setFontSize(7.5); doc.setTextColor(...mid); doc.text(sup.email.substring(0,30),cols[0],y+10); }
  y=82;
  doc.setFillColor(...beige); doc.roundedRect(ml,y-5,cw,8,1,1,'F');
  doc.setFont('helvetica','bold'); doc.setFontSize(8); doc.setTextColor(...dk);
  doc.text('POS',ml+3,y); doc.text('ARTIKEL',ml+15,y);
  doc.text('EINHEIT',ml+cw-52,y); doc.text('MENGE',ml+cw-20,y);
  y+=8;
  const showNr=o.supplier.indexOf('Preuss')>=0||o.supplier.indexOf('Getraenke')>=0;
  let pos=1, lastCat='';
  o.items.forEach(item=>{
    if(y>268){doc.addPage();y=20;}
    if(item.cat&&item.cat!==lastCat){lastCat=item.cat;doc.setFillColor(...lg);doc.rect(ml,y-3.5,cw,6.5,'F');doc.setFont('helvetica','bold');doc.setFontSize(7);doc.setTextColor(...mid);doc.text(item.cat.toUpperCase(),ml+3,y+1);y+=9;}
    if(y>268){doc.addPage();y=20;}
    if(pos%2===0){doc.setFillColor(250,249,247);doc.rect(ml,y-4,cw,7.5,'F');}
    doc.setFont('helvetica','normal');doc.setFontSize(9);doc.setTextColor(...dk);
    doc.text(String(pos),ml+3,y);
    let nm=item.name;if(showNr&&item.nr)nm+=' (Nr.'+item.nr+')';if(nm.length>52)nm=nm.substring(0,52)+'...';
    doc.text(nm,ml+15,y);
    let ut=item.unit;if(ut.length>18)ut=ut.substring(0,18);doc.text(ut,ml+cw-52,y);
    doc.setDrawColor(...beige);doc.setLineWidth(0.3);doc.roundedRect(ml+cw-25,y-4,18,7,1,1,'S');
    doc.setFont('helvetica','bold');doc.setFontSize(10);doc.setTextColor(...grn);
    doc.text(String(item.qty),ml+cw-16,y,{align:'center'});
    if(item.hint){y+=5;doc.setFont('helvetica','italic');doc.setFontSize(7);doc.setTextColor(...amr);doc.text('  Hinweis: '+item.hint.substring(0,60),ml+15,y);}
    pos++;y+=8;
  });
  if(o.note&&y<270){y+=4;doc.setFillColor(255,252,235);doc.roundedRect(ml,y-4,cw,11,1.5,1.5,'F');doc.setFont('helvetica','bold');doc.setFontSize(8);doc.setTextColor(...amr);doc.text('HINWEIS:',ml+4,y+1);doc.setFont('helvetica','normal');doc.setFontSize(8);doc.setTextColor(...dk);doc.text(doc.splitTextToSize(o.note,cw-36),ml+28,y+1);}
  doc.setFillColor(...beige);doc.rect(0,279,W,18,'F');
  doc.setFont('helvetica','normal');doc.setFontSize(7.5);doc.setTextColor(...dk);
  doc.text('Pavlova Cafe Berlin  |  Kurfuerstendamm 210, 10719 Berlin  |  Bestellung@pavlovacafe.de',W/2,285,{align:'center'});
  doc.setTextColor(...mid);
  doc.text('Bestellung '+o.id+' vom '+o.date+' um '+o.time+'  |  Besteller: '+o.user,W/2,291,{align:'center'});
}

function generatePDF(o, doDownload) {
  const {jsPDF}=window.jspdf;
  const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
  buildPDFContent(doc,o);
  const fname='Bestellung_'+o.id+'_'+o.supplier.replace(/\s+/g,'_')+'_'+o.date.replace(/\./g,'-')+'.pdf';
  if(doDownload) doc.save(fname);
  return fname;
}

function pdfVorschau(){
  const keys=Object.keys(warenkorb);if(!keys.length){meldungZeigen('Warenkorb ist leer');return;}
  const sup=SUPPLIERS[aktuellerLieferant];
  const positionen=keys.map(id=>{const p=sup.products.find(x=>x.id==id);return{name:p.name,qty:warenkorb[id],unit:p.unit,nr:p.nr||'',cat:p.cat,hint:p.hint||''};});
  const ldt=new Date();ldt.setDate(ldt.getDate()+1);
  const o={id:'Vorschau',supplier:aktuellerLieferant,email:sup.email,user:aktuellerNutzer.name,
    date:new Date().toLocaleDateString('de-DE'),
    time:new Date().toLocaleTimeString('de-DE',{hour:'2-digit',minute:'2-digit'}),
    delivDate:ldt.toLocaleDateString('de-DE'),
    items:positionen,note:document.getElementById('bestellNotiz').value};
  const {jsPDF}=window.jspdf;
  const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
  buildPDFContent(doc,o);
  doc.save('Bestellung_Vorschau.pdf');
  meldungZeigen('PDF wird gespeichert...');
}

function pdfAlsBase64(o){
  const {jsPDF}=window.jspdf;
  const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
  buildPDFContent(doc,o);
  return doc.output('datauristring').split(',')[1];
}

// ── Bestellung absenden ───────────────────────────────────────────
function bestellungAbsenden(){
  const keys=Object.keys(warenkorb);if(!keys.length)return;
  const sup=SUPPLIERS[aktuellerLieferant];
  const positionen=keys.map(id=>{const p=sup.products.find(x=>x.id==id);return{name:p.name,qty:warenkorb[id],unit:p.unit,nr:p.nr||'',cat:p.cat,hint:p.hint||''};});
  const ldt=new Date();ldt.setDate(ldt.getDate()+1);
  const bestellung={
    id:'B-'+(bestellungen.length+101),
    supplier:aktuellerLieferant,email:sup.email,user:aktuellerNutzer.name,
    date:new Date().toLocaleDateString('de-DE'),
    time:new Date().toLocaleTimeString('de-DE',{hour:'2-digit',minute:'2-digit'}),
    delivDate:ldt.toLocaleDateString('de-DE'),
    items:positionen,note:document.getElementById('bestellNotiz').value,status:'offen'
  };

  const pdfB64=pdfAlsBase64(bestellung);
  const dateiname='Bestellung_'+bestellung.id+'_'+bestellung.supplier.replace(/\s+/g,'_')+'_'+bestellung.date.replace(/\./g,'-')+'.pdf';
  const betreff='Bestellung '+bestellung.id+' – Pavlova Cafe Berlin – '+bestellung.date;
  const inhalt='Guten Tag,

anbei unsere Bestellung '+bestellung.id+' vom '+bestellung.date+' als PDF-Anlage.

'
    +'Anlieferung: '+bestellung.delivDate+'
Besteller: '+bestellung.user
    +(bestellung.note?'
Hinweis: '+bestellung.note:'')
    +'

Mit freundlichen Grüßen
Pavlova Cafe Berlin
Kurfürstendamm 210, 10719 Berlin
Tel: 030 85621805';

  bestellungen.unshift(bestellung);warenkorb={};
  document.getElementById('bestellNotiz').value='';
  badgeAktualisieren();warenkorbAnzeigen();
  const bb=document.getElementById('bestellungenBadge');bb.style.display='block';bb.textContent=bestellungen.length;

  viaSeverSenden(bestellung,pdfB64,dateiname,betreff,inhalt,sup.email).then(ok=>{
    if(!ok){
      const {jsPDF}=window.jspdf;
      const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
      buildPDFContent(doc,bestellung);doc.save(dateiname);
      const mailto='mailto:'+sup.email+'?cc='+encodeURIComponent(CC)+'&subject='+encodeURIComponent(betreff)+'&body='+encodeURIComponent(inhalt);
      setTimeout(()=>{window.location.href=mailto;},600);
      meldungZeigen('PDF gespeichert – E-Mail öffnet sich');
    }
    bestellungenAnzeigen();
    setTimeout(()=>ansichtWechseln('bestellungen'),900);
  });
}

async function viaSeverSenden(bestellung,pdfB64,dateiname,betreff,inhalt,empfaenger){
  const url=(localStorage.getItem('pv_server_url')||'').replace(/\/+$/,'');
  if(!url)return false;
  try{
    meldungZeigen('Bestellung wird gesendet…');
    const res=await fetch(url+'/api/send-order',{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({to:empfaenger,cc:CC,subject:betreff,body:inhalt,pdfBase64:pdfB64,pdfFilename:dateiname,orderId:bestellung.id}),
      signal:AbortSignal.timeout(15000)
    });
    const d=await res.json();
    if(d.ok){meldungZeigen('✅ Bestellung '+bestellung.id+' erfolgreich gesendet!');return true;}
    meldungZeigen('⚠️ Fehler: '+d.error);return false;
  }catch(e){meldungZeigen('⚠️ Kein Server – Fallback auf E-Mail-App');return false;}
}

// ── Bestellungen ──────────────────────────────────────────────────
function bestellungenAnzeigen(){
  document.getElementById('keineBestellungen').style.display=bestellungen.length?'none':'block';
  document.getElementById('bestellungsListe').innerHTML=bestellungen.map(b=>{
    const farbe=b.status==='offen'?'#EF9F27':b.status==='bestaetigt'?'#1D9E75':'#888780';
    const text=b.status==='offen'?'Offen':b.status==='bestaetigt'?'Bestätigt':'Geliefert';
    const klasse='s-'+(b.status==='offen'?'offen':b.status==='bestaetigt'?'bestaetigt':'geliefert');
    const sup=SUPPLIERS[b.supplier];
    const mailto='mailto:'+(sup?sup.email:'')+'?cc='+encodeURIComponent(CC)+'&subject='+encodeURIComponent('Bestellung '+b.id+' – Pavlova Cafe Berlin – '+b.date);
    return`<div class="bestell-karte">
      <div class="bk-kopf">
        <div style="width:8px;height:8px;border-radius:50%;background:${farbe};flex-shrink:0;"></div>
        <span class="bk-nr">${b.id}</span>
        <span class="bk-tag">${b.supplier}</span>
        <button class="status-pille ${klasse}" onclick="statusWechseln('${b.id}')">${text}</button>
      </div>
      <div class="bk-info">${b.date} ${b.time} · ${b.user} · ${b.items.length} Artikel${b.note?' · "'+b.note.substring(0,22)+'"':''}</div>
      <div class="bk-aktionen">
        <button class="aktion-btn" onclick="pdfNeuErstellen('${b.id}')">PDF herunterladen</button>
        <button class="aktion-btn" onclick="window.location.href='${mailto.replace(/'/g,"\'")}'"  >E-Mail erneut senden</button>
      </div>
    </div>`;
  }).join('');
}

function statusWechseln(id){
  const b=bestellungen.find(x=>x.id===id);if(!b)return;
  const f=['offen','bestaetigt','geliefert'];b.status=f[(f.indexOf(b.status)+1)%3];
  bestellungenAnzeigen();
}

function pdfNeuErstellen(id){
  const b=bestellungen.find(x=>x.id===id);if(!b)return;
  const {jsPDF}=window.jspdf;
  const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
  buildPDFContent(doc,b);
  doc.save('Bestellung_'+b.id+'.pdf');
  meldungZeigen('PDF gespeichert');
}

// ── Einstellungen ─────────────────────────────────────────────────
function mitarbeiterListeAnzeigen(){
  document.getElementById('mitarbeiterListe').innerHTML=mitarbeiter.map(m=>`
    <div class="einst-zeile">
      <div class="nutzer-av" style="width:30px;height:30px;font-size:11px;flex-shrink:0;">${m.id}</div>
      <div class="einst-info"><div class="einst-name">${m.name}</div></div>
      ${mitarbeiter.length>1?`<button class="loeschen-btn" onclick="mitarbeiterLoeschen('${m.id}')">×</button>`:''}
    </div>`).join('');
}

function mitarbeiterHinzufuegen(){
  const name=document.getElementById('neuerMitarbeiterName').value.trim();
  let kuerzel=document.getElementById('neuerMitarbeiterKuerzel').value.trim().toUpperCase();
  if(!name)return;
  if(!kuerzel)kuerzel=name.split(' ').map(w=>w[0]).join('').substring(0,2).toUpperCase();
  if(mitarbeiter.find(m=>m.id===kuerzel))kuerzel=kuerzel+(mitarbeiter.length+1);
  mitarbeiter.push({id:kuerzel,name});
  document.getElementById('neuerMitarbeiterName').value='';
  document.getElementById('neuerMitarbeiterKuerzel').value='';
  speichern();mitarbeiterListeAnzeigen();meldungZeigen(name+' gespeichert');
}

function mitarbeiterLoeschen(id){
  if(aktuellerNutzer.id===id){meldungZeigen('Aktiven Nutzer nicht löschbar');return;}
  mitarbeiter=mitarbeiter.filter(m=>m.id!==id);speichern();mitarbeiterListeAnzeigen();
}

function mitarbeiterZuruecksetzen(){
  if(!confirm('Mitarbeiterliste auf Standard zurücksetzen?'))return;
  mitarbeiter=[...STANDARD_MITARBEITER];aktuellerNutzer=mitarbeiter[0];
  document.getElementById('nutzerKuerzel').textContent=aktuellerNutzer.id;
  document.getElementById('nutzerName').textContent=aktuellerNutzer.name;
  speichern();mitarbeiterListeAnzeigen();meldungZeigen('Zurückgesetzt');
}

function lieferantenEmailsAnzeigen(){
  document.getElementById('lieferantenEmailListe').innerHTML=Object.entries(SUPPLIERS).map(([n,s])=>`
    <div class="einst-zeile">
      <div class="einst-info"><div class="einst-name">${n}</div><div class="einst-sub">${s.email}</div></div>
      <button class="loeschen-btn" onclick="lieferantLoeschen('${n.replace(/'/g,"\'")}')">×</button>
    </div>`).join('');
}

function lieferantHinzufuegen(){
  const name=document.getElementById('neuerLieferantName').value.trim();
  const email=document.getElementById('neuerLieferantEmail').value.trim();
  const kat=document.getElementById('neuerLieferantKategorie').value.trim()||'Allgemein';
  if(!name||!email){meldungZeigen('Name und E-Mail sind Pflichtfelder');return;}
  if(SUPPLIERS[name]){meldungZeigen('Lieferant existiert bereits');return;}
  SUPPLIERS[name]={email,cats:[kat],products:[]};
  document.getElementById('neuerLieferantName').value='';
  document.getElementById('neuerLieferantEmail').value='';
  document.getElementById('neuerLieferantKategorie').value='';
  speichern();
  lieferantenEmailsAnzeigen();
  einstellungenLieferantenPillen();
  lieferantenPillenErstellen();
  meldungZeigen(name+' angelegt');
}

function lieferantLoeschen(name){
  const standardLieferanten=['Dieter Fuhrmann','Preuss Getraenke','Terra Naturkost','Transgourmet'];
  if(!confirm(name+' wirklich löschen?'))return;
  delete SUPPLIERS[name];
  if(aktuellerLieferant===name){
    aktuellerLieferant=Object.keys(SUPPLIERS)[0];
    warenkorb={};
    badgeAktualisieren();
  }
  if(einstellungenLieferant===name){
    einstellungenLieferant=Object.keys(SUPPLIERS)[0];
  }
  speichern();
  lieferantenEmailsAnzeigen();
  einstellungenLieferantenPillen();
  einstellungenProdukteAnzeigen();
  lieferantenPillenErstellen();
  kategorienAnzeigen();
  produkteAnzeigen();
  meldungZeigen(name+' gelöscht');
}

function einstellungenLieferantenPillen(){
  document.getElementById('einstellungenLiefPillen').innerHTML=Object.keys(SUPPLIERS).map(n=>
    `<button class="lief-pille ${n===einstellungenLieferant?'aktiv':''}" onclick="einstellungenLieferantWaehlen('${esc(n)}')">${n}</button>`
  ).join('');
}

function einstellungenLieferantWaehlen(n){
  einstellungenLieferant=n;einstellungenLieferantenPillen();einstellungenProdukteAnzeigen();
}

function einstellungenProdukteAnzeigen(){
  const sup=SUPPLIERS[einstellungenLieferant];
  document.getElementById('einstellungenProduktListe').innerHTML=sup.products.map(p=>`
    <div class="einst-zeile">
      <div class="einst-info">
        <div class="einst-name">${p.name}</div>
        <div class="einst-sub">${p.unit} · ${p.cat}${p.nr?' · Nr.'+p.nr:''}${p.hint?' · '+p.hint:''}</div>
      </div>
      <button class="loeschen-btn" onclick="artikelLoeschen(${p.id})">×</button>
    </div>`).join('')||'<div class="einst-zeile"><div style="color:var(--tx2);font-size:13px;">Noch keine Artikel</div></div>';
}

function artikelHinzufuegen(){
  const name=document.getElementById('neuerArtikelName').value.trim();
  const einheit=document.getElementById('neuerArtikelEinheit').value.trim();
  const kat=document.getElementById('neuerArtikelKategorie').value.trim();
  const nr=document.getElementById('neuerArtikelNr').value.trim();
  const hinweis=document.getElementById('neuerArtikelHinweis').value.trim();
  if(!name||!einheit){meldungZeigen('Name und Einheit sind Pflichtfelder');return;}
  const sup=SUPPLIERS[einstellungenLieferant],id=++naechsteId;
  sup.products.push({id,nr,name,unit:einheit,cat:kat||sup.cats[0]||'Allgemein',hint:hinweis});
  if(kat&&!sup.cats.includes(kat))sup.cats.push(kat);
  ['neuerArtikelName','neuerArtikelEinheit','neuerArtikelKategorie','neuerArtikelNr','neuerArtikelHinweis'].forEach(i=>document.getElementById(i).value='');
  speichern();einstellungenProdukteAnzeigen();meldungZeigen(name+' gespeichert');
  if(aktuellerLieferant===einstellungenLieferant){kategorienAnzeigen();produkteAnzeigen();}
}

function artikelLoeschen(id){
  SUPPLIERS[einstellungenLieferant].products=SUPPLIERS[einstellungenLieferant].products.filter(p=>p.id!==id);
  delete warenkorb[id];badgeAktualisieren();
  speichern();einstellungenProdukteAnzeigen();
  if(aktuellerLieferant===einstellungenLieferant)produkteAnzeigen();
}

// ── Server / SMTP ─────────────────────────────────────────────────
function serverSpeichern(){
  const url=document.getElementById('serverAdresse').value.trim().replace(/\/+$/,'');
  if(!url){meldungZeigen('Bitte URL eingeben');return;}
  localStorage.setItem('pv_server_url',url);
  meldungZeigen('Server-URL gespeichert');serverStatusPruefen();
}

async function serverTesten(){
  const url=(document.getElementById('serverAdresse').value.trim()||localStorage.getItem('pv_server_url')||'').replace(/\/+$/,'');
  if(!url){meldungZeigen('Bitte zuerst URL eintragen');return;}
  meldungZeigen('Verbindung wird getestet…');
  try{
    const r=await fetch(url+'/api/status',{signal:AbortSignal.timeout(8000)});
    const d=await r.json();
    serverStatusSetzen(d.ok,d.ok?('Verbunden – SMTP: '+(d.smtp&&d.smtp.configured?d.smtp.host:'nicht konfiguriert')):'Fehler');
    meldungZeigen(d.ok?'✅ Server erreichbar!':'⚠️ Fehler: '+d.error);
  }catch(e){serverStatusSetzen(false,'Nicht erreichbar');meldungZeigen('⚠️ Server nicht erreichbar');}
}

async function serverStatusPruefen(){
  const url=(localStorage.getItem('pv_server_url')||'').replace(/\/+$/,'');
  if(!url)return;
  try{
    const r=await fetch(url+'/api/status',{signal:AbortSignal.timeout(5000)});
    const d=await r.json();
    serverStatusSetzen(d.ok,d.ok?('Verbunden – '+(d.smtp&&d.smtp.configured?d.smtp.host+':'+d.smtp.port:'SMTP nicht konfiguriert')):'Fehler');
  }catch(e){serverStatusSetzen(false,'Nicht erreichbar');}
}

function serverStatusSetzen(ok,text){
  const p=document.getElementById('serverStatusPunkt'),t=document.getElementById('serverStatusText');
  if(p)p.style.background=ok?'#1D9E75':'#E24B4A';
  if(t)t.textContent=text;
}

async function smtpSpeichern(){
  const url=(localStorage.getItem('pv_server_url')||'').replace(/\/+$/,'');
  if(!url){meldungZeigen('Zuerst Server-URL speichern');return;}
  const cfg={
    host:document.getElementById('smtpHost').value.trim(),
    port:document.getElementById('smtpPort').value.trim(),
    user:document.getElementById('smtpBenutzer').value.trim(),
    pass:document.getElementById('smtpPasswort').value.trim()
  };
  if(!cfg.host||!cfg.port||!cfg.user||!cfg.pass){meldungZeigen('Alle SMTP-Felder ausfüllen');return;}
  try{
    const r=await fetch(url+'/api/smtp-config',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(cfg),signal:AbortSignal.timeout(8000)});
    const d=await r.json();
    meldungZeigen(d.ok?'✅ SMTP gespeichert!':'⚠️ Fehler: '+d.error);
    if(d.ok)document.getElementById('smtpPasswort').value='';
  }catch(e){meldungZeigen('⚠️ Server nicht erreichbar');}
}

async function smtpTesten(){
  const url=(localStorage.getItem('pv_server_url')||'').replace(/\/+$/,'');
  if(!url){meldungZeigen('Zuerst Server-URL speichern');return;}
  meldungZeigen('SMTP wird getestet…');
  try{
    const r=await fetch(url+'/api/smtp-test',{signal:AbortSignal.timeout(15000)});
    const d=await r.json();
    meldungZeigen(d.ok?'✅ SMTP Verbindung erfolgreich!':'⚠️ '+d.error);
  }catch(e){meldungZeigen('⚠️ Server nicht erreichbar');}
}

// ── Start ─────────────────────────────────────────────────────────
laden();
lieferantenPillenErstellen();
kategorienAnzeigen();
produkteAnzeigen();
document.getElementById('nutzerKuerzel').textContent=aktuellerNutzer.id;
document.getElementById('nutzerName').textContent=aktuellerNutzer.name;
document.getElementById('warenkorbLieferant').textContent=aktuellerLieferant;
document.getElementById('warenkorbEmpfaenger').textContent=SUPPLIERS[aktuellerLieferant].email;
</script>
</body>
</html>
