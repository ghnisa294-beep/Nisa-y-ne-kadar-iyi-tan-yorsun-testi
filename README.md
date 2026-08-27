<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Nisa'yi Ne Kadar Taniyorsun?</title>

<style>

body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #ffe6f0, #eee4ff);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.oyun {
    width: 90%;
    max-width: 650px;
    background: white;
    padding: 35px;
    border-radius: 30px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.15);
    text-align: center;
}

h1 {
    color: #e85d91;
    font-size: 32px;
}

.alt-yazi {
    color: #777;
    font-size: 17px;
}

.basla {
    background: #f06292;
    color: white;
    border: none;
    padding: 18px 45px;
    border-radius: 15px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    margin-top: 25px;
}

.basla:hover {
    background: #df477b;
}

.ust {
    display: flex;
    justify-content: space-between;
    color: #9b6dcc;
    font-weight: bold;
}

.cubuk {
    width: 100%;
    height: 10px;
    background: #f1dce5;
    border-radius: 20px;
    margin: 20px 0;
}

.cubuk-dolgu {
    height: 100%;
    width: 0%;
    background: #f06292;
    border-radius: 20px;
}

.soru {
    font-size: 23px;
    font-weight: bold;
    margin: 30px 0;
}

.cevap {
    display: block;
    width: 100%;
    padding: 16px;
    margin: 10px 0;
    border-radius: 15px;
    border: 2px solid #f0dce5;
    background: #fff9fb;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    text-align: left;
}

.cevap:hover {
    background: #ffeaf2;
    border-color: #f06292;
}

.dogru {
    background: #dff7e7 !important;
    border-color: #5fbd82 !important;
}

.yanlis {
    background: #ffe0e0 !important;
    border-color: #e86b6b !important;
}

.mesaj {
    height: 30px;
    font-size: 18px;
    font-weight: bold;
    margin-top: 15px;
}

.skor {
    font-size: 50px;
    color: #9b6dcc;
    font-weight: bold;
}

.tekrar {
    background: #f06292;
    color: white;
    border: none;
    padding: 16px 40px;
    border-radius: 15px;
    font-size: 17px;
    font-weight: bold;
    cursor: pointer;
}

#oyunEkrani,
#sonucEkrani {
    display: none;
}

</style>
</head>

<body>

<div class="oyun">

    <!-- ANA EKRAN -->

    <div id="anaEkran">

        <div style="font-size:50px;">💗</div>

        <h1>NISA'YI NE KADAR TANIYORSUN?</h1>

        <p class="alt-yazi">
            Bakalim Nisa'yi gercekten taniyor musun?
        </p>

        <p>
            20 soru • Her dogru cevap 1 puan
        </p>

        <button class="basla" onclick="oyunuBaslat()">
            OYUNA BASLA
        </button>

    </div>


    <!-- OYUN EKRANI -->

    <div id="oyunEkrani">

        <div class="ust">

            <span id="soruNumarasi">
                SORU 1 / 20
            </span>

            <span id="puan">
                SKOR: 0
            </span>

        </div>

        <div class="cubuk">
            <div id="cubukDolgu" class="cubuk-dolgu"></div>
        </div>

        <div id="soru" class="soru"></div>

        <div id="cevaplar"></div>

        <div id="mesaj" class="mesaj"></div>

    </div>


    <!-- SONUC EKRANI -->

    <div id="sonucEkrani">

        <div style="font-size:60px;">🏆</div>

        <h1>OYUN BITTI!</h1>

        <div id="finalSkor" class="skor">
            0 / 20
        </div>

        <p id="basari"></p>

        <h2 id="sonucMesaji"></h2>

        <button class="tekrar" onclick="oyunuBaslat()">
            TEKRAR OYNA
        </button>

    </div>

</div>


<script>

/* =========================
   SORULAR
========================= */

