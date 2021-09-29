##Flask ile İlk Uygulama

Birçok program kullanabilirsiniz ben aşamaları gösterirken Pycharm 2021.2.2 kullanacağım. İlk olarak aşağıdaki kodu yazarak Framework’u projeye dahil ediyoruz.

```
 from flask import Flask 
```
![kod1](https://user-images.githubusercontent.com/59111328/135089596-38019db6-738c-4167-a28c-690a1e32d5f6.PNG)<br>
**Şekil 1.6**

Ardından aşağıdaki kod ile uygulamayı oluşturuyoruz.
```
app = Flask(__name__)
```
![kod2](https://user-images.githubusercontent.com/59111328/135090894-f54b4893-f681-44df-a682-a79ca5e4e527.PNG)
<br>
**Şekil 1.7**

Aşağıdaki kod ile satırımızı kontrol ediyoruz.
```
if __name__ =="__main__":
```
![kod3](https://user-images.githubusercontent.com/59111328/135091231-79a406ab-97b5-430c-8109-45256ead0564.PNG)
<br>
**Şekil 1.8**

Son olarak web sitesinde alınan syntax vb. hataları almamak için 
```
app.run(debug=True)
```
yazıyoruz ardından uygulamayı çalıştırıyoruz. Ve uygulamanın son hali Şekil 1.9’da gösterildiği gibi oluyor.

![kod4](https://user-images.githubusercontent.com/59111328/135091538-c9fc80eb-7ffc-4424-af6a-40b0c41c17ff.PNG)
<br>
**Şekil 1.9**

Projeyi çalıştırdıktan sonra Şekil 1.10’daki gibi alt kısımda bulunan linke tıklayarak uygulamaya gidiyoruz.

![kod5](https://user-images.githubusercontent.com/59111328/135091712-8c13dfb0-dd7e-4d4c-9e87-8bf56078cba0.PNG)
<br>
**Şekil 1.10**

Linke tıkladıktan sonra Şekil 1.11’deki gibi bir görüntü alıyorsak uygulama sorunsuz çalışmış demektir. Not Found şeklinde hata almamızın sebebi flask frameworkda her requeste karşılık bir response geliyor ve biz burada http://127.0.0.1:5000/ şeklinde bir resquest çalıştırdık. Fakat bu isteğe yanıt olarak response vermedik bu yüzden **Not Found** hatası aldık.

![nıt found](https://user-images.githubusercontent.com/59111328/135259927-d9af5516-58b4-4918-afc8-cd94bf591296.PNG)
<br>**Şekil 1.11**

Bir resquet oluşturduk, şimdi sıra bu resqueste karşılık bir response oluşturmakta. Bunu da Python fonksiyonlar yardımıyla yapabiliriz. Uygulamaya 
```
@app.route("/")
```  
kodunu giriyoruz. Şekil 1.12’deki gibi görüntüye sahip oluyor. 
![kod6](https://user-images.githubusercontent.com/59111328/135092468-b2ffd4e8-8264-4661-905c-c6745d0e77e8.PNG)
<br>**Şekil 1.12**

Biz bir decoreter mantığı ile bir request yaptık. Ve bu request karşılık fonksiyon yardımı ile bir response değeri döndürdük. Burada önemli olan bir yer var. **@app.route("/")** ile request yaptıktan o requeste karşılık gelecek bir response değerini döndüren fonksiyonu yazmamız gerekiyor. Son kod olarak  
```
def index(): return "Merhaba Dünya"
```
kodunu giriyoruz. Ve Şekil 1.13’teki sayfa ortaya çıkıyor.

![kod7](https://user-images.githubusercontent.com/59111328/135092810-abe4d0dd-ad95-4ea0-b516-05c10756f9ae.PNG)
<br>**Şekil 1.13**

Tüm kodlarımızı doğru bir şekilde girdikten sonra uygulamayı çalıştırıyoruz ve Şekil 1.14’deki sekme açılıyor, görüldüğü üzere başarıyla çalışıyor.

![sayfa](https://user-images.githubusercontent.com/59111328/135260014-81fea969-7a2a-4aef-8a29-1eb61aff4df6.PNG)
<br>**Şekil 1.14**

Uygulama **localhost 5000** adresinde çalışıyor. İsteğe bağlı olarak değiştirebilirsiniz. Değiştirmek için 
```
app.run(debug=True)
```
kısmını
```
app.run(debug=True,port=2000)
```
olarak değiştirmeniz yeterli olacaktır. Uygulamanın son hali Şekil 1.15’te göründüğü gibi olacaktır.

![sayfa2](https://user-images.githubusercontent.com/59111328/135260063-aecad63e-c9d6-4bb1-9a0d-02ca4822bbd9.PNG)
<br>**Şekil 1.15**
