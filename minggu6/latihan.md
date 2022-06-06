#### LATIHAN
##### Install Go
[Link Golang](https://golang.org/dl/)

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Go.png)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Go1.png)
##### Install MongoDB
[Link MongoDB](https://www.mongodb.com/download-center/community)

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Mo.png)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Mo1.png)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Mo2.png)
##### Install Mysql Community Edition
[Link Mysql](https://www.mysql.com/products/community/)

![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/my1.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/my2.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/my3.jpg)
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/my4.jpg)
##### 
#### Buat 2 contoh program Go masing-masing untuk koneksi dan membaca data dari MySQL dan MongoDB.
##### Program 1

```package main```

```import (```

```  "fmt"```

 ```   "database/sql"```

 ```   _ "github.com/go-sql-driver/mysql"```

```)```

```func main() {```

```fmt.Println("Go MySQL Tutorial")```

```  // Open up our database connection.```

```// I've set up a database on my local machine using phpmyadmin.```

  ```  // The database is called testDb```

  ```  db, err := sql.Open("mysql", "root:@tcp(127.0.0.1:3306)/minggu-06")```

   ``` // if there is an error opening the connection, handle it```

  ```  if err != nil {```

 ```       panic(err.Error())```

 ``` }```

   ``` // defer the close till after the main function has finished```

  ```  // executing```

  ```  defer db.Close()```

```}```

##### Program 2
```package main```

```import (```

```    "context"```

```    "fmt"```

```    "log"```

```    "go.mongodb.org/mongo-driver/mongo"```

```    "go.mongodb.org/mongo-driver/bson"```

```    "go.mongodb.org/mongo-driver/mongo/options"```
```)```

```type Person struct {```

```    Nama string```
```    NIM  int```
```}```

```func main() {```

```    clientOptions := options.Client().ApplyURI("mongodb://mongodb:27017")```

```    client, err := mongo.Connect(context.TODO(), clientOptions)```

```    if err != nil {```
```        log.Fatal(err)```
 ```   }```

 ```   err = client.Ping(context.TODO(), nil)```

 ```   if err != nil {```

 ```       log.Fatal(err)```
```    }```

```    fmt.Println("Connected to MongoDB!")```

```}```
##### $ docker network create container-net
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Mo3.png)
##### $ docker run -itd --name mongodb --network container-net -p 27017:27017 ruanbekker/mongodb
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/Mo4.png)
#### Dengan menggunakan Gin, buatlah RESTful API untuk membaca dara dari MySQL dan MongoDB tersebut
##### go get -u github.com/gin-gonic/gin
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin.jpg)
##### go get -u "github.com/jinzhu/gorm"
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin1.jpg)
##### go get -u "github.com/jinzhu/gorm/dialects/mysql"
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin2.jpg)
##### go get -u "github.com/go-sql-driver/mysql"
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin4.jpg)
##### go run base.go
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin5.jpg)
##### go build base.go && ./base
![](https://github.com/Tyassasmita/tekn-cloud-computing/blob/master/minggu-06/latihan3-gin6.jpg)