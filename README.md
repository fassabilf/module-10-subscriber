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

---
## Simulasi Slow Subscriber

![rabbitmq_spike](./figs/ss1.png)

Ketika publisher mengirim event lebih cepat daripada subscriber memproses (karena delay 1 detik per message), pesan akan terakumulasi di message queue RabbitMQ, tampak dari chart. Jumlah total queue sesuai dengan banyaknya event yang menunggu diproses. Pada contoh saya, total antrian sempat mencapai XX (sesuaikan dengan hasilmu).
---

## Multiple Subscribers & Reflection

### Screenshot 3 Subscriber
![multi_subscriber](./figs/ss2.png)

### Screenshot Quick Queue Drop (RabbitMQ)
![fast_queue_drop](./figs/ss3.png)

> Ketika ada banyak proses subscriber berjalan paralel, load queue yang sebelumnya menumpuk menjadi jauh lebih cepat diproses! Tiap subscriber membagi kerja pengambilan pesan dari queue, sehingga bottleneck lambat satu subscriber otomatis dibantu oleh subscriber lainnya.

**Reflection:**
- Arsitektur event-driven memang sangat scalable — masalah overload bisa diatas dengan menambah worker/subscriber baru.
- Kode publisher-subscriber masih bisa di-improve misal dengan menambah logging, auto reconnect, dan penanganan berbagai jenis event.
- Kekurangan: jika task critical order (harus urut), perlu pengaturan khusus.