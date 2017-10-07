---
title: "aaaCryptography - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Azaltıcı Etkenler hello tehdit modelleme Aracı kullanıma sunulan tehditleri"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Güvenlik çerçevesi: Şifreleme | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Web uygulaması** | <ul><li>[Yalnızca onaylanan simetrik bloğu şifreler ve anahtar uzunluklarını kullanın](#cipher-length)</li><li>[Blok şifreleme modları ve simetrik şifre başlatma vektörleri kullanım onaylanır](#vector-ciphers)</li><li>[Onaylanan Asimetrik algoritmalar, anahtar uzunlukları ve doldurma kullanın](#padding)</li><li>[Onaylanan rastgele sayı oluşturucuları kullanma](#numgen)</li><li>[Simetrik akış şifrelemeleri kullanmayın](#stream-ciphers)</li><li>[Onaylanan MAC/HMAC/anahtarlı karma algoritmaları kullan](#mac-hash)</li><li>[Yalnızca onaylanan şifreleme karma işlevlerini kullanma](#hash-functions)</li></ul> |
| **Veritabanı** | <ul><li>[Güçlü şifreleme algoritmaları tooencrypt veri hello veritabanında kullanın](#strong-db)</li><li>[SSIS paketleri şifrelenir ve dijital olarak imzalanmış](#ssis-signed)</li><li>[Dijital imza toocritical veritabanı güvenliği sağlanabilir öğeler ekleme](#securables-db)</li><li>[SQL server EKM tooprotect şifreleme anahtarları kullanın](#ekm-keys)</li><li>[Şifreleme anahtarları gösterilen tooDatabase altyapısı olmamalıdır olursa AlwaysEncrypted özelliğini kullanın](#keys-engine)</li></ul> |
| **IOT cihaz** | <ul><li>[IOT cihaz üzerinde şifreleme anahtarlarını güvenli bir şekilde saklayın](#keys-iot)</li></ul> | 
| **IOT bulut ağ geçidi** | <ul><li>[Kimlik doğrulama tooIoT Hub için yeterli uzunlukta rastgele simetrik anahtar oluşturma](#random-hub)</li></ul> | 
| **Dynamics CRM mobil istemcisi** | <ul><li>[Bir cihaz yönetim ilkesi kullanım PIN gerektirir ve Uzaktan sağlayan yerinde silme emin olun](#pin-remote)</li></ul> | 
| **Dynamics CRM Outlook istemcisi** | <ul><li>[Bir cihaz yönetim ilkesi, bir parola/PIN/otomatik kilit gerektirir ve tüm verileri (örneğin Bitlocker) şifreler yerinde olduğundan emin olun](#bitlocker)</li></ul> | 
| **Kimlik sunucusu** | <ul><li>[İmzalama anahtarları kimlik sunucusu kullanırken alınır emin olun](#rolled-server)</li><li>[Şifreleme açısından güçlü bir istemci kimliği, gizli olmasını kimlik sunucusunda kullanılan](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Yalnızca onaylanan simetrik bloğu şifreler ve anahtar uzunluklarını kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Ürünler, yalnızca şifreleri simetrik engelleme ve açıkça hello Crypto Danışmanı kuruluşunuzdaki tarafından onaylanan ilişkili anahtar uzunluklarını kullanmanız gerekir. Microsoft onaylı simetrik algoritmaları blok şifrelemeler aşağıdaki hello şunlardır:</p><ul><li>AES-128, 192 AES ve AES 256 için yeni kod kabul edilebilir</li><li>Var olan kodu ile geriye dönük uyumluluk için üç anahtar 3DES kabul edilebilir</li><li>Ürünler için simetrik blok şifrelemeler kullanma:<ul><li>Gelişmiş Şifreleme Standardı (AES) için yeni kod gereklidir</li><li>Üç anahtar Üçlü Veri Şifreleme Standardı (3DES) geriye dönük uyumluluk için var olan kodda izin verilir</li><li>RC2, DES, 2 anahtarı 3DES, DESX ve Skipjack, de dahil olmak üzere tüm diğer blok şifrelemeleri, yalnızca eski verilerin şifresini çözmek için kullanılabilir ve şifreleme için kullanılan konulmalıdır</li></ul></li><li>Simetrik blok şifreleme algoritmaları için 128 bit minimum anahtar uzunluğu gereklidir. için yeni kod önerilen blok şifreleme algoritması AES yalnızca hello (AES-128, 192 AES ve AES 256 tüm kabul edilebilir)</li><li>Üç anahtar 3DES var olan kodda zaten kullanımda, şu anda kabul edilebilir; geçiş tooAES önerilir. DES, DESX, RC2 ve Skipjack artık güvenli olarak kabul edilir. Bu algoritmalar yalnızca hello artırmak amacıyla geriye dönük uyumluluk için varolan verilerin şifresini çözmek için kullanılabilir ve veriler bir önerilen blok şifreleme kullanarak yeniden şifrelenmelidir</li></ul><p>Lütfen tüm simetrik blok şifrelemeler uygun başlatma vektörü (IV) kullanılmasını gerektiren bir onaylanan şifreleme modu ile kullanılması gerektiğini unutmayın. Uygun bir IV. genellikle rastgele bir sayı ve hiçbir zaman sabit bir değer</p><p>Kuruluşunuzun Crypto Panosu gözden geçirdikten sonra eski veya başka türlü onaylanmamış şifreleme algoritmalarının ve daha küçük anahtar uzunluğu hello kullan (olarak karşılıklı toowriting yeni veri) var olan verileri okumak için izin verilir. Ancak, bu gereksinim karşı bir özel durum için dosya gerekir. Ayrıca, zayıf şifreleme kullanılan tooread veriler olduğunda enterprise dağıtımlarda, uyarı Yöneticiler ürünleri düşünmelisiniz. Bu tür uyarılar, açıklayıcı ve eyleme dönüştürülebilir olmalıdır. Bazı durumlarda, uygun toohave Grup İlkesi denetimi hello zayıf şifreleme kullanımını olabilir</p><p>İzin verilen .NET algoritmaları yönetilen şifre çeviklik (tercih sırasına göre)</p><ul><li>AesCng (FIPS uyumlu)</li><li>AuthenticatedAesCng (FIPS uyumlu)</li><li>AESCryptoServiceProvider (FIPS uyumlu)</li><li>AESManaged (FIPS-uyumlu olmayan)</li></ul><p>Bu algoritmalar hiçbiri hello belirtilebilir lütfen unutmayın `SymmetricAlgorithm.Create` veya `CryptoConfig.CreateFromName` değişiklikleri toohello machine.config dosyasının yapmadan yöntemleri. Ayrıca, önceki too.NET .NET 3.5 sürümleri AES adlandırdığınız unutmayın `RijndaelManaged`, ve `AesCng` ve `AuthenticatedAesCng` olan > CodePlex aracılığıyla kullanılabilir ve işletim sistemi temelindeki hello CNG gerektirir</p>

## <a id="vector-ciphers"></a>Blok şifreleme modları ve simetrik şifre başlatma vektörleri kullanım onaylanır

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Tüm simetrik blok şifrelemeler onaylanan simetrik şifreleme modu ile kullanılması gerekir. yalnızca onaylanan hello modları CBC ve CTS'dır. Özellikle, işlem hello elektronik kod kitap (ECB) modu kaçınılmalıdır; Kuruluşunuzun Crypto Panosu gözden ECB kullanımını gerektirir. OFB, CFB, CTRL, CCM ve GCM tüm kullanımını veya başka bir şifreleme modu, kuruluşunuzun Crypto Kurulunca gözden geçirilmesi gerekir. Yeniden kullanma, hello aynı başlatma vektörü (IV) "akış modları, CTRL gibi şifrelemeleri" içinde blok şifrelemeler ortaya şifrelenmiş veriler toobe neden olabilir. Tüm simetrik blok şifrelemeler da bir uygun başlatma vektörü (IV) kullanılması gerekir. Uygun bir IV şifreleme açısından güçlü, rastgele ve hiçbir zaman sabit bir değer sayısıdır. |

## <a id="padding"></a>Onaylanan Asimetrik algoritmalar, anahtar uzunlukları ve doldurma kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Merhaba Engellenenler şifreleme algoritmalarının kullanımını önemli riski tooproduct güvenlik tanıtır ve kaçınılması gerekir. Ürünler ve ilişkili kuruluşunuzun Crypto Kurulunca açıkça onaylanmasını anahtar uzunlukları ve doldurma yalnızca bu şifreleme algoritmaları kullanmanız gerekir.</p><ul><li>**RSA -** şifreleme, anahtar değişimi ve imza için kullanılabilir. RSA Şifreleme yalnızca hello OAEP veya RSA KEM doldurma modu kullanmanız gerekir. Var olan kodu modu yalnızca uyumluluk için doldurma PKCS #1 v1.5 kullanabilir. Null doldurma kullanımını açıkça yasaklanmış. Anahtarları > 2048 bit = için yeni kod gereklidir. Var olan kodu anahtarlarını < için 2048 bit yalnızca geriye dönük uyumluluk bir gözden geçirme, kuruluşunuzun Crypto Panosu tarafından sonra destekleyebilir. Anahtarları < 1024 bit yalnızca şifre çözme ve doğrulama eski verileri için kullanılabilir ve değiştirilen IF şifreleme veya imzalama işlemleri için kullanılması gerekir</li><li>**ECDSA -** yalnızca imza için kullanılan. İle ECDSA > 256 bit anahtara = için yeni kod gereklidir. ECDSA dayanan imzalar hello üç NIST onaylanmış eğrilerden birini kullanmalıdır (p-256, p-384 ya da P521). Baştan sona analiz Eğriler yalnızca bir gözden geçirme, kuruluşunuzun Crypto panosu ile sonra kullanılabilir.</li><li>**ECDH -** yalnızca anahtar değişimi için kullanılabilir. İle ECDH > 256 bit anahtara = için yeni kod gereklidir. Anahtar değişimi ECDH tabanlı hello üç NIST onaylanmış eğrilerden birini kullanmalıdır (p-256, p-384 ya da P521). Baştan sona analiz Eğriler yalnızca bir gözden geçirme, kuruluşunuzun Crypto panosu ile sonra kullanılabilir.</li><li>**DSA -** sonra gözden geçirin ve kuruluşunuzun Crypto Panosu onayını kabul edilebilir olabilir. Güvenlik Danışmanı tooschedule kuruluşunuzun Crypto Panosu gözden başvurun. DSA kullanımınız onaylanırsa az 2048 bit uzunluğunda anahtarları tooprohibit kullanımını gerektiğine dikkat edin. CNG Windows 8'dan sonra anahtar uzunluğu 2048 bit ve büyük destekler.</li><li>**Diffie-Hellman -** oturum anahtar yönetimi için yalnızca kullanılabilir. Anahtar uzunluğu > 2048 bit = için yeni kod gereklidir. Var olan kodu anahtar uzunluklarını < için 2048 bit yalnızca geriye dönük uyumluluk bir gözden geçirme, kuruluşunuzun Crypto Panosu tarafından sonra destekleyebilir. Anahtarları < 1024 bit kullanılamaz.</li><ul>

## <a id="numgen"></a>Onaylanan rastgele sayı oluşturucuları kullanma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Ürünler onaylanan rastgele sayı oluşturucuları kullanmanız gerekir. Geçici rastgele işlevleri hello C çalışma zamanı işlevi rand, hello .NET Framework sınıf System.Random veya GetTickCount gibi sistem işlevleri gibi bu nedenle, hiçbir zaman böyle kodda kullanılmalıdır. Merhaba çift Eliptik Eğri rastgele sayı oluşturucu (DUAL_EC_DRBG) algoritması engellendi</p><ul><li>**CNG -** BCryptGenRandom (Merhaba çağıran [PASSIVE_LEVEL] 0'dan büyük herhangi IRQL konumunda çalışabilir sürece önerilen hello BCRYPT_USE_SYSTEM_PREFERRED_RNG bayrağı kullanın)</li><li>**CAPI -** cryptGenRandom</li><li>**Win32/64-** (yeni uygulamalar kullanması gereken BCryptGenRandom veya CryptGenRandom) RtlGenRandom * rand_s * SystemPrng (için çekirdek modu)</li><li>**. NET -** RNGCryptoServiceProvider veya RNGCng</li><li>**Windows mağazası uygulamaları -** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom veya. GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef rasgele size_t sayısı, uint8_t *bayt)</li><li>**Apple OS X (< 10.7)-** kullanım / Geliştirme/rastgele tooretrieve rastgele sayılar</li><li>**Java(including Google Android Java Code) -** java.security.SecureRandom sınıfı. (Jelly Çekirdeklere) Android 4.3 için geliştiricilere gerekir Android geçici çözüm önerilen hello izleyin ve kendi uygulamalarını tooexplicitly güncelleştirme unutmayın hello PRNG entropi /dev/urandom veya /dev/random ile başlatma</li></ul>|

## <a id="stream-ciphers"></a>Simetrik akış şifrelemeleri kullanmayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | RC4 gibi simetrik akış şifrelemeleri kullanılmamalıdır. Simetrik akış şifrelemeleri yerine ürünleri blok şifre, özellikle AES en az 128 bit anahtar uzunluğu ile kullanmanız gerekir. |

## <a id="mac-hash"></a>Onaylanan MAC/HMAC/anahtarlı karma algoritmaları kullan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Ürünler, ileti kimlik doğrulama kodu (MAC) veya karma tabanlı ileti kimlik doğrulama kodu (HMAC) algoritmaları onaylanmış yalnızca kullanmanız gerekir.</p><p>Bir ileti kimlik doğrulama kodu (MAC) bir alıcı tooverify hem hello gönderen hello özgünlüğünü ve gizli bir anahtar kullanarak selamlama iletisine hello bütünlüğünü sağlayan bilgi ekli tooa iletisi parçasıdır. Merhaba ya da bir karma tabanlı MAC kullanımını ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) veya [blok şifre tabanlı MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) tüm temel karma veya simetrik şifreleme algoritmaları; kullanımı için onaylanan sürece verilebilir mi şu anda bu içerir (HMAC SHA256, HMAC SHA384 ve SHA512 HMAC) HMAC SHA2 işlevleri hello ve hello CMAC/OMAC1 ve OMAC2 bloğu şifre tabanlı MAC bilgisayarları (bunlar dayalı AES üzerinde).</p><p>HMAC SHA1 kullanımını platform uyumluluğu için izin verilen olabilir, ancak, bir özel durum toothis yordam gerekli toofile olması ve kuruluşunuzun şifre gözden geçirme geçer. 128 bit daha HMAC'ler tooless kesilmesi izin verilmez. Müşteri yöntemleri toohash bir anahtarı ve verileri kullanarak Onaylanmadı ve kuruluşunuzun Crypto Panosu gözden geçirme önceki toouse geçmelerini gerekir.</p>|

## <a id="hash-functions"></a>Yalnızca onaylanan şifreleme karma işlevlerini kullanma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Ürünler hello SHA-2 karma algoritma ailesi, (SHA256, SHA384 ve SHA512) kullanmanız gerekir. Daha kısa bir karma gerekliyse sipariş toofit hello kısa MD5 karma değeri, aklınızda tasarlanan bir veri yapısı içinde 128-bit çıkış uzunluk gibi ürün ekipleriyle hello SHA2 karmaları (genellikle SHA256) birini kesmek. SHA384 SHA512 kesilmiş bir sürümü olduğunu unutmayın. Şifreleme karmalarını kesilmesi daha 128 bit güvenlik amacıyla tooless için izin verilmiyor. Yeni kod hello MD2, MD4, MD5, SHA-0, SHA-1 veya RIPEMD karma algoritmaları kullanmamanız gerekir. Karma çakışmaları, etkili bir şekilde bunları kıran Bu algoritmalar, bilgisayarlarda mümkündür.</p><p>.NET karma algoritmaları yönetilen şifreleme çevikliği için izin verilen (tercih sırasına göre):</p><ul><li>SHA512Cng (FIPS uyumlu)</li><li>SHA384Cng (FIPS uyumlu)</li><li>SHA256Cng (FIPS uyumlu)</li><li>SHA512Managed (FIPS-uyumlu olmayan) (kullanın SHA512 çağrıları tooHashAlgorithm.Create ya da CryptoConfig.CreateFromName algoritması adı olarak)</li><li>SHA384Managed (FIPS-uyumlu olmayan) (SHA384 olarak kullanılması çağrıları tooHashAlgorithm.Create ya da CryptoConfig.CreateFromName algoritma adı)</li><li>SHA256Managed (FIPS-uyumlu olmayan) (SHA256 olarak kullanılması çağrıları tooHashAlgorithm.Create ya da CryptoConfig.CreateFromName algoritma adı)</li><li>SHA512CryptoServiceProvider (FIPS uyumlu)</li><li>SHA256CryptoServiceProvider (FIPS uyumlu)</li><li>SHA384CryptoServiceProvider (FIPS uyumlu)</li></ul>| 

## <a id="strong-db"></a>Güçlü şifreleme algoritmaları tooencrypt veri hello veritabanında kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Bir şifreleme algoritması seçme](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Adımları** | Şifreleme algoritmaları yetkisiz kullanıcılar tarafından kolayca alınamaz veri dönüşümleri tanımlayın. SQL Server kümelerini DES, Üçlü DES, TRIPLE_DES_3KEY, RC2, RC4, 128-bit RC4'ü, DESX, 128 bit AES, 192 bit AES ve 256 bit AES gibi birkaç algoritmaları Yöneticiler ve geliştiriciler toochoose sağlar |

## <a id="ssis-signed"></a>SSIS paketleri şifrelenir ve dijital olarak imzalanmış

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Merhaba dijital imzalarla paketlerin kaynak tanımlamak](https://msdn.microsoft.com/library/ms141174.aspx), [tehdit ve güvenlik açığı azaltma (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Adımları** | Merhaba bir paketin hello tek tek veya hello paketi oluşturan kuruluşun kaynağıdır. Bilinmeyen veya güvenilmeyen bir kaynaktan bir paketi çalıştıran riskli olabilir. tooprevent yetkisiz SSIS paketleri izinsiz dijital imzalar kullanılmalıdır. Ayrıca, tooensure hello gizliliği depolama/aktarım sırasında hello paketlerin SSIS paketleri şifrelenmiş toobe sahip |

## <a id="securables-db"></a>Dijital imza toocritical veritabanı güvenliği sağlanabilir öğeler ekleme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [İmza (Transact-SQL) Ekle](https://msdn.microsoft.com/library/ms181700) |
| **Adımları** | Bir kritik veritabanı güvenliği sağlanabilir hello bütünlüğünü doğrulandı toobe sahip olduğu durumlarda, dijital imzalar kullanılmalıdır. Veritabanı güvenliği sağlanabilir öğelerle saklı yordam, işlev, derleme veya tetikleyici gibi dijital olarak imzalanabilir. Bu yararlı olabilir, bir örneği aşağıda verilmiştir: ISV (bağımsız yazılım satıcısı) destek tooa teslim yazılım tooone müşterilerinin sağlanan bize söyleyin. Destek sağlamadan önce hello ISV hello yazılımda güvenliği sağlanabilir bir veritabanı yanlışlıkla veya kötü amaçlı bir girişim tarafından değiştirilmediğini tooensure istersiniz. Hello güvenliği sağlanabilir dijital olarak imzalı değilse hello ISV dijital imzasını doğrulamak ve bütünlüğünü doğrulayamadı.| 

## <a id="ekm-keys"></a>SQL server EKM tooprotect şifreleme anahtarları kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [SQL Server Genişletilebilir anahtar yönetimi (EKM)](https://msdn.microsoft.com/library/bb895340), [Azure anahtar kasası (SQL Server) kullanarak Genişletilebilir anahtar yönetimi](https://msdn.microsoft.com/library/dn198405) |
| **Adımları** | SQL Server Genişletilebilir anahtar yönetimi akıllı kart, USB aygıtı veya EKM/HSM modülü gibi devre dışı bir aygıt depolanan hello veritabanı dosyaları toobe korumak hello şifreleme anahtarları sağlar. Bu ayrıca Veritabanı Yöneticileri (dışında hello sysadmin grubunun üyeleri) karşı veri koruması sağlar. Yalnızca hello veritabanı kullanıcının erişim tooon hello dış EKM/HSM modülü olduğunu şifreleme anahtarları kullanılarak veri şifrelenebilir. |

## <a id="keys-engine"></a>Şifreleme anahtarları gösterilen tooDatabase altyapısı olmamalıdır olursa AlwaysEncrypted özelliğini kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure, OnPrem |
| **Öznitelikleri**              | SQL sürümü - V12, MsSQL2016 |
| **Başvuruları**              | [(Veritabanı altyapısı) her zaman şifreli](https://msdn.microsoft.com/library/mt163865) |
| **Adımları** | Her zaman şifreli Azure SQL Database veya SQL Server veritabanlarına depolanan bir özellik tasarlanmış tooprotect benzeri gizli verilerin kredi kartı numaraları veya Ulusal tanımlama numaraları (örneğin ABD sosyal güvenlik numarası), ' dir. Her zaman şifreli tooencrypt hassas verileri istemci uygulamalar içinde istemcilerin ve hiçbir zaman hello şifreleme anahtarları toohello (SQL veritabanı veya SQL Server) veritabanı altyapısı ortaya. Sonuç olarak, her zaman şifreli kullanıcılar kendi hello verileri (ve görüntüleyebileceğini) arasında ayırmayı sağlar ve kişilere hello verileri yönetme (ancak hiçbir erişimi olması gerekir) |

## <a id="keys-iot"></a>IOT cihaz üzerinde şifreleme anahtarlarını güvenli bir şekilde saklayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Cihaz işletim sistemi - Windows IOT Core, cihaz bağlantısı - Azure IOT cihaz SDK'ları |
| **Başvuruları**              | [Windows IOT Core TPM'de](https://developer.microsoft.com/windows/iot/docs/tpm), [Windows IOT Core TPM'de ayarlama](https://developer.microsoft.com/windows/iot/win10/setuptpm), [Azure IOT cihaz SDK'sı TPM](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **Adımları** | Simetrik ya da sertifika özel anahtarlarını güvenli bir donanım TPM veya akıllı kart yongaları gibi depolama korumalı. Windows 10 IOT Core hello kullanıcı bir TPM destekler ve kullanılabilecek birkaç uyumlu TPM'ler: https://developer.microsoft.com/windows/iot/win10/tpm. Bu bellenim veya ayrık TPM toouse önerilir. Bir yazılım TPM yalnızca geliştirme ve sınama amacıyla kullanılmalıdır. TPM kullanılabilir ve hello anahtarları sağlanan sonra hello belirteci oluşturur hello kodu içindeki herhangi bir önemli bilgi sabit kodlama olmadan yazılması gerekir. | 

### <a name="example"></a>Örnek
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Görüldüğü gibi hello aygıt birincil anahtarı hello kodda mevcut değil. Bunun yerine, hello TPM yuva 0 konumunda depolanır. TPM aygıtı oluşturan bir kısa süreli ise SAS belirteci tooconnect toohello IOT hub'ı kullanılır. 

## <a id="random-hub"></a>Kimlik doğrulama tooIoT Hub için yeterli uzunlukta rastgele simetrik anahtar oluşturma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ağ geçidi seçim - Azure IOT Hub |
| **Başvuruları**              | Yok  |
| **Adımları** | IOT Hub cihaz kimlik kayıt defteri içerir ve bir cihaz sağlarken, otomatik olarak rastgele bir simetrik anahtar oluşturur. Bu özellik hello Azure IOT Hub kimlik kayıt defteri toogenerate hello anahtar kimlik doğrulaması için kullanılan toouse önerilir. IOT hub'ı da hello aygıt oluşturulurken belirtilen bir anahtar toobe sağlar. Bir anahtarı dışında IOT Hub cihaz sağlama işlemi sırasında oluşturulur, bu ise rastgele bir simetrik anahtar veya en az 256 bit toocreate önerilir. |

## <a id="pin-remote"></a>Bir cihaz yönetim ilkesi kullanım PIN gerektirir ve Uzaktan sağlayan yerinde silme emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM mobil istemcisi | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Bir cihaz yönetim ilkesi kullanım PIN gerektirir ve Uzaktan sağlayan yerinde silme emin olun |

## <a id="bitlocker"></a>Bir cihaz yönetim ilkesi, bir parola/PIN/otomatik kilit gerektirir ve tüm verileri (örneğin Bitlocker) şifreler yerinde olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM Outlook istemcisi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Bir cihaz yönetim ilkesi, bir parola/PIN/otomatik kilit gerektirir ve tüm verileri (örneğin Bitlocker) şifreler yerinde olduğundan emin olun |

## <a id="rolled-server"></a>İmzalama anahtarları kimlik sunucusu kullanırken alınır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Kimlik sunucusu - anahtarları, imzalar ve şifreleme](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **Adımları** | İmzalama anahtarları kimlik sunucusu kullanırken alınır emin olun. Merhaba başvurular bölümündeki Hello bağlantıyı nasıl bu kimlik sunucusuna bağlı olan kesintileri tooapplications neden olmadan planlanmalıdır açıklanmaktadır. |

## <a id="client-server"></a>Şifreleme açısından güçlü bir istemci kimliği, gizli olmasını kimlik sunucusunda kullanılan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Şifreleme açısından güçlü bir istemci kimliği, gizli olmasını kimlik sunucusunda kullanılan. bir istemci kimliği ve parolası oluşturulurken yönergeleri izleyerek hello kullanılmalıdır:</p><ul><li>Rastgele bir GUID hello istemci kimliği oluşturun.</li><li>Şifreleme açısından rastgele bir 256 bit anahtar hello gizlilik olarak oluştur</li></ul>|
