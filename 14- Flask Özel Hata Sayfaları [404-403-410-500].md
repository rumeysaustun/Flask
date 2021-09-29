# Flask Özel Hata Sayfaları [404-403-410-500]

Flask sayfasında hata durumlarının sürekli kontrol edip ilgilil sayfaya yönlendirecek errorhandler işlevini aktifleştirme işlemimiz var. Bunun için app uygulamamızın **errorhandler** fonksiyonu ile dinlemek istediğimiz hata kodunu yönlendireceğimiz sayfaya iletecek kodu yazmalıyız. Aşağıda 404 hata kodu örnek bir kullanım görebiliriz.

```
@app.errorhandler(404)
def not_found(e):
  return render_template('404.html'), 404
```
Gerekli errorhandler’i yazdık ve 404 hatasının gerçekleştiği durumda templates klasörünün içindeki  **404.html** sayfasına gerekli yönlendirmeyi yapmış olduk. Son durumda proje dosyamız aşağıdaki gibi olacaktır.
```
from flask import Flask,render_template

app = Flask(__name__)

@app.errorhandler(404)
def not_found(e):
  return render_template('404.html'), 404

@app.route("/")
def anaSayfa():
    return "Merhaba Sayfa Ziyaretçisi"

if __name__ == "__main__":
    app.run(debug=True)
```
Artık ilgili sayfa bulunmadığında verilen 404 hatası meydana geldiğinde 404.html sayfası ekrana basılacaktır. Siz diğer hata kodları içinde özel sayfaları rahatça oluşturabilirsiniz. En çok karşılaşabileceğiniz hataları aşağıdaki özet bir tablo ile görebilirsiniz.




