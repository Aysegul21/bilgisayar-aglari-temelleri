# Giriş

Bu yazımızda OSI modeli ve bilgisayar ağlarının çalışma prensiplerini ele alacağız.   
Ancak OSI modeline geçmeden önce, ağlar ve protokoller gibi bazı temel kavramları bilmek önemlidir.  
Bu kavramlar, veri iletişiminin nasıl gerçekleştiğini ve OSI modelinin neden geliştirildiğini anlamamıza yardımcı olacaktır.

---

## 1. Bilgisayar Ağı Nedir?
<img width="948" height="609" alt="image" src="https://github.com/user-attachments/assets/c6104c38-8f58-41c3-aaa4-6e74c03447bd" />

**Bilgisayar ağı**, iki veya daha fazla cihazın birbirine bağlanarak veri alışverişi yapmasına olanak sağlayan yapıdır.  

Ağlar sayesinde:
- Dosya ve bilgi paylaşımı yapılabilir,  
- İnternete erişim sağlanabilir,  
- Uygulamalar ve servisler birbirine bağlanabilir.  

**Örnek:**  
- Evdeki bilgisayar ve telefonun modeme bağlanarak internete çıkması,  
- Bir şirket içindeki tüm bilgisayarların ortak yazıcıya erişebilmesi.

---

## 2. Protokol Nedir?
<img width="516" height="356" alt="image" src="https://github.com/user-attachments/assets/6c5344a5-a964-4bd1-98c5-8a0c3f1b1afe" />

### Günlük Hayattan Örnek
İki kişi sohbet ederken bazı kurallara uyar:  
- Aynı dili kullanmak,  
- Sırayla konuşmak,  
- Karşı taraf anlamazsa kendini tekrar etmek.  

Kurallar olmadan iletişim **anlamsız ve kaotik** olur.  

### Bilgisayar Ağlarında
Bilgisayarlar da veri gönderirken benzer kurallara uyar.  
- Veri kaç parçaya bölünecek?  
- Parçalar hangi sırayla gönderilecek?  
- Karşı taraf veriyi doğru alıp almadığını nasıl kontrol edecek?  

Bu kurallara **protokol** denir.  

**Örnek Protokoller:**  
- HTTP, SMTP, FTP, TCP, UDP  

**Örnek Senaryo:**  
Bir web sayfası yüklenirken tarayıcı HTTP isteği oluşturur, TCP ile paketler gönderilir ve sunucu cevap verir.  

---

## 3. Neden Modeller Kullanıyoruz?
Ağ iletişimi karmaşıktır ve her protokol farklı görevler üstlenir.  
Bu karmaşıklığı yönetmek için iletişim süreci **katmanlara ayrılmıştır**.  

**Avantajlar:**  
- Karmaşıklığı parçalarına böler,  
- Sorun çözmeyi kolaylaştırır,  
- Standart görevler tanımlar,  
- Farklı üreticilerin cihazları arasında uyumluluk sağlar.

---

## 4. OSI Modeline Giriş
<img width="710" height="722" alt="image" src="https://github.com/user-attachments/assets/11f835a1-1f83-4154-bdc7-f72abf2f6f13" />

Tüm bu hazırlık bilgilerinden sonra, OSI modeline geçebiliriz.  

- OSI modeli, ağ iletişimini **7 katman** halinde açıklayan teorik bir çerçevedir.  
- Her katman farklı bir görev üstlenir ve kendi protokolleri vardır.  

---
## 5. OSI Katmanları

OSI modeli **7 katmandan** oluşur. Her katman farklı bir işlev üstlenir ve bir üst katmana veri iletir. Katmanları yukarıdan aşağıya doğru inceleyelim:

#### 5.1 Uygulama Katmanı (Application Layer)

> **Görev:**  
> - Kullanıcının doğrudan etkileşimde bulunduğu katmandır.  
> - Ağ üzerinden veri gönderen veya alan uygulamaların çalışmasını sağlar.  
> - Ağ hizmetlerini kullanıma sunar (ör: web tarayıcısı, veri izleme yazılımı, veri kayıt sistemleri).

