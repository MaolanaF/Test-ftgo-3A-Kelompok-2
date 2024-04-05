# Test-ftgo-3A-Kelompok-2
Repositori ini merupakan skenario test dan pengujian yang dilakukan pada aplikasi ftgo untuk memenuhi tugas mata kuliah PPLBO
# Team 
1. Fadhil Radja Assyidiq | 211524008
2. Maolana Firmansyah | 211524013
3. M. Fathul Ibad | 211524015
4. Reka Briyan Cahya | 211524024
5. Yayang Setia Budi | 211524030
6. Zacky Faishal Abror | 211524031

## Ruang Lingkup

Skenario tes ini akan fokus pada endpoint berikut:
* /orders: Digunakan untuk menambahkan order baru.
* /orders/{id}: Digunakan untuk mendapatkan detail order berdasarkan ID.
* /orders/{id}/status: Digunakan untuk mengubah status order.
* /orders/{id}/cancel: Digunakan untuk membatalkan order.


## Scenario Test

1. Penambahan Order
   * Buat request POST ke endpoint /orders dengan data order yang valid.
   * Validasi response code 201 Created.
   * Validasi response body berisi data order yang baru dibuat.

2. Perubahan Order
   * Buat request PUT ke endpoint /orders/{id}/status dengan data status order yang baru.
   * Validasi response code 200 OK.
   * Validasi response body berisi data order yang telah diperbarui.

3. Pembatalan Order
   * Buat request POST ke endpoint /orders/{id}/cancel.
   * Validasi response code 200 OK.
   * Validasi response body berisi pesan Order telah dibatalkan.


## Pengujian 
### Pengujian Create Restaurant dengan data valid

| Scenario      | Create Restaurant dengan data valid |
|:--------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Restaurant belum ada di database | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik restaurant-controller<br>3. Klik POST /restaurants<br>4. Klik Try it Out<br>5. Masukkan test data pada request body <br>6. Klik Execute |
| **Expected Result** | Data restaurant berhasil disimpan di database dan menghasilkan Result berikut:<br>{"id": 4} |
| **Actual Result** | Data restaurant berhasil disimpan di database dan menghasilkan Result berikut:<br>{"id": 4} |
| **Test Result** | PASS |
|**Test Data**|  
```json
{
  "address": {
    "city": "Bandung",
    "state": "Indonesia",
    "street1": "Jl. Pasir Kaliki",
    "street2": "Jl. Paskal",
    "zip": "40000"
  },
  "menu": {
    "menuItems": [
      {
        "id": "1",
        "name": "Kue Nastar",
        "price": "1.20"
      },
     {
        "id": "2",
        "name": "Kue Putri Salju",
        "price": "2.10"
      }

    ]
  },
  "name": "Toko Kue Lebaran"
}
```

