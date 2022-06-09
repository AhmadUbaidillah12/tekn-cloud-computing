# LATIHAN 
## Section #1 - Networking Basics
### Step 1: The Docker Network Command
#### Perintah ```Docker network``` merupakan perintah yang memungkinkan kita untuk melakukan segala hal yang berhubungan dengan manajemen administrasi jaringan, seperti membuat jaringan, menghubungkan, melihat informasi jaringan hingga mendetail sekali dan menerapkannya di kontainer yang akan kita jalankan. Pada hasil  perintah tersebut terdapat Commands: Connect yang digunakan untuk melakukan koneksi container ke jaringan yang akan dibangun, Create yang digunakan untuk membuat jaringan, Disconnect yang digunakan untuk memutus koneksi container dengan jaringan yang akan dibangun, Inspect yang digunakan untuk menampilkan detail informasi pada jaringan, ls yang digunakan untuk menampilkan daftar jaringan yang dibangun, prune yang digunakan untuk menghapus semua jaringan yang tidak lagi digunakan, dan rm yang digunakan untuk menghapus jaringan.


![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/1.jpg)

### Step 2: List networks
#### ```docker network ls``` digunakan untuk melihat daftar jaringan kontainer yang telah dibuat. Setiap jaringan mendapatkan ID dan NAME yang unik. Setiap jaringan juga dikaitkan dengan satu driver.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/2.jpg)

### Step 3: Inspect a network
```docker network inspect bridge```
#### Perintah ```Docker network inspect``` merupakan perintah yang digunakan untuk menampilkan detail informasi pada jaringan bridge.  Bridge sendiri merupakan jenis network (default) yg digunakan Docker, apabila jika akan membuat container network defaultnya secara otomatis menggunakan Bridge sebagai networknya, network jenis ini memungkinkan Docker container saling terhubung pada lingkungan network private, agar host Docker dapat mengakses port container pada network ini harus di expose portnya atau di open lewat firewall. Terdapat beberapa informasi seperti nama, id, waktu dibuat, scope, driver, support atau tidaknya terhadap Ipv6, IPAM yang digunakan untuk konfigurasi tempat IP address (IP Address Management), support atau tidaknya penyimpanan internal, support atau tidaknya  attachable, support atau tidaknya  ingress, configFrom,jaringan, dan beberapa part pendukung lainnya.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/3.jpg)

### Step 4: List network driver plugins
#### Perintah```docker info``` digunakan untuk menunjukkan banyak informasi instalasi Docker.  Perintah docker info akan menampilkan informasi seluruh sistem mengenai instalasi pada Docker. Informasi yang ditampilkan termasuk versi kernel, jumlah container dan image. Jumlah image yang ditampilkan adalah jumlah unique image. Uuntuk image yang sama ditandai dengan nama yang berbeda hanya dihitung satu kali. Docker info tersebut memuat informasi driver penyimpanan yang digunakan, informasi tambahan  seperti pool name, file data, file metadata, penyimpanan data yang digunakan, total memori, memori metadata yang digunakan, dan total memori metadata.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/4.jpg)

## Section #2 - Bridge Networking
### Step 1: The Basics
```docker network ls```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/2.jpg)

#### Perintah ```apk update```  digunakan untuk menginstall aplikasi bridge-utils pada linux, system akan mencari daftar program yang terinstall, kemudian mencari versi terkini yang terdapat di repositori. 

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/5.jpg)

#### Perintah ```apk add bridge``` merupakan perintah untuk membuat iterface Bridge, Interface Bridge sendiri adalah Interface yang biasa digunakan untuk menjembatan suatu jaringan, Interface Bridge biasa atau sering digunakan pada Komputer Server yang difungsikan untuk Virtualisasi supaya VM yang ada pada Server tersebut dapat berhubungan dengan Jaringan Luar melalui Interface Bridge yang dibuat.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/6.jpg)

#### ```brctl show``` digunakan untuk menampilkan daftar brigde pada docker host.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/7.jpg)

#### Perintah ```ip a``` untuk menampilkan  detail informasi ip bridge 172.17.0.1/16 dengan nama docker0. 

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/8.jpg)

### Step 2: Connect a container
``` docker run -dt ubuntu sleep infinity```
#### Perintah ini akan membuat container baru berdasarkan image ubuntu terbaru dan akan menjalankan perintah sleep untuk menjaga container tetap berjalan di latar belakang. Perlu diingat bahwa perintah yang diberikan pada perintah docker run akan diberikan PID 1 dalam container, dan setelah proses ini keluar, container akan berhenti running. Penggunaan –d akan menjalankan container pada Daemon mode.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/9.jpg)

#### Perintah ```docker ps``` untuk melakukan pengecekan container. Hasil perintah tersebut menandakan jika sudah terdapat image ubuntu dengan nama sleep infinity.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/10.jpg)

