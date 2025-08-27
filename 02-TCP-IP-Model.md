# Giriş

Bu yazımızda TCP/IP modeli ve bilgisayar ağlarının günümüzdeki uygulamalarını ele alacağız.  
OSI modeli teorik bir çerçeve sunarken, TCP/IP modeli **gerçek internet iletişimini yöneten ve yaygın olarak kullanılan protokol ailesidir**.  

TCP/IP modeli, dört katmandan oluşur ve OSI modeline göre daha pratiktir:  
- **Application (Uygulama) Katmanı**  
- **Transport (Taşıma) Katmanı**  
- **Internet (İnternet) Katmanı**  
- **Network Access (Ağ Erişim / Link) Katmanı**  

---

## TCP/IP ve OSI Karşılaştırması
<img width="2003" height="913" alt="image" src="https://github.com/user-attachments/assets/bcc13012-13cd-424c-80d4-29c6bb3fd659" />

TCP/IP ve OSI modelleri birbirine paralel düşünülebilir, ancak bazı farklılıklar vardır:  

| OSI Modeli Katmanı        | TCP/IP Modeli Katmanı       | Notlar |
|----------------------------|----------------------------|--------|
| Uygulama Katmanı           | Application Katmanı         | OSI’deki Uygulama, Sunum ve Oturum katmanlarını kapsar |
| Taşıma Katmanı             | Transport Katmanı           | TCP ve UDP ile uçtan uca iletişim sağlar |
| Ağ Katmanı                 | Internet Katmanı            | IP adresleri ile yönlendirme yapar |
| Veri Bağlantı ve Fiziksel Katman | Network Access Katmanı | Fiziksel ve veri iletimini kapsar, LAN/WAN üzerinde çalışır |

---

## Neden TCP/IP Modeli?

- İnternetin temel protokol mimarisidir ve tüm ağ cihazları tarafından desteklenir.  
- OSI modelinin teorik yapısına göre daha **pratik ve uygulanabilir** bir yapı sunar.  
- Taşıma ve internet katmanları sayesinde verilerin doğru ve güvenli şekilde iletilmesini garanti eder.  

---
# TCP/IP Modeli 
<img width="700" height="394" alt="image" src="https://github.com/user-attachments/assets/0a6ac8e8-0d27-46d7-8767-503f4ff8874a" />

TCP/IP modeli dört katmandan oluşur ve her katman farklı bir görevi üstlenir. Katmanlar, verinin uçtan uca güvenli, doğru ve düzenli şekilde iletilmesini sağlar.

---
## 1. Application Katmanı (Uygulama Katmanı)

> **Görevleri:**  
> - Kullanıcının doğrudan etkileşimde bulunduğu katmandır.  
> - Uygulamalar arası veri alışverişini sağlar.  
> - Veriyi uygun formata dönüştürür ve alt katmana iletir.  
> - OSI modelindeki Uygulama, Sunum ve Oturum katmanlarının işlevlerini kapsar.
>
> **Örnek Protokoller ve İşlevleri:**  
> - **HTTP / HTTPS:** Web tabanlı izleme yazılımı ile DAG sunucusu arasında veri iletimi  
> - **FTP:** DAG sisteminden ölçüm veya görüntü verilerini merkezi sunucuya aktarım  
> - **SMTP / IMAP:** Sistem uyarıları veya hata bildirimlerinin e-posta ile iletilmesi  
> - **DNS:** DAG cihazlarının ağ adları ile tanımlanması
>
> **DAG Örneği – Kullanıcı Senaryosu:**  
> 1. Astronom gözlemci, DAG teleskobundan gelen görüntü verilerini kontrol yazılımında görmek istiyor.  
> 2. Uygulama katmanı, gözlemcinin talebini veri paketi hâline getirir.  
> 3. HTTP veya FTP protokolü kullanılarak veri iletimi için alt katmana aktarılır.
>
> **Notlar:**  
> - Bu katman veriyi **hazırlar ve alt katmana teslim eder**, verinin güvenli veya eksiksiz iletilmesi alt katmanların sorumluluğundadır.  
> - Kullanıcının deneyimi doğrudan bu katmandan etkilenir; örneğin yazılımın arayüzü veya veri talep mekanizması.

---
## 2. Transport Katmanı (Taşıma Katmanı)

> **Görevleri:**  
> - Verinin **uçtan uca iletimini** sağlar.  
> - Paketlerin doğru sırayla ve eksiksiz olarak ulaşmasını garanti eder.  
> - Hata tespiti yapar; kaybolan veya hatalı paketleri yeniden iletir.
>
> **Örnek Protokoller ve İşlevleri:**  
> - **TCP (Transmission Control Protocol):** Güvenilir veri iletimi sağlar, paketlerin eksiksiz ve doğru sırada ulaşmasını garanti eder.  
> - **UDP (User Datagram Protocol):** Daha hızlı iletim sağlar, hata kontrolü yapmaz; gerçek zamanlı veri (video, sensör akışı) için uygundur.
>
> **DAG Örneği – Kullanıcı Senaryosu:**  
> 1. Application katmanından gelen DAG görüntü verisi, TCP paketlerine bölünür.  
> 2. Paketler ağ üzerinden DAG kontrol yazılımına iletilir.  
> 3. Taşıma katmanı, eksik veya hatalı paketleri tespit eder ve gerekirse yeniden gönderir.  
> 4. Hedef cihaz, tüm paketleri birleştirir ve veriyi üst katmanlara iletir.
>
> **Notlar:**  
> - Taşıma katmanı, verinin **doğru ve eksiksiz ulaşmasını** sağlar; uygulama katmanı bunu bilmek zorunda değildir.  
> - DAG yerleşkesinde, teleskop görüntüleri veya AO sisteminden gelen ölçümler bu katman sayesinde **hatasız şekilde** yazılım arayüzüne ulaşır.  
> - UDP kullanıldığında hız öncelikli, güvenlik ve sıralama ikincil olabilir; örneğin gerçek zamanlı sensör akışı için tercih edilebilir.

