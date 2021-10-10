# Flask’ta Static/Dinamik Url Yapısı

Sayfa yapımızı oluşturmak için  **app = Flask(__name__)** kodunun birkaç satır altından devam ediyoruz.İlk olarak ana sayfa oluşturarak başlıyoruz.
```
from flask import Flask,render_template

app = Flask(__name__)

@app.route("/")
def anaSayfa():
    return "Merhaba Sayfa Ziyaretçisi"

if __name__ == "__main__":
    app.run(debug=True)
```
kodlarını yazarak aşağıdaki görüntüyü elde ediyoruz.

![sayfa 3](https://user-images.githubusercontent.com/59111328/135260152-a193fc09-a44c-4ac0-9a3e-a6c98d067f95.PNG)

Birkaç ana sayfa daha ekleyerek web sitemizi düzenleyelim. İstediğimiz gibi ana sayfa ekleyebilir, seçenekleri çoğaltabiliriz.

![6](https://user-images.githubusercontent.com/59111328/136691036-fad47606-63a9-4fcb-aeed-5ed52caf934e.PNG)

Kod satırları aşağıdaki gibidir.

```
from flask import Flask,render_template
app = Flask(__name__)

@app.route("/")
def anaSayfa():
    return "Merhaba Sayfa Ziyaretçisi"

@app.route("/iletisim")
def iletisim():
    return "Buradan bizle iletişime girebilirsiniz."

@app.route("/hakkimizda")
def hakkimizda():
    return "Buradan da bizim hakkımızda bilgi sahibi olabilirsiniz."

if __name__ == "__main__":
    app.run(debug=True)
```

127.0.0.1:5000 adresinin yanına “iletisim” ve “hakkimizda” yazarak yönlendirdiğimiz sekmeye gidebiliriz.

![sayfa4](https://user-images.githubusercontent.com/59111328/135261419-bbf70f9b-127c-4950-9ab7-00477d2d043e.PNG)
<br>
![sayfa5](https://user-images.githubusercontent.com/59111328/135261250-2c9b9f76-1719-4593-a3e3-ce74e73ab267.PNG)
<br>
![sayfa6](https://user-images.githubusercontent.com/59111328/135261275-9aabe657-5376-4944-9134-a76b09be21fe.PNG)


