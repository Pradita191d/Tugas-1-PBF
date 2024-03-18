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

  Sebelum diubah mode development:
  ![Screenshot 2024-03-18 110550](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/6452a58b-97cf-4794-8163-a595cd61aaf7)

  Sesudah diubah mode development:
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/377b5f14-91be-4810-9b39-45b6cf56baa1)
  
  ## 3. Bangun Aplikasi Pertama | Halaman Statis
     ### Menerapakan aturan routing
     Buka file rute yang terletak di app/Config/Routes.php
     ```shell
     <?php

      use CodeIgniter\Router\RouteCollection;
      
      /**
       * @var RouteCollection $routes
       */
      $routes->get('/', 'Home::index');
     ```
    - codeigniter akan membuat jalur ketika ada akses yg method requestnya = get
    - alamatnya->'/' (route->base URL->localhost:8080)
    - diarahkan ke controller Home-> index (method)

    Tambahkan baris kode di bawah ini:
      ```php
      use App\Controllers\Pages;

      $routes->get('pages', [Pages::class, 'index']);
      $routes->get('(:segment)', [Pages::class, 'view']);
      ```
     ### Membuat Controller `App/Controller/Pages.php`
     Isi kode `App/Controller/Pages.php` :
     ```php
      <?php
      
      namespace App\Controllers;
      
      class Pages extends BaseController
      {
          public function index()
          {
              return view('welcome_message');
          }
      
          public function view($page = 'home')
          {
              // ...
          }
      }
     ```
      
     ### Membuat Tampilan
     - Tampilan pertama adalah header yang disimpan di `App/Views/templates/header.php`<br>
       Isi kode:
       ```php
       <!doctype html>
       <html>
       <head>
          <title>CodeIgniter Tutorial</title>
       </head>
       <body>
          <h1><?= esc($title) ?></h1>
       ```
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/a748d3e7-db31-4c5c-830b-e0f6f1cbe661)

   - Tampilan kedua adalah footer yang disimpan di `App/Views/templates/header.php`
     Isi kode:
     ```  php
     <em>&copy; 2022</em>
         </body>
     </html>
     ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/fe7758ef-ab5f-433b-a02a-a0537612771d)


     
     

     
     
     
     

     
  
  
  
     
     
  
      
      
     
     
  