const sorular = [

{
    soru: "Nisa'nin en sevdigi yemek hangisidir?",
    cevaplar: [
        "Pizza",
        "Manti",
        "Tavuklu pilav",
        "Hamburger"
    ],
    dogru: 2
},

{
    soru: "Nisa'nin sevmedigi bir yemek var mi?",
    cevaplar: [
        "Evet, bir suru var",
        "Sadece sebze",
        "Sadece balik",
        "Yok"
    ],
    dogru: 3
},

{
    soru: "Nisa bos zamaninda en cok ne yapmayi sever?",
    cevaplar: [
        "Kitap okumak",
        "Yeni filmler izlemek",
        "Spor yapmak",
        "Yemek yapmak"
    ],
    dogru: 1
},

{
    soru: "Nisa'nin en sevdigi renk hangisidir?",
    cevaplar: [
        "Siyah",
        "Pembe",
        "Mavi",
        "Beyaz"
    ],
    dogru: 3
},

{
    soru: "Nisa'nin en sevdigi sarkici kimdir?",
    cevaplar: [
        "Ahmet Kaya",
        "Tarkan",
        "Sezen Aksu",
        "Mabel Matiz"
    ],
    dogru: 0
},

{
    soru: "Nisa'nin en sevdigi sarki hangisidir?",
    cevaplar: [
        "Kumralim",
        "Dardayim",
        "Ben Seni Cok Sevdim",
        "Resimdeki Gozyaslari"
    ],
    dogru: 1
},

{
    soru: "Nisa'nin en sevdigi dizi hangisidir?",
    cevaplar: [
        "Yargi",
        "Medcezir",
        "Sonyaz",
        "Kiralik Ask"
    ],
    dogru: 2
},

{
    soru: "Nisa hangi ulkeye gitmek ister?",
    cevaplar: [
        "Italya",
        "Fransa",
        "Amerika",
        "Ispanya"
    ],
    dogru: 3
},

{
    soru: "Nisa sabah insani mi gece insani mi?",
    cevaplar: [
        "Sabah insani",
        "Gece insani",
        "Ikisi de",
        "Hicbiri"
    ],
    dogru: 1
},

{
    soru: "Nisa sinirlendiginde genellikle ne yapar?",
    cevaplar: [
        "Susup bekler",
        "Uyur",
        "Bazen sinirini sucsuz insanlardan cikarir",
        "Hemen ortamdan gider"
    ],
    dogru: 2
},

{
    soru: "Nisa en cok neye guler?",
    cevaplar: [
        "Sadece komik videolara",
        "Sadece esprilere",
        "Hicbir seye",
        "Her seye"
    ],
    dogru: 3
},

{
    soru: "Nisa insanlarda en sevmedigi ozellik nedir?",
    cevaplar: [
        "Sessiz olmak",
        "Insanlari kucuk dusurmek",
        "Cok konusmak",
        "Utangac olmak"
    ],
    dogru: 1
},

{
    soru: "Nisa insanlarda en cok hangi ozelligi sever?",
    cevaplar: [
        "Kibirli olmak",
        "Cok konusmak",
        "Mutevazi olmak",
        "Cok ciddi olmak"
    ],
    dogru: 2
},

{
    soru: "Nisa'ya yapilabilecek en guzel surpriz nedir?",
    cevaplar: [
        "Sadece pahali hediyeler",
        "Tatile goturmek",
        "Her sey",
        "Sadece cicek"
    ],
    dogru: 2
},

{
    soru: "Nisa alisveris yaparken en cok ne alir?",
    cevaplar: [
        "Kitap",
        "Makyaj malzemesi",
        "Ayakkabi",
        "Teknolojik urun"
    ],
    dogru: 1
},

{
    soru: "Nisa telefonda en cok hangi uygulamayi kullanir?",
    cevaplar: [
        "Instagram",
        "YouTube",
        "TikTok",
        "WhatsApp"
    ],
    dogru: 2
},

{
    soru: "Nisa'nin en buyuk hayallerinden biri nedir?",
    cevaplar: [
        "Guzellik merkezi acmak",
        "Futbolcu olmak",
        "Yazar olmak",
        "Ogretmen olmak"
    ],
    dogru: 0
},

{
    soru: "Nisa'nin bir diger buyuk hayali nedir?",
    cevaplar: [
        "Bir ada satin almak",
        "Butun dunyayi gezmek",
        "Uzaya gitmek",
        "Yarismaya katilmak"
    ],
    dogru: 1
},

{
    soru: "Nisa'yi en hizli ne mutlu eder?",
    cevaplar: [
        "Sadece pahali hediyeler",
        "Sadece tatil",
        "Ufacik bir hediye bile",
        "Para"
    ],
    dogru: 2
},

{
    soru: "Nisa'nin en belirgin huyu nedir?",
    cevaplar: [
        "Kiskanc olmasi",
        "Merhametli olmasi",
        "Sinirli olmasi",
        "Cok ciddi olmasi"
    ],
    dogru: 1
}

];


