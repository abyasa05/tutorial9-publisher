## Refleksi Tutorial 9

> Berapa banyak data yang dikirimkan ke _message broker_ dalam sekali _run_?

Dalam sekali run, sebanyak 5 data akan dikirimkan melalui method `publish_event`.

> URL `“amqp://guest:guest@localhost:5672` sama dengan yang terdapat pada program _subscriber_, apa maksudnya?

_Publisher_ dan _subscriber_ mengakses URL yang sama agar keduanya terkoneksi kepada _queue_ yang sama dalam server _message broker_. Dalam hal ini, _publisher_ akan mengirimkan _message_ ke _queue_ dalam server _message broker_ sementara _subscriber_ akan menerima message melalui _queue_ yang sama.


![Screenshot tampilan RabbitMQ](/images/Screenshot_1.png)
<br/>

![Run publisher](/images/Screenshot_2.png)
![Message diterima subscriber](/images/Screenshot_3.png)
Pada kasus ini, _publisher_ mengirimkan _message_ dengan nama "user_created" ke _queue_ dalam server RabbitMQ sebanyak 5 kali, di mana _message_ ini berisi data berupa `user_id` dan `user_name` (yang tersimpan dalam objek UserCreatedEventMessage). Lalu, _subscriber_ akan mendeteksi _message_ dengan nama "user_created" pada _queue_ yang sama dan jika diterima, maka _message_ tersebut akan diproses oleh `UserCreatedHandler` yang kemudian menghasilkan pesan _output_ di konsol.