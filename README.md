# Nisa-y-ne-kadar-iyi-tan-yorsun-testi
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nisa'yi Ne Kadar Taniyorsun?</title>
<style>
* {
    box-sizing: border-box;
}
body {
    margin: 0;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #ffe4ef, #f8e9ff);
    display: flex;
    justify-content: center;
    align-items: center;
    color: #333;
}
.kutu {
    width: 90%;
    max-width: 700px;
    background: white;
    border-radius: 30px;
    padding: 35px;
    box-shadow: 0 15px 40px rgba(0,0,0,0.12);
}
.baslangic {
    text-align: center;
}
.baslik {
    color: #e84d82;
    font-size: 32px;
    margin-bottom: 10px;
}
.aciklama {
    color: #777;
    font-size: 17px;
    margin-bottom: 30px;
}
.buton {
    border: none;
    border-radius: 15px;
    padding: 16px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    transition: 0.2s;
}
.basla {
    background: #e84d82;
    color: white;
    padding: 17px 45px;
}
.basla:hover {
    background: #d6386d;
    transform: scale(1.03);
}
.ust {
    display: flex;
    justify-content: space-between;
    margin-bottom: 15px;
    font-weight: bold;
}
.soru-sayisi {
    color: #e84d82;
}
.skor {
    color: #9875d4;
}
.progress {
    width: 100%;
    height: 12px;
    background: #f0dce5;
    border-radius: 20px;
    overflow: hidden;
    margin-bottom: 30px;
}
.progress-bar {
    height: 100%;
    width: 5%;
    background: #e84d82;
    transition: 0.4s;
}
.soru-kutu {
    background: #fff4f8;
    border-radius: 20px;
    padding: 25px;
    text-align: center;
    margin-bottom: 25px;
}
.soru {
    font-size: 22px;
    font-weight: bold;
    line-height: 1.4;
}
.secenek {
    width: 100%;
    margin: 8px 0;
    background: #fafafa;
    color: #333;
    border: 2px solid #f0dce5;
}
.secenek:hover {
    background: #ffe4ef;
    border-color: #e84d82;
}
.dogru {
    background: #b9efcf !important;
    border-color: #52b879 !important;
}
.yanlis {
    background: #ffc5c5 !important;
    border-color: #e85b5b !important;
}
.mesaj {
    text-align: center;
    font-size: 18px;
    font-weight: bold;
    min-height: 25px;
    margin-top: 15px;
}
.final {
    text-align: center;
}
.final-skor {
    font-size: 60px;
    color: #9875d4;
    font-weight: bold;
    margin: 20px;
}
.final-mesaj {
    font-size: 20px;
    line-height: 1.5;
    margin-bottom: 30px;
}
.gizli {
    display: none;
}
</style>
</head>
<body>
<div class="kutu">
    <!-- BASLANGIC -->
    <div id="baslangic" class="baslangic">
        <div class="baslik">
            💗 NISA'YI NE KADAR TANIYORSUN?
        </div>
        <div class="aciklama">
            Bakalim Nisa'yi gercekten taniyor musun?
            <br><br>
            20 soru • 20 puan
        </div>
        <button class="buton basla" onclick="oyunuBaslat()">
            OYUNA BASLA
        </button>
    </div>
    <!-- OYUN -->
    <div id="oyun" class="gizli">
        <div class="ust">
            <div class="soru-sayisi" id="soruSayisi">
                SORU 1 / 20
            </div>
            <div class="skor" id="skor">
                SKOR: 0
            </div>
        </div>
        <div class="progress">
            <div class="progress-bar" id="progressBar"></div>
        </div>
        <div class="soru-kutu">
            <div class="soru" id="soru">
                Soru
            </div>
        </div>
        <div id="secenekler"></div>
        <div class="mesaj" id="mesaj"></div>
    </div>
    <!-- FINAL -->
    <div id="final" class="final gizli">
        <div class="baslik">
            🎉 OYUN BITTI!
        </div>
        <div class="final-skor" id="finalSkor">
            0 / 20
        </div>
        <div class="final-mesaj" id="finalMesaj">
        </div>
        <button class="buton basla" onclick="yenidenOyna()">
            TEKRAR OYNA
        </button>
    </div>
</div>
<script>
const sorular = [
    {
        soru: "Nisa'nin en sevdigi yemek hangisidir?",
        secenekler: ["Pizza", "Manti", "Tavuklu pilav", "Hamburger"],
        cevap: 2
    },
    {
        soru: "Nisa'nin sevmedigi bir yemek var mi?",
        secenekler: ["Evet, bir suru var", "Sadece sebze",
                    "Sadece balik", "Yok"],
        cevap: 3
    },
    {
        soru: "Nisa bos zamaninda en cok ne yapmayi sever?",
        secenekler: ["Kitap okumak", "Yeni filmler izlemek",
                    "Spor yapmak", "Yemek yapmak"],
        cevap: 1
    },
    {
        soru: "Nisa'nin en sevdigi renk hangisidir?",
        secenekler: ["Siyah", "Pembe", "Mavi", "Beyaz"],
        cevap: 3
    },
    {
        soru: "Nisa'nin en sevdigi sarkici kimdir?",
        secenekler: ["Ahmet Kaya", "Tarkan",
                    "Sezen Aksu", "Mabel Matiz"],
        cevap: 0
    },
    {
        soru: "Nisa'nin en sevdigi sarki hangisidir?",
        secenekler: ["Kumralim", "Dardayim",
                    "Ben Seni Cok Sevdim", "Resimdeki Gozyaslari"],
