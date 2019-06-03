---
title: "Mencoba LINE Front-end Framework (LIFF)"
description: "Halo, hari ini saya akan membahas teknologi lain yang diberikan oleh LINE. Setelah sebelumnya kita mencoba LINE Messaging API, sekarang kita akan mencoba LINE Front-end Framwork. Menurut situs resmi…"
date: "2018-06-30T13:57:45.006Z"
categories: 
  - Python
  - Tutorial
  - Line
  - Line Front End Framework
  - JavaScript

published: true
canonical_link: https://medium.com/tkcbi/mencoba-line-front-end-framework-liff-ff2a6e9df0ea
redirect_from:
  - /mencoba-line-front-end-framework-liff-ff2a6e9df0ea
---

![**Sumber:** [https://medium.com/linedevth/introduction-to-liff-7d708e2f42ec](https://medium.com/linedevth/introduction-to-liff-7d708e2f42ec)](./asset-1.png)

Halo, hari ini saya akan membahas teknologi lain yang diberikan oleh LINE. Setelah sebelumnya kita mencoba LINE Messaging API, sekarang kita akan mencoba LINE Front-end Framwork.

#### Apa sih LINE Front-end Framework itu?

Menurut situs resmi LINE Developers, LINE Front-end Framework atau bisa disingkat LIFF adalah teknologi yang memungkinkan aplikasi web dapat berjalan di dalam aplikasi LINE. LIFF juga memungkinkan untuk aplikasi web dapat memperoleh LINE user ID atau token yang dapat digunakan oleh aplikasi web untuk mengirimkan pesan langsung kepada pengguna.

#### Ukuran aplikasi LIFF

LIFF dapat ditampilkan dengan 3 ukuran yang berbeda. Satu aplikasi LIFF tidak dapat menggunakan beberapa ukuran sekaligus, namun ukuran dapat diganti jika perlu.

![**Sumber:** [https://developers.line.me/en/docs/liff/overview/](https://developers.line.me/en/docs/liff/overview/)](./asset-2.png)

1.  Compact — Aplikasi LIFF akan ditampilkan 50% dari ukuran layar.
2.  Tall — Aplikasi LIFF akan ditampilkan 75% dari ukuran layar.
3.  Full — Aplikasi LIFF akan ditampilkan 100% dari ukuran layar.

### Membuat aplikasi LIFF

Kali ini kita akan membuat aplikasi yang dapat digunakan untuk membuat gambar di aplikasi LINE dan dapat langsung kita kirimkan sebagai pesan.

![](./asset-3.gif)

#### Membuat channel

Untuk membuat LIFF app terlebih dahulu kita harus memiliki LINE Channel. Cara membuatnya sama seperti membuat channel untuk LINE messaging API, bedanya hanya pada kolom webhook kita tidak perlu untuk mengisinya karena kita hanya membutuhkan channel access token untuk membuat LIFF app kita. Panduan untuk membuat channel dapat dilihat dari artikel berikut

[**Membuat LINE Bot dengan Python**  
_Tutorial lengkap memanfaatkan LINE Messaging API dan Python Flask untuk membuat chatbot_medium.com](https://medium.com/tkcbi/membuat-line-bot-dengan-python-33b85878ba40 "https://medium.com/tkcbi/membuat-line-bot-dengan-python-33b85878ba40")[](https://medium.com/tkcbi/membuat-line-bot-dengan-python-33b85878ba40)

#### Membuat Aplikasi Web

Disini saya menggunakan Flask untuk membuat aplikasi web. Anda juga dapat membuat aplikasi web dengan cara Anda sendiri.

Step 1 — Buat folder project baru

```
mkdir liffapp
```

Step 2 — Buat virtual environment dan aktifkan

```
cd liffapp
pipenv --three
pipenv shell
```

Step 3 — Install dependencies yang diperlukan

```
pipenv install flask
pipenv install flask-bootstrap
pipenv install pillow
```

Step 4 — Buat file baru dengan nama `app.py` kemudian ketik atau salin kode berikut

<Embed src="https://gist.github.com/farazaulia/06429029ca6a2f5f18fcb7766e4b9eed.js" aspectRatio={0.357} />

Diatas adalah kode untuk kita membuat web service dengan Flask. Dari kode diatas terlihat kita harus mengimport terlebih dahulu dependecies yang akan kita gunakan seperti Flask, Flask-bootstrap dan Pillow.

Seperti pada umumnya, kita harus mengatur route dari web yang akan kita buat. Pada route `/` akan menampilkan template index.html kepada user dan route `/saveimage` akan melakukan penyimpanan gambar dari user.

Step 5 — Buat tampilan aplikasi

Tampilan aplikasi akan dibuat menggunakan html, css dan javascript. Pertama, buat folder templates kemudian file index.html didalaman.

```
templates
└── index.html
```

Kemudian Anda dapat mengetik ataupun menyalin kode berikut.

<Embed src="https://gist.github.com/farazaulia/444220ecd971cabbb776d1c284ffb95d.js" aspectRatio={0.357} />

> **NOTE:** Ganti **drawr.serveo.net** yang terdapat pada originalContenUrl & previewImageUrl dengan url aplikasi web Anda.

Sedikit penjelasan untuk kode diatas.

Untuk menggunakan LIFF kita harus mengimport LIFF SDK dan beberapa library JavaScript lainnya seperti jQuery dan Signature Pad. Disini kita menggunakan Signature Pad sebagai canvas untuk kita menggambar nanti.

Aplikasi web kita dapat berinteraksi dengan user yang ada di chat room menggunakan LIFF API seperti `liff.getProfile()` untuk mendapatkan profile user dan token reply serta `liff.sendMessage()` untuk mengirimkan pesan langsung ke aplikasi LINE.

Untuk mengetahui fungsi-fungsi apa saja yang tersedia, silahkan buka website dokumentasi resminya.

[**API reference**  
_LINE Front-end Framework documentation_ developers.line.me](https://developers.line.me/en/docs/liff/reference/ "https://developers.line.me/en/docs/liff/reference/")[](https://developers.line.me/en/docs/liff/reference/)

#### Deploy LIFF App

Deploy aplikasi Anda ke Heroku agar dapat diakses.

Anda dapat mengikuti langkah yang terdapat pada artikel ini [https://medium.com/tkcbi/membuat-line-bot-dengan-python-33b85878ba40](https://medium.com/tkcbi/membuat-line-bot-dengan-python-33b85878ba40).

### Daftarkan LIFF App ke Channel

Sebelum kita dapat menggunakan LIFF App, kita harus mendaftarkan app kita terlebih dahulu ke channel yang sudah kita buat sebelumnya dengan cara.

```
curl -XPOST \
-H "Authorization: Bearer YOUR_CHANNEL_ACCESS_TOKEN" \
-H "Content-Type: application/json" \
-d '{
    "view": {
        "type": "SIZE_OF_LIFF",
        "url": "URL_OF_YOUR_APPLICATION"
    }
}' \
https://api.line.me/liff/v1/apps
```

Keterangan:

1.  **YOUR\_CHANNEL\_ACCESS\_TOKEN **— channel access token yang didapatkan dari developer console channel kita.
2.  **SIZE\_OF\_LIFF** — ukuran LIFF app kita seperti yang telah dijelaskan sebelumnya. Terdapat 3 ukuran yang bisa dipilih: `compact`, `tall` dan `full`.
3.  **URL\_OF\_YOUR\_APPLICATION **— URL halaman web Heroku saat kita mendeploy aplikasi. (Harus HTTPS)

Return yang diberikan berupa id app kita

```
{"liffId":"1234567890-XXXXXXXX"}
```

Untuk mengaksesnya copy link `line://app/1234567890-XXXXXXXX` ke chat room. Klik link tersebut, aplikasi akan muncul pada chat room Anda. Selamat mencoba…

**Referensi**

[**LIFF, our latest product for third party developers : LINE Engineering Blog**  
_LIFF is one of our latest products out for LINE Messaging API users. So, what is LIFF? LIFF stands for the LINE…_engineering.linecorp.com](https://engineering.linecorp.com/en/blog/detail/299 "https://engineering.linecorp.com/en/blog/detail/299")[](https://engineering.linecorp.com/en/blog/detail/299)

[**มารู้จักกับ LIFF — สิ่งที่จะมาเติมเต็มในการทำ Chat Bot กัน!**  
_สวัสดีครับ วันนี้อยากจะมาแนะนำ API ตัวใหม่ ล่าสุด เพิ่งแกะกล่องสดๆร้อนๆ จาก LINE นั่นก็คือ “LIFF” ครับ!_medium.com](https://medium.com/linedevth/introduction-to-liff-7d708e2f42ec "https://medium.com/linedevth/introduction-to-liff-7d708e2f42ec")[](https://medium.com/linedevth/introduction-to-liff-7d708e2f42ec)
