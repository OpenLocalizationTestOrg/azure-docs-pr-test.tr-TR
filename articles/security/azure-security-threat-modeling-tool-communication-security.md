---
title: "Güvenlik - Microsoft tehdit modelleme aracı - Azure aaaCommunication | Microsoft Docs"
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
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Güvenlik çerçevesi: İletişim güvenliği | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Azure Event hub'ı** | <ul><li>[Güvenli iletişim tooEvent SSL/TLS kullanarak Hub](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Hizmet hesabının ayrıcalıklarını ve özel Services veya ASP.NET sayfaları hello onay CRM'ın güvenlik saygı denetleyin](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[Veri Yönetimi ağ geçidi bağlantı şirket içi SQL Server tooAzure Data Factory sırasında kullanın](#sqlserver-factory)</li></ul> |
| **Kimlik sunucusu** | <ul><li>[Tüm trafiği tooIdentity HTTPS bağlantısı üzerinden sunucusu olduğundan emin olun](#identity-https)</li></ul> |
| **Web uygulaması** | <ul><li>[X.509 sertifikaları tooauthenticate SSL, TLS ve DTLS bağlantıları kullanılan doğrulayın](#x509-ssltls)</li><li>[Azure App Service'te özel etki alanı için SSL sertifikası yapılandırma](#ssl-appservice)</li><li>[Tüm trafiği tooAzure uygulama hizmeti HTTPS bağlantısı üzerinden zorla](#appservice-https)</li><li>[HTTP katı taşıma güvenliği (HSTS) etkinleştir](#http-hsts)</li></ul> |
| **Veritabanı** | <ul><li>[SQL server bağlantı şifreleme ve sertifika doğrulaması emin olun](#sqlserver-validation)</li><li>[Force şifreli iletişim tooSQL sunucusu](#encrypted-sqlserver)</li></ul> |
| **Azure Depolama** | <ul><li>[Depolama HTTPS üzerinden olduğunda bu iletişimi tooAzure emin olun](#comm-storage)</li><li>[HTTPS etkinleştirilirse blob indirdikten sonra MD5 karma değeri doğrulanamıyor](#md5-https)</li><li>[Kullanım SMB 3.0 uyumlu istemci tooensure aktarım sırasında veri şifreleme tooAzure dosya paylaşımları](#smb-shares)</li></ul> |
| **Mobil istemci** | <ul><li>[Sertifika sabitleme uygulama](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[HTTPS enable - aktarım kanalının güvenliğini sağlayın.](#https-transport)</li><li>[WCF: Kümesi ileti güvenlik koruma düzeyi tooEncryptAndSign](#message-protection)</li><li>[WCF: en az ayrıcalıklı hesap toorun WCF hizmeti kullanın.](#least-account-wcf)</li></ul> |
| **Web API** | <ul><li>[Tüm trafiği tooWeb API'leri HTTPS bağlantısı üzerinden zorla](#webapi-https)</li></ul> |
| **Azure Redis Önbelleği** | <ul><li>[Bu iletişim tooAzure Redis önbelleği SSL üzerinden olduğundan emin olun](#redis-ssl)</li></ul> |
| **IOT alan ağ geçidi** | <ul><li>[Aygıt tooField ağ geçidi iletişimin güvenliğini sağlama](#device-field)</li></ul> |
| **IOT bulut ağ geçidi** | <ul><li>[Aygıt tooCloud SSL/TLS kullanarak, ağ geçidi iletişim güvenli](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Güvenli iletişim tooEvent SSL/TLS kullanarak Hub

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Event hub'ı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Adımları** | AMQP veya HTTP bağlantıları tooEvent hub'ı kullanarak SSL/TLS güvenli |

## <a id="priv-aspnet"></a>Hizmet hesabının ayrıcalıklarını ve özel Services veya ASP.NET sayfaları hello onay CRM'ın güvenlik saygı denetleyin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Hizmet hesabının ayrıcalıklarını ve özel Services veya ASP.NET sayfaları hello onay CRM'ın güvenlik saygı denetleyin |

## <a id="sqlserver-factory"></a>Veri Yönetimi ağ geçidi bağlantı şirket içi SQL Server tooAzure Data Factory sırasında kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Data Factory | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Bağlantılı hizmet - Azure ve şirket içi türleri |
| **Başvuruları**              |[Şirket içi ve Azure Data Factory arasında veri taşıma](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [veri yönetimi ağ geçidi](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Adımları** | <p>corpnet veya bir güvenlik duvarının arkasındaysa korumalı gerekli tooconnect toodata kaynaklarını Hello veri yönetimi ağ geçidi (DMG) aracıdır.</p><ol><li>Merhaba makineyi kilitleme hello DMG aracı yalıtır ve zarar veya hello veri kaynak makinede Gözetimi hatalı çalışan programların önler. (Örn. en son güncelleştirmelerin yüklü olmalıdır, etkinleştirme minimum gerekli bağlantı noktaları, denetlenen hesapları sağlama, Denetim etkinse, disk şifreleme etkin vs.)</li><li>Veri ağ geçidi anahtarı sık aralıklarla veya hello DMG hizmet hesabı parolası yeniler her Döndürülmüş gerekir</li><li>Bağlantı hizmeti aracılığıyla veri transits şifrelenmelidir</li></ol> |

## <a id="identity-https"></a>Tüm trafiği tooIdentity HTTPS bağlantısı üzerinden sunucusu olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [IdentityServer3 - anahtarları, imzalar ve şifreleme](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html), [IdentityServer3 - dağıtım](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Adımları** | Varsayılan olarak, HTTPS üzerinden tüm gelen bağlantıları toocome IdentityServer gerektirir. IdentityServer ile iletişim yalnızca güvenli aktarım üzerinden yapılır kesinlikle zorunludur. Bu gereksinim nerede gevşetilebilir SSL boşaltma gibi belirli dağıtım senaryoları vardır. Daha fazla bilgi için hello başvurularda Hello kimlik sunucusunu dağıtım sayfasına bakın. |

## <a id="x509-ssltls"></a>X.509 sertifikaları tooauthenticate SSL, TLS ve DTLS bağlantıları kullanılan doğrulayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>SSL, TLS ve DTLS kullanan uygulamalar, tam olarak hello X.509 sertifikalarını bağlandıkları hello varlıkların doğrulamanız gerekir. Bu doğrulama için hello sertifikaların içerir:</p><ul><li>Etki alanı adı</li><li>Geçerlilik Tarihleri (başlangıç ve sona erme tarihleri)</li><li>İptal durumu</li><li>Kullanım (örneğin, sunucu kimlik doğrulaması sunucuları, istemcileri için istemci kimlik doğrulaması için)</li><li>Güven zinciri. Merhaba platformu tarafından güvenilen veya açıkça hello Yöneticisi tarafından yapılandırılan tooa kök sertifika yetkilisi (CA) sertifikaları zincirine bağlı olmalıdır</li><li>Sertifikanın ortak anahtarı anahtar uzunluğu olmalıdır > 2048 bit</li><li>Karma algoritma SHA256 olmalıdır ve üstü |

## <a id="ssl-appservice"></a>Azure App Service'te özel etki alanı için SSL sertifikası yapılandırma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | EnvironmentType - Azure |
| **Başvuruları**              | [Azure uygulama hizmetinde bir uygulama için HTTPS'yi etkinleştir](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Adımları** | Varsayılan olarak Azure zaten HTTPS hello joker sertifikası ile her uygulama için etkinleştirir *. azurewebsites.net etki alanı. Ancak, tüm joker etki alanları gibi kendi sertifika ile özel bir etki alanı kullanmak kadar güvenli değildir [bakın](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). Hangi dağıtılan hello uygulama üzerinden erişilen hello özel etki alanı için SSL tooenable önerilir.|

## <a id="appservice-https"></a>Tüm trafiği tooAzure uygulama hizmeti HTTPS bağlantısı üzerinden zorla

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | EnvironmentType - Azure |
| **Başvuruları**              | [Azure uygulama Hizmeti'nde HTTPS enforce] https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Adımları** | <p>Azure hello etki alanının joker nitelikli bir sertifikası ile Azure uygulama hizmetleri için HTTPS zaten sağlar ancak *. azurewebsites.net, onu zorla HTTPS. Ziyaretçilerin hala hello uygulamanın güvenliği tehlikeye atabilir HTTP kullanarak hello uygulamaya erişmeyi ve bu nedenle HTTPS açıkça zorunlu toobe sahiptir. ASP.NET MVC uygulamaları hello kullanması gereken [RequireHttps filtre](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) yeniden HTTPS üzerinden gönderilen güvenli olmayan bir HTTP isteği toobe zorlar.</p><p>Alternatif olarak, Azure App Service ile birlikte hello URL yeniden yazma modülü, kullanılan tooenforce HTTPS olabilir. URL yeniden yazma modülü hello istekleri tooyour uygulama edilmeden önce uygulanan tooincoming istekleri geliştiriciler toodefine kuralları etkinleştirir. URL yeniden yazma kuralları Merhaba uygulaması hello kök dizininde depolanmış bir web.config dosyasında tanımlanır</p>|

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnekte tüm gelen trafiği toouse HTTPS zorlayan bir temel URL yeniden yazma kuralı içerir
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Bu kural bir HTTP durum kodu 301 (kalıcı yeniden yönlendirme) döndürerek çalışan bir sayfaya HTTP kullanarak hello kullanıcı isteğinde bulunduğunda. Merhaba 301 yeniden yönlendirmeleri hello isteği toohello hello ziyaretçi aynı URL'ye, HTTPS hello istekle değiştirir hello HTTP bölümü ancak istedi. Örneğin, HTTP://contoso.com yeniden yönlendirilen tooHTTPS://contoso.com olur. 

## <a id="http-hsts"></a>HTTP katı taşıma güvenliği (HSTS) etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [OWASP HTTP katı taşıma güvenliği kopya sayfası](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Adımları** | <p>HTTP katı Aktarım güvenlik (HSTS) web uygulaması tarafından özel yanıt üstbilgisi hello kullanılarak belirtilen bir güvenlik katılımı yeniliktir. Bu üst desteklenen bir tarayıcı aldıktan sonra bu tarayıcı iletişimlerle HTTP toohello belirtilen etki alanı gönderilmesini engeller ve bunun yerine tüm iletişimler HTTPS üzerinden gönderir. Ayrıca, HTTPS istekleri tarayıcılarda geçişli tıklatma önler.</p><p>tooimplement HSTS, bir Web sitesi için genel olarak, kod veya yapılandırma yapılandırılmış toobe yanıt üstbilgisi aşağıdaki hello sahiptir. Strict-aktarım-güvenliği:, max-age 300; = includeSubDomains HSTS tehditleri aşağıdaki hello ele alır:</p><ul><li>Kullanıcı yer işaret yeniden veya el ile http://example.com türleri ve konu tooa man-in--middle saldırgan: HSTS HTTP isteklerini tooHTTPS hello hedef etki alanı için otomatik olarak yeniden yönlendirir</li><li>Web tamamen HTTPS yanlışlıkla HTTP bağlantılarını içerir veya HTTP üzerinden içerik hizmet hedeflenen toobe uygulama: HSTS HTTP isteklerini tooHTTPS hello hedef etki alanı için otomatik olarak yeniden yönlendirir</li><li>ADAM-in--middle saldırgan geçersiz bir sertifika kullanarak bir kurban kullanıcı toointercept trafiğinden çalışır ve hello kullanıcı hello hatalı sertifika kabul edeceği planlamaktadır: HSTS kullanıcı toooverride hello geçersiz sertifika iletiye izin verme</li></ul>|

## <a id="sqlserver-validation"></a>SQL server bağlantı şifreleme ve sertifika doğrulaması emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure  |
| **Öznitelikleri**              | SQL sürümü - V12 |
| **Başvuruları**              | [SQL veritabanı için bağlantı dizelerini yazma üzerinde en iyi yöntemler güvenli](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **Adımları** | <p>SQL veritabanı ile bir istemci uygulama arasındaki tüm iletişimler, her zaman Güvenli Yuva Katmanı (SSL) kullanılarak şifrelenir. SQL veritabanı şifrelenmemiş bağlantıları desteklemiyor. uygulama kodu veya araçları ile toovalidate sertifikalar açıkça şifreli bir bağlantı isteği ve hello sunucu sertifikaları güveniyor musunuz. Uygulama kodu veya Araçlar şifreli bir bağlantı isteme, şifreli bağlantıları hala alacağı</p><p>Ancak, bunlar hello sunucu sertifikaları doğrulamamasına ve bu nedenle çok uygulanmadıkça olacaktır "Merhaba ortadaki adam" saldırılarına. ADO.NET uygulama kodu toovalidate sertifikalarla ayarlamak `Encrypt=True` ve `TrustServerCertificate=False` hello veritabanı bağlantı dizesi içinde. SQL Server Management Studio aracılığıyla toovalidate sertifikaları hello Bağlan tooServer iletişim kutusunu açın. Merhaba bağlantı Özellikler sekmesinde şifrele bağlantısına tıklayın</p>|

## <a id="encrypted-sqlserver"></a>Force şifreli iletişim tooSQL sunucusu

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | OnPrem |
| **Öznitelikleri**              | SQL sürümü - MsSQL2016, SQL sürüm - MsSQL2012, SQL sürümü - MsSQL2014 |
| **Başvuruları**              | [Şifreli bağlantıları toohello veritabanı altyapısı etkinleştir](https://msdn.microsoft.com/library/ms191192)  |
| **Adımları** | SSL etkinleştirme şifreleme SQL Server örneklerini ve uygulamalar arasında ağlar üzerinden aktarılan verilerin hello güvenliğini artırır. |

## <a id="comm-storage"></a>Depolama HTTPS üzerinden olduğunda bu iletişimi tooAzure emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure depolama aktarım düzeyinde şifreleme – HTTPS kullanarak](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Adımları** | tooensure hello güvenliğini Azure Storage veri aktarım sırasında her zaman hello HTTPS protokolünü hello REST API'leri çağırma veya erişme depolama nesneleri, kullanın. Ayrıca, paylaşılan erişim kullanılan toodelegate olabilen imzaları, tooAzure depolama nesnelere erişmek, yalnızca o hello HTTPS protokolü herkes SAS belirteci bağlantılarıyla dışarı gönderme olacak sağlama paylaşılan erişim imzaları kullanırken kullanılabilir bir seçenek toospecify içerir Merhaba uygun protokolünü kullanır.|

## <a id="md5-https"></a>HTTPS etkinleştirilirse blob indirdikten sonra MD5 karma değeri doğrulanamıyor

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | StorageType - Blob |
| **Başvuruları**              | [Windows Azure Blob MD5 genel bakış](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **Adımları** | <p>Windows Azure Blob hizmeti mekanizmaları tooensure veri bütünlüğü hem hello uygulama ve Aktarım katmanı sağlar. Toohelp HTTP yerine HTTPS ve blok blobları çalıştığınız toouse gereken herhangi bir nedenden dolayı MD5 denetimi kullanabilirsiniz, aktarılan hello BLOB'ları hello bütünlüğünü doğrulayın</p><p>Bu ağ/aktarım katmanı hataları korumadan, ancak mutlaka Ara saldırılarla yardımcı olur. Aktarım düzeyi güvenlik sağlayan HTTPS kullanırsanız, MD5 denetimi kullanarak yedekli ve gereksiz.</p>|

## <a id="smb-shares"></a>Dosya paylaşımları SMB 3.0 uyumlu istemci tooensure aktarım sırasında veri şifreleme tooAzure kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Mobil istemci | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | StorageType - dosya |
| **Başvuruları**              | [Azure File Storage](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Windows istemcileri için Azure dosya depolama SMB desteği](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Adımları** | Azure File Storage HTTPS hello REST API kullanırken destekler, ancak bir SMB dosya paylaşımına tooa VM bağlı olarak daha yaygın olarak kullanılır. SMB 2.1 bağlantıları yalnızca hello içinde aynı izin için şifrelemeyi desteklemiyor Azure bölgesinde. Ancak, SMB 3.0 Şifreleme destekler ve Windows Server 2012 R2 ile kullanılabilir, Windows 8, Windows 8.1 ve Windows 10, çapraz bölge izin vererek erişmek ve erişim hello masaüstünde bile. |

## <a id="cert-pinning"></a>Sertifika sabitleme uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, Windows Phone |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Sertifika ve ortak anahtar sabitleme](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Adımları** | <p>Sertifika sabitleme Man-In--Middle (MITM) saldırılarına karşı defends. Sabitleme olan kendi beklenen X509 ile bir ana bilgisayar ilişkilendirme hello işlemi sertifikası veya ortak anahtar. Bir sertifika veya ortak anahtar bilinen veya bir konak için görülen sonra hello sertifikası veya ortak anahtar ilişkili ya da 'sabitlenmiş' toohello bir ana bilgisayardır. </p><p>Bu nedenle, bir saldırganın SSL el sıkışması hello anahtarı saldırganın sunucusundan sırasında SSL MITM saldırı farklı olacaktır toodo çalıştığında hello sertifikanın anahtarı sabitlenmiş ve hello isteği atılacak, böylece MITM sertifika önleme sabitleme tarafından sağlanabilir ServicePointManager'ın uygulama `ServerCertificateValidationCallback` temsilci.</p>|

### <a name="example"></a>Örnek
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>HTTPS enable - aktarım kanalının güvenliğini sağlayın.

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | Merhaba uygulama yapılandırması, HTTPS için tüm erişim toosensitive bilgileri kullanılır emin olmalısınız.<ul><li>**Açıklama:** bir uygulama hassas bilgileri işler ve ileti düzeyi şifreleme kullanmaz durumunda, yalnızca toocommunicate şifrelenmiş taşıma kanalı üzerinden izin verilmelidir.</li><li>**ÖNERİLER:** HTTP aktarımı devre dışı bırakıldığından emin olun ve HTTPS aktarımı yerine etkinleştirin. Örneğin, hello yerine `<httpTransport/>` ile `<httpsTransport/>` etiketi. Merhaba uygulama yalnızca güvenli bir kanal üzerinden erişilebilir bir ağ yapılandırması (Güvenlik Duvarı) tooguarantee kullanmayın. Bir felsefi açısından bakıldığında, Merhaba uygulaması kendi güvenlik hello ağdaki bağlı olmaması gerekir.</li></ul><p>Bunlar geliştikçe bir pratik açısından bakıldığında, hello kişilerin sorumlu hello ağ güvenliğini sağlamak için her zaman hello uygulamanın hello güvenlik gereksinimlerini izlemek değil.</p>|

## <a id="message-protection"></a>WCF: Kümesi ileti güvenlik koruma düzeyi tooEncryptAndSign

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Adımları** | <ul><li>**Açıklama:** koruma düzeyi ayarlandığında koruma "hiçbiri" devre dışı bırakma iletisi çok. Gizliliği ve bütünlük uygun düzeyde bir ayar ile elde edilir.</li><li>**ÖNERİLER:**<ul><li>zaman `Mode=None` -ileti koruma devre dışı bırakır</li><li>zaman `Mode=Sign` -işaretlerini ancak selamlama iletisine şifrelemez; veri bütünlüğü önemli olduğunda kullanılmalıdır</li><li>zaman `Mode=EncryptAndSign` -işaretleri ve selamlama iletisine şifreler</li></ul></li></ul><p>Şifreleme devre dışı kapatarak ve iletinizi toovalidate hello hello bilgilerinin endişeler olmadan gizliliği bütünlüğünü yeterlidir yalnızca imzalama göz önünde bulundurun. Bu işlemler için yararlı olabilir veya hizmet içinde sözleşmeleri toovalidate hello özgün gönderen gerekiyor, ancak hiçbir hassas veriler iletilir. Merhaba koruma düzeyini azaltır, bu selamlama iletisine tüm kişisel bilgileri (PII) içermiyor dikkatli olun.</p>|

### <a name="example"></a>Örnek
Merhaba hizmetinin hello işlemi tooonly oturum selamlama iletisine yapılandırılması ve örnek hello gösterilir. Hizmet sözleşmesi örneği `ProtectionLevel.Sign`: hello aşağıda ProtectionLevel.Sign hello hizmet sözleşmesini düzeyinde kullanma örneği verilmiştir: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Örnek
İşlemi sözleşme örneği `ProtectionLevel.Sign` (ayrıntılı denetim için): hello aşağıdadır kullanma örneği `ProtectionLevel.Sign` hello OperationContract düzeyi adresindeki:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: en az ayrıcalıklı hesap toorun WCF hizmeti kullanın.

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Adımları** | <ul><li>**Açıklama:** WCF hizmetleri yönetici veya yüksek ayrıcalıklı hesap altında çalışmaz. Hizmetleri güvenliğinin aşılması durumunda yüksek etkileri neden olur.</li><li>**ÖNERİLER:** , WCF hizmeti, uygulamanızın saldırı yüzeyini küçültmek ve, gerçekleşirse hello potansiyel hasarı azaltmak için en az ayrıcalıklı hesap toohost kullanın. Merhaba hizmet hesabı ek erişim hakları MSMQ gibi altyapı kaynaklardaki gerektiriyorsa, hello WCF Hizmeti çalıştırabilmeniz için hello olay günlüğü, performans sayaçları ve hello dosya sistemi, uygun izinleri toothese kaynakları verilmelidir başarılı bir şekilde.</li></ul><p>Hizmetinizi hello özgün çağıran adına tooaccess belirli kaynaklar gerekirse, kimliğe bürünme ve temsilci tooflow hello arayanın kimliği için bir aşağı akış yetkilendirme denetimi kullanın. Bir geliştirme senaryosunda ayrıcalıkları daha az olan özel bir yerleşik hesap hello yerel ağ hizmeti hesabı kullanın. Bir üretim senaryosunda, en az ayrıcalıklı özel etki alanı hizmeti hesabı oluşturun.</p>|

## <a id="webapi-https"></a>Tüm trafiği tooWeb API'leri HTTPS bağlantısı üzerinden zorla

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | MVC5, MVC6 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Bir Web API denetleyicisi SSL zorlama](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Adımları** | Bir uygulama, bir HTTPS ve HTTP bağlaması içeriyorsa, istemcilerin HTTP tooaccess hello sitesini kullanmaya devam edebilirsiniz. tooprevent tooprotected API'leri ister bir eylem filtresi tooensure her zaman HTTPS üzerinden bu, kullanın.|

### <a name="example"></a>Örnek 
Merhaba aşağıdaki kod SSL için denetler bir Web API kimlik doğrulama filtre gösterir: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
SSL iste Bu filtre tooany Web API eylemler ekleyin: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Bu iletişim tooAzure Redis önbelleği SSL üzerinden olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Redis Cache | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure Redis SSL desteği](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Adımları** | Redis sunucu SSL hello kutu dışı desteklemez ancak Azure Redis önbelleği desteklemez. TooAzure Redis önbelleği bağlanan ve istemci StackExchange.Redis gibi SSL destekliyorsa SSL kullanmanız gerekir. Varsayılan olarak SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için devre dışıdır. SSL desteği, redis istemcileri üzerinde bir bağımlılık olmadıkça hello güvenli varsayılanlar değiştirilmediğinden emin olun. |

Redis tasarlanmış toobe güvenilen ortamlar içinde güvenilen istemcileri tarafından erişilebilir olduğunu unutmayın. Bu genellikle, iyi bir olmadığı anlamına gelir tooexpose hello Redis örneği doğrudan toohello fikir internet veya güvenilmeyen istemcilerin doğrudan erişebileceği tooan ortamı genel olarak, hello Redis TCP bağlantı noktası veya UNIX yuva. 

## <a id="device-field"></a>Aygıt tooField ağ geçidi iletişimin güvenliğini sağlama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | IP tabanlı cihazlar için hello iletişim protokolü genellikle SSL/TLS kanal tooprotect veri aktarım kapsüllenmiş. SSL/TLS desteklemeyen diğer protokoller için taşıma veya ileti katmanında güvenliği sağlayan güvenli sürümlerini hello protokolü varsa araştırın. |

## <a id="device-cloud"></a>Aygıt tooCloud SSL/TLS kullanarak, ağ geçidi iletişim güvenli

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [İletişim protokolü seçin](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Adımları** | HTTP/AMQP veya MQTT protokolleri kullanarak SSL/TLS güvenli hale getirin. |
