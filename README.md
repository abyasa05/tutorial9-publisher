## Refleksi Tutorial 9

> Berapa banyak data yang dikirimkan ke _message broker_ dalam sekali _run_?

Dalam sekali _run_, sebanyak 5 data akan dikirimkan ke _message broker_ melalui method `publish_event`.

> URL `“amqp://guest:guest@localhost:5672` sama dengan yang terdapat pada program _subscriber_, apa maksudnya?

_Publisher_ dan _subscriber_ mengakses URL yang sama agar keduanya terkoneksi kepada _queue_ yang sama dalam server _message broker_. Dalam hal ini, _publisher_ akan mengirimkan _message_ ke _queue_ dalam server _message broker_ sementara _subscriber_ akan menerima message melalui _queue_ yang sama.<br/>


![Screenshot tampilan RabbitMQ](/images/Screenshot_1.png)<br/>


![Run publisher](/images/Screenshot_2.png)
![Message diterima subscriber](/images/Screenshot_3.png)
Pada kasus ini, _publisher_ mengirimkan _message_ dengan nama "user_created" ke _queue_ dalam server RabbitMQ sebanyak 5 kali, di mana _message_ ini berisi data berupa `user_id` dan `user_name` (yang tersimpan dalam objek UserCreatedEventMessage). Lalu, _subscriber_ akan mendeteksi _message_ dengan nama "user_created" pada _queue_ yang sama dan jika diterima, maka _message_ tersebut akan diproses oleh `UserCreatedHandler` yang kemudian menghasilkan pesan _output_ di konsol.<br/>


![Message rate spike](/images/Screenshot_4.png)
Grafik ini mengindikasikan frekuensi pengiriman _message_ dalam beberapa menit terakhir. Dalam kasus ini, _publisher_ dijalankan secara berkali-kali pada waktu yang berdekatan sehingga memicu peningkatan frekuensi _message_ yang masuk ke dalam server. Peningkatan pada periode tersebut pun ditampilkan dalam grafik.<br/>


![Queued message spike](/images/Screenshot_5.png)
Dalam kasus ini, saya menjalankan _publisher_ sebanyak 5 kali dalam waktu yang berdekatan. Maka, bisa dibilang bahwa terdapat 25 _message_ yang masuk ke dalam server pada kurun waktu tersebut. Karena _subscriber_ memiliki _delay_ sebesar 10 ms dalam memproses satu _message_, sebagian _message_ yang masuk ke dalam server harus menunggu di dalam _queue_ sebelum diproses oleh _subscriber_. Pada puncaknya, terdapat sekitar 16 _message_ yang tersimpan di dalam _queue_. Jumlah _message_ ini tentu dipengaruhi oleh beberapa faktor seperti frekuensi/kecepatan _message_ yang masuk serta kecepatan _subscriber_ dalam memproses suatu _message_.<br/>