> **DAG Yerleşkesi Örneği:**  
> - DAG teleskobunda adaptif optik sistemi üzerinden görüntü verilerini izlemek için kullanılan **kontrol yazılımı** bu katmanda çalışır.  
> - Astronom gözlemciler, bilgisayar arayüzü üzerinden teleskobun durumu, AO sisteminin düzeltme verileri ve kamera görüntülerine erişir.

> **Örnek Protokoller:**  
> - **HTTP:** Web tabanlı izleme panelleri veya veri raporlama arayüzleri  
> - **FTP:** DAG verilerini merkezi sunucuya aktarım  
> - **SMTP:** Sistem uyarıları veya hata bildirimlerinin e-posta ile iletilmesi  
> - **DNS:** Teleskop ve sunucu cihazlarının ağ adları ile tanımlanması  

> **Senaryo:**  
> 1. Gözlem odasındaki kontrol bilgisayarından DAG verilerini görmek için izleme yazılımı açılır.  
> 2. Yazılım HTTP veya FTP protokolleriyle veri sunucusuna istekte bulunur.  
> 3. Sunucu, veri paketlerini gönderir ve yazılım ekranda görüntüleri ve AO düzeltme bilgilerini gösterir.  

> **Not:**  
> - Bu katman **veriyi iletmeye başlamaz**, sadece veriyi oluşturur ve alt katmanlara iletir.  
> - Kullanıcı (gözlemci) ile en yakın katmandır; kullanıcı deneyimi doğrudan buradan etkilenir.

#### 5.2 Sunum Katmanı (Presentation Layer)

> **Görev:**  
> - Veriyi uygulama katmanı için uygun hale getirir.  
> - Şifreleme, sıkıştırma ve veri formatlama işlemlerini yapar.  
> - Uygulamanın aldığı veya gönderdiği veriyi “anlaşılır” formata dönüştürür.

> **DAG Yerleşkesi Örneği:**  
> - DAG teleskobunda AO sisteminden gelen görüntü verileri, sunucuda işlenmiş raw veriler şeklindedir.  
> - Sunum katmanı, bu verileri astronom gözlemcilerin kullanacağı **grafik arayüzde görüntüye dönüştürür** ve gerekirse şifreler.  
> - Ayrıca, veriler sunucudan izleme yazılımına aktarılırken sıkıştırılır, böylece ağ üzerinden hızlı iletim sağlanır.

> **Örnek Protokoller ve İşlevleri:**  
> - **HTTPS:** Sunucu ile izleme yazılımı arasındaki veri iletimini şifreler  
> - **MIME (Multipurpose Internet Mail Extensions):** E-posta ve veri formatlarını standart hale getirir  
> - **JPEG, PNG, FITS:** Teleskop görüntü dosyalarının standardize edilmesini sağlar

> **Senaryo:**  
> 1. AO sisteminden gelen ham görüntü verisi sunucuya aktarılır.  
> 2. Sunum katmanı, veriyi gözlemci yazılımının anlayacağı formatta işler ve gerekirse şifreler.  
> 3. İzleme yazılımı veriyi alır ve ekranda düzgün bir şekilde gösterir.

> **Not:**  
> - Bu katman, **veriyi iletmek yerine veriyi “hazırlayan” katmandır**.  
> - Kullanıcının veriyi anlamasını ve uygulamanın doğru işlem yapmasını sağlar.

#### 5.3 Oturum Katmanı (Session Layer)

> **Görev:**  
> - İki cihaz arasındaki iletişim oturumlarını yönetir.  
> - Bağlantının başlatılması, sürdürülmesi ve sonlandırılmasından sorumludur.  
> - Veri alışverişinin düzenli ve güvenli bir şekilde yapılmasını sağlar.

