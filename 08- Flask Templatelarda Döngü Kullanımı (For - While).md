# Flask Templatelarda Döngü Kullanımı (For - While)

## FOR Döngüsünü HTML Sayfada Kullanma

Bir HTML sayfasında elemanları For döngüsüne sokmak istediğimizde kullanacağımız blok yapısı şu şekilde olacaktır:

```
{% for item in dizi %}
   {{ item }}
{% endfor %}
```

Yukarıdaki kullanım şekli bir diziyi for döngüsüne sokarken kullanırken bir de en klasik kullanım tarzımız olan döngü sayısını belirlediğimiz for döngü yapısını gösterelim:

```
{% for item in range(sayi) %}
   {{ item }}
{% endfor %}
```
Her şeyden önce gerekli **route**’u yazalım ve **donguler.html** isimli sayfayı oluşturalım. Route yazma işini hatırlamayanlar hızlıca bu konudaki diğer yazılarıma bakabilirler.
Ardından dosyamıza şu alanı ekleyelim ve hazır eklerken alışveriş listesi isminde bir dizi oluşturup html sayfamıza değişken olarak gönderelim.

```
@app.route('/donguler')
def donguler():
  listeler = ["Ekmek","Domates","Islak Mendil","Su"]
   return render_template("donguler.html", listeler=listeler)
```

Şimdi de **donguler.html** sayfamıza for blok yapısını ekleyerek kullanalım

```
<ul>
{% for liste in listeler %}
    <li>{{ liste }}</li>
{% endfor %}
</ul>
```

Şimdi örneğimizin çıktısını görelim:

![donguler](https://user-images.githubusercontent.com/59111328/135282652-dc039e4c-68cd-4187-8504-35854ba1a241.PNG)

For döngümüzle HTML sayfasına dizi elemanlarını yazdırdık. Şimdi ise aynı örneği dizi kullanmadan sadece sayılarla yapalım:

```
<ul>
{% for sayi in range(12) %}

    <li>{{ sayi }}</li>

{% endfor %}
</ul>
```

Şimdi ekran çıktısını kontrol edelim:

![donguler2](https://user-images.githubusercontent.com/59111328/135282852-29251040-a45b-4262-9cc2-82f25bb923a8.PNG)

## WHILE Döngüsünü HTML Sayfada Kullanma

Bu döngüyü direkt while söz dağarcığı ile kullanamayacağız. Bunun yerine while benzeri bir döngüyü nasıl oluşturacağımızı göstereceğim. Öyleyse kullanım tarzımız olan if ile hemen başlayalım:
```
{% if True %}
        // bu alanı istediğiniz gibi kullanabilirsiniz
{% endif %}
```

Bu komut bloku ile döngümüz sonsuza kadar dönecektir. Siz değeri False yapana kadar da dönmeye devam edecek. Bu kullanım tarzını istediğiniz gibi değiştirebilir ve kontrol alanları ekleyebilirsiniz:

```
{% if sayi>1 %}
        // bu alanı istediğiniz gibi kullanabilirsiniz
{% endif %}
```

Burada olduğu gibi sayı değişkeniniz 1’den büyük olduğu sürece döngünüz while gibi davranacaktır. Siz sonsuz döngüye girmesini engellemek için sayı değerini yeri gelince 1’den küçük yapmalısınız.
