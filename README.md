# CoronaBuster

## Amaç ve Gerekçe

CoronaBuster Projesinin amacı, bir virüs salgınında temas izlemesi (contact tracing) yapmayı kolaylaştırmaktır. Temas izlemesi, hasta olduğu belli olan bir kişinin kimlerle fiziksel olarak temasta bulunduğunu tespit etmek anlamına gelir. 

Temas izlemesi, salgınların yayılma hızını ciddi ölçüde azaltan halk sağlığı uygulamalarının başında gelir; çünkü temas izlemesi yoluyla, hastalık taşıma şüphesi bulunan insanlar, semptomlar ortaya çıkmadan ve hastaneye ulaşmadan, ortaya çıkarılabilir. 

Mevcut koşullarda, bu uygulama DSÖ (Dünya Sağlık Örgütü) ve dünya devletlerinin ilgili sağlık kurumları tarafından büyük ölçüde manuel süreçlerle yürütülüyor. Bu yüzden, ancak salgının başlangıç aşamasında uygulanabiliyor. Hastalık, binlerce insana bulaştıktan sonra, kaynak yetersizliğinden dolayı temas izlemesinin yapılma ihtimali kalmıyor. Bu durumda, Covid-19 salgınında olduğu gibi, halk sağlığı kurumlarının elinde salgını durdurmak için, tek araç olarak hastalığın yoğun olduğu merkezleri (epicenter) kapatmak (lockdown) kalıyor. Ne var ki, bu çözüm ancak kısa süreli uygulanabilecek bir çözüm. Eğer salgın 4-6 hafta içinde, kapatma sonucunda yok edilemezse, bu durumda ekonominin ve tedarik süreçlerinin aksamaması için, kapatmayı kaldırmak gerekiyor. Bu ise, doğal olarak, salgının ömrünün uzamasına ve hem ekonomi hem de halk sağlığı üzerinde bedelin katlanarak artmasına neden oluyor. 

Bizim önerdiğimiz proje, temas izlemesi yapmayı hem son derece düşük maliyetli ve otomatik bir hale getiriyor, hem de bunu yaparken insanların kişisel mahremiyet haklarını koruyor. Bunun için önerdiğimiz çözüm, cep telefonlarının bluetooth sinyallerini kullanmaya dayanıyor. 

## Faydalar

Corona salgınından dolayı milyonlarca insan çalışamıyor. Temas izleme otomasyonu sayesinde, potansiyel hastaların tespiti son derece kolay ve neredeyse sıfır maliyetli bir hale gelecek. Bu sayede, hasta olsun olmasın herkesin eve kapanması zorunluluğu hafifleyecek. Sadece hasta olanlar ve potansiyel hastalık şüphesi taşıyanları tecrit edilmesi ve test edilmesiyle, salgın kontrol altına alınabilecek.

BLE ile virus pozitif kullanıcılar ile kontak suresi ve mesafe hesaplayarak kullanıcılar için risk scoru hesaplama yolu ile:
- Birey hedefli karantina
- Maske dağıtımı
- Covid-19 labratuar testi  
gibi uygulamaların optimizasyonu hedeflenmekte.

## Çözümün Özet Tarifi

Şu an, neredeyse herkesin üzerinde bluetooth destekli bir akıllı telefon bulunuyor. Telefonların yaydığı bluetooth sinyalinin yaklaşık 10 metrelik bir menzili bulunuyor. Telefonlara yükleyeceğimiz bir yazılım modülüyle, her bir kişinin yakın çevresindeki insanların şifrelenmiş güvenli kaydını tutacağız. Daha sonra, bir kişinin hasta olduğu bilgisi bize ulaştığında, bu kişiyle yakın temasta bulunmuş diğer insanları tespit edeceğiz ve bu insanlara uyarı mesajı göndereceğiz.

