<!DOCTYPE html>
<html lang="ms">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Perjalanan Nur Ilmu — Super Study Mode</title>
<style>
:root{--bg:#0a0a0a;--panel:#111;--accent:#1f6feb;--muted:#bfbfbf;--cta:#ff6b6b;--scorebg:#222;}
body{margin:0;padding:18px;font-family:Inter,ui-sans-serif,system-ui,Segoe UI,Roboto,"Helvetica Neue",Arial;color:#eee;background:var(--bg);}
.wrap{max-width:900px;margin:18px auto;padding:16px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;border:1px solid rgba(255,255,255,0.03);}
h1{margin:0 0 8px;color:var(--cta)}
#log{white-space:pre-wrap;background:var(--panel);padding:14px;border-radius:10px;min-height:300px;max-height:60vh;overflow:auto;border:1px solid rgba(255,255,255,0.02)}
#choices{display:flex;flex-direction:column;gap:8px;margin-top:12px}
button.choice{background:var(--accent);color:#fff;border:none;padding:10px 12px;border-radius:8px;cursor:pointer;text-align:left;font-weight:700}
.small{color:var(--muted);font-size:0.95rem;margin-top:8px}
.meta{display:flex;gap:10px;align-items:center;margin-bottom:10px;flex-wrap:wrap}
.pill{background:#111;padding:6px 10px;border-radius:999px;color:var(--muted);font-weight:600}
#scoreboard{background:var(--scorebg);padding:10px;border-radius:10px;margin-bottom:12px;font-weight:700;color:#fff;text-align:right}
footer{margin-top:14px;color:var(--muted);font-size:0.9rem}
@media (max-width:520px){body{padding:10px}.wrap{padding:12px}}
</style>
</head>
<body>
<div class="wrap">
<h1>Perjalanan Nur Ilmu — Super Study Mode</h1>
<div class="meta">
<div class="pill">Role: Saif (pelajar)</div>
<div class="pill">NPC: James · Gorga · Fufufafa</div>
<div class="pill">Mode: Interaktif / KBAT / Quiz</div>
</div>
<div id="scoreboard">Markah: 0</div>
<div id="log"></div>
<div id="choices"></div>
<div class="small">Tip: Klik pilihan untuk bergerak. Jawab soalan KBAT dengan bijak untuk dapat markah maksimum. Betul +1, Salah -1, Final Case +2.</div>
<footer>Salin & simpan sebagai <code>game.html</code>. Buka di Chrome/Firefox (HP/PC).</footer>
</div>
<script>
const logEl = document.getElementById('log');
const choicesEl = document.getElementById('choices');
const scoreEl = document.getElementById('scoreboard');
let state = {current:'start',memory:{},score:0,visited:new Set()};

function write(text){ logEl.innerHTML=text; logEl.scrollTop=0; }
function updateScore(){ scoreEl.innerText = 'Markah: '+state.score; }
function setOptions(arr){
choicesEl.innerHTML='';
arr.forEach(o=>{
  const btn=document.createElement('button');
  btn.className='choice';
  btn.innerText=o.text;
  btn.onclick=()=>{ if(o.onClick)o.onClick(); else goTo(o.next); };
  choicesEl.appendChild(btn);
});
}
function goTo(scene){
state.current=scene;
if(FLAG_MAP[scene]) mark(FLAG_MAP[scene]);
render();
}
function mark(key){ state.memory[key]=true; state.visited.add(key); }
function askMCQ(question,optionsArray,correctIndex,nextOnDone){
write("SOAL (KBAT):\n\n"+question);
setOptions(optionsArray.map((opt,idx)=>({
  text:opt,
  onClick:()=>{
    const correct=Array.isArray(correctIndex)?correctIndex.includes(idx):(idx===correctIndex);
    if(correct){ state.score+=1; write("Betul! +1 markah\n\n"+question+"\nJawapan anda: "+opt); }
    else{ state.score-=1; write("Salah! -1 markah\n\n"+question+"\nJawapan anda: "+opt+"\nJawapan betul: "+optionsArray[correctIndex]); }
    updateScore();
    setOptions([{text:"Teruskan",next:nextOnDone}]);
  }
})));
}

const SCENES={};
FLAG_MAP={};

// START
SCENES.start=function(){
const t=`Kau terjaga di madrasah bercahaya. Di hadapan ada 6 pintu:\n1) Al-Qur'an\n2) Hadis\n3) Aqidah\n4) Fiqh\n5) Sirah\n6) Akhlak\nPilih untuk mula ulangkaji.`;
write(t);
setOptions([
{text:"Al-Qur'an (Idgham & Amanah)",next:"alquran_intro"},
{text:"Hadis (Halal/Haram)",next:"hadis_intro"},
{text:"Aqidah (Malaikat & Ujian)",next:"aqidah_intro"},
{text:"Fiqh (Solat/Puasa/KBAT)",next:"fiqh_intro"},
{text:"Sirah (Sahabat & Kepimpinan)",next:"sirah_intro"},
{text:"Akhlak (Ibu Bapa & Jiran)",next:"akhlak_intro"},
{text:"Final Case Gabungan Semua Topik",next:"final_case"}
]);
};

// AL-QUR'AN
SCENES.alquran_intro=function(){
const t=`Bidang Al-Qur'an — Idgham Mitslain.\nRingkasan:\n- Dua huruf sama bertemu digabung.\n- Contoh: م + م → bunyi gabung.\nSedia untuk quiz?`;
write(t);
setOptions([{text:"Quiz Idgham Mitslain",onClick:()=>askMCQ(
"Idgham Mitslain melibatkan penggabungan huruf yang sama?",
["Ya, gabungkan","Tidak, berbeza"],0,"alquran_amanah"
)}]);
};

SCENES.alquran_amanah=function(){
const t=`Amanah: tanggungjawab terhadap harta & nyawa.\n- Jangan guna harta orang tanpa izin.\n- Lindungi nyawa.\n- Kaitkan dengan etika profesional.`;
write(t);
setOptions([{text:"Pergi ke Hadis",next:"hadis_intro"},{text:"Kembali ke Madrasah",next:"start"}]);
};

// HADIS
SCENES.hadis_intro=function(){
const t=`Bidang Hadis — Halal/Haram.\nLangkah:\n1) Rujuk Al-Quran/Hadis sahih\n2) Semak sumber produk\n3) Elak syubhah\nSedia untuk KBAT?`;
write(t);
setOptions([{text:"Quiz Hadis",onClick:()=>askMCQ(
"Peniaga jual 'halal' tanpa sijil. Apa patut buat?",
["Terus beli","Rujuk pihak berautoriti/elak"],1,"aqidah_intro"
)},{text:"Kembali ke Madrasah",next:"start"}]);
};

// AQIDAH
SCENES.aqidah_intro=function(){
const t=`Bidang Aqidah — Malaikat & Perbezaan manusia.\n- Malaikat dicipta dari cahaya, tak makan/minum, tiada nafsu.\n- Tugas: sampaikan wahyu, catat amal, jaga utusan.\nPilih topik seterusnya.`;
write(t);
setOptions([{text:"Pergi ke Fiqh",next:"fiqh_intro"},{text:"Ulang Hadis",next:"hadis_intro"},{text:"Kembali ke Madrasah",next:"start"}]);
};

// FIQH
SCENES.fiqh_intro=function(){
const t=`Fiqh — Solat berjemaah, solat sunat, puasa.\n- Makmum masbuq: sempurnakan baki selepas imam salam.\n- Solat sunat: tambah pahala.\n- Puasa: syarat sah, qada', kifarah, fidyah.`;
write(t);
setOptions([{text:"Quiz Makmum Masbuq",onClick:()=>askMCQ(
"Jika makmum masbuq dan imam sudah salam, apa patut buat?",
["Tunggu imam ulang solat","Sempurnakan baki sendiri & salam"],1,"fiqh_solat_sunat"
)},{text:"Quiz Puasa",onClick:()=>askMCQ(
"Pelajar jatuh sakit Ramadan, apa perlu buat?",
["Teruskan puasa","Berbuka, qada' selepas sembuh"],1,"fiqh_solat_sunat"
)},{text:"Kembali ke Madrasah",next:"start"}]);
};

SCENES.fiqh_solat_sunat=function(){
const t=`Solat sunat menambah pahala & menampung kekurangan fardhu. Pilih seterusnya.`;
write(t);
setOptions([{text:"Quiz Puasa Lanjutan",onClick:()=>askMCQ(
"Apa beza qada' & fidyah?",
["Qada': ganti puasa; Fidyah: bayar gantian jika tak mampu","Keduanya sama"],0,"fiqh_puasa_extra"
)},{text:"Kembali ke Fiqh menu",next:"fiqh_intro"}]);
};

SCENES.fiqh_puasa_extra=function(){
const t=`Siapa perlu qada'? Sakit, haid, travel → qada'. Sengaja tinggal puasa → kifarah/fidyah mungkin.`;
write(t);
setOptions([{text:"Kembali ke Madrasah",next:"start"}]);
};

// SIRAH
SCENES.sirah_intro=function(){
const t=`Sirah — Fokus sahabat awal & kepimpinan Nabi di Madinah.\n- Bilal, Khadijah, Abu Bakar.\n- Piagam Madinah: adil kepada semua.\n- Wanita teladan: Sumayyah RA (syuhada), Aisyah RA (perawi & pelajar ilmu).`;
write(t);
setOptions([{text:"Quiz Sirah",onClick:()=>askMCQ(
"Siapa perawi hadis & banyak sumbang ilmu?",
["Sumayyah RA","Aisyah RA"],1,"sirah_extra"
)},{text:"Kembali ke Madrasah",next:"start"}]);
};

SCENES.sirah_extra=function(){
const t=`Kepimpinan Nabi: Piagam Madinah, adil, diplomasi, bantu semua lapisan masyarakat.`;
write(t);
setOptions([{text:"Pergi ke Akhlak",next:"akhlak_intro"},{text:"Kembali ke Madrasah",next:"start"}]);
};

// AKHLAK
SCENES.akhlak_intro=function(){
const t=`Akhlak — Hormat ibu bapa, santuni jiran, adab di masjid.`;
write(t);
setOptions([{text:"Kuiz Akhlak (Ibu Bapa)",onClick:()=>askMCQ(
"Pelajar marah ibu sebab dilarang keluar malam, apa patut buat?",
["Membalas marah","Bertenang & berbicara sopan"],1,"akhlak_jiran"
)},{text:"Santuni jiran",next:"akhlak_jiran"},{text:"Kembali ke Madrasah",next:"start"}]);
};

SCENES.akhlak_jiran=function(){
const t=`Santuni jiran: bantu asas, pilih cara sesuai, kaitkan hikmah.`;
write(t);
setOptions([{text:"Masjid: Hikmah & Adab",next:"masjid_adab"},{text:"Semak Ending",next:"check_endings"}]);
};

SCENES.masjid_adab=function(){
const t=`Masjid: Bersihkan diri, salam, jangan bising. Kaitkan adab dengan komuniti.`;
write(t);
setOptions([{text:"Kembali ke Madrasah",next:"start"},{text:"Semak Ending",next:"check_endings"}]);
};

// FINAL CASE
SCENES.final_case=function(){
const t=`FINAL CASE — Gabungan Semua Topik:\nGuru muda kawal program Ramadan. Keluarga miskin minta bantuan; produk ragu status halal; pelajar makmum masbuq.`;
write(t);
setOptions([
{text:"A. Bantu lengkap, semak halal, urus bapa & ibu mengandung, bimbing makmum masbuq (+2)",onClick:()=>{
state.score+=2; updateScore(); write("Pilihan A: tindakan holistik & hikmah (+2 markah)"); setOptions([{text:"Teruskan",next:"check_endings"}]);
}},
{text:"B. Hanya beri makanan tanpa semak halal (-0)",onClick:()=>{
write("Pilihan B: kurang lengkap (tiada markah)"); setOptions([{text:"Teruskan",next:"check_endings"}]);
}}
]);
};

// ENDINGS
SCENES.check_endings=function(){
const s=state.score;
let chosen;
if(s>=10) chosen='secretEnding';
else if(s>=7) chosen='goodEnding';
else if(s>=4) chosen='unexpectedEnding';
else chosen='badEnding';
goTo(chosen);
};

SCENES.secretEnding=function(){ write("SECRET ENDING — Kefahaman menyeluruh, aplikasi praktikal, tahap A!"); setOptions([{text:"Main Lagi",next:"start"}]);};
SCENES.goodEnding=function(){ write("GOOD ENDING — Lulus cemerlang, jawapan lengkap & hikmah. Tahniah!"); setOptions([{text:"Main Lagi",next:"start"}]);};
SCENES.unexpectedEnding=function(){ write("UNEXPECTED ENDING — Ada kefahaman, tetapi perlu ulang topik & lebih mendalam."); setOptions([{text:"Ulang Topik",next:"start"}]);};
SCENES.badEnding=function(){ write("BAD ENDING — Perlu perbaiki, ulang topik & kuiz lagi."); setOptions([{text:"Ulang Topik",next:"start"}]);};

function render(){ const fn=SCENES[state.current]; if(!fn){ write("Scene not found: "+state.current); setOptions([{text:"Kembali ke start",next:"start"}]); return; } fn();}
window.onload=()=>{ setTimeout(()=>goTo('start'),120); };
</script>
</body>
</html>
