---
title: Kriptoparalar ve Blockchain Algoritması
date: 2021-03-25
description: 
category: Kitap
permalink: kriptoparalar-ve-blockchain
tags: [Kriptopara, Blockchain, Kriptografi]
---

Kriptopara kullanmak için pek fazla detay bilmeye gerek yok. Yine de bu yeni teknolojinin temellerini bilmek önemli. Bir yazıyla bu teknolojinin tüm detaylarını kavramıyor olsam da iyi bir tanışma yapabileceğimi düşündüm. Bu yazıda Blockchain'in işleyişine basit bir açıklama getirirken, etrafında dolaşan delilik halini bir yana bırakıp bu yeni ve devrimsel teknolojiyi anlamaya çalışacağız.

<div class="row" style="margin-bottom: 2.5rem; margin-top: 2.5rem;">
   <div class="ten columns"><img class="u-max-full-width" src="https://derinmavi.io/images/a2ls9-xmgav.png" alt="Kriptopara Bitcoin"></div>
   <div class="two column"></div>
</div>

Dünya Blockchain'i 2008 yılında Satoshi Nakomoto ismiyle yayınlanan makale ile tanıdı. Nakomoto bir manada anonim kalsa da açık kaynaklı, merkezi olmayan ilk dijital para birimi bitcoin bu şekilde doğdu. (Orjinal bitcoin makalesine)[https://bitcoin.org/bitcoin.pdf] internet üzerinden ulaşmak mümkün.

Son yıllarda Bitcoin'in değerindeki büyük artış ile beraber kriptoparalar ilgi çeken bir konu haline geldi. İlgi sahibi insanların hepsi yeterince bilinçli değil. Sonuç olarak bu durumu istismar eden pek çok kişi de türedi. Konuyla ilgili materyal çok ama hepsi aynı kalitede değil. Biz daha çok işleyişi anlamaya 3Blue1Brown kanalınınki gibi videolar fayda sağlayacaktır. Bu kanalın videosu aslında büyük ölçüde bir blog yazısından alınmış. Her ikisine de bu yazının kaynaklar bölümünden ulaşabilirsiniz. 

Coinleri üretmek için kullanılan yazılım *açık kaynaklı* olduğuna dikkat edelim. Bu isteyen herkesin kriptopara üretebileceği anlamına geliyor. Bu coinlerin hepsine güvenmek pek doğru değil. Bugün binlerce altcoin var ve bu kriptoparalar dizayn tercihleri anlamında farklılaşabiliyorlar. 

###  Blok Zinciri Nasıl Çalışıyor?

Bir arkadaş grubu olarak aramızda birbirimize borçlarımızı yazdığımız bir defter (ledger) var diyelim. Bu defter de dijital bir dosya da olabilir google drive gibi bir yerde tutuyoruz. Bu defter hepimiz tarafından erişilebilir ve içerisinde kimin kime ne kadar ödediği yazıyor.

```
Muhasebe Defteri:
-------------------
Ahmet Mehmet'e 20 lira öder.
Ayşe Ahmet'e 40 lira öder.
Mehmet Ali'ye 30 lira öder.
Ali Mehmet'e 10 lira öder.
```
Şimdi hepimiz dosyaya ulaşabiliyoruz ve aramızdan isteyen herkes listeye yeni kayıt ekleyebilir. Her ayın sonunda dosyaya bakıyoruz. Listeye bakıp paraları geçiyoruz. Eğer eksideysen borcunu kasaya koyuyorsun. Artıdaysan parayı kasadan alıyorsun. O zaman protokolümüz de şu oldu.

```
Protokol:
İsteyen herkes deftere satır ekleyebilir.
Her ayın sonunda gerçek parayla değişim yapılır.
```

Burada problem şu. Dosya herkese açık olduğundan Ali gidip Ahmet bana 100 lira verecek yazabilir. O zaman bir şekilde Ahmet'in Ali'ye ödeme yaptığı bu işlemi onayladığından emin olmamız lazım.

İşte burada kriptografiye işin içerisine giriyor. Dijital imzalar. Ahmet bir satırı bir kalemle imzalasa aşağıdaki <ahmet_imza> yazan yeri imzalamış olur. Bu imzadan biz ahmet in bu işlemi gördüğünü ve onayladığını anlamış oluruz.

