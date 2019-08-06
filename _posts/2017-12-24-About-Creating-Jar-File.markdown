---
layout: post
title:  "Java(Maven) projemizden .jar dosyası nasıl oluşturuyoruz?"
date:   2017-12-24 12:19:58 +0300
categories: jekyll update
---

Merhaba Yıldız Tozları,

Daha önce CLI nedir ve nasıl projemizde kullanırız üzerine yazı yazmıştım.Yarın ödevin son günü ama :) Bugün belki ödevin kodunu yazmış fakat nasıl jar dosyası üreteceğini konusunda zorlananlar için nasıl jar dosyası oluşturabileceklerini göstermeye çalışacağım. Öncelikle üretmeye çalıştığımız şey ne ve ne içeriyor bilmemiz lazım.Onun için tanım ile başlayalım.

#### **JAR dosyası nedir?**

[Buradan](https://www.wikiwand.com/en/JAR_(file_format)) da okuyabileceğiniz gibi.(Eğer Wikipedia'ya erişemiyorsanız. **Wikiwand** eklentisini kullanabilirsiniz.Gayet hoş bir görünüm sağlıyor ve Wikipedia yasağını(!) aşıyor.) JAR birçok java sınıf dosyasını, kılavuz verisini(metadata) ve proje kaynaklarını(metin, resim, vs. gibi) dağıtım için kümeleyen, çalıştırılabilir bir paket fosya formatı. Yani bizim projemizle ilgili her şey bu jar dosyasının içinde olacak.Artık JAR'ın ne olduğunu öğrendiğimize göre üretmeye çalışabiliriz.
#### **JAR dosyası Java(Maven) projesinde nasıl üretilir?**

Öncelikle **_pom.xml_** dosyamıza jar dosyası üretmek için gerekli olan direktifleri yazıyoruz.Aşağıda screenshotta **öğrendiğim kadarıyla**, yorum ile detaylandırdım.Detaylı incelemenizi öneriyorum.

![Screenshot1]({{ "/assets/JAR-Blogpost/screenshot1.png" | absolute_url }})
(Bu direktifleri daha önce **JewelCLI** için eklediğimiz direktiflerin altına yazıyoruz unutmayın.)

Gerekli direktifleri yazdıktan sonra jar dosyasını oluşturmak için aşağıdaki adımları takip etmeniz gerekiyor.

**Not:**Bu adımları izlediğim bir video'da öğrendim belki başka yolla da üretiliyordur ille böyle olacak diye bir şey şöylemiyorum.

#### **Adım 1**

Önce View-->Tool Window-->Maven Projects'e tıklayın, tıkladıktan sonra sağ tarafta aşağıdaki gibi bir görünüm elde edeceksiniz.

![Screenshot2]({{ "/assets/JAR-Blogpost/screenshot2.png" | absolute_url }})

#### **Adım 2**

Şimdi bunlardan sırayla **_clean_**, **_install_** ve **_assembly::assembly_**'e çift tıklayarak ya da yukardaki çalıştır butonuna(Yeşil Üçgen) basarak çalıştırın.

#### **Adım 3**

Çalıştırdıktan sonra bunları dosya ağacınızda **_target_** adlı bir dosyanın oluştuğunu  ve bunun içinde jar dosyanızın oluştuğunu göreceksiniz aşağıdaki gibi.

![Screenshot3]({{ "/assets/JAR-Blogpost/screenshot3.png" | absolute_url }})

#### **Adım 4**

Jar dosyanıza **trending.jar**'a sağ tıklayınca açılan seçeneklerden **Show in Folders**'a tıklayarak ya da direkt projenizin bulunduğu dosyaya giderek ulaşabilirsiniz.Jar dosyanızı çalıştırmak içinse sadece **java -jar trending.jar gerekliargüman1 gerekliargüman2 ...** yapmanız yeterli. Aşağıda nasıl yapıldığını görebilirsiniz.

![Screenshot4]({{ "/assets/JAR-Blogpost/screenshot4.png" | absolute_url }})

Aynı dizin altında **_all_tweets.txt_** dosyası olmadığı için sadece argümanları bastırdı o kadar.Buraya kadar yazdığım kodlara [github hesabımdan](https://github.com/koksalmis/trending) ulaşabilirsiniz.

**Not:**Ödevin deadline'ı geçtikten sonra eğer vaktim olursa, ödevin tamamlanmış halini github hesabımda paylaşacağım.

Teşekkür Ederim.

Enes Köksalmış