/* =========================
   DEGISKENLER
========================= */

let mevcutSoru = 0;
let puan = 0;
let cevapVerildi = false;


/* =========================
   OYUNU BASLAT
========================= */

function oyunuBaslat() {

    mevcutSoru = 0;
    puan = 0;
    cevapVerildi = false;

    document.getElementById("anaEkran").style.display = "none";
    document.getElementById("sonucEkrani").style.display = "none";
    document.getElementById("oyunEkrani").style.display = "block";

    soruGoster();
}


/* =========================
   SORUYU GOSTER
========================= */

function soruGoster() {

    cevapVerildi = false;

    let soru = sorular[mevcutSoru];

    document.getElementById("soruNumarasi").textContent =
        "SORU " + (mevcutSoru + 1) + " / 20";

    document.getElementById("puan").textContent =
        "SKOR: " + puan;

    document.getElementById("cubukDolgu").style.width =
        ((mevcutSoru + 1) / 20 * 100) + "%";

    document.getElementById("soru").textContent =
        soru.soru;

    document.getElementById("mesaj").textContent = "";

    let cevapKutusu =
        document.getElementById("cevaplar");

    cevapKutusu.innerHTML = "";

    let harfler = ["A", "B", "C", "D"];

    for (let i = 0; i < 4; i++) {

        let buton = document.createElement("button");

        buton.className = "cevap";

        buton.textContent =
            harfler[i] + ") " + soru.cevaplar[i];

        buton.onclick = function() {
            cevapKontrol(i, buton);
        };

        cevapKutusu.appendChild(buton);
    }
}


/* =========================
   CEVABI KONTROL ET
========================= */

function cevapKontrol(secim, buton) {

    if (cevapVerildi) {
        return;
    }

    cevapVerildi = true;

    let dogruCevap =
        sorular[mevcutSoru].dogru;

    let butonlar =
        document.querySelectorAll(".cevap");


    if (secim === dogruCevap) {

        puan++;

        buton.classList.add("dogru");

        document.getElementById("mesaj").textContent =
            "DOGRU! 🎉";

        document.getElementById("mesaj").style.color =
            "#4caf70";

    }

    else {

        buton.classList.add("yanlis");

        butonlar[dogruCevap].classList.add("dogru");

        document.getElementById("mesaj").textContent =
            "YANLIS! 😭";

        document.getElementById("mesaj").style.color =
            "#e85d5d";
    }


    document.getElementById("puan").textContent =
        "SKOR: " + puan;


    setTimeout(function() {

        mevcutSoru++;

        if (mevcutSoru < sorular.length) {

            soruGoster();

        }

        else {

            sonucEkrani();

        }

    }, 1000);
}


/* =========================
   SONUC EKRANI
========================= */

function sonucEkrani() {

    document.getElementById("oyunEkrani").style.display =
        "none";

    document.getElementById("sonucEkrani").style.display =
        "block";


    let yuzde =
        Math.round((puan / 20) * 100);


    document.getElementById("finalSkor").textContent =
        puan + " / 20";


    document.getElementById("basari").textContent =
        "Basari oranin: %" + yuzde;


    let mesaj = "";


    if (puan === 20) {

        mesaj =
            "🏆 EFSANE! Nisa'yi senden iyi taniyan yok!";

    }

    else if (puan >= 17) {

        mesaj =
            "🥇 MUKEMMEL! Nisa'yi baya iyi taniyorsun.";

    }

    else if (puan >= 14) {

        mesaj =
            "🥈 COK IYI! Nisa hakkinda baya bilgi sahibisin.";

    }

    else if (puan >= 10) {

        mesaj =
            "🥉 FENA DEGIL! Biraz daha Nisa bilgisi lazim.";

    }

    else if (puan >= 5) {

        mesaj =
            "😅 ZAYIF! Nisa'yi biraz daha taniman lazim.";

    }

    else {

        mesaj =
            "💀 FELAKET! Sen bu teste nasil girdin?";

    }


    document.getElementById("sonucMesaji").textContent =
        mesaj;
}

</script>

</body>
</html>
