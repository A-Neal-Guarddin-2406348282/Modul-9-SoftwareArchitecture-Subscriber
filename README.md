## Memahami AMQP dan Connection String

**a. Apa itu AMQP?**
AMQP (Advanced Message Queuing Protocol) adalah protokol standar terbuka di lapisan aplikasi (*application layer*) yang digunakan untuk *middleware* berorientasi pesan. Protokol ini mengatur bagaimana aplikasi klien (seperti *publisher* dan *subscriber* milik saya) berkomunikasi dengan *message broker* (seperti RabbitMQ). AMQP memastikan pesan dirutekan, diantrekan, dan dikirim secara aman serta andal antar sistem.

**b. Apa arti `guest:guest@localhost:5672`?**
Ini adalah *string* koneksi (URI) yang digunakan oleh aplikasi untuk terhubung ke *message broker* RabbitMQ.
* **`guest` yang pertama**: Merupakan **username** *default* untuk otentikasi/masuk ke server RabbitMQ.
* **`guest` yang kedua**: Merupakan **password** *default* yang berpasangan dengan *username* tersebut.
* **`localhost:5672`**: Menunjukkan lokasi dari server *broker* tersebut. `localhost` berarti server RabbitMQ berjalan di komputer lokal (mesin yang sama), dan `5672` adalah *port* jaringan standar yang digunakan untuk lalu lintas data AMQP.