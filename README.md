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

  ## - Instalasi Komposer

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

  ## - Jalankan Aplikasi

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

  ## - Halaman Statis | Bangun Aplikasi Pertama

  ### Menerapkan aturan routing

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

  ### - Bangun Aplikasi Pertama | Bagian Berita
  **Buat Database** <br>
  - Pertama kita buat database ci4 <br>
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/1e614c65-ea8c-4573-8828-5e159acf42f8)
  - Buat tabel news <br>
  ```shell
  CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
  );
  ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/2131d2cc-eb39-42bb-baf7-e67781ea15b4)

  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/b3af07c4-dbe3-45e0-8e93-6199ccb013dc)
  - Isikan data ke tabel dengan perintah INSERT INTO <br>
  ```shell
  INSERT INTO news VALUES
  (1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
  (2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
  (3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
  ```
  ![Screenshot 2024-03-18 151842](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/ae7a1d02-6b8d-4ccd-9034-9671268f9bd3)

  **Hubungkan ke database** <br>
  Untuk menghubungkan ke database, kita perlu file konfigurasi lokal, `.env`, yang telah dibuat pada saat awal menginstall CodeIginiter4. <br>
  Sebelumnya, seperti di bawah ini: <br>
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/66511598-ea2e-4d8c-93d7-fabe23b056e9) <br>
  Hilangkan tanda '#' untuk menjalankan kode tersebut. <br>
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/ef57bdde-76ee-4049-8912-d6b281b2f807) <br>

  **Buat Models Berita** <br>
  Buka direktori app/Models dan buat file baru bernama NewsModel.php dan tambahkan kode berikut. <br>
  ```php
  <?php

  namespace App\Models;
  
  use CodeIgniter\Model;
  
  class NewsModel extends Model
  {
      protected $table = 'news';
  }
  ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/40aa9a83-b4ec-497c-bf72-a4deb65744ed) <br>
  **Tambahkan Metode NewsModel::getNews()** <br>
  ```php
   public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
  ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/2808ff57-2fd4-49a1-931f-17896db8e727) <br>

  Kode ini dapat dijalankan untuk menjalankan dua query berbeda. Dua metode yang digunakan yaitu findAll() dan first(), disediakan oleh kelas CodeIgniter\Model. Kita sudah mengetahui tabel mana yang akan digunakan berdasarkan properti $table  yang kita atur sebelumnya di kelas NewsModel. Ini adalah metode pembantu yang menggunakan pembuat kueri untuk menjalankan perintah pada tabel saat ini dan mengembalikan kumpulan hasil dalam format pilihan Anda. Dalam contoh ini, findAll() mengembalikan array dari array. <br>
  
  **Tampilkan Berita**
  - Buat Controller News.php di `App/Controller` <br>
  ```php
  <?php

  namespace App\Controllers;
  
  use App\Models\NewsModel;
  
  class News extends BaseController
  {
      public function index()
      {
          $model = model(NewsModel::class);
  
          $data['news'] = $model->getNews();
      }
  
      public function show($slug = null)
      {
          $model = model(NewsModel::class);
  
          $data['news'] = $model->getNews($slug);
      }
  }
  ```
  ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/fb1da725-d680-4223-89e7-fef552893f41) <br>
  
  - Menambahkan routing rules
  Pada `Routes.php` yangs sebelumnya sudah ada, ubah menjadi di bawah ini: <br>
  ```php
  <?php
  
  // ...
  
  use App\Controllers\News; // Add this line
  use App\Controllers\Pages;
  
  $routes->get('news', [News::class, 'index']);           // Add this line
  $routes->get('news/(:segment)', [News::class, 'show']); // Add this line
  
  $routes->get('pages', [Pages::class, 'index']);
  $routes->get('(:segment)', [Pages::class, 'view']);
  ```
   ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/bf0ad4aa-d4e6-4524-bc02-e8b3988e4b91) <br>
   - Melengkapi `Controllers/News.php`<br>
   ```php
   <?php

    namespace App\Controllers;
    
    use App\Models\NewsModel;
    
    class News extends BaseController
    {
        public function index()
        {
            $model = model(NewsModel::class);
    
            $data['news'] = $model->getNews();
        }
    
        public function show($slug = null)
        {
            $model = model(NewsModel::class);
    
            $data['news'] = $model->getNews($slug);
        }
    }
   ```
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/d56ef0ac-7368-4e0c-b821-3849a75773f8) <br>
     
  Kode di atas mengambil semua catatan berita dari model dan menugaskannya ke variabel. Nilai judul juga ditetapkan ke $data['title'] elemen dan semua data diteruskan ke tampilan. Anda sekarang perlu membuat tampilan untuk merender item berita. <br>
  - Mengubah index() di Controllers/News.php <br>
  ```php
  <?php

  namespace App\Controllers;
  
  use App\Models\NewsModel;
  
  class News extends BaseController
  {
      public function index()
      {
          $model = model(NewsModel::class);
  
          $data = [
              'news'  => $model->getNews(),
              'title' => 'News archive',
          ];
  
          return view('templates/header', $data)
              . view('news/index')
              . view('templates/footer');
      }
  
      // ...
  }
  ```
  
  - Buat File Views/news/index.php <br>
     Isi kode: <br>
     ```php
     <h2><?= esc($title) ?></h2>

    <?php if (! empty($news) && is_array($news)): ?>
    
        <?php foreach ($news as $news_item): ?>
    
            <h3><?= esc($news_item['title']) ?></h3>
    
            <div class="main">
                <?= esc($news_item['body']) ?>
            </div>
            <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>
    
        <?php endforeach ?>
    
    <?php else: ?>
    
        <h3>No News</h3>
    
        <p>Unable to find any news for you.</p>
    
    <?php endif ?>
     ``` <br>
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/6b28b831-e6f8-4a05-9f68-d3943494498f) <br>
     - Melengkapi File Controller/News.php <br>
     ```php
     <?php
    
      namespace App\Controllers;
      
      use App\Models\NewsModel;
      
      class News extends BaseController
      {
          public function index()
          {
              $model = model(NewsModel::class);
      
              $data = [
                  'news'  => $model->getNews(),
                  'title' => 'News archive',
              ];
      
              return view('templates/header', $data)
                  . view('news/index')
                  . view('templates/footer');
          }
      
          }
     ```
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/fc904c19-bcda-4d27-af39-3b34a8f23277) <br>

    **Buat `App/Views/news/view.php`** <br>
    ```php
     <h2><?= esc($news['title']) ?></h2>
     <p><?= esc($news['body']) ?></p>
     ``` 
     ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/1ca5812c-9373-4ac0-8a9f-099acd39ecad)

    **Saat akses URL : http://localhost:8080/news**
    ![image](https://github.com/Pradita191d/Tugas-1-PBF/assets/134593226/9ff6307c-003d-4d6b-96e3-97f848a29dca)

  ### - Ikhtisar CodeIgniter4 | Struktur Aplikasi

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

### - MVC | Ikhtisar CodeIgniter4

**Apa itu MVC?** <br>
MVC adalah singkatan dari Models, Views, dan Controllers. <br>

- Models: digunakan untuk mengelola data aplikasi dan membantu menegakkan aturan bisnis khusus yang mungkin diperlukan aplikasi. <br>

- Views: file sederhana, dengan sedikit atau tanpa logika, yang menampilkan informasi kepada pengguna. <br>

- Controllers: bertindak sebagai kode perekat, menyusun data bolak-balik antara tampilan (atau pengguna yang melihatnya) dan penyimpanan data. <br>

**Komponen MVC** <br>

- **Views** biasanya berbentuk HTML dengan jumlah PHP yang sangat sedikit. Tampilan ini biasa disimpan di `app/Views`. <br>
- **Models** bertugas memelihara satu tipe data untuk suatu aplikasi. Dalam hal ini, tugas model memiliki dua bagian: menerapkan aturan bisnis pada data saat diambil dari, atau dimasukkan ke dalam database; dan menangani penyimpanan dan pengambilan data sebenarnya dari database. Model biasanya disimpan di `app/Models`. <br>
- **Controller** memiliki beberapa peran berbeda untuk dimainkan. Yang paling jelas adalah mereka menerima masukan dari pengguna dan kemudian menentukan apa yang harus dilakukan dengannya. Controller biasanya disimpan di `app/Controllers`.