> **DAG Yerleşkesi Örneği:**  
> - DAG teleskobunda adaptif optik sistemi ile kontrol yazılımı arasında açılan **izleme oturumu** bu katmanda yönetilir.  
> - Gözlemci, teleskopun kameralarından sürekli veri akışı almak istediğinde oturum açılır ve bağlantı süresince devam eder.  
> - Oturum sonunda bağlantı düzgün bir şekilde kapatılır, veri kaybı veya karışıklık önlenir.

> **Örnek Protokoller ve İşlevleri:**  
> - **RPC (Remote Procedure Call):** Sunucudaki fonksiyonları oturum boyunca çalıştırır  
> - **NetBIOS:** Oturum açma ve bilgisayarlar arası kaynak paylaşımı  
> - **SMB (Server Message Block):** Dosya ve veri paylaşım oturumlarını yönetir

> **Senaryo:**  
> 1. Gözlem odasındaki bilgisayar, DAG verilerini almak için izleme yazılımını başlatır.  
> 2. Oturum katmanı, cihazlar arasında güvenli ve sürekli bir bağlantı oluşturur.  
> 3. Gözlem bittiğinde oturum katmanı bağlantıyı düzgün bir şekilde kapatır ve kaynakları serbest bırakır.

> **Not:**  
> - Oturum katmanı, **veriyi doğrudan iletmez**, ancak verinin düzenli ve güvenli bir şekilde aktarılmasını garanti eder.  
> - DAG sistemindeki sürekli veri akışları ve kontrol komutları bu katman sayesinde yönetilir.

#### 5.4 Taşıma Katmanı (Transport Layer)

> **Görev:**  
> - Verinin uçtan uca iletimini sağlar.  
> - Paketlerin doğru sırayla ve eksiksiz ulaştığından emin olur.  
> - Hata kontrolü yapar ve gerektiğinde veriyi tekrar yollar.

> **DAG Yerleşkesi Örneği:**  
> - DAG teleskobundan AO sistemine veya kontrol yazılımına gelen görüntü verileri, **TCP protokolü** ile paketler halinde taşınır.  
> - Eğer bir paket kaybolursa veya hatalı gelirse, taşıma katmanı bunu tespit eder ve paketi tekrar gönderir.  
> - Bu sayede teleskop verileri hatasız olarak gözlemcinin ekranına ulaşır.

> **Örnek Protokoller ve İşlevleri:**  
> - **TCP (Transmission Control Protocol):** Güvenilir iletim sağlar; paketlerin eksiksiz ve doğru sırada ulaşmasını garanti eder  
> - **UDP (User Datagram Protocol):** Hızlı iletim sağlar; hata kontrolü yapmaz, genellikle düşük gecikme gereken durumlar için kullanılır  

> **Senaryo:**  
> 1. AO sisteminden gelen bir görüntü verisi, TCP paketlerine bölünür.  
> 2. Paketler ağ üzerinden DAG kontrol yazılımına iletilir.  
> 3. Taşıma katmanı, eksik veya hatalı paketleri tespit edip yeniden gönderir.  
> 4. Kontrol yazılımı, tüm paketleri birleştirip ekranda görüntüyü oluşturur.

> **Not:**  
> - Taşıma katmanı, OSI modelinde verinin **uçtan uca güvenli iletimini** sağlar.  
> - DAG yerleşkesinde sürekli veri akışı ve AO düzeltmeleri bu katmanın düzgün çalışmasına bağlıdır.

#### 5.5 Ağ Katmanı (Network Layer)

> **Görev:**  
> - Veriyi kaynaktan hedefe yönlendirir (routing).  
> - IP adreslerini kullanarak cihazlar arası veri yollarını belirler.  
> - Paketlerin farklı ağlar üzerinden doğru hedefe ulaşmasını sağlar.

> **DAG Yerleşkesi Örneği:**  
> - DAG yerleşkesindeki farklı cihazlar (AO sistemi, teleskop kameraları, kontrol bilgisayarları, merkezi sunucu) arasında veri iletimi yapılır.  
> - Ağ katmanı, bu cihazlara verinin hangi yoldan ulaşacağını belirler ve paketleri yönlendirir.  
> - Örneğin, AO düzeltme verileri kameradan kontrol bilgisayarına doğru yönlendirilir.

