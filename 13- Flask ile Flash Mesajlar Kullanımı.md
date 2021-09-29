# Flask ile Flash Mesajlar Kullanımı

```from flask import Flask, flash``` komutuyla **flash kütüphanesini** projeye dahil ediyoruz.

Proje dosyamızda istediğiniz bir sayfa veya durum için **flash()  fonksiyonu** ile uyarı mesajı oluşturabilirsiniz.
```flash(mesaj, kategori)``` 

Komutu biraz daha açacak olursak; <br>
**mesaj:** Kullanıcıya gösterilecek olan uyarı mesajıdır.<br>
**kategori:** Uyarı mesajının türüdür ve opsiyoneldir. Hata mesajı ise error,bilgi mesajı ise **info,uyarı mesajı** ise **warning** terimini kullanabilirsiniz

Flash mesajınızı istediğiniz yerde oluşturabilirsiniz. Oluşturduğunuz mesajları HTML sayfasında göstermek için ise aşağıdaki kod blogunu kullanmanız gerekiyor.

```
{% with messages = get_flashed_messages() %}
   {% if messages %}
      {% for message in messages %}
         {{ message }}
      {% endfor %}
   {% endif %}
{% endwith %} 
```
Yukarıdaki örneği HTML sayfasında kullandığınızda oluştururken uyarı mesajını ekranda görebilirsiniz. 


## Flash Uyarı Mesajı Örneği
```
@app.route('/hata')
def hata():
   flash("Merhaba, bu bilgi mesajıdır")
   return render_template("hata.html")
```
Komutu ile bir flash mesajı oluşturuyoruz.

Şimdi ise **hata.html** sayfasını düzenleyelim ve uyarımızı gösterelim.
```
<!DOCTYPE html>
<html>
<head>
    <title>Hata Mesajı!</title>  
</head>
<body>

    <h1>Merhaba!</h1>

    {% with messages = get_flashed_messages() %}
        {% if messages %}
            {% for message in messages %}
                {{ message }}
            {% endfor %}
        {% endif %}
    {% endwith %}


</body>
</html>
```
Ekrana çıktısı bu şekilde olacaktır:

![hata mesajı](https://user-images.githubusercontent.com/59111328/135299752-ffbd8fa1-551a-44ec-96e1-0e8a8642a9a3.PNG)

## Uyarı Tipiyle Flash Mesajı Örneği

Verdiğimiz uyarının kategorisini ayarlayarak sayfamızda özellik ayarlayabiliriz. Mesela hata mesajının arka plan rengini yeşil renk ayarlamak. Ayrıyeten eror,info,warning diye 3 çeşit uyarı kategorisinin olduğunu unutmayınız.

Öncelikle bir hata mesajını proje sayfasında örnek olarak oluşturalım:
```
@app.route('/hata')
def hata():
   flash("Merhaba, bu hata mesajıdır","error")
   return render_template("proje.html")
```
Sonuç sayfamızda olan **proje.hmtl** sayfasında ise bu sefer özel bir class ile arka plan ayarlayalım:
```
<!DOCTYPE html>
<html>
<head>
    <title>Hata Mesajı!</title> 

        <style>
        .error{
            display: inline-block;
            background-color: blue;
            color: yellow;
            padding: 5px
        }
        </style>

</head>
<body>

    <h1>Merhaba!</h1>

    {% with messages = get_flashed_messages(with_categories=true) %}
        {% if messages %}
            <ul class=flashes>
                            {% for category, message in messages %}
                                <li class="{{ category }}">{{ message }}</li>
                            {% endfor %}
                        </ul>
        {% endif %}
    {% endwith %}


</body>
</html>
```
Ekran çıktısı bu şekilde olacaktır:

![renkli hata](https://user-images.githubusercontent.com/59111328/135300460-84ddb900-9512-4a53-a0b2-2209f455c327.PNG)

## Flash Mesaj Kategorilerini Filtreleme

Eğer bir flash mesaj ayarlanmışsa HTML sayfasında bu mesajı gösterebiliyoruz. Sadece istenilen flash uyarı mesaj kategorilerinin gösterilmesini istiyorsanız aşağıda örneği verilen uyarı kategorisini kullanabilirisiniz.
```
{% with errors = get_flashed_messages(category_filter=["error"]) %}
{% if errors %}
<div class="alert-message block-message error">
  <a class="close" href="#">×</a>
  <ul>
    {%- for msg in errors %}
    <li>{{ msg }}</li>
    {% endfor -%}
  </ul>
</div>
{% endif %}
{% endwith %}
```