Bütün bu işlemleri yaparken, hem Türkiye'nin KVKK (Kişisel Verileri Koruma Kurumu) mevzuatıyla, hem de AB'nin GDPR (General Data Protection Regulation) mevzuatıyla uyumlu bir şekilde, insanların kişisel bilgilerinin mahremiyetini koruyacak bir çözüm tasarlıyoruz. 

Bilgi mahremiyetini korumak için sistem tasarımımızda şu iki kritik kısıt bulunuyor:

- Temasların tespit edilmesi için gerekli olan minimum seviyede bilgi sunucu tarafına gönderilecek.
- Telefonların birbirlerine gönderecekleri mesajlarda (beacon mesajı), gönderen telefonun kimliğini ortaya çıkaracak veri bulunmayacak.

## Nasıl Çalışır?

### Tüm Süreç

Önkoşul: 

- Mobil istemci telefona yüklenmiş ve gerekli izinler verilmiş olmalı.

#### Normal Akış (Normal Flow)

1. Telefon

## Gereksinimler

### Fonksiyonel Olmayan Gereksinimler

NFR001: Telefonun piline eklenecek ekstra yük, %1'i geçmeyecek.

NFR002: Telefonun hafızasına günlük en fazla 5 MB veri yazılacak.

NFR003: Sunucu tarafında en fazla 6 haftalık veri saklanacak. 

Kişisel bilgilerin mahremiyetini korumak için, olabildiğince az veri tutmamız gerekiyor.

Eski verinin üzerine kademeli (incremental) bir şekilde yeni veriyi yazacağız (overwrite).

NFR004: Telefonun lokasyon, bluetooth servislerini kullanma izini alınacak.

SDK'nın gömüldüğü host uygulamanın bu izinleri kullanıcıdan alması gerekiyor. Partner firmaların  uygulamaları, bu izinleri zaten kendi işleyişleri için muhtemelen almış olacaktır. 

NFR005: Partner uygulamalar

## Teknik Çözüm

### Mobil İstemci

Mobil istemciyi, bir SDK modülü olarak dağıtacağız, esas olarak. Bu SDK, hali hazırda insanların yaygın bir şekilde kullandığı, teslimat (getir, banabi, yemeksepeti gibi), bankacılık (İşBankası, Enpara gibi) gibi uygulamaların (host uygulama) içine gömülecek.

Mobil istemciyi hazırladıktan sonra, popüler uygulama üreticileriyle bağlantıya geçeceğiz. Bunların arasından hızlı bir şekilde öncü partner olmak isteyen partnerleri seçeceğiz. İlk etapta, SDK'yı bu partnerlerin uygulamalarına ekleyeceğiz. Uygulama canlı ortamda bir süre test edildikten sonra, geniş yayılım için, yeni partnerlerle bağlantı kurup uygulamanın yayılımını olabildiğince artırmaya çalışacağız.

Daha fazla teknik dökğmantasyon için: https://github.com/CoronaBuster/docs

## 



### Nasıl yardım edebilirim?
Aşağıdaki niteliklere sahipseniz bizim ile iletişime gecebilirsiniz. 

İletişim için "Kimler yardım etmek istiyor?" başlıklı issue'ya comment bırakabilirsiniz https://github.com/CoronaBuster/CoronaBuster/issues/1 


#### Eksikler
- Lead Frontend developer 
  - Admin paneli ve landing page den sorumlu olacak, ve koordinasyonu sağlayacak
  - 2 projede de react kullanmaya karar verdik (populerlik yüzünden). react deneyimi gerekli
  - Proje ile ilgili pull requestlerin codereview'inden sorumlu olacak, ve gerekli dönüşü sağlayacak
  - Gerektiğinde todoları kendisi kodlayacak
  - İş dağılımını yapabilecek
- Backend Developer
  - Akka, Java, Scala, JSON, AkkaHttp konularında deneyimli developer
  - Code review ve geri dönüş yapabilmeli pull requestler için
  - Parquet dosya formatı ile ve big data projelerinde daha önce çalışmak büyük bir artı olur