> **Örnek Protokoller ve İşlevleri:**  
> - **IP (Internet Protocol):** Paketleri doğru hedef IP adresine yönlendirir  
> - **ICMP (Internet Control Message Protocol):** Hata mesajlarını ve durum bildirimlerini iletir  
> - **ARP (Address Resolution Protocol):** IP adreslerini fiziksel MAC adresine çevirir

> **Senaryo:**  
> 1. AO sistemi verilerini kontrol bilgisayarına gönderir.  
> 2. Ağ katmanı, paketlerin IP adreslerini kontrol eder ve uygun rotayı belirler.  
> 3. Paketler farklı ağ cihazlarından geçerek hedefe ulaşır.  
> 4. Hedef cihaz, paketleri alır ve bir üst katmana iletir.

> **Not:**  
> - Ağ katmanı, **verinin hangi yol üzerinden gideceğini belirler**, veri içeriğini değiştirmez.  
> - DAG yerleşkesindeki farklı cihazlar arası veri iletimi bu katmana bağlıdır.

#### 5.6 Veri Bağlantı Katmanı (Data Link Layer)

> **Görev:**  
> - Aynı ağ içindeki cihazlar arasında güvenli ve hatasız veri iletimi sağlar.  
> - Fiziksel adresleme (MAC adresleri) yapar.  
> - Hata tespit ve düzeltme mekanizmalarını uygular.  
> - Paketleri çerçevelere (frames) böler ve iletir.

> **DAG Yerleşkesi Örneği:**  
> - DAG yerleşkesindeki AO sistemi ve kontrol bilgisayarı arasında **LAN üzerinden veri iletimi** yapılır.  
> - Veri, ağ kartları aracılığıyla çerçeve (frame) formatına dönüştürülür ve MAC adresiyle hedef cihaza gönderilir.  
> - Hatalı çerçeveler tespit edilirse yeniden iletim sağlanır.

> **Örnek Protokoller ve İşlevleri:**  
> - **Ethernet:** LAN üzerinde veri iletimi sağlar, çerçeve yapısını ve MAC adreslerini kullanır  
> - **PPP (Point-to-Point Protocol):** İki cihaz arasında doğrudan bağlantı kurar  
> - **Switch ve Bridge protokolleri:** Çerçeveleri yönlendirir ve ağ trafiğini düzenler

> **Senaryo:**  
> 1. AO sistemi verilerini kontrol bilgisayarına gönderir.  
> 2. Veri çerçevelere bölünür, MAC adresi eklenir.  
> 3. Switch aracılığıyla doğru cihaz bulunur ve veri iletilir.  
> 4. Hata tespit edilirse çerçeve yeniden gönderilir.

> **Not:**  
> - Veri Bağlantı Katmanı, **aynı ağdaki cihazlar arasında güvenli ve düzenli veri iletiminden** sorumludur.  
> - DAG yerleşkesindeki LAN üzerinden cihazlar arası iletişim bu katmana bağlıdır.

#### 5.7 Fiziksel Katman (Physical Layer)

> **Görev:**  
> - Veriyi **bit seviyesinde** iletir (0 ve 1).  
> - Elektriksel sinyaller, radyo dalgaları veya optik sinyaller aracılığıyla fiziksel ortam üzerinden aktarımı sağlar.  
> - Kablolar, fiber optik hatlar, switch portları gibi fiziksel bağlantılardan sorumludur.

> **DAG Yerleşkesi Örneği:**  
> - DAG yerleşkesinde AO sistemi, kameralar, kontrol bilgisayarları ve sunucular arasındaki veri **fiziksel bağlantılar üzerinden** iletilir.  
> - Örneğin, fiber optik kablolar veya Ethernet kabloları üzerinden görüntü ve kontrol verileri taşınır.  
> - Fiziksel katman, iletim ortamının doğru çalışmasını ve sinyal bütünlüğünü sağlar.

