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
   
    - Tampilan kedua adalah footer yang disimpan di `App/Views/templates/header.php`
      Isi kode:
      ```php
      <em>&copy; 2022</em>
               </body>
           </html>
      ```

  ### Menambah Logika Controller
  Buat home.php dan about.php di `App/Views/pages`<br>
  Isi kode:
     ```php
      <!DOCTYPE html>
      <html lang="en">
      <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
      </head>
      <body>
          <h1>Hello World!</h1>
      </body>
      </html>
     ```
     Susunan direktori:
  
     ![Screenshot 2024-03-18 125834](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/f57c2f28-aa90-49a8-82e1-22be209366f7)


   ### Halaman Lengkap::view() Metode
   Halaman ini dibuat di `App/Controllers/Pages.php`
   Isi Kode:
     ```php
     <?php

      namespace App\Controllers;
      
      use CodeIgniter\Exceptions\PageNotFoundException; // Add this line
      
      class Pages extends BaseController
      {
          // ...
      
          public function view($page = 'home')
          {
              if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
                  // Whoops, we don't have a page for that!
                  throw new PageNotFoundException($page);
              }
      
              $data['title'] = ucfirst($page); // Capitalize the first letter
      
              return view('templates/header', $data)
                  . view('pages/' . $page)
                  . view('templates/footer');
          }
      }
     ```
     Jalankan alamat `http://localhost:8080/home` maka akan tampil seperti di bawah ini: <br> <br>
  ![Screenshot 2024-03-18 131756](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/ae2fdfaf-99bb-48ba-9296-cbc0d4f4ed42)

  ### 4. Struktur Aplikasi | Ikhtisar CodeIgniter4
  Struktur direktori default: `app/`, `public/`, `writable/`, `test/` dan `vendor/` atau `system/` <br>
  - `app/` sebagai inti dari aplikasi <br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/e1f69923-dfb6-4896-8a01-f30fcdf51fea)
  - `public/` untuk menyimpan aset->dapat di modifikasi <br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/f69fa981-5924-4431-a29f-e0b46d5c02a0)
  - `writable/` digunakan jika codeiginter akan mengisi otomatis <br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/a4565ee7-a600-452b-bae3-75fc3eef6ec7)
  - `test/` digunakan apabila aplikasi menjalankan testing <br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/9cd5ac26-7e40-4d02-8432-2a34e51bd2f0)
  - `vendor/` <br> <br>
  Tempat menyimpan dependency aplikasi. Dependency dapat berarti suatu library yang digunakan dalam suatu aplikasi, dapat juga berarti ketergantungan antara satu aplikasi dengan aplikasi yang lain). Vendor dikelola oleh composer.json <br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/0d3096b3-c92f-468f-9460-c8f9b7d39557)
  - `system/`<br> <br>
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/0d36831c-b6f3-49c2-b475-05edaf54ee8d)

   ### 5. MVC | Ikhtisar CodeIgniter4
   **Apa itu MVC?** <br>
   MVC adalah singkatan dari Models, Views, dan Controllers. <br>
   
   - Models: digunakan untuk mengelola data aplikasi dan membantu menegakkan aturan bisnis khusus yang mungkin diperlukan aplikasi. <br> 
   
   - Views: file sederhana, dengan sedikit atau tanpa logika, yang menampilkan informasi kepada pengguna. <br>
   
   - Controllers: bertindak sebagai kode perekat, menyusun data bolak-balik antara tampilan (atau pengguna yang melihatnya) dan penyimpanan data. <br> 
   
   **Komponen MVC** <br>
   - **Views** biasanya berbentuk HTML dengan jumlah PHP yang sangat sedikit. Tampilan ini biasa disimpan di `app/Views`. <br>
   - **Models** bertugas memelihara satu tipe data untuk suatu aplikasi. Dalam hal ini, tugas model memiliki dua bagian: menerapkan aturan bisnis pada data saat diambil dari, atau dimasukkan ke dalam database; dan menangani penyimpanan dan pengambilan data sebenarnya dari database. Model biasanya disimpan di `app/Models`. <br>
   - **Controller** memiliki beberapa peran berbeda untuk dimainkan. Yang paling jelas adalah mereka menerima masukan dari pengguna dan kemudian menentukan apa yang harus dilakukan dengannya. Controller biasanya disimpan di `app/Controllers`. 
     
   
   
   
   
   
     
      
     
        
        
   
        
        
        
        
   
        
     
  
  
     
     
  
      
      
     
     
  
