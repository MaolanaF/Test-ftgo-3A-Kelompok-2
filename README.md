# Test-ftgo-3A-Kelompok-2
Repositori ini merupakan skenario test dan pengujian yang dilakukan pada aplikasi ftgo untuk memenuhi tugas mata kuliah PPLBO
# Team 
1. Fadhil Radja Assyidiq | 211524008
2. Maolana Firmansyah | 211524013
3. M. Fathul Ibad | 211524015
4. Reka Briyan Cahya | 211524024
5. Yayang Setia Budi | 211524030
6. Zacky Faishal Abror | 211524031

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
```|