```
Ahmet Mehmet'e 20 lira öder. <ahmetin_imzası>
```
Fakat dijital ortama geçtiğimizde bunun yerine Ahmet'e bir kod verilmesi daha anlamlı olur. Bu kodu görüldüğünde işlemin Ahmet tarafından onaylandığı anlaşılacak. Fakat yeni problemimiz şu ki bu sefer de Ahmet bu kodu bir kere kullandığında herkes görebilir hale gelir. 

Bunun yerine sistemi kullanan herkese iki adet kod vereceğiz. Public Key ve Secret Key olarak. Public key yani herkes tarafından bilinen kodu paylaşabilirler ama Secret Key'i gizli kalacak. Şimdi Ahmet gizli koduyla aşağıdaki gibi imzalayabilir. Public Key'in kullanımına daha sonra geleceğiz.

```
İmzala(Mesaj, Secret Key) = İmza
```
Ahmet Mehmet'e 20 lira ödediği işlemi "imzala" fonksiyonunu kullanarak imzaladı. Bunu yaparken de yukarıda gördüğümüz gibi secret key'ini kullandı.

Daha sonra isteyen bir kişi Ahmet'in public key'i ile imza mesaj eşleşmesinin doğru olup olmadığına bakabilir. Ahmetin public key'i herkese açık.

```
Dogrula(Mesaj, İmza, Public Key) = İmzalamış ya da İmzalamamış (True/False)
```

Dogrulama ile Ahmet'in gizli anahtarını (secret key) bilmesek de public key'i imza ve mesajla yanyana getirerek. İşlemin geçerliliğini denetleyebiliyoruz. Eğer 1 dönerse (true) dönerse imza gerçek. 0 dönerse (false) o işlem geçersiz demektir.

Ayrıca imzalanan her doküman için imza değişeceğinden biri Ahmet'in bir imzasına bakarak buradan edindiği bilgiyle bir başka işlemini  imzalayamaz. Başka bir değişle kendisine açık olan imza, mesaj, public key üçlüsünden secret key'i öğrenemez.

Burada imzamız 256 bit bir koddan oluşuyor. 2 üzeri 256 tane ihtimal olabilir. 256 bit bir kodun nasıl göründüğüne bakacak olursak:

```
256 Bit Binary:
111100100101111010000100011111101000101001010000100100000101011010011010110001001010001011001010101010001101000010101110110110101011010011100010011010001110100001101110111011100111001011110100010010001000011001001100100011000101001010010100100000001001110

256 Bit ASCII Formatta:
z%C*F-JaNdRgUkXp2s5u8x/A?D(G+KbP

256 Bit Yalnızca Hex:
92F423F4528482B4D6251655468576D5A7134743777397A24432646294A404E
```

Gördüğümüz gibi bu bilgi çok az yer kaplıyor. Modern bilgisayar sistemleriyle taşınması çok kolay. Ama kırılması neredeyse imkansız. Burada şifreleme kısmında biraz daha detaya girecek olursak doğrulama fonksiyonumuz aşağıdaki gibiydi:

```
Dogrula(Mesaj, 256 Bit İmza, Public Key) = True (İmzalamış)
```

Burada herkes public key'e imzaya ve mesaja sahip olabilir. İstediği gibi doğrulamaları deneyebilir. Ama imzayı oluşturan secret keyi bilemediğinden başka bir mesaj için imza üretemez. Astronomik bir CPU gücüne sahip olması gerekir. Bu da pratikte mümkün olmayacağından imzayı oluşturan kişinin secret key'in sahibi Ahmet olduğundan emin oluyoruz.

Şimdi defterimize geri dönecek olursak,

```
Muhasebe Defteri:
0 Ahmet Mehmet'e 20 lira öder. <imza>
1 Ayşe Ahmet'e 40 lira öder. <imza>
2 Mehmet Ali'ye 30 lira öder. <imza>
3 Ali Mehmet'e 10 lira öder. <imza>
```

