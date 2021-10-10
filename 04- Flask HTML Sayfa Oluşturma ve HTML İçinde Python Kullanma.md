# Flask HTML Sayfa Oluşturma ve HTML İçinde Python Kullanma 

Önceki adımlarda sayfa yönlendirmelerimizi (route) hazırlayarak sayfa bağlantılarımızı oluşturmuştuk ve sayfalara mesajlar girmiştik. Şimdi ise sayfalarımıza HTML temalarımızı ve içeriklerimizi nasıl gireceğimizi öğreneceğiz.

İlk olarak sol tarafta bulunan dosyaların içinden çalışma dosyamızı bulalım ve resimde gösterildiği şekilde adını değiştirelim. Ben **FlaskProjesi** olarak değiştirdim.

![1](https://user-images.githubusercontent.com/59111328/136693025-6d8d5b30-4f5d-4f1c-923b-097bad41e61e.png)

Daha sonra işaretlenen kısıma basıp yeni klasör oluşturuyoruz ve adını koyuyoruz. 

![3](https://user-images.githubusercontent.com/59111328/136693056-5238685a-4463-49f8-a929-9bcd04884859.png)

Çalışma dosyamızı yeni oluşturduğumuz bu klasörün içine atıyoruz ve klasöre çift tıklıyoruz.

![4](https://user-images.githubusercontent.com/59111328/136693136-c6ee7634-e742-4e0b-b27f-6e45d7fafdab.png)

Tekrardan yeni bir klasör oluşturuyoruz. Adını **templates** koyuyoruz. Klasörün adı **templates** olmak zorunda.

![5](https://user-images.githubusercontent.com/59111328/136693173-9abc6b87-0269-456e-ab27-cf2b09f8ba0d.png)

**templates** klasörünün içine girip sağ tık yapıyoruz ve **new file** diyoruz.

![6](https://user-images.githubusercontent.com/59111328/136693198-ebbbd273-ec96-4f27-9357-9ae9f760c05f.png)

Oluşturduğumuz yeni dosyanın adını **hakkimizda.html** yapıyoruz.

![7](https://user-images.githubusercontent.com/59111328/136693233-1c293167-1cb4-43e5-92dd-07e951b39968.png)

Yeni oluşturduğumuz bu klasöre sağ tık yapıp **open with** seçeneğinden **editor**'e basıyoruz.

![8](https://user-images.githubusercontent.com/59111328/136693272-2c1dc10e-059b-4fca-beb0-9a7cb24e4967.png)

Açılan HTML dosyamıza 

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>{{ sayfabasligi }}</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    Merhaba, burası {{ sayfabasligi }} ve sayfa numarası {{ sayfaid }} dir
</body>
</html>

```
kodlarını yazıyoruz.

![html](https://user-images.githubusercontent.com/59111328/136693316-98db9636-9d2e-4699-9015-7f488487e267.PNG)

Çalışma sayfamıza geri dönüp HTML sayfasına yönlendirmeyi yazıyoruz. **render_template** fonksiyonu ile route'a ilgili sayfaya gidildiğinde hangi dosyanın yükleneceğini gösterebiliyoruz. Aşağıdaki kodları çalışma dosyamıza yazıp çalıştırıyoruz.

```
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def index():
    id = 3
    return render_template("hakkimizda.html", sayfabasligi="Hakkımızda Sayfası", sayfaid = id)

if __name__ == '__main__':
   app.run()

```
![son hali](https://user-images.githubusercontent.com/59111328/136693397-6e0dc095-b005-42dc-8bea-8596536210f7.PNG)

Linke tıkladığımız zaman karşımıza çıkan sayfa şöyledir:

![html sayfası](https://user-images.githubusercontent.com/59111328/135271620-161269c0-86fa-46aa-86fd-a5c33854ee3f.PNG)

Gönderdiğimiz değişkenleri {{ }} blokları arasına almamız ile Python değişkenlerimizi HTML sayfalarımıza taşımış olduk. Gördüğünüz üzere HTML içinde Python komutları kullanmak ve Flask ile olabildiğince esnek sayfalar oluşturmak işte bu kadar kolay.

