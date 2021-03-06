# Flask ile İlk Uygulama

Birçok program kullanabilir, ben aşamaları gösterirken **Miniconda3** kullanacağım. İlk olarak aşağıdaki kodu yazarak Framework’u projeye dahil ediyoruz.

```
 from flask import Flask 
```

![1](https://user-images.githubusercontent.com/59111328/136690294-bffd9f67-5c17-41d9-b789-0a20cf10a6c8.PNG)
<br>
**Şekil 1.6**

Ardından aşağıdaki kod ile uygulamayı oluşturuyoruz.
```
app = Flask(__name__)
```
![2](https://user-images.githubusercontent.com/59111328/136690316-0d2e017f-7c27-4ade-a4e3-f0e34f1e2195.PNG)
<br>
**Şekil 1.7**

Aşağıdaki kod ile satırımızı kontrol ediyoruz.
```
if __name__ =="__main__":
```
![3](https://user-images.githubusercontent.com/59111328/136690344-fde86d2a-0af2-4f42-bcf1-06d1c5071ec9.PNG)
<br>
**Şekil 1.8**

Son olarak 
```
app.run()
```
yazıyoruz ardından uygulamayı çalıştırıyoruz. Ve uygulamanın son hali Şekil 1.9’da gösterildiği gibi oluyor.

![3](https://user-images.githubusercontent.com/59111328/136690860-60ce145f-b87a-46f4-9aa9-679f2e164f72.PNG)
<br>
**Şekil 1.9**

Projeyi çalıştırdıktan sonra Şekil 1.10’daki gibi alt kısımda bulunan linke tıklayarak uygulamaya gidiyoruz.

![3](https://user-images.githubusercontent.com/59111328/136690880-c8cde8db-a35e-4eef-bfa4-d4d341d15220.PNG)
<br>
**Şekil 1.10**

Linke tıkladıktan sonra Şekil 1.11’deki gibi bir görüntü alıyorsak uygulama sorunsuz çalışmış demektir. Not Found şeklinde hata almamızın sebebi flask frameworkda her requeste karşılık bir response geliyor ve biz burada http://127.0.0.1:5000/ şeklinde bir resquest çalıştırdık. Fakat bu isteğe yanıt olarak response vermedik bu yüzden **Not Found** hatası aldık.

![nıt found](https://user-images.githubusercontent.com/59111328/135259927-d9af5516-58b4-4918-afc8-cd94bf591296.PNG)
<br>**Şekil 1.11**

Bir resquet oluşturduk, şimdi sıra bu resqueste karşılık bir response oluşturmakta. Bunu da Python fonksiyonlar yardımıyla yapabiliriz. Uygulamaya 
```
@app.route("/")
```  
kodunu giriyoruz. Şekil 1.12’deki gibi görüntüye sahip oluyor. <br>
![4](https://user-images.githubusercontent.com/59111328/136690924-7de7623f-8845-4462-bd78-de33e34835f4.PNG)
<br>**Şekil 1.12**

Biz bir decoreter mantığı ile bir request yaptık. Ve bu request karşılık fonksiyon yardımı ile bir response değeri döndürdük. Burada önemli olan bir yer var. **@app.route("/")** ile request yaptıktan o requeste karşılık gelecek bir response değerini döndüren fonksiyonu yazmamız gerekiyor. Son kod olarak  
```
def index(): 
    return "Merhaba Dünya"
```
kodunu giriyoruz. Ve Şekil 1.13’teki sayfa ortaya çıkıyor.

![5](https://user-images.githubusercontent.com/59111328/136690957-0600bf93-3b83-44c8-a084-96b6863485c2.PNG)
<br>**Şekil 1.13**

Tüm kodlarımızı doğru bir şekilde girdikten sonra uygulamayı çalıştırıyoruz ve Şekil 1.14’deki sekme açılıyor, görüldüğü üzere başarıyla çalışıyor.

![sayfa](https://user-images.githubusercontent.com/59111328/135260014-81fea969-7a2a-4aef-8a29-1eb61aff4df6.PNG)
<br>**Şekil 1.14**

Uygulama **localhost 5000** adresinde çalışıyor. İsteğe bağlı olarak değiştirebilirsiniz. Değiştirmek için 
```
app.run()
```
kısmını
```
app.run(port=2000)
```
olarak değiştirmeniz yeterli olacaktır. Uygulamanın son hali Şekil 1.15’te göründüğü gibi olacaktır.

![sayfa2](https://user-images.githubusercontent.com/59111328/135260063-aecad63e-c9d6-4bb1-9a0d-02ca4822bbd9.PNG)
<br>**Şekil 1.15**
