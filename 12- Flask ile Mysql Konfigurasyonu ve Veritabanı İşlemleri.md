# Flask ile Mysql Konfigurasyonu ve Veritabanı İşlemleri

## Kütüphanelerin Eklenmesi

Python'un temeli olarak ilk önce işe gerekli kütüphanelerimizi ekleyerek başlıyoruz. Bunun için 3 kütüphaneyi pip komutuyla indiriniz ve dosyanızın başına ekleyiniz.

```
pip install flask-mysqldb
```
 

Yükleme tamamlandıktan sonra **flask_mysqldb**  kütüphanesini proje dosyanızın başına ekleyiniz.
```
from flask import Flask, render_template, request, redirect
from flask_mysqldb import MySQL
 ```


## Mysql Konfigürasyonu

Kütüphanemizi projemize ekledikten sonra artık veritabanı bilgilerimizi uygulamamıza tanıtmamız gerekiyor. Bunun için aşağıdaki kodları ekleyiniz ve **host,user,password,db** değişkenlerini kendi veritabanınızın bilgileriyle düzenleyiniz.
```
app = Flask(__name__)


app.config['MYSQL_HOST'] = "localhost"
app.config['MYSQL_USER'] = "root"
app.config['MYSQL_PASSWORD'] = "123456"
app.config['MYSQL_DB'] = "pytest"
app.config['MYSQL_CURSORCLASS'] = "DictCursor"

mysql = MySQL(app)
```
Buradaki ```mysql = MySQL(app)``` komutu ile app içine tanımladığımız config bilgilerini mysql değişkenimize bağlıyoruz.

## Örnek Bir Tablo Oluşturulması

Bu örneğimizde kullanacağımız basit bir veritabanı tablosunu direkt **PHPMyAdmin** üzerinden oluşturabilirsiniz. Bu yazıdaki örnekte kullanacağım tablo yapısı şu şekildedir.

