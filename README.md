# Publisher - README

Nama: Faiz Assabil Firdaus  
NPM: 2306224354

---

### a. Berapa data/dokumen yang publisher kirim sekali run?

Pada satu kali run, program publisher mengirimkan **5 event** ke message broker (RabbitMQ).  
Setiap event berisi data `UserCreatedEventMessage` berbeda, dengan user id dari 1 sampai 5.

---

### b. Penjelasan url "amqp://guest:guest@localhost:5672"

- **amqp**: adalah protokol (Advanced Message Queuing Protocol) yang digunakan untuk komunikasi dengan message broker.
- **guest:guest**: bagian pertama adalah username (“guest”), bagian kedua adalah password (“guest”) untuk login ke RabbitMQ.
- **localhost**: berarti RabbitMQ berjalan di komputer lokal (sendiri).
- **5672**: port default yang digunakan RabbitMQ untuk menerima koneksi AMQP.

Jadi, url ini digunakan oleh aplikasi untuk terkoneksi ke server RabbitMQ lokal memakai user guest.