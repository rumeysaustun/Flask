# Flask Ajax Kullanımı ile Sayfa Yenilemeden Veri Gönderme & Alma

Python Flask ile Jquery Ajax yapılarını kullanarak sayfamızı yenilemeden istediğiniz sayfaya veri gönderip alabilirsiniz. Ajax kullanarak hızlı sayfalar elde ederken daha rahat bir iletişim kontrolüne de sahip olursunuz.

Route Yazma ve Kütüphaneleri Ekleme

İlk olarak kütüphaneleri ekliyoruz, from flask import Flask,render_template,request.




Ardından Flaskı tanımlayalım, app = Flask(__name__).

Şimdi ise templates klasöründe yer alacak proje sayfasının gösterileceği index route bölümünü yazalım. 

@app.route("/")
def anaSayfa():
    return render_template("index.html")


Ana sayfa tasarımın birazdan göstereceğim ama temelde bu sayfada bir sayı yazarak /hesapla adresine sahip olan sayfamıza göndereceğiz. /hesapla route kısmı ise aldığı sayının karesini hesaplayıp sonucu bize döndürecektir.

@app.route("/hesapla", methods=['POST','GET'])
def hesapla():
    if request.method == 'POST':
        sayi = request.form.get('sayi') 
        sonuc = int(sayi)**2
        return str(sonuc)
    else:
        return "Bu sayfayı görmek için yetkiniz yok!"



Yukarıda yazdığımız route ile aynı Form işlemlerinde yaptığımız örnekte olduğu gibi gelen sayi değişkenini yakaladık ve karesini alan matematik işlemini yaptıktasn sonra return ile geri döndürdük. Şimdi proje dosyasının üzerindeki son işlemimiz olan Flask’ı başlatarak buradaki işlemlerimizi tamamlayalım.


if __name__ == "__main__":
    app.run(debug=True)












Son durumda proje sayfamız şu şekilde görünüyor olacaktır

from flask import Flask,render_template,request 

app = Flask(__name__)

@app.route("/")
def anaSayfa():
    return render_template("index.html")


@app.route("/hesapla", methods=['POST','GET'])
def hesapla():
    if request.method == 'POST':
        sayi = request.form.get('sayi') 
        sonuc = int(sayi)**2
        return str(sonuc)
    else:
        return "Bu sayfayı görmek için yetkiniz yok!"


if __name__ == "__main__":
    app.run(debug=True

Ajax Sayfasının Oluşturulması ve Ajax İşlemleri

Yukarıdaki temel işlemleri yaptıktan sonra ana sayfamızı yönlendirdiğimiz proje sayfasını tasarlayacağız. Basit birkaç eleman ile kullanıcıdan alacağımız sayıyı tekrar aynı sayfada ekrana basmamız gerekiyor. Bunun için Jquery kütüphanesini eklemeyi unutmamak lazım. Ardından Ajax fonksiyonumuzu yazarak işlemlerimizi tamamlayabiliriz.

Ajax kütüphanesinin eklenmesi için aşağıdaki kodu kullanabilirsiniz.

<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>








Bu ekleme işleminin ardından ise gonder idli bastığımızda çalışacak Ajax komutları şu şekilde olacaktır. 

$.ajax( {
        url: '/hesapla',
        type: 'POST',
        data: {
                sayi: $('#sayi').val()
        },
        success: function ( donen_veri ) {
                $('#sonuc').html(donen_veri)
        },
        error: function ( donen_veri ) {
                $('#sonuc').html(donen_veri)
        }
} );

Burada url veriyi göndereceğimiz sayfa type işlemin tipi, data göndereceğimiz verileri ve bu verilerin değişkeni isimleri, succes başarılı işlem sonrası çalışacak komutlar, error  hatalı işlem sonrası çalışacak komutlardır.
























Proje sayfamızın son hali şu şekilde olacaktır:,

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Flask Ajax Örneği</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

    <input type="number" id="sayi" placeholder="Sayı Giriniz"> 
    <input type="submit" id="gonder" value="Gönder"> <br><br>

    Sayının karesi: <strong id="sonuc">-</strong>


<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script type=text/javascript>

    $(function() {
        $('#gonder').bind('click', function() {

            $.ajax( {
                url: '/hesapla',
                type: 'POST',
                data: {
                    sayi: $('#sayi').val()
                },
                success: function ( donen_veri ) {
                    $('#sonuc').html(donen_veri)
                },
                error: function ( donen_veri ) {
                    $('#sonuc').html(donen_veri)
                }
            } );

        });
    });

</script>
</body>
</html>





input ile aldığımız sayıyı Ajax ile gönderip /hesapla route bölümünden dönen veriyi succes  ile ilgili HTML sonuc idsine yazdırdığımız örneğimiz sonucu ekran görüntüsü şu şekilde olacaktır. 






