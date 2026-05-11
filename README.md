# Tutorial 9 - Subscriber

***Oleh Neal Guarddin - 2406348282***

### a. Apa itu AMQP?
**AMQP (Advanced Message Queuing Protocol)** adalah standar protokol terbuka di lapisan aplikasi (*application layer*) yang dirancang khusus untuk *message-oriented middleware*. Protokol ini menyediakan aturan baku yang memungkinkan berbagai sistem atau aplikasi untuk saling berkirim pesan secara asinkron, aman, dan andal.

Di dalam *repository* ini, saya menggunakan AMQP sebagai jalur komunikasi agar aplikasi *subscriber* bisa terhubung dengan *message broker* (yaitu RabbitMQ). Aplikasi saya memanfaatkan *library* `crosstown_bus` untuk mendengarkan *event* dari antrean.

Berikut adalah *snippet* kode dari `src/main.rs` di mana saya mengonfigurasi koneksi AMQP:

```rust
fn main() {
    // Terhubung ke broker menggunakan protokol AMQP
    let listener =
        CrosstownBus::new_queue_listener("amqp://guest:guest@localhost:5672".to_owned()).unwrap();
        
    _ = listener.listen("user_created".to_owned(), UserCreatedHandler{},
                        crosstown_bus::QueueProperties { 
                            auto_delete: false, 
                            durable: false,
                            use_dead_letter: true 
                        }
                    );

    loop {}
}
```

### b. Apa maksud dari `guest:guest@localhost:5672`, apa itu *guest* pertama, apa itu *guest* kedua, dan untuk apa `localhost:5672`?

* **Maksud `guest:guest@localhost:5672`**: Ini adalah URL koneksi (*Connection URI*) yang digunakan oleh program untuk 
memberitahu `crosstown_bus` cara melakukan otentikasi dan ke mana harus terhubung (server RabbitMQ).
* ***Guest* pertama**: Merupakan **username** *default* bawaan yang disediakan oleh RabbitMQ untuk proses otentikasi 
(masuk/login ke *broker*).
* ***Guest* kedua**: Merupakan **password** *default* dari RabbitMQ yang berpasangan dengan *username* tersebut.
* **Kegunaan `localhost:5672`**: Bagian ini menunjukkan lokasi server. `localhost` berarti *message broker* (RabbitMQ) 
sedang berjalan di komputer lokal (mesin yang sama), sedangkan `5672` adalah nomor **port** TCP di mana RabbitMQ secara *default* menunggu (*listen*) jalur komunikasi masuk untuk AMQP.
* 