# Flask Sayfaya Kaynak Dosyaları Ekleme (CSS,JS,IMG vs).md

Örnek olarak yine örnek bir hakkimizda.html dosyası oluşturarak dosyalarımızı bu HTML kodların arasına dahil ediyoruz.Şimdi Flask'ın kullanacağımız js, css, resim vs. dosyaları dahil etmemiz için gerekli olan static klasörünü oluşturuyoruz.

![11](https://user-images.githubusercontent.com/59111328/136693811-0cee7ee2-a90a-4a93-928e-425911609418.png)


Bundan sonra kodlarımıza dahil edeceğimiz bütün sabit dosyalar static klasörünün içinde olacaktır. Bu klasörün içeriğini daha düzenli olması adına css, js ve img gibi alt klasörlere ayırabiliriz. Örnek olarak bir dizin şu şekilde olabilir:

![222](https://user-images.githubusercontent.com/59111328/136693826-8c898a50-053e-4b9b-95ec-d92b1fee8cad.png)

Artık bu klasörlerin içini kullanacağımız dosyalarla doldurabiliriz. Örnek olarak img klasörünün içine **manzara.jpg** adlı bir resim ekleyelim.

![33](https://user-images.githubusercontent.com/59111328/136693857-01d6f243-159b-4644-a433-44970dff7520.png)


Ardından nasıl kodlarımıza dahil edeceğimizi görelim. Bunun için örnek oluşturduğumuz HTML dosyasının içine girelim ve dahil etmek istediğimiz alanda aşağıdaki kod yapısını kullanalım. Örnek olarak ben bir resim dahil etmek istiyorum:

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
