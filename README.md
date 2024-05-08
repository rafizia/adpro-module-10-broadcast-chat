Nama: Muhammad Rafi Zia Ulhaq<br>
NPM: 2206814551<br>
Kelas: Pemrograman Lanjut B<br>

# Module 10 - Broadcast Chat

### Original Code of Broadcast Chat

![alt text](https://github.com/rafizia/adpro-module-10-broadcast-chat/blob/master/src/image/Image-1.png?raw=true)

Saat kita mengetikkan sebuah pesan pada *client*, pesan itu akan dikirim melalui koneksi `WebSocket` ke *server*. Setiap pesan yang diterima *server* akan dicetak pada *console server* tersebut, kemudian diformat dengan menambahkan alamat *client* sebagai *prefix* kemudian mengirimkannya kembali melalui *broadcast channel*. Dengan menggunakan *broadcast channel*, *server* dapat mengirim pesan tersebut ke semua *client* yang terhubung. Sehingga pesan yang kita ketik dan kirim ke *server* akan diterima kembali oleh *client* kita sendiri serta *client* yang terhubung dengan *server* tersebut.

### Modifying the Websocket Port

![alt text](https://github.com/rafizia/adpro-module-10-broadcast-chat/blob/master/src/image/Image-2.png?raw=true)

Agar tetap dapat berjalan dengan baik, selain mengubah *port* pada `client.rs`, kita juga perlu mengubah *port* pada `server.rs`. Hal ini karena jika keduanya memiliki *port* yang berbeda satu sama lain, *client* tidak akan dapat terhubung dengan *server*.

### Add Some Information to Client

![alt text](https://github.com/rafizia/adpro-module-10-broadcast-chat/blob/master/src/image/Image-3.png?raw=true)

Untuk menambahkan informasi IP dan *port* dari setiap *client*. Kita dapat merubah beberapa kode pada `client.rs` dan `server.rs`. Pada `client.rs` kita hanya perlu mengganti kode `println!("From server: {}", text)` menjadi `println!("Rafi's Computer - From server: {}", text)`, sedangkan pada `server.rs` kita dapat mengganti kode `bcast_tx.send(text.into())?` menjadi
```
let formatted_message = format!("{addr:?}: {}", text);
bcast_tx.send(formatted_message)?;
```