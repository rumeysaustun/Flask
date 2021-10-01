# Flask Templatelarda Koşul Kullanımı (If - Else)

İlk olarak gerekli route yönlendirmesini yaparak başlıyoruz.

```
@app.route('/ifelse')
def ifelse():
   return render_template("ifelse.html", toplam = 3)
```

Sayfa url adresimizi oluştururken aynı zamanda toplam isimli bir değişkeni de örneklerde kullanmak için gönderiyoruz. Değer olarak rastgele 3 seçeneğini kullanacağız. Ardından yeni oluşturacağımız ifelse.html sayfamıza gerekli koşul bölümünü ekleyelim. İlgili if else koşul bölümü şu şekilde olmalıdır:
```
{% if [KOŞUL] %}
    [İŞLEMLER]    
{% else %}
    [İŞLEMLER]
{% endif %}
```
Eğer birden fazla koşulunuz varsa onun için birde **elif** bölümü eklemeniz gerekecektir.
```
{% if [KOŞUL1] %}
    [İŞLEMLER]
{% elif [KOŞUL2] %}
    [İŞLEMLER]
{% elif [KOŞUL3] %}
    [İŞLEMLER]
{% else %}
    [İŞLEMLER]
{% endif %}
```
Kendi örneğimize gelirsek, gönderdiğimiz toplam değeri istediğimiz değer mi diye oldukça basit bir kontrol yapalım ve ardından ekrana bilgi mesajı yazdıralım. Öyleyse ifelse.html sayfamız şu şekilde olabilir:

![ifelse](https://user-images.githubusercontent.com/59111328/135280669-91641a98-c4f6-4a89-b533-9705c32b7f8f.PNG)

Kodları:

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>If Else Koşulları</title>

</head>
<body>
<h1>If Else Koşulları</h1>
    <h3>
        {% if [toplam==3] %}
    Toplam = 3
{% else %}
    Toplam # 3
{% endif %}
</h3>

    <p>
         {% if [toplam==3] %}
    Toplam 3'tür
{% else %}
    Toplam 3 değildir
{% endif %}
    </p>
</body>
</html>
```
