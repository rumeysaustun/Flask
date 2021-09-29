# Flask ile Session ve Cookies Kullanımı

## Cookkies Nedir?

Cookies veya diğer bilinen adıyla çerezler; kullanıcı bilgileri, oturum bilgileri gibi istenilen verilerin ziyaret eden kullanıcının tarayıcısında depolandığı bilgilerdir. Örnek olarak sitenizi ziyaret eden kullanıcıların ad, soyad, kullanıcı adı, sepetteki ürünleri gibi bilgilerini çerezler aracılığıyla ilgili kişinin tarayıcısında depolayabilir, aynı kullanıcının diğer ziyaretlerinde bu bilgileri kullanabilirsiniz. 

## Flask ile Cookies Kullanımı

Cookies ile tutacağınız veriler dictionary yapısıyla oluşturulur ve sayfalarınıza make_response() fonksiyonuyla gönderilirler. Tabi ilk olarak make_response kütüphanesini dahil etmeyi unutmayınız.

## Çerezleri Depolama

```
from flask import make_response
@app.route('/')
def index():
    resp = make_response(render_template('anasayfa.html'))
    resp.set_cookie('ad', 'Levent')
        resp.set_cookie('soyad', 'Kalkavan')
    return resp
```
Örnekte göreceğiniz üzere ayarladığınız çerez bilgileri make_response fonksiyonu ile istediğiniz sayfaya iletilmek için tutulur ve çevirme işlemleri yapılır. Peki bu tuttuğunuz verileri nasıl okunur?

## Çerezleri Okuma
```
from flask import request

@app.route('/')
def index():
    ziyaretciadi = request.cookies.get('ad')
```

Burada ise depoladığınız çerezleri okuyabilmek için request kütüphanesini dahil ediyoruz ve okumak istediğimiz sayfanın route kısmında cookies.get ile tuttuğumuz verileri alıyoruz. Artık aldığınız bu verileri sayfanıza daha önceki derste öğrendiğimiz yöntemlerle gönderebilir ve kullanabilirsiniz.

```request.cookies.get(key)``` yapısı yerine ```cookies[key]``` ile de çerezlerinizi okuyabilirsiniz ama eğer bu key değişkende çerez oluşturulmamışsa KeyError if the cookie is missing. şeklinde hata alırsınız. Bu nedenle request.cookies.get(key) yapısını kullanmanız daha kullanışlıdır.

## Session Nedir?

Çerezlerle fonksiyonel olarak aynı işleve sahip olan Session veya diğer adıyla oturum, çerezlerin aksine tarayıcı yerine sunucuda depolanırlar ve depolanan verilerin geçerlilik süreleri mevcuttur. Bir session oluşturduğunuzda oluşturduğunuz veri sunucudaki tmp klasörü gibi bir alanda depolanır (bu konum özelleştirilebilir) ve depolanan bu içeriğe özel bir id verilir. Böylece oluşturduğunuz sessiona tekrar ulaşmak istediğinizde bu id ile sunucuya gider ve o id nin işaret ettiği veriyi alırsınız.

## Flask İle Session Kullanımı?

Flask ile session kullanabilmek için öncelikle saklamak istediğiniz verileri kriptografi kullanarak şifrelemelisiniz. Bunun sebebi, çerezlerin üstünde tutulan session verilerinin başkaları tarafından değiştirilmesini engellemektir. Ne de olsa sunucuda sakladığınız veriler başkaları tarafından erişilebilir konumdadırlar. Öyleyse ilk olarak gerekli kütüphanelerim dahil edelim ve kendimize secret key oluşturalım. Unutmayın secret key rastgele bytelardan oluşmaktadır.

```
from flask import Flask, session, redirect, url_for, escape, request
app = Flask(__name__)
app.secret_key = b'_5#y2L"F4Q8z\n\xec]/'
```

Ardından bir route içerisinde istediğimiz sessionları oluşturalım. Aşağıdaki örnekte form üzerinden gelen verilerini sessiona atayacağız:

```
@app.route('/giris', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        session['ad'] = request.form['ad']
                session['soyad'] = request.form['soyad']
        return redirect(url_for('anasayfa'))
```

Gördüğünüz üzere ```session['ad'] = "Levent"``` yapısı ile session oluşturabiliyoruz. Peki bu oluşan sessionu nasıl okuyabiliriz?

```
@app.route('/')
def index():
    if 'ad' in session:
        return 'Merhaba %s' % escape(session['ad'])
    return 'Giriş yapmadınız!'
```
if ile kontrol edebilmemizin dışında direkt ```session['ad']``` yapısını bir değişkene atayarak da kullanabilirsiniz. Son olarak oluşturduğunuz bir sessionu silmek için session.pop() fonskiyonunu kullanabilirsiniz:

```
@app.route('/cikisyap')
def logout():
    session.pop('ad', None)
    return redirect(url_for('index'))
```


