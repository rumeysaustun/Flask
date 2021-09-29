# Flask Sayfaya Kaynak Dosyaları Ekleme (CSS,JS,IMG vs).md

Örnek olarak yine örnek bir hakkimizda.html dosyası oluşturarak dosyalarımızı bu HTML kodların arasına dahil ediyoruz.Şimdi Flask'ın kullanacağımız js, css, resim vs. dosyaları dahil etmemiz için gerekli olan static klasörünü oluşturuyoruz. Bundan sonra kodlarımıza dahil edeceğimiz bütün sabit dosyalar static klasörünün içinde olacaktır. Bu klasörün içeriğini daha düzenli olması adına css, js ve img gibi alt klasörlere ayırabiliriz. Örnek olarak bir dizin şu şekilde olabilir:

![bir](https://user-images.githubusercontent.com/59111328/135273440-1e0cacfa-0c0d-4352-89db-e881210d5350.png)

Artık bu klasörlerin içini kullanacağımız dosyalarla doldurabiliriz. Ardından nasıl kodlarımıza dahil edeceğimizi görelim. Bunun için örnek oluşturduğumuz HTML dosyasının içine girelim ve dahil etmek istediğimiz alanda aşağıdaki kod yapısını kullanalım. Örnek olarak ben bir resim dahil etmek istiyorum:

```
{{ url_for('static', filename='img/manzara.jpg') }}
```

filename içerisindeki adresi istediğimiz gibi değiştirerek tüm dosyalarımızı dahil edebiliriz. Örneğin bir css dosyanızı dahil etmek için şu şekilde kullanabilirsiniz:

```
{{ url_for('static', filename='css/main.css') }}
```

Sayfaya örnek olarak dahil ettiğim resim ve tüm kod yapısını örnek olarak inceleyebilirsiniz:
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Hakkımızda</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" type="text/css" media="screen" href="{{ url_for('static', filename='css/main.css') }}">
    <script src="{{ url_for('static', filename='js/main.js') }}"></script>
</head>
<body>

    <h1>Manzara Fotoğrafları</h1>
    <p>Güneş Batarken Çekilen Bir Manzara Fotoğrafı</p>

    <img src="{{ url_for('static', filename='img/manzara.jpg') }}" width="400px" alt="manzara">

</body>
</html>
```

Ekran çıktısı şu şekilde olacaktır:

![manzara](https://user-images.githubusercontent.com/59111328/135274542-6791e1d7-9a22-4e2f-b9ce-ceed087f72b1.PNG)