Yukarıdaki gibi her satır parayı ödeyen kişi tarafından imzalandı. Aslında hala bir açığımız var. O da aynı satırın tekrar eklenebilmesi. Onu da sıra numarası vererek çözüyoruz. Bu sıra numarası mesaja dahil ediliyor böylece imzalama sonrası imzaya da dahil olmuş oluyor. Protokolümüz de aşağıdaki gibi oldu.

```
Protokol:
İsteyen herkes deftere satır ekleyebilir.
Her ayın sonunda gerçek parayla değişim yapılır.
Sadece imzalı işlemler geçerlidir.
```

Protokolümüzde hala karşılıklı güven gerektiren bir durum var. Ya Mehmet herkese borç takıp ay sonunda da ödemezse? Herkesin sahip olduğundan fazlasını harcamasını engellersek bunun önüne geçmiş oluyoruz. 
Böyle olunca aslında herkesin her ay gerçek parayla değişim yapmasına da gerek kalmıyor. Bu kuralı da kaldırarak yerine herkesin sahip olduğundan daha fazla harcamaması kuralını getirelim.

```
Protokol:
İsteyen herkes deftere satır ekleyebilir.
Kimse sahip olduğundan fazlasını harcayamaz.
Sadece imzalı işlemler geçerlidir.
```

Eğer Ahmet Mehmet'e sahip olmadığı 1000000 lirayı göndermek isterse bu geçersiz olacak. Tıpkı imzalanmayan bir işlemin geçersiz olması gibi.

Burada dikkat etmemiz gereken nokta artık bir işlemi onaylamak için o noktaya kadar aradaki tüm geçmiş işlemleri de bilmemiz gerektiği. Çünkü biri para göndermek istediğinde o paraya sahip mi bilmemiz gerekir. Bugün kriptoparalarda birazcık optimizasyon yapılabilse de yine bu gerekli.

Son işlemle artık gerçek lira ile bağlantımız tamamen kesildi. Artık kendi para birimimizi oluşturduk. 10 lira yerine artık 10 coin diyebiliriz ve artık tüm para akışı bu defter üzerinden yürütülebilir.

```
Muhasebe Defteri:
0 Ahmet Mehmet'e 20 coin öder. <imza>
1 Ayşe Ahmet'e 40 coin öder. <imza>
2 Mehmet Ali'ye 30 coin öder. <imza>
3 Ali Mehmet'e 10 coin öder. <imza>
```

Coin'leri gerçek parayla değiştirmeniz mümkün. Coin'imiz tıpkı diğer para birimleri gibi birbiriyle değiş tokuş edilebilir. Ama bu değişim protokolümüzde yer almıyor. Coin'imizin kendi başına bağımsız bir değeri var.

Özetleyecek olursak burada para birimimiz "işlem geçmişi" oldu. Son derece teorik coin'imiz Bitcoin gibi kriptoparalara benziyor. Eğer bir websitesi oluşturup işlemleri oradan yaparsak herkes kullanabilir. Ama bu fiziksel bir lokasyona güvenmek olur. Ayrıca bu deftere kim yeni satırları ekleme kuralını kontrol edecek? Bu bağımlılıkları da ortadan kaldırmak gerekiyor.

Diyelim ki bir websitesi kurmak yerine herkes bilgisayarında defterin bir kopyasını bulundursun.  İşlemimiz "Ahmet Mehmet'e 20 coin öder." işlemi yapıldığında bu ağ üzerinde bir yayınlansın. Bu sayede diğerleri de kendi muhasebe defterlerine bu satırı eklesin.

Peki bu durumda defterler üzerinde nasıl uzlaşma sağlayacağız?  Bir mesaj geldiğinde herkesin mesajı alıp aynı sırayla kaydettiğini nasıl bileceğiz? Burası aslında sorunun en önemli kısmı geliyoruz. Bulmacanın kalbi burası. 

Protokolümüze öyle bir ekleme yapacağız ki protokolü kullanan kişiler defterlerinin bir diğeriyle aynı olduğundan emin olacak. Aslında orjinal bitcoin makalesinde yer alan problem de bu.

Bitcoin'in bulduğu çözüm üzerinde en fazla işlem gücü harcanmış defteri kontrol etmek. Bunun için cryptographic hash function' kullanıyor. Eğer üzerine harcanmış işlem gücünü hangisine güveneceğiniz konusunda temel alırsanız hileli işlemler ve çakışan defterler oluşturmak yapılabilir olmaktan çıkıyor. Bu konuya daha sonra döneceğiz.

