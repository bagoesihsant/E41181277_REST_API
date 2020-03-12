# Dokumentasi Workshop Web Framework 4

## REST API
   Sebelum kita memulai, kita harus mengetahui apa itu **_REST_**, **_REST_** adalah singkatan bahasa inggris dari _**RE**presentational **S**tate **T**ransfer_ yang merupakan suatu gaya arsitektur perangkat lunak untuk pendistribusian sistem hipermedia seperti _www_.
   <br><br>
   Istilah ini diperkenalkan pertama kali pada tahun 2000, pada disertasi doktoral **_Roy Fielding_**. Pada arsitektur **_REST_**, **_REST Server_** menyediakan _resources_ ( sumber daya/data ) dan **_REST Client_** mengakses serta menampilkan _resources_ tersebut untuk penggunaan selanjutnya.

## Requirements
   Hal - hal yang diperlukan untuk memulai REST API menggunakan Code Igniter :
   
   - [REST Library](https://github.com/chriskacerguis/codeigniter-restserver) untuk Code Igniter yang dibuat oleh [chirskacerguis](https://github.com/chriskacerguis/).
   - atau [Code Igniter](https://github.com/ardisaurus/ci-restserver) yang sudah terintegrasi dengan REST Library yang dibuat oleh [ardisaurus](https://github.com/ardisaurus/).
   - [XAMPP](https://www.apachefriends.org/download.html) versi 7.2.28 atau lebih.
   - [PHP](https://www.php.net/) versi 7.2.28 atau lebih.
   - [Visual Studio Code](https://code.visualstudio.com/) sebagai text editor atau text editor favorit anda.
   
## Instalasi
   
   1. Dalam kesempatan kali ini, saya menggunakan [Code Igniter](https://github.com/ardisaurus/ci-restserver) yang sudah terintegrasi oleh REST API yang dibuat oleh [ardisaurus](https://github.com/ardisaurus/ci-restserver).
   
   2. Setelah mendownload Code Igniter milik [ardisaurus](https://github.com/ardisaurus/ci-restserver), ekstrak dan letakkan pada folder htdocs.
      
      ![ImageDokumentasi1]()
      
   3. Kemudian buka folder tersebut dalam text editor anda.
   
   4. Setelah membuka dalam text editor, buka folder **application/config**, kemudian buka file **_autoload.php_**.
      
      ![ImageDokumentasi2]()
      
   5. Kemudian temukan baris yang berisi kode berikut :
      ```php
      $autoload['libraries'] = array()
      ```
   6. Kemudian ubah menjadi berikut :
      ```php
      $autoload['libraries'] = array('database')
      ```
   7. Fungsi kode tersebut adalah memuat library **_database_** untuk digunakan nantinya.
   
   8. Kemudian temukan baris yang berisi kode berikut :
      ```php
      $autoload['helper'] = array()
      ```
   9. Kemudian ubah menjadi berikut :
      ```php
      $autoload['helper'] = array('url')
      ```
   10. Fungsi kode tersebut adalah memuat library **_url_** untuk digunakan nantinya.
   
   11. Setelah selesai mengedit **_autoload.php_**, buka folder **application/config**, kemudian buka file **_config.php_**.
       
       ![ImageDokumentasi3]()
       
   12. Kemudian temukan baris kode berikut :
       ```php
       $config['base_url'] = '';
       ```
   13. Kemudian ubah isi dari kode tersebut menjadi link yang anda gunakan untuk membuka REST API Code Igniter, contoh :
       ```php
       $config['base_url'] = 'https://www.contohlinkbuka.com/';
       ```
   14. Fungsi dari mengisi kode tersebut adalah ketika anda menggunakan library **_url_** dan ingin mengetikkan link, anda tidak perlu lagi mengetikkan seluruh link melainkan hanya tinggal memanggil method **_base_url()_**.
   
   15. Setelah selesai mengedit **_config.php_**, buka folder **application/config**, kemudian buka file **_database.php_**.
       
       ![ImageDokumentasi4]()
       
   16. Kemudian temukan baris kode berikut :
       ```php
       $db['default'] = array(
           'dsn'	=> '',
           'hostname' => 'localhost',
           'username' => '',
           'password' => '',
           'database' => '',
           'dbdriver' => 'mysqli',
           'dbprefix' => '',
           'pconnect' => FALSE,
           'db_debug' => (ENVIRONMENT !== 'production'),
           'cache_on' => FALSE,
           'cachedir' => '',
           'char_set' => 'utf8',
           'dbcollat' => 'utf8_general_ci',
           'swap_pre' => '',
           'encrypt' => FALSE,
           'compress' => FALSE,
           'stricton' => FALSE,
           'failover' => array(),
           'save_queries' => TRUE
          );
       ```
   17. Kemudian ubah baris kode berikut sesuai username dan password database anda, kemudian isi bagian database dengan database yang ingin anda pakai, dalam kasus ini username saya adalah **root** dan tidak memliki password, serta database yang saya pakai adalah **kontak**.
       ```php
       $db['default'] = array(
           'dsn'	=> '',
           'hostname' => 'localhost',
           'username' => 'root',
           'password' => '',
           'database' => 'kontak',
           'dbdriver' => 'mysqli',
           'dbprefix' => '',
           'pconnect' => FALSE,
           'db_debug' => (ENVIRONMENT !== 'production'),
           'cache_on' => FALSE,
           'cachedir' => '',
           'char_set' => 'utf8',
           'dbcollat' => 'utf8_general_ci',
           'swap_pre' => '',
           'encrypt' => FALSE,
           'compress' => FALSE,
           'stricton' => FALSE,
           'failover' => array(),
           'save_queries' => TRUE
          );
       ``` 
  18. Fungsi dari kode tersebut adalah menyambungkan Code Igniter dengan database yang kita pilih dengan cara menginputkan nama database menggunakan username dan password yang kita berikan.
  
## Peggunaan
   Berikut ini adalah cara menggunakan REST API dalam Code Igniter :
   
   1. Setelah selesai mengedit **_database.php_**, buka folder **application/controllers** kemudian buat file baru bernama **_Kontak.php_**.
      
      ![ImageDokumentasi5]()
      
   2. Kemudian ketikkan kode berikut ini :
      ```php
      <?php
         defined('BASEPATH') OR exit('No direct script access allowed');
         
         require APPPATH. '/libraries/REST_Controller.php';
         use Restserver\Libraries\REST_Controller;
         
         class Kontak extends REST_Controller {
            
            function __construct($config = 'rest')
            {
               parent::__construct($config);
            }
            
            function index_get()
            {
               $id = $this->get->('id');
               if($id == '')
               {
                  $kontak = $this->db->get('telepon')->result();
               }else
               {
                  $this->db->where('id',$id);
                  $kontak = $this->db->get('telepon')->result();
               }
               $this->response($kontak,200);
            }
            
            function index_post()
            {
               $data = array(
                        'id'  => $this->post('id'),
                        'nama'   => $this->post('nama'),
                        'nomor'  => $this->post('nomor')
               );
               $insert = $this->db->insert('telepon',$data);
               if($insert)
               {
                  $this->response($data, 200);
               }else
               {
                  $this->response(array('status' => 'fail',502));
               }
            }
            
            function index_put()
            {
               $id = $this->put('id');
               $data = array(
                        'id'  => $this->put('id'),
                        'nama' => $this->put('nama'),
                        'nomor' => $this->put('nomor')
                        
               );
               $this->db->where('id',$id);
               $update = $this->db->update('telepon',$data);
               if($update)
               {
                  $this->response($data,200);
               }else
               {
                  $this->response(array('status' => 'fail',502));
               }
            }
            
            function index_delete()
            {
               $id = $this->delete('id');
               $this->db->where('id',$id);
               $delete = $this->db->delete('telepon');
               if($delete)
               {
                  $this->response(array('status' => 'success'),201);
               }else
               {
                  $this->response(array('status' => 'success',502));
               }
            }
            
         }
      ?>
      ```
   
   
