# Tugas-1-PBF
- Definisi Framework
   Framework merupakan kerangka kerja yang digunakan membantu dalam pembuatan perangkat lunak, salah satunya website.
- Alasan perlu menggunakan framework
  Ada beberapa alasan mengapa kita memerlukan framework, diantaranya:
   - Mempersingkat waktu
   - Struktur aplikasi terorganisir(rapih)
   - Terdapat tools & libraries
   - Fleksible : bisa terkoneksi dengan database berbeda atau aplikasi pihak ke-3.
- Framework CodeIgniter
   Ada beberapa contoh framework untuk bahasa pemrograman PHP, tetapi kali ini saya akan menjelaskan salah satunya saja yaitu CodeIgniter.
   Di bawah ini akan dijabarkan beberapa cara kita menginstall dan menggunakan framework CodeIgniter:
  ## 1. Instalasi Komposer
  Komposer adalah package manager atau kumpulan dari beberapa library yang akan kita gunakan untuk menginstall CodeIgniter.
  Sebelum kita menginstall CodeIgniter, ada beberapa yang harus kita persiapkan, diantaranya:
  - Teks Editor -> VSCode
  - Web Browser -> Chrome
  - Web Server -> PHP 7.2+, MySQL 5.1+, Phpmyadmin -> Laragon
  - Komposer
  ### Buka terminal pada laragon
     Ketikkan:
     ```shell
     composer create-project codeigniter4/appstarter project-name
     ```
     ##### Note: untuk project-name bisa diubah sesuai dengan nama project yang akan dibuat.
  ### Konfigurasi Awal
  #### Update komposer
  Ketikkan:
  ```shell
  composer update
  ```
  ## 2. Jalankan Aplikasi
     Ketikkan:
     ```shell
     cd project-name
     php spark serve
     ```
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/a6950c20-31ec-49de-8c9c-d2ff03278252)
     #### Note: salin URL lalu tuliskan ke web browser
     Akan tampil seperti di bawah ini:
      ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/bca77c15-4db7-403a-ac3a-0dc299fe3d46)

  #### Ubah baseURL pada .env
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/24db219f-ab76-47ae-988d-09e034c1d0ae)

  ##### Note: untuk alamat local server disesuaikan dengan alamat pada saat menjalankan project

    #### Atur ke Mode Development di file .env
  ```shell
  CI_ENVIRONMENT = development
  ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/843162a3-62dc-40fb-986e-89dbd04bd9d6)
  
  ## 3. Bangun Aplikasi Pertama | Halaman Statis
     ### Menerapakan aturan routing
     Mari kita siapkan aturan routing. Buka file rute yang terletak di app/Config/Routes.php
     ```shell
     <?php

      use CodeIgniter\Router\RouteCollection;
      
      /**
       * @var RouteCollection $routes
       */
      $routes->get('/', 'Home::index');
     ```
    - Codeigniter akan membuat jalur ketika ada akses yg method requestnya = get
    - alamatnya->'/' (route->base URL->localhost:8080)
    - diarahkan ke controller Home-> index (method)
  

     
  
  
  
     
     
  
      
      
     
     
  