#### Perintah ```brctl show``` akan menampilkan interface bridge yang telah dibuat, yaitu docker0.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/11.jpg)

``` docker network inspect bridge```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/12.jpg)

### Step 3: Test network connectivity
``` ping -c5 172.17.0.2```
#### Pada proses ping diatas akan melakukan ping IP address dari container interface bridge docker0 dengan perintah ping -c5 172.17.0.2. 
#### Pada output hasil ping nya menandakab bahwa host pada docker dapat melakukan ping pada container dalam interface bridge yang telah dibuat.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/13.jpg)

``` docker ps```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/14.jpg)

#### ```docker exec -it fcdbadcccbf6 /bin/bash``` akan menjalankan shell di dalam container ubuntu

#### ```apt-get update && apt-get install -y iputils-ping``` akan melakukan install iputils-ping yang merupakan perintah ping pada Linux. Cara kerja ping sendiri dengan mengirim rangkaian pesan Internet Control Message Protocol ke target host dan menunggu pesan Echo dari dan ke host dan Perangkat. Pesan tersebut memberitahukan User mengenai eksekusi jaringan.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/28.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/29.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/30.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/31.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/32.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/33.jpg)

#### ```ping -c5 www.github.com``` menandakan bahwa jaringan host docker sudah dapat terkoneksi dengan jaringan luar (web github)

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/15.jpg)

### Step 4: Configure NAT for external connectivity
#### Perintah ```docker run --name web1 -d -p 8080:80 nginx``` menjalankan container baru dengan nama container nginx langsung dari docker hub dengan port 8080:80 pada Daemon mode.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/16.jpg)

``` docker ps```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/17.jpg)

#### Perintah ```curl 127.0.0.1:8080``` akan membuat host menjadi terhubung dengan container nginx. Hasilnya akan menampilkan struktur kode interface image nginx.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/18.jpg)

## Section #3 - Overlay Networking
### Step 1: The Basics
``` docker swarm init --advertise-addr $(hostname -i)```
#### docker swarm init --advertise-addr $(hostname -i) akan melakukan inisialisasi docker swarm. Penggunaan --advertise-addr digunakan jika alamat node lain mencapai node manager pertama bukanlah alamat yang sama dengan yang dibaca oleh node manajer. Misalnya, dalam pengaturan cloud yang mencakup wilayah yang berbeda, host memiliki alamat internal untuk akses di dalam wilayah dan alamat eksternal yang digunakan untuk akses dari luar wilayah itu. Dalam hal ini, kita harus menentukan alamat eksternal dengan --advertise-addr sehingga node dapat menyebarkan informasi itu ke node lain yang kemudian terhubung ke sana.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/19.jpg)

#### Perintah docker swarm join berfungsi untuk mendaftarkan server/host worker pada docker swarm master.
``` docker swarm join --token SWMTKN-1-1t59fxncbeths7ykym6vomvqeg7jlxqb4wi1b08dd96c1g8jbx-280hzwqz7kr41ncm50ad8ytxn 192.168.0.48:2377```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/46.jpg)

``` docker node ls```
#### docker node ls akan menampilkan node / host / server apa saja yang telah terdaftar, pada tampilan sudah terdapat 2 node yang telah terdaftar, yaitu node1 dan node2 yang dimana kedua node tersebut saling berhubungan, node 1 menyebarkan informasi ke node 2 yang kemudian terhubung ke sana

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/21.jpg)

### Step 2: Create an overlay network
``` docker network create -d overlay overnet```
#### Pada perintah docker network create -d overlay overnet. Jaringan overlay mengelola komunikasi di antara Docker daemon yang berjalan dalam swarm. Jaringan overlay dibuat dengan cara yang sama seperti jaringan yang ditentukan User untuk container. Pada perintah tersebut, User akan melampirkan service ke satu atau lebih jaringan overlay yang ada  untuk mengaktifkan komunikasi service ke service. Jaringan overlay tersebut merupakan jaringan Docker yang menggunakan driver jaringan overlay.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/22.jpg)

```docker network ls```
#### Pada tampilan tersebut driver jaringan overlay dengan nama jaringan overnet sudah berhasil terpasang.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/23.jpg)

### Run the same docker network ls command from the second terminal. 

```docker network ls```
#### Pada tampilan tersebut jaringan "overnet" tidak muncul dalam daftar jaringan. Ini karena Docker hanya memperluas jaringan overlay ke host ketika hanya diperlukan saja ketika host menjalankan perintah dari layanan yang dibuat di jaringan.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/24.jpg)   

