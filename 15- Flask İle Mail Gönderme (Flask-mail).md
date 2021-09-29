# Flask İle Mail Gönderme (Flask-mail)

İlk olarak pip install Flask-Mail komutuyla kütüphaneyi yüklüyoruz. Kütüphaneyi yükledikten sonra from flask_mail import Mail, Message komutu ile projeye dahil ediyoruz.

Konfigürasyon Tanımlarını Ayarlama 
Kütüphaneyi projeye dahil ettikten sonra mail sunucu ayarlarını tanımlayabilmek için gerekli konfigürasyon bilgilerini yazmaya sıra geldi. Kullandığınız mail sunucuya ait bağlantı bilgilerini kullanarak aşağıdaki kodları kendi projenizde düzenleyebilirsiniz. Bu bilgileri nereden bulacağı bilmeyenler için aşağıdaki örneği Gmail üzerinden göstereceğim. Böylece Gmail bilgilerinizi girerek hemen kullanmaya başlayabilirsiniz. Fakat Gmail yerine mail kutusu kullananlar, mail sunucularının STMP ayarlarını girerek kullanabilirler.

from flask import Flask
from flask_mail import Mail, Message

app = Flask(__name__)

app.config['MAIL_SERVER']='smtp.gmail.com'
app.config['MAIL_PORT'] = 465
app.config['MAIL_USERNAME'] = 'xxxx@gmail.com'
app.config['MAIL_PASSWORD'] = '******'
app.config['MAIL_USE_TLS'] = False
app.config['MAIL_USE_SSL'] = True

mail = Mail(app)

NOT: Gmail ile gönderim yapmak istiyorsanız yukarıdaki ayarlara ek olarak Gmail hesabınızdan daha az güvenli uygulamalara erişime izin vermeniz gerekir.

Mail Gönderme Fonksiyonunun Yazılması
Gerekli ayarları yaptıktan sonra artık ilk çalışmamızı gerçekleştirebiliriz. Bunun için hemen bir route yazıp küçük bir mail gönderimi yapalım.

@app.route('/mail-gonder/')
def mailgonder():
    try:
        msg = Message("Merhaba Kerteriz Blog Takipçisi!",
          sender="gonderici@gmail.com",
          recipients=["alici@email.com"])
        msg.body = "Merhaba!\nPython ve Flask ile programlama nasıl gidiyor?"           
        mail.send(msg)
        return 'Mail başarıyla gönderildi!'
    except Exception, e:
        return(str(e))

HTML Mail İçeriği:  Eğer mesajınızda HTML ögeleri yer alacaksa msg.body yerine msg.html kullanabilirsiniz. Örn:

msg.html = "<strong>Merhaba!</strong><br><em>Python ve Flask ile programlama nasıl gidiyor?<em>"

Toplu Mail Gönderimi: Yukarıdaki örnekte sadece bir alıcı belirttik. Siz daha fazla mail adresine aynı anda toplu mail göndermek istiyorsanız aşağıdaki gibi kod yapsını kullanabilirsiniz.

liste = ["xx@mail.com","yy@mail.com","zz@mail.com"]

with mail.connect() as conn:
    for mail in liste:
        mesaj = '...'
        baslik = "Merhaba!" 
        msg = Message(recipients=[mail],
                      body=mesaj,
                      subject=baslik)

        conn.send(msg)

Mail Eki Yükleme: Göndereceğiniz maillere isterseniz dosya da ekleyebilirsiniz. Böylece eklerle beraber daha zengin bir mail gönderimi yapabilirsiniz. Bunun için öncelikle Konfigürasyon kısmında MAIL_ASCII_ATTACHMENTS ayarını True’ya ayarlayabilirsiniz.  

with app.open_resource("resim.png") as fp:
    msg.attach("resim.png", "image/png", fp.read())

Kod Önizlemesi
Son durumda proje dosyamız şu şekilde olacaktır:

from flask import Flask
from flask_mail import Mail, Message

app = Flask(__name__)

app.config['MAIL_SERVER']='smtp.gmail.com'
app.config['MAIL_PORT'] = 465
app.config['MAIL_USERNAME'] = 'xxxx@gmail.com'
app.config['MAIL_PASSWORD'] = '******'
app.config['MAIL_USE_TLS'] = False
app.config['MAIL_USE_SSL'] = True

mail = Mail(app)

@app.route('/mail-gonder/')
def mailgonder():
    try:
        msg = Message("Merhaba Sayfa Takipçisi!",
          sender="gonderici@gmail.com",
          recipients=["alici@email.com"])
        msg.body = "Merhaba!\nGünün Nasıl Geçiyor?"           
        mail.send(msg)
        return 'Mail başarıyla gönderildi!'
    except Exception as e:
        return(str(e)) 

if __name__ == '__main__':
   app.run(debug = True)



Artık /mail-gonder/ sayfasına gidip maili görebilirsiniz.






