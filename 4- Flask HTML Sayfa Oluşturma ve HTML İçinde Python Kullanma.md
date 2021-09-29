# 4- Flask HTML Sayfa Oluşturma ve HTML İçinde Python Kullanma 

Önceki adımlarda sayfa yönlendirmelerimizi (route) hazırlayarak sayfa bağlantılarımızı oluşturmuştuk ve sayfalara mesajlar girmiştik. Şimdi ise sayfalarımıza HTML temalarımızı ve içeriklerimizi nasıl gireceğimizi öğreneceğiz.

İlk olarak çalışma dosyanızın olduğu dizinde templates isimli klasör oluşturalım. Ardından HTML sayfalarınızı bu klasöre koyalım. Örneğin **iletisim.html**, **hakkimizda.html** gibi sayfalarınızı bu klasöre koyalım.

![birleşmiş](https://user-images.githubusercontent.com/59111328/135268882-371533b6-c1f3-411c-9f14-8a72786e30f4.png)

Bu klasör içinde alt klasörler oluşturarak HTML dosyalarınızı bölümlere ayırabiliriz (musteripaneli, yonetim, alanlar vs). Ama unutmayın ki ana klasörün adı **templates** olmak zorunda. Buna dikkat ettikten sonra sıradaki adıma geçebiliriz.

Artık sayfalarımız hazır olduğuna göre (HTML temalarınızı hazırladığınızı varsayıyorum) yönlendirmelerimizi sadece bir mesajla değilde ilgili HTML dosyasını göstererek yapabiliriz. Bunun için route kodunuz şu şekilde olmalıdır:

```
@app.route('/hakkimizda')
def hakkimizda():
   return render_template("hakkimizda.html")
```

Karşımıza **hakkimizda.html** sayfası geliyor. Örnekte göreceğiniz üzere **render_template** fonksiyonu ile route'a ilgili sayfaya gidildiğinde hangi dosyanın yükleneceğini gösterebiliyoruz.

```
@app.route('/hakkimizda')
def hakkimizda():
     id = 3
     return render_template("hakkimizda.html", sayfabasligi="Hakkımızda Sayfası", sayfaid = id) 

```

Yukarıda gördüğünüz gibi iki şekilde de değişkenlerimizi HTML sayfalarınıza taşıyabiliriz. Peki bu taşıdığımız değişkenleri nasıl göstereceğiz? Bunun için hemen alttaki HTML sayfasını inceleyelim.

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
Bu kodları **hakkimizda.html** dosysına yazdığımız zaman karşımıza çıkan sayfa şöyledir.

![html sayfası](https://user-images.githubusercontent.com/59111328/135271620-161269c0-86fa-46aa-86fd-a5c33854ee3f.PNG)

Gönderdiğimiz değişkenleri {{ }} blokları arasına almamız ile Python değişkenlerimizi HTML sayfalarımıza taşımış olduk. Gördüğünüz üzere HTML içinde Python komutları kullanmak ve Flask ile olabildiğince esnek sayfalar oluşturmak işte bu kadar kolay.

