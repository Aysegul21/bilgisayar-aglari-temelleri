# HTTP Protokolü

<img width="1938" height="1116" alt="image" src="https://github.com/user-attachments/assets/1375bc4e-9bb8-4651-a93c-dc394d4dfb25" />

---

## 1. HTTP Nedir?

HTTP (**HyperText Transfer Protocol**), internet üzerindeki **istemci (client)** ve **sunucu (server)** arasında veri iletimini sağlayan bir **uygulama katmanı protokolüdür**. Web tarayıcıları (Chrome, Firefox vb.) ile web sunucuları arasında iletişimi sağlar ve internetin en yaygın kullanılan protokolüdür.

**Örnek:** Atatürk Üniversitesi Astrofizik Araştırma ve Uygulama Merkezi’nin (ATASAM) web sitesine [https://atasam.atauni.edu.tr/](https://atasam.atauni.edu.tr/) bağlanıldığında, tarayıcı ile sunucu arasındaki iletişim HTTP üzerinden gerçekleşir. Kullanıcı anasayfayı ziyaret ettiğinde tarayıcı bir **HTTP isteği (request)** gönderir ve sunucu bir **HTTP yanıtı (response)** döner.

---

## 2. HTTP’nin Çalışma Prensibi

HTTP, istemci (tarayıcı) ve sunucu arasındaki veri iletimini aşağıdaki aşamalarla gerçekleştirir:
### 2.1 Bağlantı Kurulması

Tarayıcı, sunucuya TCP bağlantısı kurar. Bu işlem, üçlü el sıkışma (three-way handshake) ile gerçekleşir.

Eğer bağlantı HTTPS üzerinden ise, TCP bağlantısı kurulduktan sonra TLS/SSL handshake gerçekleşir; böylece veri şifrelenir ve güvenli bir iletişim kanalı oluşturulur.

Modern tarayıcılar, performansı artırmak için keep-alive connection (HTTP persistent connection) kullanır; böylece birden fazla HTTP isteği aynı TCP bağlantısı üzerinden gönderilebilir.

HTTP için varsayılan port 80, HTTPS için 443’tür.

HTTP/2 ve HTTP/3 sürümleri, bağlantıyı daha verimli yönetir; multiplexing ile aynı bağlantıda paralel istekler yapılabilir ve gecikmeler azaltılır.

---

### 2.2 İstek Gönderme (Request)

İstemci, sunucuya bir HTTP isteği yollar. Örnek **GET isteği**:

```
GET /duyurular HTTP/1.1
Host: atasam.atauni.edu.tr
User-Agent: Mozilla/5.0
Accept: text/html
```

* **GET /duyurular** → "duyurular" sayfasının talebi
* **Host** → Hedef sunucu adresi
* **User-Agent** → Tarayıcı bilgisi; sunucuya cihaz ve tarayıcı uyumluluğu hakkında bilgi verir
* **Accept** → İstemcinin kabul edebileceği veri türü

*Not:* HTTP’de GET dışında **POST, PUT, DELETE, PATCH** gibi metodlar da vardır; farklı amaçlarla veri gönderme, güncelleme veya silme işlemleri için kullanılır.

---

### 2.3 Sunucunun İşlemesi

Sunucu, gelen HTTP isteğini alır ve işler. Bu aşamada şu işlemler yapılabilir:

* **Statik içerik sunma:** Daha önce hazırlanmış HTML, CSS, JS veya medya dosyaları istemciye gönderilir.
* **Dinamik içerik oluşturma:** Sunucu, veritabanı sorguları veya iş mantığı çalıştırarak isteğe özel içerik üretir.
* **Doğrulama ve yetkilendirme:** Gerekirse kullanıcı doğrulaması ve erişim kontrolü uygulanır.
* **Önbellekleme (Caching):** Daha hızlı yanıt vermek için sık kullanılan içerikler geçici olarak saklanabilir.

Sunucu, bu işlemleri tamamladıktan sonra HTTP yanıtını hazırlayıp istemciye gönderir.

---

### 2.4 Yanıt Gönderme (Response)

Sunucu, HTTP yanıtını istemciye iletir. Örnek bir yanıt:

```
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 4521
```

* **200 OK** → İstek başarıyla işlendi
* **Content-Type** → Dönen verinin türü (ör. text/html, application/json)
* **Content-Length** → Verinin boyutu (byte)

*Not:* Yaygın diğer HTTP durum kodları:

* **301 Moved Permanently** → Kalıcı yönlendirme
* **404 Not Found** → İstenen kaynak bulunamadı
* **500 Internal Server Error** → Sunucuda hata oluştu

Sunucu, isteğe bağlı olarak **Set-Cookie**, **Cache-Control** gibi başlıklarla ek bilgiler de gönderebilir.

---
### 2.5 Bağlantının Kapatılması veya Sürdürülmesi

* HTTP/1.1’de varsayılan olarak **Keep-Alive** aktif olup, aynı TCP bağlantısı üzerinden birden fazla istek yapılabilir.
* HTTP/2 ve HTTP/3 sürümleri, bağlantıyı daha verimli yönetir; **multiplexing** sayesinde aynı bağlantıda paralel istekler yapılabilir ve gecikmeler azaltılır.
* İstekler tamamlandıktan sonra sunucu ve istemci bağlantıyı kapatabilir veya yeniden kullanılmak üzere açık bırakabilir.

---

### 2.6 HTTP’nin Temel Özellikleri

* **Stateless (Durumsuz)** → Her HTTP isteği bağımsızdır; sunucu önceki isteği hatırlamaz.
* **Metin Tabanlı** → HTTP mesajları okunabilir düz metindir.
* **Katmanlı Yapı** → TCP/IP üzerinden çalışır; güvenlik için HTTPS kullanılabilir.
* **Genişletilebilir (Extensible)** → Header’lar ve yeni protokol sürümleri ile ek özellikler uygulanabilir.

---

## 3. HTTP İstek ve Yanıt Akışı

ATASAM web sitesinin duyurular sayfasına erişim örneği:

### 3.1 İstek Gönderme

```
GET /duyurular HTTP/1.1
Host: atasam.atauni.edu.tr
User-Agent: Mozilla/5.0
Accept: text/html
```

### 3.2 Yanıt Gönderme

```
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 4521

<!-- HTML içerik: Duyurular sayfası -->
```

### 3.3 Bağlantının Kapanması veya Sürekliliği

İşlem tamamlandıktan sonra bağlantı **Keep-Alive** ile sürdürülür veya kapanır.


### 3.4 Uygulamalı Örnek: curl ile İstek Gönderme

Terminal veya komut satırından ATASAM duyurular sayfasına istek göndermek için:

<img width="812" height="162" alt="image" src="https://github.com/user-attachments/assets/5a35ca71-50d9-4690-9a5a-0bb80c08eea5" />

Resimde görüldüğü gibi:

```
aysegul@aysegul:~$ curl -L https://atasam.atauni.edu.tr/duyurular
<!DOCTYPE html>
<html lan="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Atatürk Üniversitesi Astrofizik Araştırma ve Uygulama Merkezi</title>
```

Bu örnek üzerinden HTTP akışını yorumlayalım:

1. **İstek Gönderme (Request)**

   * `curl -L https://atasam.atauni.edu.tr/duyurular` komutu ile terminalde bir **HTTP GET isteği** gönderiliyor.
   * `-L` parametresi, varsa yönlendirmeleri takip eder.

2. **Sunucunun Yanıtı (Response)**

   * Sunucu, HTTP yanıtını HTML formatında döndürüyor.
   * `<!DOCTYPE html>` → Yanıtın bir HTML belgesi olduğunu gösteriyor.
   * `<html lang="tr">` → Sayfanın dili Türkçe olarak belirlenmiş.
   * `<title>...</title>` → Tarayıcı başlığında görünecek metni içeriyor.

3. **Özetle**

   * Terminal üzerinden yaptığımız basit `curl` isteği, web tarayıcısının yaptığı HTTP iletişimin aynısını gösteriyor.
   * İstek → Sunucu → HTML yanıtı şeklinde HTTP akışını somut olarak gözlemleyebiliyoruz.


---

## 4. HTTP Metodları

HTTP, istemci ile sunucu arasındaki veri alışverişinde farklı türde işlemler yapılmasını sağlayan çeşitli metodlar sunar. En yaygın kullanılanlar şunlardır ve bu metodları anlamak için terminal üzerinden istek gönderip alınan çıktılarla uygulamalı bir şekilde inceleyebiliriz.
### 4.1 GET

* **Amaç:** Sunucudan veri almak.
* **Özellik:** Sunucu üzerinde değişiklik yapmaz (idempotent).
* **Örnek:**

<img width="812" height="162" alt="image" src="https://github.com/user-attachments/assets/5a35ca71-50d9-4690-9a5a-0bb80c08eea5" />


### 4.2 POST

* **Amaç:** Sunucuya veri göndermek ve genellikle yeni kaynak oluşturmak.
* **Örnek:**


<img width="812" height="315" alt="image" src="https://github.com/user-attachments/assets/eb0a3e1d-a9d3-47f1-863d-7245de5f80bd" />


### 4.3 PUT

* **Amaç:** Mevcut bir kaynağı güncellemek veya oluşturmak.
* **Örnek:**


<img width="812" height="249" alt="image" src="https://github.com/user-attachments/assets/567dd3de-f2b6-4577-a183-87c93d79c56e" />


### 4.4 DELETE

* **Amaç:** Sunucudaki bir kaynağı silmek.
* **Örnek:**


<img width="812" height="249" alt="image" src="https://github.com/user-attachments/assets/e2b725aa-4d3c-4525-85ca-77cf42715c69" />


### 4.5 HEAD

* **Amaç:** Yalnızca yanıt başlıklarını almak; içerik gelmez.
* **Örnek:**


<img width="812" height="169" alt="image" src="https://github.com/user-attachments/assets/7524d381-8a66-4977-ab32-28fff397f310" />


### 4.6 PATCH

* **Amaç:** Mevcut kaynağın kısmi olarak güncellenmesi.
* **Örnek:**


<img width="812" height="249" alt="image" src="https://github.com/user-attachments/assets/9b1e1f30-95d2-49bd-b10b-b6bffab69867" />

---

## 5. HTTP Durum Kodları

HTTP, istemciden gelen isteklere sunucunun yanıtını **veri** ile birlikte **durum kodları** aracılığıyla da bildirir. Bu kodlar, isteğin başarılı olup olmadığını, yönlendirme gerekip gerekmediğini veya bir hata durumunu anlamamıza yardımcı olur.

Durum kodları **100–599** aralığındadır ve sınıf numarasına göre gruplandırılır:

---

### 1xx – Bilgilendirme (Informational)

İstemciye isteğin alındığını ve işleme devam edildiğini bildirir.
**Örnekler:**

* `100 Continue` → İstek başlıkları alındı, devam edebilir.
* `101 Switching Protocols` → İstemci farklı bir protokole geçebilir.

### 2xx – Başarılı (Success)

İstek başarıyla alındı, anlaşıldı ve işlendi.
**Örnekler:**

* `200 OK` → İstek başarıyla işlendi ve veri döndü.
* `201 Created` → Yeni bir kaynak oluşturuldu.
* `204 No Content` → Başarılı ama geri dönecek içerik yok.

### 3xx – Yönlendirme (Redirection)

İstemciye başka bir konuma yönlendirme yapması gerektiğini bildirir.
**Örnekler:**

* `301 Moved Permanently` → Kaynak kalıcı olarak taşındı; istemci yeni konuma yönlendirilmeli.
* `302 Found` → Kaynak geçici olarak taşındı.
* `307 Temporary Redirect` → Geçici yönlendirme, HTTP yöntemi değişmez.

### 4xx – İstemci Hataları (Client Error)

İstemcinin hatalı bir istek yaptığını gösterir.
**Örnekler:**

* `400 Bad Request` → İstek hatalı veya eksik.
* `401 Unauthorized` → Yetkilendirme gerekli.
* `403 Forbidden` → Erişim yasak.
* `404 Not Found` → İstenen kaynak sunucuda bulunamadı.

### 5xx – Sunucu Hataları (Server Error)

Sunucuda bir sorun oluştuğunu gösterir.
**Örnekler:**

* `500 Internal Server Error` → Sunucu tarafında genel bir hata oluştu.
* `502 Bad Gateway` → Geçersiz yanıt alındı.
* `503 Service Unavailable` → Sunucu geçici olarak hizmet veremiyor.

---

**Terminal Örneği:**

<img width="812" height="156" alt="image" src="https://github.com/user-attachments/assets/294f75b6-57e5-4a2c-8ac4-45b28bcb5cfd" />

> Yukarıdaki örnekte `curl -I` komutuyla sadece HTTP başlıkları alındı. `301 Moved Permanently` durumu, kaynak URL’nin kalıcı olarak başka bir adrese taşındığını gösteriyor. Eğer `-L` seçeneğini kullanırsak, curl otomatik olarak yönlendirmeyi takip eder ve yeni konumdan içeriği getirir.

---

## 6. HTTP Başlıkları (Headers)

HTTP başlıkları, istemci ve sunucu arasında gönderilen **ek bilgi paketleri**dir. Bu başlıklar, isteğin veya yanıtın nasıl işleneceğini, içeriğin türünü, yetkilendirme bilgilerini ve diğer önemli detayları belirtir.

Başlıklar, iki ana gruba ayrılır:

* **Request Headers (İstek Başlıkları)** → İstemcinin sunucuya gönderdiği bilgiler, örneğin hangi veri türlerini kabul ettiği veya hangi tarayıcıyı kullandığı.
* **Response Headers (Yanıt Başlıkları)** → Sunucunun istemciye verdiği bilgiler, örneğin veri tipi, sunucu yazılımı veya yönlendirme adresi.

**Terminal Üzerinden Örnek Kullanım:**

Sadece HTTP başlıklarını almak için:

```
curl -I https://atasam.atauni.edu.tr/duyurular
```

**Örnek Çıktı:**

<img width="812" height="156" alt="image" src="https://github.com/user-attachments/assets/294f75b6-57e5-4a2c-8ac4-45b28bcb5cfd" />

Bu çıktıyı inceleyelim:

* **Server: Apache** → Sunucunun kullandığı yazılımı gösterir.
* **Location** → Eğer kaynak taşınmışsa, yönlendirilecek yeni URL.
* **Content-Type** → Dönen verinin türü (ör. text/html, application/json).

> Bu başlıklar sayesinde istemci, sunucudan gelen veriyi doğru şekilde işleyebilir ve gerekli yönlendirmeleri uygulayabilir.

---

## 7. HTTPS ve Güvenlik
<img width="609" height="345" alt="image" src="https://github.com/user-attachments/assets/f9d7935b-32df-4e1f-8b6e-f0d6aaad996d" />

HTTP’nin güvenli versiyonu olan **HTTPS (HyperText Transfer Protocol Secure)**, istemci ve sunucu arasındaki veri iletimini **şifreleyerek korur**. Bu sayede bilgiler, üçüncü kişiler tarafından okunamaz veya değiştirilemez.

### 7.1 HTTPS’in Temel Özellikleri

* **TLS/SSL Kullanımı** → Veriler, **TLS (Transport Layer Security)** veya eski sürüm **SSL** ile şifrelenir.
* **Veri Gizliliği** → İstemci ile sunucu arasındaki tüm iletişim şifrelenir, üçüncü taraflar tarafından ele geçirilemez.
* **Kimlik Doğrulama** → Sunucunun gerçekliği doğrulanır; sahte sitelere karşı koruma sağlar.
* **Bütünlük (Integrity)** → Verilerin iletim sırasında değiştirilmediği garanti edilir.

### 7.2 Terminal Üzerinden Kontrol Örneği

HTTPS bağlantısını test etmek için terminalde `curl` kullanılabilir:

```
curl -I https://atasam.atauni.edu.tr
```

**Örnek Çıktı:**

<img width="812" height="177" alt="image" src="https://github.com/user-attachments/assets/6f63eb23-8f4b-419a-b576-3cdcb95c8def" />


> Burada HTTP/2 kullanımı ve TLS sayesinde güvenli veri iletimi görülüyor.


---

## 8. HTTP ve HTTPS Arasındaki Farklar

HTTP ve HTTPS, temel olarak veri iletimi için aynı protokolü kullanır, ancak HTTPS **güvenlik katmanı** ekler. Farkları şu şekilde özetleyebiliriz:

| Özellik              | HTTP                                | HTTPS                                                      |
| -------------------- | ----------------------------------- | ---------------------------------------------------------- |
| **Port**             | 80                                  | 443                                                        |
| **Güvenlik**         | Şifreleme yok, veri açık gönderilir | TLS/SSL ile şifrelenir, veri güvenli                       |
| **Kimlik Doğrulama** | Yok                                 | Sunucu doğrulaması yapılır                                 |
| **Veri Bütünlüğü**   | Yok                                 | Veri iletim sırasında değiştirilemez                       |
| **Performans**       | Hafif, hızlı                        | Şifreleme nedeniyle biraz daha fazla işlem gücü gerektirir |

### 8.1 Örnek Terminal Kullanımı

HTTPS’in etkinliğini görmek için aynı URL’yi HTTP ve HTTPS ile kontrol edebiliriz:

```
curl -I http://atasam.atauni.edu.tr
```

```
curl -I https://atasam.atauni.edu.tr
```

**Beklenen Davranış:**

* HTTP isteği çoğu zaman **301 Moved Permanently** yanıtıyla HTTPS’e yönlendirilir.
* HTTPS isteği, doğrudan güvenli bağlantı ile **200 OK** yanıtı döndürür.

> Bu yönlendirme, sitelerin güvenliği artırmak ve veri gizliliğini sağlamak için yaygın olarak uygulanır.

---

## 9. HTTP/2 ve HTTP/3 Protokollerinin Avantajları
<img width="686" height="386" alt="image" src="https://github.com/user-attachments/assets/be124b91-4f2d-45c5-8c11-b4a094a83fc5" />


HTTP’nin daha yeni sürümleri olan **HTTP/2** ve **HTTP/3**, özellikle modern web uygulamalarının performans ve güvenlik ihtiyaçlarını karşılamak için geliştirilmiştir.

### 9.1 HTTP/2

* **Paralel İstekler** → Tek bağlantı üzerinden birden fazla isteğin aynı anda gönderilmesini sağlar (multiplexing).
* **Header Sıkıştırma** → HTTP başlıklarını sıkıştırarak bant genişliğini verimli kullanır.
* **Sunucu İtmesi (Server Push)** → Sunucu, istemcinin ileride ihtiyaç duyabileceği kaynakları önceden gönderebilir.
* **Daha Az Gecikme** → Tek bağlantı üzerinden tüm veri iletimi gecikmeleri azaltır.

### 9.2 HTTP/3

* **UDP Tabanlı** → TCP yerine QUIC protokolü üzerinde çalışır; paket kaybında yeniden iletim daha hızlıdır.
* **Daha Hızlı Bağlantı Kurulumu** → TLS el sıkışması ve QUIC birleşik yapısı sayesinde hızlı açılır.
* **Daha İyi Mobil Performans** → Ağ değişikliklerinde (Wi-Fi → Mobil veri gibi) bağlantı kopmadan devam edebilir.

### 9.3 Özet

| Özellik                   | HTTP/1.1 | HTTP/2     | HTTP/3             |
| ------------------------- | -------- | ---------- | ------------------ |
| **Bağlantı Türü**         | TCP      | TCP        | QUIC (UDP tabanlı) |
| **Paralel İstek**         | Hayır    | Evet       | Evet               |
| **Header Sıkıştırma**     | Hayır    | Evet       | Evet               |
| **Sunucu İtmesi**         | Hayır    | Evet       | Evet               |
| **Bağlantı Kurulma Hızı** | Orta     | Daha hızlı | En hızlı           |
| **Mobil Dayanıklılık**    | Düşük    | Orta       | Yüksek             |

> Modern web siteleri HTTP/2 ve HTTP/3’ü destekleyerek hem hız hem de kullanıcı deneyimi açısından avantaj sağlar.

---

# HTTP Protokolü – Final Özet

HTTP (**HyperText Transfer Protocol**), istemci ile sunucu arasında **veri iletimi ve iletişim** sağlayan bir uygulama katmanı protokolüdür. Temel özellikleri:

* **Stateless (Durumsuz):** Her istek bağımsızdır.
* **Metin tabanlı:** İnsan tarafından okunabilir.
* **Çeşitli metodlar:** GET, POST, PUT, DELETE gibi işlemler yapılabilir.
* **Durum kodları:** 200, 301, 404, 500 gibi yanıtları belirtir.
* **Başlıklar (Headers):** İstek ve yanıtla ilgili ek bilgileri taşır.

**Uygulamalı Örnekler:**

* Terminal üzerinden `curl` komutlarıyla HTTP istekleri gönderebilir ve sunucudan gelen yanıtları görebiliriz.
* `curl -I https://atasam.atauni.edu.tr/duyurular` ile sadece başlıkları alıp yönlendirme ve sunucu bilgilerini inceleyebiliriz.
* `curl -L https://atasam.atauni.edu.tr/duyurular` ile tam sayfa içeriğini alabiliriz.

**Not:** HTTP ile başlayan her bağlantı, günümüzde çoğunlukla HTTPS üzerinden güvenli hale getirilir.