``` docker network inspect overnet```
#### Perintah docker network inspect overnet tersebut berjalan pada node2, yang merupakan perintah yang digunakan untuk menampilkan detail informasi pada jaringan overnet yang telah dibuat.  Terdapat beberapa informasi seperti nama, id, waktu dibuat, scope, driver, support atau tidaknya terhadap Ipv6, IPAM yang digunakan untuk konfigurasi tempat IP address (IP Address Management), support atau tidaknya penyimpanan internal, support atau tidaknya  attachable, support atau tidaknya  ingress, configFrom,jaringan, dan beberapa part pendukung lainnya. Pada IP 10.0.0.1 menunjukkan bahwa IP tersebut merupakan IP  dari container yang berjalan pada node2.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/25.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/26.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/27.jpg)

### Step 3: Create a service

``` docker service create --name myservice \```

```--network overnet \```

```--replicas 2 \```

```ubuntu sleep infinity```
#### Pada proses tersebut dijalankan pada node1 untuk membuat service baru dengan nama nyservice yang berjalan pada jaringan overnet, maka jaringannya akan menjadi terdapat 2 proses jaringan.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/34.jpg)

```docker service ls```
#### pada perintah tersebut melakukan cek service yang telah dibuat, disana sudah terdapat myservice yang telah dibuat.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/35.jpg)

``` docker service ps myservice ```
#### Pada docker service ps myservice tersebut, terdapat 2 service  yaitu myservice.1 dan myservice.2
#### Itu menandakan bahwa pembuatan replika service dari my service telah berhasil dilakukan
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/36.jpg)

#### Now that the second node is running a task on the “overnet” network it will be able to see the “overnet” network. Lets run docker network ls from the second terminal to verify this.

``` docker network ls```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/47.jpg)

#### We can also run docker network inspect overnet on the second terminal to get more detailed information about the “overnet” network and obtain the IP address of the task running on the second terminal.

``` docker network inspect overnet```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/48.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/49.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/50.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/51.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/52.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/53.jpg)

### Step 4: Test the network

``` docker network inspect overnet```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/37.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/38.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/39.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/40.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/41.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/42.jpg)

``` docker ps```
#### Pada docker ps dijalankan untuk mendapatkan id container dari myservice yang akan digunakan untuk instalasi

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/43.jpg)

``` docker exec -it fcdbadcccbf6 /bin/bash```

``` apt-get update && apt-get install -y iputils-ping```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/28.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/29.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/30.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/31.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/32.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/33.jpg)

``` ping -c5 10.0.0.3```
#### Pada ping -c5 myservice tersebut telah berhasil, menandakan bahwa host pada docker dapat melakukan ping pada container myservice dalam interface bridge yang telah dibuat. 
#### Pada ping 10.0.0.3. tersebut menandakan bahwa kedua proses dari jaringan myservice yang berada di jaringan overlay yang sama pada kedua node tersebut dapat menggunakan jaringan ini untuk berkomunikasi.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/44.jpg)

### Step 5: Test service discovery

``` cat /etc/resolv.conf```
#### Pada proses tersebut. Didalam direktori container myservice, kita masuk ke file resolv.conf. di dalam file tersebut berisi IP 8.8.8.8 milik node1 dan ip 8.8.4.4 milik node2.
#### IP tersebut akan mengirimkan semua permintaan DNS dari container ke resolver embeded DNS yang berjalan di dalam container. Semua container Docker menjalankan server DNS embeded di alamat IP tersebut.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/45.jpg)

``` ping -c5 myservice```
#### Pada hasil ping tersebut menunjukkan bahwa container dapat melakukan ping service myservice dengan menggunakan namanya. Untuk alamat IP yang dikembalikan ketika dilakukan ping adalah 10.0.0.2. dimana IP tersebut adalah IP virtual yang ditetapkan untuk service myservice saya.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/54.jpeg)

``` docker service inspect myservice```
#### Perintah tersebut akan menampilkan informasi seluruh sistem mengenai instalasi pada Docker. Informasi yang ditampilkan termasuk versi kernel, jumlah container dan image. Jumlah image yang ditampilkan adalah jumlah unique image. Uuntuk image yang sama ditandai dengan nama yang berbeda hanya dihitung satu kali. Docker info tersebut memuat informasi driver penyimpanan yang digunakan, informasi tambahan  seperti pool name, file data, file metadata, penyimpanan data yang digunakan, total memori, memori metadata yang digunakan, dan total memori metadata. Pada output hasil bagian akhirnya, virtual IP yang terdaftar adalah 10.0.0.2, ini menandakan bahwa virtual IP yang tercantum disana cocok dengan IP yang dikembalikan ketika dilakukan ping myservice.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/55.jpeg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/56.jpeg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/57.jpeg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/58.jpeg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/59.jpeg)

## Cleaning Up

#### ```docker service rm myservice``` akan menghapus service myservice 

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/60.jpeg)

``` docker ps```

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/61.jpeg)

```docker swarm leave --force```
#### docker swarm leave –force akan menghapus node1 dan node2 dari Swarm.

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-10/62.jpeg)