#### Step 1: Setup
1. Membuat direktori projek
##### membuat direktori dengan perintah ``` $ mkdir composetest```. Lalu masuk direktori dengan perintah ``` $ cd composetest```. Direktori ini nantinya digunakan untuk melakukan build image docker dengan compose.
	
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/l1.jpg)

2. Membuat file ```app.py```
##### Membuat file app.py dengan isi projek seperti pada gambar dibawah ini.
##### Pada file app.py tersebut, melakukan import time dan redis dari library pada framework flask. Redis nanti digunakan sebagai container pada image yang akan dibuild. Pada variabel app digunakan untuk inisiasi nama app. Sedangkan pada cache digunakan untuk inisiasi host dan port yang akan berjalan di container redis, yaitu host dengan nama “redis” dan port 6379.
##### Pada fungsi get_hit_count() yang mengembalikan nilai waktu, saat kondisi true, kmaka akan mengembalikan cache dan melakukan eksepsi error jika terjadi error.  Pada route terdapat fungsi hello yang akan memanggil nilai waktu dari proses yang dilakukan di fungsi get_hit_count() dan mengembalikan output 'Hello World! I have been seen {} times.\n'.format(count) diikuti nilai waktu.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/l2.jpg)

3. Membuat file ```requirements.txt```
##### Membuat file requirement.txt. Pada file requirement.txt tersebut berisi komponen yang dibutuhkan dalam proses build, yaitu framework flask dan redis
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/l3.jpg)

#### Step 2: Create a Dockerfile
##### Membuat file DockerFile menggunakan perintah ```vim dockerfile```
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/21.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/22.jpg)
##### Dockerfile di atas merupakan script yang yang berisi dari serangkaian perintah yang akan dieksekusi secara otomatis dan berurutan untuk membuat sebuah image.Dengan Docker, proses akan sangat ringan dan cepat dibandingkan dengan virtual mesin yang berbasis hypervisor. 
##### Pada isi Dockerfile tersebut, akan melakukan build image dengan Python 3.7 image alpine. Dockerfile akan melakukan set direktory aktivitasnya di direktori /code. Lalu Dockerfile tersebut akan melakukan set variabel environment yang digunakan oleh framework flask. Selanjutnya melakukan install gcc sehingga package phyton seperti MarkupSafe dan SQLAlchemy dapat melakukan compile secara cepat. Lalu melakukan copy file requirements.txt dan menginstall dependensi Python. Lalu selanjutnya melakukan copy direktori yang digunakan. Ke dalam workdir dalam image. Lalu yang terakhir mengatur perintah default untuk container ke flask run.
#### Step 3: Define services in a Compose file
##### Membuat File docker-compose.yml menggunakan perintah ``` vim docker-compose.yml```
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/31.jpg)
##### ketikkan isi file tersebut, seperti pada gambar dibawah ini.
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/32.jpg)
##### Pada konfigurasi di atas, terdapat sebuah service yang akan mewakili sebuah container Docker. Dengan demikian, konfigurasi di atas akan menjalankan instance dari container web. Pada Docker, setiap container dibuat berdasarkan image. Untuk web, image akan dibuat berdasarkan isi Dockerfile di redis:alpine.

#### Step 4: Build and run your app with Compose
1. Start up your application by running ```docker-compose up```
##### Bila ini adalah pertama kalinya saya menjalankan perintah, Docker akan men-download beberapa image seperti MySQL dan Node.js dari Docker Hub sehingga harus sabar menunggu.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/41.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/411.jpg)
##### Penjelasan 
##### Step 1/9, dari image python:3.7-alpine , akan melakukan pull dari library python

##### Step 2/9, akan Menghapus container  perantara e96193fb6702

##### Step 3/9, akan menjalankan enfironment flask framework pada app.py

##### Step 4/9, pada environment flask menjalankan host 0.0.0.0

##### Step 5/9, akan menjalankan apk dengan melakukan instalasi beberapa komponen dari alpine

##### Step 6/9, akan mencopy apa yang dibutuhkan pada proses build container pada requirements.txt, yaitu flask dan redis

##### Step 7/9, akan melakukan instalasi yang dibutuhkan pada proses build container pada requirements.txt, yaitu flask dan redis dengan menggunakan pip, dengan melakukan download flask framework dan redis dan beberapa package pendukungnya. Setelah didwonload, maka dilakukan build MarkupSafe dan dilakukan proses install

##### Step 8/9, melakukan copy

##### Step 9/9, menjalankan build image alpine yang menggunakan flask framework
##### Setelah itu dijalankan pada url ip machine dan port 5000: http://192.168.99.100:5000
2. Enter http://localhost:5000/ in a browser

``` Hello World! I have been seen 1 times.```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/42.jpg)
##### Pada percobaan diatas dilakukan dengan memanggil lewat ip machine 192.168.99.100 dengan diikuti port 5000, hasilya menghasilkan output 'Hello World! I have been seen 1 times.’. angka 1 menunjukan berapa kali halaman tersebut dikunjungi. Seperti ditampilan percobaan yang kedua, ketika direfresh maka angkanya menjadi 2 times, yang menandakan halaman tersebut dikunjungi sebanyak 2 kali.
3. Refresh the page.

``` Hello World! I have been seen 2 times.```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/43.jpg)

4. Untuk melihat image yang telah dibuat dengan menggunakan perintah ```docker image ls```.
##### Docker image adalah blueprint Docker container yang berisi aplikasi dan semua yang Anda butuhkan untuk menjalankan aplikasi.Docker image terdiri dari serangkaian filesystem yang mewakili instruksi dalam Dockerfile image dan membentuk aplikasi perangkat lunak yang dapat dieksekusi.
##### Saat proses build selesai, image baru akan terdaftar dalam daftar image seperti repository redis dengan tag alpine.
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/44.jpg)
#### Step 5: Edit the Compose file to add a bind mount
###### Edit file ``` docker-compose.yml``` seperti gambar dibawah ini.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/5.jpg)
##### Pada konfigurasi di atas, terdapat dua buah service yang masing-masing akan mewakili sebuah container Docker. Dengan demikian, konfigurasi di atas akan menjalankan dua instance dari container yang berbeda: web dan redis.Pada Docker, setiap container dibuat berdasarkan image. Untuk redis, image akan dibuat berdasarkan isi Dockerfile di folder redis.
#### Step 6: Re-build and run the app with Compose. 
##### Docker akan men-download beberapa image seperti MySQL dan Node.js dari Docker Hub sehingga harus sabar menunggu.
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/6.jpg)
#### Step 7: Update the application
1. Ubah pesan pada file app.py dari ``` Hello World``` menjadi ``` Hello from Docker!```
2. Refresh the app in your browser

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/72.jpg)
#### Step 8: Experiment with some other commands
``` docker-compose up -d``` digunakan untuk Restart docker-compose. dan perintah ``` docker-compose ps ``` digunakan untuk melihat informasi service yang berjalan.
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/8.jpg)

``` docker-compose run web env```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/81.jpg)

``` docker-compose stop```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/82.jpg)

``` docker-compose down --volumes```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/83.jpg)

### Where to go next
[LINK](https://docs.docker.com/compose/wordpress/)
1. Membuat direktori projek ```my_wordpress```
2. Membuat file ```docker-compose.yml```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/84.jpg)

#### Build the project
##### run ```docker-compose up -d```
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/85.jpg)

#### Bring up WordPress in a web browser
``` http://localhost:8000```
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/86.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/87.jpg)
#### Shutdown
``` docker-compose down```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-08/88.jpg)