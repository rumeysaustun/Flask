# Kurulumlar

## Miniconda Kurulumu

- [Buradan](https://docs.conda.io/en/latest/miniconda.html#windows-installers) Miniconda'nın uygun versiyonu indirilir.
- İndirilen .exe uzantılı dosya açılır.
- Gelen ekranda **next** butonuna basılır.<br>
![next](https://user-images.githubusercontent.com/59111328/136394599-d7d4fd20-8633-48c0-9225-5a85670ab534.PNG)
- **I agree** butonuna basılır. <br>
![I agree](https://user-images.githubusercontent.com/59111328/136394741-8dbf531d-e21e-41b0-b981-04aee62fa097.PNG)
- **Just me** seçilip **Next** tuşuna basılır.<br>
![just me](https://user-images.githubusercontent.com/59111328/136394841-8e0d15f9-3ff8-4c19-af7c-90a743c2ef65.PNG)
- İndirilecek klasör seçilir ve **next** butonuna basılır.<br>
![kalsör](https://user-images.githubusercontent.com/59111328/136395003-9ec22eb7-3645-44a0-9346-9d66f9792724.PNG)
- **Install** tuşuna basarak inmesi beklenir.<br>
![install](https://user-images.githubusercontent.com/59111328/136395298-540a4040-9778-4466-b589-d032cd728bfe.PNG)
![yaparken](https://user-images.githubusercontent.com/59111328/136395540-9c4b2494-a47e-433c-ace2-cbe6a5492b56.PNG)
- İndirme bittikten sonra **Next** tuşuna basılır.<br>
![nxt](https://user-images.githubusercontent.com/59111328/136395702-3370f72d-ddb0-4f3c-a622-d48251910e67.PNG)
- Kurulum **finish** tuşuna basarak bitirilir.<br>
![finish](https://user-images.githubusercontent.com/59111328/136395855-b09809a7-711e-4bab-888e-eadaa9bf4530.PNG)
- **Anaconda Prompt (miniconda3)** açılır ve 
```
conda install -c conda-forge jupyterlab
```
komutu yazılır.<br>
![komut istemi](https://user-images.githubusercontent.com/59111328/136396190-be1dd2c8-7ccc-4738-afff-e78d90379416.PNG)
- Devam etmesi için **y** yazıp enter'a basıyoruz.<br>
![y](https://user-images.githubusercontent.com/59111328/136396461-3f51a8cc-992a-4cf3-8a84-d545c0485ace.PNG)
- Kurulum bittikten sonra 
```
jupyter-lab
``` 
yazarak çalıştırılır.<br>
![jpy](https://user-images.githubusercontent.com/59111328/136396687-3ed530b2-fbb4-4fbc-b15c-e6277159aa19.PNG)
- Çıkan sayfadan **Notebook** bölümünden **pyhon** seçilip kodlamaya başlanır.<br>
<img src="https://user-images.githubusercontent.com/59111328/136397399-33dfd632-f22e-43a6-a514-53e1df8e6961.PNG" width="500"><br>
![hello](https://user-images.githubusercontent.com/59111328/136398058-8e4a46b9-7683-4b6a-83b3-d487e98349ba.PNG)

## Flask Kurulumu

- İlk olarak **Anaconda Prompt (miniconda3)** komut ekranı açılır.
- Flask'ı indirmek için ekrana 
```
pip install Flask
```
komutu girilir.<br>

![flask indir](https://user-images.githubusercontent.com/59111328/136689349-a3beef94-85a7-459a-a9c5-c472bb34ea77.PNG)


- Deneme amacıyla 
```
python
>>> import flask
```
komutu girilir. Hata yok ise kurulum başarılıdır. ```exit()``` ile çıkış yapılabilir.

![python](https://user-images.githubusercontent.com/59111328/136689357-9a335818-a737-41e4-8202-580860332594.PNG)


- Geliştiricimizi açmak için
```
jupyter-lab
```
komutu girilir. 

![lab](https://user-images.githubusercontent.com/59111328/136689362-3802a37a-14db-47c2-8648-759a2c0731fe.PNG)


- Açılan geliştirme ortamında ilk FLask projemizi denemek amacıyla aşağıdaki kodlar yazılır ve çalıştırılır.

```
from flask import Flask

app = Flask(__name__)
@app.route('/')

def hello():

    return "Hello World!"
if __name__ == '__main__':

   app.run()
```
![run](https://user-images.githubusercontent.com/59111328/136689366-0df9adf6-d7fe-488c-9887-3c383a2e9c38.PNG)

- Alt kısımda çıkan **http://127.0.0.1:5000/** yönlendiriciye tıklanır.

![helloworld](https://user-images.githubusercontent.com/59111328/136689370-3fff9125-9d8f-41e5-a377-33d11fa85172.PNG)