> **Örnek Donanım ve Protokoller:**  
> - **Ethernet kabloları (Cat5, Cat6), Fiber Optik Kablolar**: Veri iletim ortamı  
> - **RJ45, SC/ST konektörleri**: Fiziksel bağlantı noktaları  
> - **Sinyal standardları (RS-232, RS-485, Optical signals)**: Bit iletim formatları  

> **Senaryo:**  
> 1. AO sisteminden gelen görüntü verisi fiziksel kablolar üzerinden kontrol bilgisayarına iletilir.  
> 2. Veri Bağlantı Katmanı çerçeveler halinde organize eder, ancak fiziksel katman sinyali taşır.  
> 3. Sunucuya ulaşan bitler üst katmanlar tarafından işlenir ve görüntü ekrana gelir.

> **Not:**  
> - Fiziksel katman, **verinin temel iletiminden sorumludur**, veri içeriğini anlamaz.  
> - DAG yerleşkesindeki tüm cihazlar arası veri akışı, bu katman sayesinde mümkün olur.

## 6. OSI Modeli Örneği: DAG Yerleşkesinde Veri Akışı
<img width="535" height="332" alt="image" src="https://github.com/user-attachments/assets/14485881-bdf2-48bb-9a6e-a8b5c73df0a3" />

Diyelim ki bir astronom gözlemci, DAG teleskobundan gelen görüntü verilerini kontrol yazılımında görmek istiyor. Bu veri, OSI modelindeki **7 katman** boyunca nasıl ilerler, adım adım inceleyelim:

1. **Uygulama Katmanı:**  
   - Gözlemci kontrol yazılımını açar ve DAG verilerini talep eder.  
   - HTTP veya FTP protokolleri kullanılır.

2. **Sunum Katmanı:**  
   - Sunucu, ham görüntü verisini yazılımın anlayacağı formata dönüştürür (ör: FITS → görüntü).  
   - Gerekirse veriyi şifreler ve sıkıştırır.

3. **Oturum Katmanı:**  
   - Gözlemci ve sunucu arasında güvenli bir **oturum** açılır.  
   - Veri akışı boyunca oturum sürdürülür.

4. **Taşıma Katmanı:**  
   - Veriler TCP paketlerine bölünür.  
   - Paketlerin eksiksiz ve doğru sırada ulaştığından emin olunur.

5. **Ağ Katmanı:**  
   - Paketler, IP adresleri kullanılarak DAG cihazları arasında yönlendirilir.  
   - Farklı cihazlar ve ağlar arasında doğru rota belirlenir.

6. **Veri Bağlantı Katmanı:**  
   - Paketler çerçevelere dönüştürülür ve MAC adresleri ile hedef cihaz bulunur.  
   - Hata tespiti yapılır, gerekirse çerçeveler yeniden gönderilir.

7. **Fiziksel Katman:**  
   - Çerçeveler, bit seviyesinde **fiziksel kablolar veya fiber optik hatlar** üzerinden iletilir.  
   - Sunucuya ulaşan bitler bir üst katmana iletilir.

---

### Özet Senaryo

- Gözlemci: “AO sisteminden görüntü verilerini al” der.  
- Uygulama ve Sunum Katmanı: Veriyi talep eder ve uygun formata getirir.  
- Oturum Katmanı: Güvenli bir bağlantı kurar.  
- Taşıma Katmanı: Paketleri hazırlar ve kontrol eder.  
- Ağ Katmanı: Paketleri hedefe yönlendirir.  
- Veri Bağlantı Katmanı: Aynı ağdaki cihazlara güvenli iletim sağlar.  
- Fiziksel Katman: Bitleri kablo veya fiber üzerinden taşır.

 Bu süreç, DAG yerleşkesindeki **AO sistemi, kontrol bilgisayarı ve sunucu** arasında veri iletiminin **hatta eksiksiz ve güvenli şekilde** gerçekleşmesini sağlar.

---
