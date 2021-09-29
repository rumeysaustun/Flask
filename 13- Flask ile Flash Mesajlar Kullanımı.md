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

Şimdi ise **hata.html **sayfasını düzenleyelim ve uyarımızı gösterelim.
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





