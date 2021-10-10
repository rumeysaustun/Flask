# Flask Template Inheritance ve Blocklar (Include & Extends)

İlk olarak templates klasörün içine şablon bir sayfa oluşturuyoruz ve adına **hizmetler** adını veriyoruz.

![1](https://user-images.githubusercontent.com/59111328/136694180-9da44c7d-3abf-4b9e-a326-ccc760193762.PNG)

Örnek bir şablon olacağı ve her sayfada sadece hizmet başlığı ile metini değiştiğinden dolayı basit bir HTML kodlama yapmak için aşağıdakileri yazıyoruz:
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Hizmetler Sayfası</title>

</head>
<body>

    <h3>Hizmet Adı</h3>    

    <p>Hizmet açıklaması bu alanda yer alacaktır</p>

</body>
</html>

```

Yukarıdaki yazılan kodları sekmeye yazdıktan sonra aşağıdaki görüntüyü elde ediyoruz.

![2](https://user-images.githubusercontent.com/59111328/136694187-1f01ee0c-fccf-4a9b-aadf-665ad499cc3e.PNG)

Dosyamıza hizmetler isimli sayfayı oluşturmak için gerekli route’u ekleyelim

```
@app.route('/hizmetler')
def hizmetler():
   return render_template("hizmetler.html")

```
Tarayıcıda çalıştırdığımız zaman sayfanın nasıl göründüğüne bakalım:

![hizmetlere](https://user-images.githubusercontent.com/59111328/135275939-7b1609e9-f46d-4f9b-9794-dbc72871c61d.PNG)

Bu şablonu kalıtım (inheritance) kullanarak diğer sayfalarda kullanabiliriz. Bunun için ilk yapmamız gereken şey yeni bir hizmet sayfası oluşturalım ve adını **bahçe işleri** koyalım. Ardından gerekli route işlemini gerçekleştirelim.

![3](https://user-images.githubusercontent.com/59111328/136694198-cebde9c0-28d6-4ed6-893c-1e525ef1e7b7.PNG)


```
@app.route('/bahce-isleri')
def bahceisleri():
   return render_template("bahçe işleri.html")
```

Şablon sayfamız olan **hizmetler.html** isimli dosyamızda değiştireceğimiz alanları block haline getirerek şablonu kullandığımız diğer sayfalarda dinamik hale getirmiş olacağız. **hizmetler.html** dosyasının son hali şu şekilde olacaktır:

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>Hizmetler Sayfası</title>

</head>
<body>

    {% block hizmetadi %}
    <h3>Verilen Hizmet Adı
</h3> 
    {% endblock %}


    {% block hizmetaciklamasi %}
    <p>Verilen hizmetin açıklaması bu alanda yer alacaktır</p>
    {% endblock %}

</body>
</html>
```

Şablonumuzda dinamik olmasını istediğimiz alanları block içerisine aldık ve blocklara isim verdik. Kullandığımız block yapısı tam haliyle şu şekildedir:

```
{% block blockadi %}
.
.
.
{% endblock %}
```

Artık diğer sayfalarımızda bu block alanlarını block isimleriyle çağırarak dilediğimiz gibi değiştireceğiz. İlk olarak yeni oluşturduğumuz **bahçe işleri.html** sayfamıza gidelim ve extends yapısıyla şablon sayfamızı çağıralım.

```
{% extends "hizmetler.html" %}
```

Şimdi tarayıcıdan bahce-isleri sayfasına bakalım ve hizmetler sayfasının birebir aynısını gördüğümüzü doğrulayalım. Gördüğümüz üzere sayfamızda sadece bir satırlık extend bloğu yer almasına rağmen şablonun birebir aynısı yeni sayfamızda da yer alıyor.

![bahce isleri](https://user-images.githubusercontent.com/59111328/135277586-ae0bf57c-2365-42c1-9de1-312b19a20b1e.PNG)

Son olarak ise değiştirmek istediğimiz sayfaları **bahçe işleri.html** sayfasında blockları kullanarak değiştirelim ve şu hale sokalım:

```
{% extends "hizmetler.html" %}

{% block hizmetadi %}
<h3>Bahçe İşleri</h3>
{% endblock %}


{% block hizmetaciklamasi %}
<p>Bahçenize kendi bahçemiz gibi özenle bakarız.</p>
{% endblock %}

```
Şimdi tarayıcıda nasıl göründüğüne bakalım:

![bahcaa](https://user-images.githubusercontent.com/59111328/135277828-3548d183-a0b7-4c01-bc42-6aadf36edbad.PNG)

