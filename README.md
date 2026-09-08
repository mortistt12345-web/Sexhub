# Sexhub
Sexhub- Short Videos &amp; Photos
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>SEXHUB</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    background: #08080d;
    color: white;
}

header {
    text-align: center;
    padding: 35px 15px;
    background: linear-gradient(135deg, #17102b, #09090e);
}

.logo {
    margin: 0;
    font-size: 45px;
    letter-spacing: 8px;
}

.subtitle {
    color: #aaa;
}

.container {
    width: 92%;
    max-width: 1000px;
    margin: auto;
}

.upload-box {
    margin: 25px 0;
    padding: 25px;
    background: #15151d;
    border-radius: 18px;
    text-align: center;
}

.upload-buttons {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
}

.upload-btn {
    display: inline-block;
    padding: 14px 22px;
    border-radius: 10px;
    background: #6c35de;
    color: white;
    font-weight: bold;
    cursor: pointer;
}

.upload-btn:hover {
    background: #824df0;
}

input[type="file"] {
    display: none;
}

h2 {
    margin-top: 35px;
}

.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 18px;
    padding-bottom: 40px;
}

.card {
    background: #15151d;
    border: 1px solid #292936;
    border-radius: 15px;
    overflow: hidden;
    padding-bottom: 12px;
}

.card img,
.card video {
    width: 100%;
    max-height: 400px;
    object-fit: cover;
    display: block;
}

.card-info {
    padding: 10px 14px;
}

.filename {
    color: #aaa;
    font-size: 14px;
    word-break: break-all;
}

.delete-btn {
    border: 0;
    background: #d9364f;
    color: white;
    padding: 9px 15px;
    border-radius: 8px;
    cursor: pointer;
}

.empty {
    text-align: center;
    color: #777;
    padding: 30px;
}

footer {
    text-align: center;
    padding: 25px;
    color: #666;
}
</style>
</head>

<body>

<header>
    <h1 class="logo">MORTIS</h1>
    <p class="subtitle">SHORT VIDEOS • PHOTOS</p>
</header>

<div class="container">

    <div class="upload-box">

        <h2>İçerik Ekle</h2>

        <p>
            Fotoğraf veya kısa video seç.
        </p>

        <div class="upload-buttons">

            <label class="upload-btn">
                📷 FOTOĞRAF YÜKLE
                <input
                    type="file"
                    id="photoInput"
                    accept="image/*"
                    multiple
                >
            </label>

            <label class="upload-btn">
                🎬 VİDEO YÜKLE
                <input
                    type="file"
                    id="videoInput"
                    accept="video/*"
                    multiple
                >
            </label>

        </div>

    </div>

    <h2>Fotoğraflar</h2>

    <div id="photoGallery" class="gallery">
        <div class="empty">
            Henüz fotoğraf yok.
        </div>
    </div>

    <h2>Short Videolar</h2>

    <div id="videoGallery" class="gallery">
        <div class="empty">
            Henüz video yok.
        </div>
    </div>

</div>

<footer>
    © 2026 MORTIS
</footer>

<script>

const photoInput = document.getElementById("photoInput");
const videoInput = document.getElementById("videoInput");

const photoGallery = document.getElementById("photoGallery");
const videoGallery = document.getElementById("videoGallery");


function removeEmpty(element) {
    const empty = element.querySelector(".empty");

    if (empty) {
        empty.remove();
    }
}


function createCard(file, type) {

    const card = document.createElement("div");
    card.className = "card";

    const info = document.createElement("div");
    info.className = "card-info";

    const filename = document.createElement("div");
    filename.className = "filename";
    filename.textContent = file.name;

    const deleteButton = document.createElement("button");
    deleteButton.className = "delete-btn";
    deleteButton.textContent = "Sil";

    const objectURL = URL.createObjectURL(file);

    deleteButton.onclick = function () {
        URL.revokeObjectURL(objectURL);
        card.remove();

        if (type === "photo" && photoGallery.children.length === 0) {
            photoGallery.innerHTML =
                '<div class="empty">Henüz fotoğraf yok.</div>';
        }

        if (type === "video" && videoGallery.children.length === 0) {
            videoGallery.innerHTML =
                '<div class="empty">Henüz video yok.</div>';
        }
    };


    if (type === "photo") {

        const image = document.createElement("img");

        image.src = objectURL;
        image.alt = file.name;

        card.appendChild(image);

    } else {

        const video = document.createElement("video");

        video.src = objectURL;
        video.controls = true;
        video.playsInline = true;

        card.appendChild(video);
    }


    info.appendChild(filename);
    info.appendChild(deleteButton);

    card.appendChild(info);

    return card;
}


photoInput.addEventListener("change", function () {

    removeEmpty(photoGallery);

    for (const file of this.files) {

        if (file.type.startsWith("image/")) {

            const card = createCard(file, "photo");

            photoGallery.appendChild(card);
        }
    }

    photoInput.value = "";
});


videoInput.addEventListener("change", function () {

    removeEmpty(videoGallery);

    for (const file of this.files) {

        if (file.type.startsWith("video/")) {

            const card = createCard(file, "video");

            videoGallery.appendChild(card);
        }
    }

    videoInput.value = "";
});

</script>

</body>
</html>
