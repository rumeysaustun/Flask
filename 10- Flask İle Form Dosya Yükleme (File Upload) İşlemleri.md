# Flask İle Form Dosya Yükleme (File Upload) İşlemleri

## Form Sayfası Oluşturulma

İlk olarak yapmamız gereken şey **dosyayukleme.html** isimli sayfamızı oluşturarak formumuza dosya yükleme butonunu koyalım ve form tipimizi ```enctype=multipart/form-data``` olarak belirleyelim. Ek olarakta sayfamızın içine flash mesajlarımızı ve resim yüklendikten sonra yüklenen resimi göstereceğimiz alanlar ekleyelim. Ardından formumuzu **POST** edelim.
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Dosya Yükleme</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    {% with mesajlar = get_flashed_messages() %}
        {% if mesajlar %}
          <ul class=flashes>
          {% for mesaj in mesajlar %}
            <li>{{ mesaj }}</li>
          {% endfor %}
          </ul>
        {% endif %}
      {% endwith %}

    <form action="/dosyayukle" method="post" enctype=multipart/form-data>    
        <input type="file" name="dosya">
        <input type="submit" value="Gönder">
    </form>

    {% if dosya %}
        <br>
        <img width="250px" src="{{ url_for('static', filename='yuklemeler/'+ dosya) }}" />
    {% endif %}

</body>
</html>
```

## Gerekli Kütüphanelerin ve Configlerin Eklenmesi

Flask ve dosya yükleme bileşenlerimizi çalıştırabilmek için kütüphaneleri sayfanın en üstünde dahil etmeyi unutmayın. Ardından dosya yolu , izin verilen uzantılar gibi ilk değişken tanımlamalarımızı yapalım. İlk olarak kütüphaneler:

```
import os
from flask import Flask, render_template, request, redirect, abort, flash, url_for
from werkzeug.utils import secure_filename
```

Ardından basit tanımlarımızı halledelim:

```
YUKLEME_KLASORU = 'static/yuklemeler'
UZANTILAR = set(['txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif'])
```

Şimdi Flask başlayabilir:

```
app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = YUKLEME_KLASORU
app.secret_key = "Flask_Dosya_Yukleme_Ornegi"
```

## Güvenlik Kontrolleri

Formlardan neler yükleneceğini bilemeyiz. Bunun için ilk olarak güvenlik önlemlerini almak bize fayda sağlayacaktır. İlk güvenlik önlemi olan dosya uzantısı kontrolüdür. Çünkü saldırganlar **.php** veya **.exe** uzantılı gibi sunucu tarafından çalıştırılabilen dosyalarla kendi zararlı kodlarını sunucumuzda aktif edebilirler. Öyleyse sayfanın en başında eklediğimiz **UZANTILAR** isimli dizimiz ile gelen dosyanın bu uzantılardan birine sahip olup olmadığını kontrol edelim:

```
def uzanti_kontrol(dosyaadi):
   return '.' in dosyaadi and \
   dosyaadi.rsplit('.', 1)[1].lower() in UZANTILAR
```

Peki ne yaptık? İlk olarak **uzanti_kontrol()** isimli fonksiyonumuz ile dosyaadi isimli bir parametre aldık ve önce bu dosya adı bir uzantıya sahip mi diye (içinde . varsa uzantıya sahiptir), ardından da uzantısı bizim izin verdiğimiz dosya uzantılarından biri mi diye kontrol ettik. Eğer bu iki testten başarıyla geçerse **True**, geçemezse **False** dönecektir.

Şimdi ise **secure_filename()** fonksiyonu ile dosyanın sahip olduğu isim bizim için bir tehdit içeriyor mu diye kontrol edeceğiz. Nasıl yani derseniz diye hemen küçük bir örnek verelim. Diyelim ki saldırganın sitemizin temel dosyaları olan resimleri vs değiştirmek istiyor. Site logomuzu, yazı resimlerini kendi resimleriyle değiştirmek istiyor ve bunu yapmak içinde dosya adını **"../../../../home/images/logo.png"** gibi bir formatta hazırladı ve dosya yükleme işlemini gerçekleştirdi. Sonuç olarak saldırgan bizim izin verdiğimiz klasöre değil, kendi istediği klasöre yüklemiş olduğu dosyasını. Tabi bu her sistemde çalışmayabilir ama emin olun o talihsiz siz olmak istemezsiniz. Bu nedenle şu şekilde küçük ama etkili bir kontrol mekanizması ekleyelim:
```
dosyaadi = secure_filename(dosya.filename)
```
Bu sayede **"../../../../home/images/logo.png"** şeklindeki bir dosya yeni adı **"home_images_logo.png"** olacaktır.

## Route İle Formdan Gelen Dosyayı Alma

Basit bir form sayfasını oluşturduktan sonra verileri ```action="/dosyayukle"``` etiketi ile **/dosyayukle** sayfasına post edeceğimizi belirtmiş olduk. Öyleyse hemen ilgili route u oluşturalım ve daha öncesinde yazdığımız güvenlik önlemlerini dahil edelim:

**Form ile dosya yükleme işlemi**

```
@app.route('/dosyayukle', methods=['POST'])
def dosyayukle():
   if request.method == 'POST':
        # formdan dosya gelip gelmediğini kontrol edelim
      if 'dosya' not in request.files:
         flash('Dosya seçilmedi')
         return redirect('dosyayukleme')         
        # kullanıcı dosya seçmemiş ve tarayıcı boş isim göndermiş mi
      dosya = request.files['dosya']                    
      if dosya.filename == '':
         flash('Dosya seçilmedi')
         return redirect('dosyayukleme')
        # gelen dosyayı güvenlik önlemlerinden geçir
      if dosya and uzanti_kontrol(dosya.filename):
         dosyaadi = secure_filename(dosya.filename)
         dosya.save(os.path.join(app.config['UPLOAD_FOLDER'], dosyaadi))
         #return redirect(url_for('dosyayukleme',dosya=dosyaadi))
         return redirect('dosyayukleme/' + dosyaadi)
      else:
         flash('İzin verilmeyen dosya uzantısı')
         return redirect('dosyayukleme')
   else:
      abort(401)
```

Sonrada form sayfalarımızı oluşturduğumuz sayfaların route kısımlarını yazalım:

**Form ile dosya yükleme sayfası**
```
@app.route('/dosyayukleme')
def dosyayukleme():
   return render_template("dosyayukleme.html")
```

**Form ile dosya yükleme sayfası - Sonuç**
```
@app.route('/dosyayukleme/<string:dosya>')
def dosyayuklemesonuc(dosya):
   return render_template("dosyayukleme.html", dosya=dosya)
```

## Sonuç

Artık form yapımız ile rahatlıkla dosya yükleme işlemini yapabiliyoruz. Aşağıdaki resimde çalışan örneklerini görebilirsiniz.

Resimler:

![copy](https://user-images.githubusercontent.com/59111328/135291051-1a22d58d-7029-4fc3-8743-dbf08f55f158.PNG)