Öncelikle hash fonksiyonlarını anlamamız gerekiyor. Hash function'lar içerisine aktardığımız veriyle tek taraflı bir kod üretiyor. Herhangi bir mesajı hashleyebiliyoruz. Tersine çevirmek imkansız olmasa da yeterince zor. Aslında çoğumuz farkında olmadan bu şifreleme algoritmasını kullanıyoruz. Modern güvenliğin büyük bir kısmı kriptografik hash fonksiyonlarına dayanıyor. Mesela bir websitesine girdiğimizde https bağlantı için sertifika sha256 algoritması ile hash'leniyor.

İnternetten bir websitesine girip "test" sözcüğünü hashlersek:

```
SHA256("test") = 9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08
```

Şimdi bu fonksiyonu defterde nasıl kullanabileceğimize bakalım. 

```
Muhasebe Defteri:
0 Ahmet Mehmet'e 20 coin öder. <imza>
1 Ayşe Ahmet'e 40 coin öder. <imza>
2 Mehmet Ali'ye 30 coin öder. <imza>
3 Ali Mehmet'e 10 coin öder. <imza>
<özel numaram (proof of work)>
```
Burada bir ekleme daha da yaptık. Listenin sonuna özel bir numara ekledik. Defterin tamamı bu özel numarayla birlikte sha256 ile hashlendi. Şimdi bir kural daha koyuyoruz. Bu numara öyle bir numara olmalı ki listenin tamamı bu numarayla sha256 ile hashlendiğinde çıkan sonucun ilk 30 bitin tamamı 0 olmalı. 

Bu numarayı bulmak için gerekli deneme sayısı 1/2üzeri30 yani milyonda 1. Sha256 düz bir hash fonksiyonu değil kriptografik olduğundan özel numara ancak deneyerek bulabilir. Yani neredeyse tamamını deneyecek. Şanslıysa ilk denemelerde de bulabilir.

Numarayı bulmak maliyetli olsa da bulup bulunamadığını kontrol etmek ise oldukça kolay ve maliyetsiz. Sadece hash i çalıştırıp ilk 30 hanesi 0 mı diye bakabiliriz. Bu konsepte proof of work deniyor. Yani yapılan işin kanıtına çok daha az çaba harcayarak ulaşabiliyoruz.

Burada dikkat edersek işin tamamı defterdeki işlemlere bağlı. Eğer defterde bir işlem değişse numara baştan değişecek yeni numarayı bulmak için tekrar numara avına çıkacağız. Bir milyon tahmin daha yapmamız gerekecek. Böylece yeni liste yeni numara hashlendiğinde 30 hanesi 0 olan yeni bir liste oluşmuş olacak.

Bitcoin'in orjinal makalesinde belirtilen fikir en çok iş harcanan defteri seçmekti. İlk olarak verilen her bir defteri bloklara ayırıyoruz. Her blok işlemleri ve özel numarayı içeriyor. (proof of work) Bu özel numarayla hashlendiğinde sıfırlarla başlayan hash'i çıkartıyor. Bu numaraya 30 demiştik 60 diyelim ama daha sonra daha sistematik bir biçimde seçeceğiz.

Bir işlem nasıl göndericisi tarafından imzalandıysa valid sayılıyorsa aynı şekilde block da proof of work'ü varsa valid sayılıyor.

Ayrıca her bloğun sıralı olduğundan emin olmak için bir block header'ında öteki block'un hash'ini taşıyor. Böylece blockların birindeki bir değeri ya da blockların sırasını değiştirmek demek  ardından gelecek blockları da değiştirmek demek. Böylece bütün block'lar için 60 sıfırı sağlayacak özel numaralar (proof of work) tekrar bulunmak zorunda block lar birbirlerine bu şekilde zincirlendiklerinden artık defter değil blockchain ismini kullanıyoruz.

