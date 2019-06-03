---
title: "Cara deploy website dengan mudah dan gratis di Netlify"
description: "Deploy web statis dengan mudah dan murah di Netlify kurang dari 5"
date: "2018-08-17T03:08:39.484Z"
categories: 
  - Netlify
  - Vuejs
  - Deploy
  - Tutorial
  - Website

published: true
canonical_link: https://medium.com/tkcbi/cara-deploy-website-dengan-mudah-dan-gratis-di-netlify-c2ea0a8a2e40
redirect_from:
  - /cara-deploy-website-dengan-mudah-dan-gratis-di-netlify-c2ea0a8a2e40
---

![sumber: [https://www.heavybit.com/wp-content/uploads/2016/05/netlify-content.jpg](https://www.heavybit.com/wp-content/uploads/2016/05/netlify-content.jpg)](./asset-1.jpeg)

[Netlify](https://www.netlify.com/) adalah layanan SaaS yang memberikan kemudahan untuk kita mem-publish web statis.

### Prerequisites

-   **Website — **Hal pertama yang dibutuhkan adalah sebuah halaman website. Pada kesempatan ini saya akan mencontohkannya dengan website yang telah saya buat menggunakan Vue JS.
-   **Git Repository — **Hal selanjutnya yang dibutuhkan adalah source code halaman website Anda harus disimpan disebuah repository git. Saya menggunakan [Github](https://github.com/), namun Anda juga dapat menggunakan layanan lainnya seperti [Bitbucket](https://bitbucket.org/) atau [Gitlab](https://gitlab.com).

### Deploying

Buat akun atau login ke Netlify di [https://app.netlify.com/](https://app.netlify.com/)

Setelah login dan masuk ke halaman dashboard, tekan tombol **New site from Git**

![](./asset-2.png)

Kemudian pilih provider git yang Anda inginkan dan beri izin akses pada aplikasi, disini saya memilih github.

![](./asset-3.png)

Setelah terhubung dengan provider git Anda, maka repository yang ada di akun Anda akan ditampilkan. Kemudian pilih project repository yang ingin di deploy ke Netlify.

![](./asset-4.png)

Saya memilih project **todo-vue**. Isi form bagaimana website Anda akan di build.

![](./asset-5.png)

Karena saya menggunakan Vue JS maka perintah untuk **build command** adalah `npm run build` dan untuk **publish directory** adalah folder `dist` (contoh lainnya dilihat di: [https://www.netlify.com/docs/continuous-deployment/#common-configuration-directives](https://www.netlify.com/docs/continuous-deployment/#common-configuration-directives)). Terakhir tekan **Deploy site** dan tunggu beberapa saat hingga website Anda selesai di build.

### Selamat, Website Anda telah LIVE!

Untuk melakukan deploy selanjutnya, Anda hanya perlu melakukan push ke repository project git Anda dan Netlify akan secara otomatis memperbarui website Anda.

**Referensi**

[**Docs | Netlify**  
_Netlify builds, deploys, and hosts your front end. Learn how to get started, see examples, and view documentation for…_www.netlify.com](https://www.netlify.com/docs/ "https://www.netlify.com/docs/")[](https://www.netlify.com/docs/)

[**farazaulia/todo-vue**  
_Download source code todo-vue app_github.com](https://github.com/farazaulia/todo-vue "https://github.com/farazaulia/todo-vue")[](https://github.com/farazaulia/todo-vue)