![image](https://user-images.githubusercontent.com/59111328/135296682-eb1df46e-a0bf-4e09-aac5-d445422beefa.png)

 
## Örnek Form İçin Route Ekleme

Basit bir örnek için hızlıca kullanıcılardan isim ve yaş bilgisi alacağımız bir form sayfası ve bu formdan gelen verileri alacağımız bir route yazalım. Eğer bu kısımları hatırlamıyorsanız önceki adımlara bakmanızı öneriyorum. Gerekli Routeleri yazalım:

## Kullanıcıdan Alınacak Form Sayfası İçin Route
**Mysql Kullanıcı Ekleme**
```
@app.route('/kullaniciekle')
def kullaniciekle():
   return render_template("kullaniciekle.html")
```

## Kullanıcıdan Alınacak Form Sayfası İçin HTML Sayfa (kullaniciekle.html)
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Kullanıcı Ekle</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    <form action="/kullanicieklesonuc" method="post">

        <input type="text" name="isim" placeholder="İsminiz"> <br>
        <input type="number" name="yas" placeholder="Yaşınız"> <br>

        <input type="submit" value="Gönder">
    </form>

</body>
</html>
```
## Formdan Gelen Verileri Alarak Veritabanına Ekleyecek Route

**Mysql Kullanıcı Ekleme**
```
@app.route('/kullanicieklesonuc', methods=['POST'])
def kullanicieklesonuc():
   if request.method == 'POST':
      isim = request.form.get('isim')
      yas = request.form.get('yas')

      cursor = mysql.connection.cursor()

      sorgu = "INSERT INTO kullanicilar VALUES(%s,%s,%s)"

      cursor.execute(sorgu,(None,isim,yas))
      mysql.connection.commit()
      cursor.close()


      return render_template("kullanicieklesonuc.html",isim=isim,yas=yas)

   else:
      return render_template("kullanicieklesonuc.html",hata="Formdan veri gelmedi!")
```













**İşin önemli kısmı olan bu route bölümünü açıklayalım:**

```isim = request.form.get('isim')``` : Formdan gelen isim değişkenini alıyoruz
```yas = request.form.get('yas')``` : Formdan gelen yaş değişkenini alıyoruz
```cursor = mysql.connection.cursor()``` : Bu tanımlama ile bir cursor oluşturuyoruz ve yukarıda oluşturduğumuz mysql değişkenine atadığımız veritabanını bağlıyoruz.
```sorgu = "INSERT INTO kullanicilar VALUES(%s,%s,%s)" ```: Veritabanında çalıştırılacak SQL komutudur. Bu sorguya SELECT, INSERT, UPDATE, DELETE, ALTER gibi komutlarınızı yazabilir ve değişkenleri %s ile belirtebilirsiniz.
```cursor.execute(sorgu,(None,isim,yas)) ```: Yazılan sorguyu cursor aracılığı ile çalıştırıyoruz. parantez içindeki (None,isim,yas) bölümü sorgunun içinde yazdığımız %s e denk gelen değişkenlerdir. Ben tablomda bir auto increment sütunu tuttuğum için None ile boş değer gönderdim.
```mysql.connection.commit() ```: Yapılan değişikleri kaydetmek ve veritabında uygulamak için gerekli olan commit fonksiyonu. Eğer bu kısmı yazmazsanız değişiklikleriniz veritabanınızda uygulanmayacaktır.
```cursor.close() ```: Veritabanı bağlantısını sonlandırıyoruz.

## İşlem Sonucu Gösteren Sayfa HTML Kodu (kullanicieklesonuc.html)

Yukarıda  yazdığımız rpute sonucuna göre bizi bu sayfaya yönlendirecek ve formdan gelen verileri gösterecektir. Eğer bir hata meydana gelirse {{hata}} değişkeni ile ekrana yazacağız. Bu işlemler için aşağıdaki kodda yer alan alanımız yeterli olacaktır:

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
    <strong>Yaş:</strong> {{ yas }} <br>

</body>
</html>
```

## SELECT, UPDATE, INSERT, DELETE İşlemleri
Yukarıda **INSERT** komutu için bir örnek yapmıştık ve nasıl kullanacağını gördük. Şimdi sıradan temel SQL komutlarını işleyeceğiz.

### SELECT KULLANIMI
Tablolardaki kayıtları getirmek için kullanacağımız **SELECT** komutları için kullanımımız şu şekildedir:


*SELECT ile tek bir sonuç döndürme*, SELECT sorgunuzun sonucunda tek bir satır dönecekse aşağıdaki gibi bir kullanımı örnek alabilirsiniz.
```
id = 5
cursor = mysql.connection.cursor()

sorgu = "SELECT * FROM kullanicilar WHERE id = %s"
kontrol = cursor.execute(sorgu,(id,))

if kontrol > 0:
    data = cursor.fetchone()
    isim = data["isim"]
    yas = data["yas"]
else:
    print("Kayıt bulunamadı!")
```

Bu komutta önemli olan kısımlardan birisi ```cursor.execute(sorgu,(id,))``` kısmında **idden** sonra **,** koymamızdır. Çünkü execute fonksiyonu sorgu komutundan sonra değişkenleri **tuple (demet)** değişkeniyle kabul eder. Tek elemanlı bir demetiniz varsa da değişkenden sonra virgül koymazsanız Python bunun bir demet olduğunu algılamaz. 
```if kontrol > 0 ```kontrolü ise kontrol değişkenine atadığımız  ```cursor.execute(sorgu,(id,))```  işleminin dönüş değerini kontrol eder. Eğer kayıt yoksa 0 değeri döneceği için bu bölüm ile tabloda aradığınız sorguya aşt değer dönüp dönmediğini anlayabilirsiniz.



*SELECT ile birden fazla sonuç döndürme*, SELECT sorgunuzun sonucunda birçok satır dönecekse aşağıdaki gibi bir kullanımı örnek alabilirsiniz. 
```
id = 5
cursor = mysql.connection.cursor()

sorgu = "SELECT * FROM kullanicilar"
kontrol = cursor.execute(sorgu)

if kontrol > 0:
    datas = cursor.fetchall()

    for data in datas:
        print("İsim: ",data[0])
        print("Yaş: ",data[1])
else:
    print("Kayıt bulunamadı!")
```
Farkettiğiniz üzere tek bir sonuç dönecek komutlarda **fetchone()** fonksiyonunu kullanırken birden fazla sonucun yani dizinin döneceği komutlarda **fetchall()** fonksiyonunu kullanıyoruz. İsterseniz bu dönen dizi direkt HTML sayfanıza ```return render_template("sonuc.html",veriler = datas)``` fonksiyonu ile göndererek değerleri orada da yazdırabilirsiniz. HTML sayfasına nasıl veri göndereceğnizi unuttuysanız [Flask HTML Sayfa Oluşturma ve HTML İçinde Python Kullanma](https://github.com/rumeysaustun/Flask/blob/main/4-%20Flask%20HTML%20Sayfa%20Olu%C5%9Fturma%20ve%20HTML%20%C4%B0%C3%A7inde%20Python%20Kullanma.md#flask-html-sayfa-olu%C5%9Fturma-ve-html-i%CC%87%C3%A7inde-python-kullanma), bölümünden bakabilirsiniz.

## UPDATE Kullanımı
Daha önceden eklediğimiz herhangi bir değerde güncelleme yapmak istediğimizde UPDATE komutunu kullanırız. Değiştirilecek verileri ayarladığınız bir sayfada aşağıdaki örnekte yer aldığı gibi **UPDATE** komutunu kullanabilirsiniz:

```
yeniIsim = "Yunus"
yeniYas = "35"
id = 5
cursor = mysql.connection.cursor()

sorgu = "UPDATE kullanicilar SET isim = %s, yas = %s WHERE id = %s"
kontrol = cursor.execute(sorgu,(yeniIsim,yeniYas,id))
mysql.connection.commit()
```

## INSERT Kullanımı
İlk başta gördüğümüz örneklerde de olduğu gibi buraya da kısa bir özet kod blogu koyalım:
```
isim = "Levent"
yas = 20

cursor = mysql.connection.cursor()
sorgu = "INSERT INTO kullanicilar VALUES(%s,%s,%s)"

cursor.execute(sorgu,(None,isim,yas))
mysql.connection.commit()
```
Burada demette yer alan **none** değişkeni tablomuzda yer alan id isimli **Auto Increment** özelliğine sahip sütunun boş değişkenidir.



## DELETE Kullanımı
Veritabanından bir satır silmek istediğinizde **DELETE** komutu ile bunu yapabilirsiniz. Bunun için aşağıdaki örnek kullanımı baz alarak kendi kodunuzu geliştirebilirsiniz:
```
id = 5
cursor = mysql.connection.cursor()

sorgu = "DELETE FROM kullanicilar WHERE id = %s"
kontrol = cursor.execute(sorgu,(id,))
mysql.connection.commit()
```