Güncellenmiş protokolümüzle artık dünyadaki herkes block üretici olabilir. Block üreticileri yayınlanan işlemleri dinleyerek bir block oluşturur ve iş yaparak 60 sıfırı sağlayacak özel numarayı bulmaya çalışırlar. Bulduklarında block'u yayınlarlar. Yaptığı bu iş için block üreticiyi ödüllendirmek için block 'u oluşturduğunda ödül olarak özel bir işlem oluşturmasına imkan tanınır. Hiç yoktan 10 coin kazanır gibi.

Block üreticisinin yaptığı işe karşı kazandığı block ödülü genel kurallara bir istisnadır. Bu para hiçbir yerden gelmez bu nedenle imzalanması gerekmez. Böylece ekonomimizdeki toplam coin'lerin sayısı da her bir block ile artmış olur. 

İşte bu block üretme işlemine mining denir. Çünkü büyük miktarda iş gerektirir ve ekonomiye yeni coin'ler katar. Ama miner'lar hakkında çok şey duysak da aslında yaptıkları işlemleri dinlemek. Block'lar üretmek ve yayınlamak ve bunu yaparken de yeni coinlerle ödüllendirilmektir. 

Miner'ın perspektifinden her bir block minyatür bir piyango gibidir. Herkes mümkün olduğunca hızlı biçimde numaraları tahmin etmeye çalışır. Ta ki bir şanslı kişi  block hash'inin çok sayıda sıfırla başlamasını sağlayan özel numarayı bulup block'u yayınlayana kadar.

Sistemi ödeme yapmak için kullanan biri ise işlemleri dinlemek yerine minerlar tarafından broadcast edilen blockları dinleyerek kendi kişisel blockchain kopyalarını güncellerler. 

Protokolün önemli özelliği eğer çakışan işlemler içeren iki ayrı blok zinciri söz konusu olduğunda uzun olanını referans almasıdır.  İçerisine en fazla işgücü konmuş olanı doğru kabul eder. Eğer eşitlik durumu oluşursa eşitliği bozacak ek bir blok gelene kadar beklersiniz.

Merkezi bir otorite olmasa ve herkes kendi kopyasını barındırıyor olsa dahi eğer herkes bu bir block chain e en fazla işgücü konduğuna kanaat getirirse merkezi olmayan bir uzlaşmaya gidilmiş olur.

Peki birisi bu özelliği hileli şekilde kendi yararına kullanmak isterse ne olacak? Hangi işlemin geçerli olduğunun kabul edildiğine ve sistemin neyin güvenli yaptığını anlamak amacıyla bu sistemde birinin nasıl  kandırılabileceğine bakalım.

Ahmet Mehmeti hileli bir blockla kandırmaya çalışıyor olsun. Göndereceği block Ahmet Mehmet'e 100 coin gönderir işlemini içeren bir block hazırlıyor. Fakat bunu network'ün geri kalanına broadcast etmiyor. Böylece networkün geri kalanı Ahmet'in Mehmet'e 100 coin gönderdiğini bilmiyor. 

Ahmet'in bunu yapabilmesi için öncelikle geçerli bir proof of work'ü bütün minerlardan önce bulması gerekiyor. Her biri kendi block'u üzerinde çalışıyorlar. Bu olabilecek bir durum. Ama Mehmet bu sırada öteki minerları da duyuyor. Bu nedenle Ahmet tekrar tekrar proof of work sağlayarak tek başına Mehmet'in blockchain'indeki özel fork'u ilerletmek durumunda. Bu özel fork minerların geri kalanından farklı. Hatırlaylım ki Mehmet her zaman en uzun zincire güvenecek. 

Ahmet networkteki diğer tüm minerların toplamından daha hızlı bir biçimde bulacak olursa bir şans eseri bir kaç blok bunu devam ettirebilir. Ama Ahmet ağdaki tüm kullanıcıların toplamının %50'sine yakın bir işlem kaynağına sahip değilse öteki minerların üzerinde çalıştığı öteki blockchain Ahmet'in Mehmet'in bilgisayarında oluşturduğu kırılgan blockchaininden daha hızlı büyüyecektir. Bir süre sonra Mehmet artık Ahmet'den duyduğunu red edecek herkesin üzerinde çalıştığı daha uzun zinciri seçecektir. 