---
## 3. Internet Katmanı (İnternet Katmanı)

> **Görevleri:**  
> - Veriyi kaynak cihazdan hedef cihaza yönlendirir.  
> - IP adreslerini kullanarak cihazlar arası rotayı belirler.  
> - Paketlerin farklı ağlardan geçmesini ve doğru hedefe ulaşmasını sağlar.
>
> **Örnek Protokoller ve İşlevleri:**  
> - **IP (Internet Protocol):** Paketleri hedef IP adresine yönlendirir.  
> - **ICMP (Internet Control Message Protocol):** Hata mesajları ve durum bildirimleri gönderir.  
> - **ARP (Address Resolution Protocol):** IP adreslerini fiziksel MAC adresine çevirir.
>
> **DAG Örneği – Kullanıcı Senaryosu:**  
> 1. Taşıma katmanından gelen TCP paketleri, hedef DAG kontrol yazılımının IP adresine yönlendirilir.  
> 2. Paketler ağ cihazları (router, switch) üzerinden doğru rotayı izleyerek hedefe ulaşır.  
> 3. Eğer yol üzerinde bir hata veya yönlendirme problemi olursa, ICMP ile durum bildirimi yapılır.  
> 4. Hedef cihaz paketleri alır ve üst katmana (Transport) iletir.
>
> **Notlar:**  
> - Internet katmanı **paketlerin doğru yolda ilerlemesini** sağlar, verinin içeriğini değiştirmez.  
> - DAG yerleşkesinde farklı cihazlar (AO sistemi, kameralar, kontrol bilgisayarı) arasında veri akışı bu katmana bağlıdır.  
> - IP adresleme ve routing, verinin karmaşık ağlar üzerinden sorunsuz iletilmesi için kritik öneme sahiptir.

---
## 4. Network Access Katmanı (Ağ Erişim Katmanı)

> **Görevleri:**  
> - Paketleri fiziksel ağ üzerinden iletir.  
> - Veri çerçeveleri (frames) oluşturur ve MAC adreslerini kullanır.  
> - Hata tespiti ve düzeltme mekanizmalarını uygular.
>
> **Örnek Protokoller ve Donanım:**  
> - **Ethernet:** LAN üzerinden veri iletimi, çerçeve ve MAC adresleme  
> - **Wi-Fi:** Kablosuz veri iletimi  
> - **PPP (Point-to-Point Protocol):** İki cihaz arasında doğrudan bağlantı  
> - **Switch / Bridge protokolleri:** Ağ trafiğini yönetir ve çerçeveleri yönlendirir
>
> **DAG Örneği – Kullanıcı Senaryosu:**  
> 1. Internet katmanından gelen paketler, çerçeve formatına dönüştürülür ve hedef cihazın MAC adresi eklenir.  
> 2. LAN, Wi-Fi veya fiber optik kablolar üzerinden DAG kontrol yazılımına iletilir.  
> 3. Switch veya bridge gibi ağ cihazları doğru cihazı bulur ve veriyi aktarır.  
> 4. Hatalı çerçeveler tespit edilirse yeniden gönderilir.
>
> **Notlar:**  
> - Network Access katmanı, verinin **fiziksel ortam üzerinden güvenli ve düzenli iletiminden** sorumludur.  
> - DAG yerleşkesinde AO sistemi, kameralar ve kontrol bilgisayarı arasındaki veri akışı bu katmanın düzgün çalışmasına bağlıdır.  
> - Fiziksel iletim sırasında veri, bit seviyesinde (0 ve 1) aktarılır; veri içeriği bu katmanda işlenmez.

## Örnek Senaryo

Düşünün ki bir gözlemci, uzaktan bir teleskop sisteminden **ölçüm veya görüntü verisi** almak istiyor. Bu durumda TCP/IP modeli üzerinden veri akışı şu şekilde gerçekleşir:  

1. **Application Katmanı:**  
   - Gözlemci, yazılım arayüzünden veri talep eder.  
   - Gönderilecek veri türü ve formatı belirlenir.  

2. **Transport Katmanı:**  
   - Veri TCP paketlerine bölünür.  
   - Paketlerin eksiksiz ve doğru sırada ulaşması sağlanır; hatalı paketler tekrar gönderilir.  

3. **Internet Katmanı:**  
   - Paketler hedef cihazın IP adresine yönlendirilir.  
   - Gerekirse farklı ağlardan geçerek doğru rotayı izler.  

4. **Network Access Katmanı:**  
   - Paketler fiziksel ağ üzerinden iletilir (LAN, kablo, Wi-Fi vb.).  
   - Bitler fiziksel ortam üzerinden aktarılır ve üst katmanlar veriyi işler.  

Bu örnek, TCP/IP katmanlarının görevlerini **gerçek bir veri talebi bağlamında** gösterir ve katmanlar arası işleyişi daha anlaşılır hâle getirir.

