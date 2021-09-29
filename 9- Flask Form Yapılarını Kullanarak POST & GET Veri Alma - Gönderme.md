# Flask Form Yapılarını Kullanarak POST & GET Veri Alma - Gönderme

## HTML Form Yapısını Oluşturma

İlk işimiz bir HTML sayfa oluşturarak içine basit bir form yapısı yerleştirmek olacaktır. Bunun için form.html isimli dosyayı templates klasörünün içine oluşturuyoruz. Methodumuzu başlangıç olması için POST seçelim ve ardından form hedefini "/verilerial" isimli sayfamız olarak belirleyelim. Sizde aşağıdaki örneği kullanabilirsiniz:
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