Peki bu ne anlama gelir? Demek ki yeni duyduğunuz bir block'a hemen güvenmemeniz gerekiyor. Bunun yerine üzerine eklenecek yeni block'ları beklemenmesi gerekiyor. Eğer zincirin büyümeğe devam ettiğinden emin olursanız bu noktada herkesin kullandığı zincir olduğuna emin olabilirsiniz. 

Bu şekilde tüm ana fikirlerin üzerinden geçmiş oluyoruz. Proof of work tabanlı bu dağıtık defter sistemi aşağı yukarı Bitcoin protokolünün çalışma şeklini tanımlıyor. Aynı şekilde diğer kriptoparaların da çalışma biçimini gösteriyor. 

* Dijital İmzalar
* Defter parabirimi
* Decentralize
* Proof Of Work
* Block Chain

Son olarak toparlamamız gereken bazı detaylar var. Block'un hash'i 60 sıfır ile başlamak zorunda demiştik. Gerçek Bitcoin protokolünde periyodik olarak bu sıfırların sayısı dinamik olarak değiştirilerek aşağı yukarı 10 dakikada bir block'un bulunması sağlanıyor. Böylece miner sayısı arttıkça zorlaşıyor. 10 dakikada yalnızca 1 tane kazanan olabiliyor.

Daha yeni kriptoparaların daha kısa blok yenilenme zamanları var.

```
BTC: 10 dakika
ETH : 15 saniye
XRP: 3.5 saniye
LTC: 2.5 dakika
```

Bitcoin içerisindeki tüm para block ödülünden geliyor.
Block ödülleri aşağıdaki gibi:

```
Ocak 2009 - Kasım 2012: 50 BTC
Kasım 2012 - Haziran 2016 : 25 BTC
Temmuz 2016 - Şubat 2020 : 12.6 BTC
Şubat 2020 - Ekim 2023 : 6.25 BTC
```

block explorer sitesinden bitcoin blockchain'inin durumunu görebiliyoruz. Buradan bitcoin blockchain'inin mevcut durumunu görüp inceleyebiliyoruz.

İlk blocklara baktığımız zaman miner a verilen 50 bitcoin dışında bir işlem olmadığını görüyoruz.

Fakat her bir 210.000 blokta yani aşağı yukarı 4 yılda bu ödül yarıya düşüyor. Şu anda ödül 6.25 BTC.

Bu ödül zamanla geometrik olarak düştüğünden 21.000.000 milyon bitcoinden daha yüksek bir bitcoin olamaz. Ama bu yine de minerları para kazanmaktan alıkoymayacak. Block ödülünün yanında minerlar aynı zamanda işlem ücreti de alabilirler. 

Her bir işlem yapıldığında opsiyonel olarak o block'un miner a para gönderebiliyorsun. Bunun amacı miner'ı yaptığın broadcast'i bir sonraki block'a eklemek amacıyla teşvik etmek. 

Bitcoin içerisinde her bir blok aşağı yukarı 2400 işlem barındırabiliyor. Bunun gereksiz biçimde sınırlayıcı olduğu yönünde bir çok eleştiri var.  Karşılaştırma yapılacak olursa VISA saniyede 1700 işlem yapıyor. 24.000'den fazlasını yapabilecek durumdalar.

Bu yavaş işlem durumu Bitcoin'in daha yüksek işlem bedellerine sahip olmasına sebep oluyor.  Çünkü minerların yeni bloklar içerisine koymak için hangi işlemleri seçeceğini bu belirliyor .

Şu anda 15.37 dolar. Aslında bu kripto paraların kapsamlı bir gözden geçirmesi olmaktan çok uzak. Burada ele alınmayan bir çok ayrıntı ve farklı dizayn tercihleri var. Merkle ağaçları, proof of work'e alternatifler, scripting gibi. Yine de iyi bir giriş olduğunu düşünüyorum. Umarım faydalı olmuştur. Başka bir yazıda görüşmek dileğiyle...

### Kaynaklar
* 3Blue1Brown - https://www.youtube.com/watch?v=bBC-nXj3Ng4&ab_channel=3Blue1Brown
* Michael Nielsen Blog Makalesi : How The Bitcoin Protocol Actually Works - https://michaelnielsen.org/ddi/how-the-bitcoin-protocol-actually-works/
