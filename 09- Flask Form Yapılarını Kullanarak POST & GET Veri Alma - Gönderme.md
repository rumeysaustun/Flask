# Flask Form Yapılarını Kullanarak POST & GET Veri Alma - Gönderme

## HTML Form Yapısını Oluşturma

İlk işimiz bir HTML sayfa oluşturarak içine basit bir form yapısı yerleştirmek olacaktır. Bunun için **form.html** isimli dosyayı **templates** klasörünün içine oluşturuyoruz. Methodumuzu başlangıç olması için **POST** seçelim ve ardından form hedefini **"/verilerial"** isimli sayfamız olarak belirleyelim. Sizde aşağıdaki örneği kullanabilirsiniz:
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Form Yapısı</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    <form action="/verilerial" method="post">

        <input type="text" name="isim" placeholder="İsminiz"> <br>
        <input type="text" name="mesaj" placeholder="Mesajınız"> <br>

        <input type="submit" value="Gönder">
    </form>

</body>
</html>
```

Formumuz şöyle gözükmektedir:

![form yapısı](https://user-images.githubusercontent.com/59111328/135284720-d0bf21a0-5675-4bf3-9ac6-31ed7c13794f.PNG)

## Route Yazma ve Form Yapısını Oluşturma

Sıra sayfamızda gerekli **route** işlemlerini yaparak yönlendirmeleri oluşturmanın sırası geldi. Oluşturmamız gereken sayfalar; kullanıcıların form yapısını doldurup göndereceği **/mesajyazin** sayfası ve bu formdan gelen verileri alıp işleyeceğimiz **/verilerial** sayfasıdır. İşe ilk olarak route yazarak başlıyoruz:

```
@app.route('/mesajyazin')
def mesajyazin():
   return render_template("form.html")
```

## Gelen Verileri Göstereceğimiz Sayfayı Oluşturalım

Formdan gelen verileri göstereceğimiz html sayfasını oluşturalım. HTML sayfamızın adını **verilerigoster.html** yapabiliriz:

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Form Verilerini Göster</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    <h1>Formdan Gelen Veriler:</h1>

    {{ hata }} <br>

    <strong>İsim:</strong> {{ isim }} <br>
    <strong>Mesaj:</strong> {{ mesaj }} <br>

</body>
</html>
```

## Form İçin Route Yazma ve Kütüphaneleri Ekleme

Bu aşamada dosyamızda gerekli form verilerini almak için route yazacağız ve kontrolleri sağlayacağız. Ama unutmadan request kütüphanesini de dahil ederek ```from flask import Flask, render_template, request``` blogunu sayfamızın üstünde görelim.

```
@app.route('/verilerial', methods=['POST', 'GET'])
def verilerial():
   if request.method == 'POST':
      isim = request.form.get('isim') 
      mesaj = request.form.get('mesaj')

      return render_template("verilerigoster.html",isim=isim,mesaj=mesaj)

   else:
      return render_template("verilerigoster.html",hata="Formdan veri gelmedi!")
```

Yukarıdaki gördüğünüz kodlarda **methods=['POST', 'GET']** parametresi ile sayfamızın hangi form methodlarını kabul edeceğini belirttik. Eğer sadece **POST** yazsaydık sayfamız yalnızca **POST** ile gelen istekleri kabul edecekti.

```
if request.method == 'POST' 
```
ile sayfada yine bir **POST** kontrolü yaptık ama siz bu kontrolleri gelen veriler boş mu dolu mu şeklinde kullanabilirsiniz.

Son olarak aldığımız verileri oluşturduğumuz **verilerigoster.html** sayfasına göndererek ekranda gösterdik. Çıktısı ise şu şekilde oldu:

![gelenveri](https://user-images.githubusercontent.com/59111328/135286833-2038da9e-b638-4fff-94c6-d22d154a14de.PNG)

Eğer form sayfası üzerinden değilde direkt **verilerigoster.html** sayfasına girseydik ekran çıktısı aşağıdaki gibi olacaktı. Çünkü bu şekilde sayfaya girdiğimizde sayfaya **GET** yöntemiyle girmiş oluyoruz:

![veri gelmed](https://user-images.githubusercontent.com/59111328/135286885-d6725c8e-e33f-4db4-a645-11ee2c07a94b.PNG)







