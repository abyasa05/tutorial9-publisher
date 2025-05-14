## Refleksi Tutorial 9

> Berapa banyak data yang dikirimkan ke _message broker_ dalam sekali _run_?

Dalam sekali run, sebanyak 5 data akan dikirimkan melalui method `publish_event`.

> URL `“amqp://guest:guest@localhost:5672` sama dengan yang terdapat pada program _subscriber_, apa maksudnya?

_Publisher_ dan _subscriber_ mengakses URL yang sama agar keduanya terkoneksi kepada _queue_ yang sama dalam server _message broker_. Dalam hal ini, _publisher_ akan mengirimkan _message_ ke _queue_ dalam server _message broker_ sementara _subscriber_ akan menerima message melalui _queue_ yang sama.