### Pengujian Create Restaurant dengan field tidak lengkap
| Scenario      | Create Restaurant dengan field tidak lengkap |
|:--------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Restaurant belum ada di database | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik restaurant-controller<br>3. Klik POST /restaurants<br>4. Klik Try it Out<br>5. Masukkan test data pada request body <br>6. Klik Execute |
| **Expected Result** | Data restaurant tidak berhasil disimpan di database |
| **Actual Result** | Data restaurant tidak berhasil disimpan di database dan menghasilkan Result berikut:<br> { "timestamp": "2024-04-05T15:41:05.369+0000","status": 500,"error": "Internal Server Error", "message": "JSON conversion problem: Unexpected character ('}' (code 125)): was expecting double-quote to start field name; nested exception is com.fasterxml.jackson.databind.JsonMappingException: Unexpected character ('}' (code 125)): was expecting double-quote to start field name\n at [Source: (PushbackInputStream); line: 13, column: 17] (through reference chain: net.chrisrichardson.ftgo.restaurantservice.domain.CreateRestaurantRequest[\"menu\"] >net.chrisrichardson.ftgo.restaurantservice.domain.RestaurantMenu[\"menuItems\"]->java.util.ArrayList[0])", "path": "/restaurants"} |
| **Test Result** | PASS |
|**Test Data**  |
```json
{
  "address": {
    "city": "Bandung",
    "state": "Indonesia",
    "street1": "Jl. Pasir Kaliki",
    "street2": "Jl. Paskal",
    "zip": "40000"
  },
  "menu": {
    "menuItems": [
      {
        "id": "1",
        "name": "Kue Nastar"
      },
     {
        "id": "2",
        "name": "Kue Putri Salju",
        "price": "2.10"
      }
    ]
  },
  "name": "Toko Kue Lebaran"
}
```
### Pengujian Get Restaurant yang terdapat di database
| Scenario      | Get Restaurant yang terdapat di database |
|:--------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Restaurant ada dengan restaurantId = 4 di database | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik restaurant-controller<br>3.Klik GET /restaurants/{restaurantId}<br>4. Klik Try it Out<br>5.  Masukkan restaurant Id <br>6. Klik Execute |
| **Expected Result** | Data Restaurant berhasil di GET dengan restaurantId= 4 <br>{ "id": 4, "name": "Toko Kue Lebaran" } |
| **Actual Result** |  Data Restaurant berhasil di GET dengan restaurantId= 4 <br>{ "id": 4, "name": "Toko Kue Lebaran" }  |
| **Test Result** | PASS |
|**Test Data**  | restaurantId = 4 |

### Pengujian Get Restaurant yang tidak ada di database
| Scenario      | Get Restaurant yang tidak ada di database|
|:--------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Restaurant dengan restaurantId = 6 | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik restaurant-controller<br>3. Klik GET /restaurants/{restaurantsId}<br>4. Klik Try it Out<br>5. Masukkan restaurant Id<br>6. Klik Execute |
| **Expected Result** | Data restaurant tidak berhasil di GET dengan restaurantId = 6<br> Terjadi Error<br>Error:<br>Response headers<br>connection: keep-alive<br> content-length: 0 <br> date: Fri05 Apr 2024 15:46:50 GMT<br>keep-alive: timeout=60 |
| **Actual Result** | Data restaurant tidak berhasil di GET dengan restaurantId = 6 <br> Terjadi Error<br>Error:<br>Response headers<br>connection: keep-alive<br> content-length: 0 <br> date: Fri05 Apr 2024 15:46:50 GMT<br>keep-alive: timeout=60 |
| **Test Result** | PASS |
|**Test Data**  | restauranId = 6 |

### Pengujian Create Consumer dengan data yang valid
| Scenario      | Create Consumer dengan data yang valid |
|:--------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Costumer belum ada di database | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik consumer-controller<br>3. Klik POST /consumer<br>4. Klik Try it Out<br>5. Masukkan restaurant ID <br>6. Klik Execute |
| **Expected Result** | Data consumer berhasil disimpan di database |
| **Actual Result** | Data consumer berhasil disimpan di database dan menghasilkan Result berikut: <br>{"consumerId": 2} |
| **Test Result** | PASS |
|**Test Data**  |
```json
{
  "name": {
    "firstName": "Salahudin",
    "lastName": "Ilyas"
  }
}
```
### Pengujian Create Consumer dengan field tidak lengkap 
| Scenario          | Create Cunsomer dengan field tidak lengkap                                           |
|:------------------|:---------------------------------------------------------------------------------|
| **Preconditions** | 1. Aplikasi FTGO sudah dijalankan<br>2. Data Consumer belum ada di database     | 
| **Steps To Execute** | 1. Mengakses Swagger UI pada localhost:8084/swagger-ui/index.html<br>2. Klik consumer-controller<br>3. Klik POST /consumers<br>4. Klik Try it Out<br>5. Masukkan restaurant Id<br>6. Klik Execute |
| **Expected Result** | Data consumer tidak berhasil disimpan di database                                |
| **Actual Result** | Data consumer berhasil disimpan di database dan menghasilkan Result berikut: <br>{"consumerId": 5} |
| **Test Result**   | FAIL                                                                           |
| **Test Data**     | 
```json
{
  "name": {
    "firstName": "Salahudin"
  }
}
```