- Android UI Lead
  - Android app ve UI'larının tasarımından sorumlu olacak
  - Code review ve geri dönüş yapabilmeli pull requestler için
- IOS UI Lead
  - Android app ve UI'larının tasarımından sorumlu olacak
  - Code review ve geri dönüş yapabilmeli pull requestler için
- Android SDK Lead
  - Bluetooth Low Energy ile kontak tracing yapıyoruz
  - Background servis kullanılarak, periodik olarak BLE advertisment paketi yayınlıyoruz
  - Ve diğer telefonlardan yayınlanan BLE paketlerini scan ediyoruz
- IOS SDK Lead
  - Bluetooth Low Energy ile kontak tracing yapıyoruz
  - Background servis kullanılarak, periodik olarak BLE advertisment paketi yayınlıyoruz
  - Ve diğer telefonlardan yayınlanan BLE paketlerini scan ediyoruz
- Hukuk ve Mahremiyet, KVKK konularında uzman avukat
  - KVKK uyumlu terms and privacy statementların yazılması
- Privacy & Security lead
  - Gereğinden daha fazla data toplanmaması ve kullanıcı mahremiyetinin ihlal edilmeğinden sorumlu olacak
  - Potensiyel mahremiyet problemlerinin raporu hazırlayacak ve yapabiliyorsa çözüm sunacak
- Art director
  - Mobile application, Admin paneli, landing page, proje görselleri, tanıtım broşurleri vb. grafiksel içeriklerin
  - Hazırlanması, kordinasyonu ve iş dağılımı
- Eğer Türkiyede populer bir mobil application'ın yöneticisi iseniz
  - Bu yaptığımız yazılımın hızlı bir şekilde Türkiye genelinde yayılması için populer app'ler entegre etmek en iyi çözüm.
  - Size vereceğim SDK ile kendi uygulamanıza CoronaBuster'ı entegre edebilirsiniz.
- Devops sorrumlusu
  - CI/CD
  - AWS autoscale, ec2, network loadbalancer
  - Jenkins
  - Docker
  - Sistem ve data güvenliği
  - gibi konulara hakim devops uzmanı
  - Proje çıktılarının deploy edilmesi ve sistemin sağlıklı bir şekilde çalışması için gerekenlerden sorumlu olacak
- Siz?
  - Bu konulardışında nasıl yardım edebilirsiniz siz söyleyin?
  - Örneğin bu dökümantasyonda gördüğünüz hataları yada eksikleri düzeltebilirsiniz
  - Yada aklınızda başka bir şeey varsa o da olur
  - Zaman karşı yarıştığımızı unutmayalım her türlü yardım önemli


### Projeler / repolar
- https://github.com/CoronaBuster/CoronaBuster - Project general inforrmation
- https://github.com/CoronaBuster/api - Backend API
- https://github.com/CoronaBuster/android-app - Android App
- https://github.com/CoronaBuster/android-sdk - Android SDK
- https://github.com/CoronaBuster/ios-app - iOS APP
- https://github.com/CoronaBuster/ios-sdk - iOS SDK
- https://github.com/CoronaBuster/admin-dashboard - Admin site, SPA
- https://github.com/CoronaBuster/docs - Design and documentation
- https://github.com/CoronaBuster/www - Landing page

### Bütün repoları clonelamak için:
```bash
mkdir coronabuster
cd coronabuster
git clone git@github.com:CoronaBuster/api.git
git clone git@github.com:CoronaBuster/android-app.git
git clone git@github.com:CoronaBuster/android-sdk.git
git clone git@github.com:CoronaBuster/ios-app.git
git clone git@github.com:CoronaBuster/ios-sdk.git
git clone git@github.com:CoronaBuster/CoronaBuster.git
git clone git@github.com:CoronaBuster/admin-dashboard.git
git clone git@github.com:CoronaBuster/docs.git
git clone git@github.com:CoronaBuster/www.git
```
