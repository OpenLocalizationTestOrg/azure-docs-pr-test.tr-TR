---
title: "aaaAuthorization - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Güvenlik çerçevesi: Yetkilendirme | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Makine güven sınırı** | <ul><li>[Uygun ACL'ler yapılandırılmış toorestrict yetkisiz erişim toodata hello aygıtta olduğundan emin olun](#acl-restricted-access)</li><li>[Hassas kullanıcıya özgü uygulama içeriği kullanıcı profili dizininde depolanır emin olun](#sensitive-directory)</li><li>[Dağıtılan hello uygulamaları en az ayrıcalıkla çalıştırdığınızdan emin olun](#deployed-privileges)</li></ul> |
| **Web uygulaması** | <ul><li>[İş mantığı akışları işlerken sıralı adım sipariş zorla](#sequential-logic)</li><li>[Mekanizması tooprevent numaralandırma hız sınırı uygulama](#rate-enumeration)</li><li>[Uygun yetkilendirme yerinde olduğundan ve en düşük ayrıcalık ilkesini ardından emin olun](#principle-least-privilege)</li><li>[İş mantığı ve kaynak erişim yetkilendirme kararları gelen isteği parametrelere dayanmalıdır değil](#logic-request-parameters)</li><li>[Bu içerik sağlamak ve kaynakları numaralandırılabilir veya zorlama gözatma yoluyla erişilebilir değil](#enumerable-browsing)</li></ul> |
| **Veritabanı** | <ul><li>[En az ayrıcalıklı hesapları kullanılan tooconnect tooDatabase sunucusu olduğundan emin olun](#privileged-server)</li><li>[Satır düzeyi güvenlik RLS tooprevent kiracılar birbirinin verilerine erişmesini uygulama](#rls-tenants)</li><li>[Sysadmin rolünün yalnızca geçerli gerekli kullanıcıların olmalıdır](#sysadmin-users)</li></ul> |
| **IOT bulut ağ geçidi** | <ul><li>[Ağ geçidi tooCloud bağlanmak en az ayrıcalıklı belirteç kullanma](#cloud-least-privileged)</li></ul> |
| **Azure Event hub'ı** | <ul><li>[Cihaz belirteçleri oluşturmak için bir yalnızca gönderme izinleri SAS anahtarı kullan](#sendonly-sas)</li><li>[Doğrudan erişim toohello olay hub'ı sağlamak erişim belirteçleri kullanmayın](#access-tokens-hub)</li><li>[SAS kullanarak Hub hello minimum gerekli izinlere sahip olduğunu anahtarları tooEvent Bağlan](#sas-minimum-permissions)</li></ul> |
| **Azure belge DB** | <ul><li>[Kaynak belirteçleri tooconnect tooDocumentDB mümkün olduğunca kullanın](#resource-docdb)</li></ul> |
| **Azure güven sınırı** | <ul><li>[Ayrıntılı erişim yönetimi tooAzure aboneliği etkinleştir RBAC kullanarak](#grained-rbac)</li></ul> |
| **Service Fabric güven sınırı** | <ul><li>[RBAC kullanarak istemcinin erişim toocluster işlemlerini kısıtlamak](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Güvenlik modelleme gerçekleştirmek ve alan düzeyinde güvenliğin kullanmanız gerektiğinde](#modeling-field)</li></ul> |
| **Dynamics CRM portalı** | <ul><li>[Güvenlik modelleme hello portal hello CRM kalanından farklı olduğu için bu hello güvenlik modeli göz önünde bulundurarak portal hesaplarının gerçekleştirin](#portal-security)</li></ul> |
| **Azure Depolama** | <ul><li>[Azure Table Storage varlıklarda bir dizi hassas izin ver](#permission-entities)</li><li>[Rol tabanlı erişim denetimi (RBAC) tooAzure depolama hesabı Azure Kaynak Yöneticisi'ni kullanarak etkinleştirin](#rbac-azure-manager)</li></ul> |
| **Mobil istemci** | <ul><li>[Örtük kaçış veya algılama kök dizini değiştirme uygulanması](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[WCF'de zayıf sınıf başvurusu](#weak-class-wcf)</li><li>[WCF uygulayan yetkilendirme denetimi](#wcf-authz)</li></ul> |
| **Web API** | <ul><li>[ASP.NET Web API'de uygun yetkilendirme mekanizması uygulayın](#authz-aspnet)</li></ul> |
| **IOT cihaz** | <ul><li>[Farklı izin düzeyleri gereken çeşitli eylemler destekliyorsa hello Aygıt yetkilendirme denetimleri gerçekleştirin](#device-permission)</li></ul> |
| **IOT alan ağ geçidi** | <ul><li>[Farklı izin düzeyleri gereken çeşitli eylemler destekliyorsa hello alan ağ geçidi yetkilendirme denetimleri gerçekleştirin](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Uygun ACL'ler yapılandırılmış toorestrict yetkisiz erişim toodata hello aygıtta olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Uygun ACL'ler yapılandırılmış toorestrict yetkisiz erişim toodata hello aygıtta olduğundan emin olun|

## <a id="sensitive-directory"></a>Hassas kullanıcıya özgü uygulama içeriği kullanıcı profili dizininde depolanır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Hassas kullanıcıya özgü uygulama içeriği kullanıcı profili dizininde depolanır emin olun. Merhaba, birden çok kullanıcı birbirinin verilerine erişmesini makine tooprevent budur.|

## <a id="deployed-privileges"></a>Dağıtılan hello uygulamaları en az ayrıcalıkla çalıştırdığınızdan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Dağıtılan hello uygulama en az ayrıcalıkla çalıştırdığınızdan emin olun. |

## <a id="sequential-logic"></a>İş mantığı akışları işlerken sıralı adım sipariş zorla

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Bu aşama gerçekçi İnsan zamanında işlenmekte olan tüm adımda tooenforce hello uygulama tooonly işlem iş mantığı akışları sıralı adım sırada istediğiniz ve bozuk, işlemez orijinal bir kullanıcı tarafından çalıştırılan tooverify sırada atlandı adımlar, başka bir kullanıcıdan adımları işlenen ya da işlemleri çok hızlı bir şekilde gönderildi.|

## <a id="rate-enumeration"></a>Mekanizması tooprevent numaralandırma hız sınırı uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Hassas tanımlayıcıları rastgele olduğundan emin olun. Anonim sayfalarında CAPTCHA denetim uygulayın. Hata ve özel durum belirli veri ortaya çıkarır değil emin olun|

## <a id="principle-least-privilege"></a>Uygun yetkilendirme yerinde olduğundan ve en düşük ayrıcalık ilkesini ardından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Hello İlkesi, bir kullanıcı hesabı temel toothat kullanıcılar iş olan ayrıcalıkları vermek anlamına gelir. Örneğin, bir yedekleme kullanıcı tooinstall yazılım gerekmez: Bu nedenle, hello yedekleme kullanıcı hakları yalnızca toorun yedekleme ve yedekleme ile ilgili uygulamaları vardır. Yeni yazılım yükleme gibi başka ayrıcalıklar, engellenir. Hello İlkesi de genellikle normal bir kullanıcı hesabı içinde çalışır ve ayrıcalıklı, parola korumalı hesabı (diğer bir deyişle, bir süper kullanıcı) açar tooa kişisel bilgisayar kullanıcının geçerlidir yalnızca zaman hello durum kesinlikle, talep. </p><p>Bu ilkeyi uygulanan tooyour web uygulamaları da olabilir. Yerine yalnızca rol tabanlı kimlik doğrulama yöntemlerini oturumları kullanarak bağlı olarak bunun yerine tooassign toousers bir veritabanı tabanlı kimlik doğrulama sistemi yoluyla ayrıcalıkları istiyoruz. Merhaba kullanıcı doğru yalnızca şimdi biz ona gerçekleştirilmesine hangi eylemleri ile ayrıcalıkları tooverify atamak belirli bir rol o kullanıcıyla hello sistemde ayrıcalıklı tooperform atamak yerine oturum açarsa hala sipariş tooidentify oturumlarında kullanırız. Bir kullanıcı hello atama tooexpire ilk sahip değilse, hello oturum bağlı değildir beri değişikliklerinizi hello anında uygulanacak daha az ayrıcalıklar atanan toobe sahipse de bu yöntemin büyük pro, olur.</p>|

## <a id="logic-request-parameters"></a>İş mantığı ve kaynak erişim yetkilendirme kararları gelen isteği parametrelere dayanmalıdır değil

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Bir kullanıcı kısıtlı tooreview olup olmadığını denetlemeye her sunucu tarafı işlenen belirli veri hello erişim kısıtlamaları olmalıdır. Merhaba UserID oturum açma üzerinde oturum değişkeni içinde saklanmalıdır ve kullanılan tooretrieve kullanıcı verilerini hello veritabanından olmalıdır |

### <a name="example"></a>Örnek
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Artık olası bir saldırganın yapabilir değil değiştirmesine ve hello hello veri almak için tanımlayıcı işlenen sunucu tarafı beri hello uygulama işlemi değiştirebilirsiniz.

## <a id="enumerable-browsing"></a>Bu içerik sağlamak ve kaynakları numaralandırılabilir veya zorlama gözatma yoluyla erişilebilir değil

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Hassas statik ve yapılandırma dosyaları hello web-kök tutulmalıdır değil. İçerik gerekli değil toobe için ortak, uygun erişim denetimleri uygulanması gereken veya hello kaldırılmasını içerik kendisi.</p><p>Ayrıca, zorunlu gözatma genellikle yanılma teknikleri toogather bilgilerle tooaccess deneyerek sayıda URL'ler olası tooenumerate dizinleri ve dosyaları bir sunucuda olarak birleştirilir. Saldırganlar genellikle varolan tüm çeşitlemelerini denetleyin dosyaları. Örneğin, bir parola dosya arama psswd.txt, password.htm, password.dat ve diğer Çeşitleme dahil olmak üzere dosyaları kapsayan.</p><p>Bu, deneme yanılma saldırısı algılanması için özellikleri toomitigate çalışır eklenmelidir.</p>|

## <a id="privileged-server"></a>En az ayrıcalıklı hesapları kullanılan tooconnect tooDatabase sunucusu olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [SQL veritabanı izinleri hiyerarşi](https://msdn.microsoft.com/library/ms191465), [SQL veritabanı güvenliği sağlanabilir öğeler](https://msdn.microsoft.com/library/ms190401) |
| **Adımları** | En az ayrıcalıklı hesapları kullanılan tooconnect toohello veritabanı olmalıdır. Uygulama oturum açma hello veritabanında kısıtlanması ve seçili saklı yordamlar yalnızca yürütme. Uygulamanın oturum açma hiçbir doğrudan tablo erişimi olmalıdır. |

## <a id="rls-tenants"></a>Satır düzeyi güvenlik RLS tooprevent kiracılar birbirinin verilerine erişmesini uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure, OnPrem |
| **Öznitelikleri**              | SQL sürüm - V12, SQL sürümü - MsSQL2016 |
| **Başvuruları**              | [SQL Server satır düzeyi güvenlik (RLS)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Adımları** | <p>Satır düzeyi güvenlik (örneğin, grubu üyeliği veya yürütme bağlamı) sorgu yürütülürken hello kullanıcı hello özellikler temelinde bir veritabanı tablosundaki müşteriler toocontrol erişim toorows sağlar.</p><p>Satır düzeyi güvenlik (RLS) hello tasarım ve uygulamanızda güvenlik kodlama basitleştirir. RLS tooimplement kısıtlamalar veri satırı erişimi sağlar. Örneğin çalışanları ilgili tootheir departmanı olan veri satırına erişmesini ya da Müşteri'nin veri erişim tooonly hello veri ilgili tootheir şirket kısıtlama.</p><p>Merhaba erişim kısıtlama mantığı hello veritabanı katmanı bulunan yerine koyma hello verilerden başka bir uygulama katmanı. veri erişimini herhangi bir katmanı denenir her zaman hello veritabanı sistem hello erişim kısıtlamaları uygular. Bu hello güvenlik sistemi daha güvenli ve sağlam hello güvenlik sistemi yüzey alanını hello azaltarak hale getirir.</p><p>|

Lütfen unutmayın. Bu RLS Giden kutusu veritabanı özellik olarak, geçerli yalnızca tooSQL Server 2016'dan başlayarak ve Azure SQL veritabanı. Merhaba Giden kutusu RLS özellik uygulanmıyor varsa, veri erişimi kısıtlanmış kullanarak görünümleri ve yordamları olduğunu güvence altına

## <a id="sysadmin-users"></a>Sysadmin rolünün yalnızca geçerli gerekli kullanıcıların olmalıdır

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [SQL veritabanı izinleri hiyerarşi](https://msdn.microsoft.com/library/ms191465), [SQL veritabanı güvenliği sağlanabilir öğeler](https://msdn.microsoft.com/library/ms190401) |
| **Adımları** | Merhaba SysAdmin sabit sunucu rolünün üyeleri çok sınırlı ve hiçbir zaman uygulamaları tarafından kullanılan hesapları içermesi gerekir.  Lütfen hello roldeki kullanıcılar hello listesini gözden geçirin ve tüm gereksiz hesaplarını kaldırın|

## <a id="cloud-least-privileged"></a>Ağ geçidi tooCloud bağlanmak en az ayrıcalıklı belirteç kullanma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ağ geçidi seçim - Azure IOT Hub |
| **Başvuruları**              | [IOT hub'ı erişim denetimi](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Adımları** | En az ayrıcalık tooCloud ağ geçidi (IOT Hub) bağlanma izinleri toovarious bileşenleri sağlar. Tipik bir örnektir – aygıt yönetimi ve sağlama bileşeni registryread/yazma kullanıyorsa, hizmet bağlantı olay işlemcisi (ASA) kullanır. Tek bir cihazı Cihaz kimlik bilgilerini kullanarak bağlan|

## <a id="sendonly-sas"></a>Cihaz belirteçleri oluşturmak için bir yalnızca gönderme izinleri SAS anahtarı kullan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Event hub'ı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Adımları** | Bir SAS anahtarı kullanılan toogenerate tek tek cihaz belirteçleri ' dir. Belirtilen yayımcı için yalnızca gönderme izinleri SAS anahtar oluşturma hello cihaz belirteci sırasında kullanma|

## <a id="access-tokens-hub"></a>Doğrudan erişim toohello olay hub'ı sağlamak erişim belirteçleri kullanmayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Event hub'ı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Adımları** | Toohello event hub'ı doğrudan erişim veren bir belirteç toohello aygıt verilmemelidir. Yalnızca tooa yayımcı belirlemek ve varsa kara yardımcı olacak erişmenizi hello cihaz için en az ayrıcalıklı bir belirteci kullanan bir dolandırıcı toobe bulunamadı veya cihazın güvenliği.|

## <a id="sas-minimum-permissions"></a>SAS kullanarak Hub hello minimum gerekli izinlere sahip olduğunu anahtarları tooEvent Bağlan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Event hub'ı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Adımları** | En az ayrıcalık toohello olay hub'ı bağlanmak izinleri toovarious arka uç uygulamaları sağlar. Her bir arka uç uygulama için ayrı SAS anahtarları oluştur ve yalnızca gerekli hello izinleri - gönderme, alma veya Yönet toothem sağlayın.|

## <a id="resource-docdb"></a>Kaynak belirteçleri tooconnect tooCosmos DB mümkün olduğunca kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure belge DB | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Kaynak belirteci DocumentDB izni kaynakla ilişkili olan ve yakalamaları hello arasındaki ilişki bir veritabanı ve hello izin hello kullanıcı kullanıcının belirli bir DocumentDB uygulama kaynak için (örneğin, koleksiyon ve belge) sahip. Merhaba istemci ana veya salt okunur anahtarları - son kullanıcı uygulamayı bir mobil veya masaüstü istemcisi gibi gibi işleme ile güvenilemez her zaman kaynak belirteci tooaccess hello DocumentDB kullanın. Ana anahtar veya bu anahtarları güvenli bir şekilde depolayan arka uç uygulamalardan salt okunur tuşlarını kullanın.|

## <a id="grained-rbac"></a>Ayrıntılı erişim yönetimi tooAzure aboneliği etkinleştir RBAC kullanarak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure güven sınırı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Rol atamaları toomanage erişim tooyour Azure aboneliği kaynakları kullanın](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Adımları** | Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, kullanıcıların işlerini tooperform gerektiğini yalnızca hello erişim miktarını verebilirsiniz.|

## <a id="cluster-rbac"></a>RBAC kullanarak istemcinin erişim toocluster işlemlerini kısıtlamak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure |
| **Başvuruları**              | [Service Fabric istemciler için rol tabanlı erişim denetimi](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Adımları** | <p>Azure Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı. Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar.</p><p>Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir. Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.</p><p>Her biri için ayrı sertifikaların sağlayarak hello küme oluşturma sırasında hello iki istemci rolleri (Yönetici ve istemci) belirtin.</p>|

## <a id="modeling-field"></a>Güvenlik modelleme gerçekleştirmek ve alan düzeyinde güvenliğin kullanmanız gerektiğinde

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Güvenlik modelleme gerçekleştirmek ve alan düzeyinde güvenliğin kullanmanız gerektiğinde|

## <a id="portal-security"></a>Güvenlik modelleme hello portal hello CRM kalanından farklı olduğu için bu hello güvenlik modeli göz önünde bulundurarak portal hesaplarının gerçekleştirin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM portalı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Güvenlik modelleme hello portal hello CRM kalanından farklı olduğu için bu hello güvenlik modeli göz önünde bulundurarak portal hesaplarının gerçekleştirin|

## <a id="permission-entities"></a>Azure Table Storage varlıklarda bir dizi hassas izin ver

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | StorageType - tablosu |
| **Başvuruları**              | [Nasıl toodelegate erişim SAS kullanarak Azure depolama hesabınızdaki tooobjects](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Adımları** | Belirli iş senaryolarda, Azure Table Storage toodifferent tarafların caters gerekli toostore hassas verileri olabilir. Toodifferent ülkelerde ilgili örn., hassas verileri. Bir kullanıcı veri belirli tooa belirli bir ülke erişebilmesi gibi Böyle durumlarda, SAS imzaları hello bölüm ve satır anahtarı aralıkları, belirterek oluşturulabilir.| 

## <a id="rbac-azure-manager"></a>Rol tabanlı erişim denetimi (RBAC) tooAzure depolama hesabı Azure Kaynak Yöneticisi'ni kullanarak etkinleştirin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Nasıl toosecure depolama hesabı rol tabanlı erişim denetimi ile (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Adımları** | <p>Yeni bir depolama hesabı oluşturduğunuzda, Klasik veya Azure Resource Manager dağıtım modelini seçin. Azure kaynakları oluşturma hello Klasik modeli yalnızca ya hep ya hiç erişim toohello abonelik sağlar ve buna karşılık, depolama hesabı hello.</p><p>Hello Azure Resource Manager modeli ile bir kaynak grubu ve Denetim erişim toohello Yönetim düzeyi Azure Active Directory'yi kullanarak, belirli bir depolama hesabının içinde hello depolama hesabı yerleştirin. Örneğin, diğer kullanıcıların hello depolama hesabı bilgilerini görüntüleyebilirsiniz, ancak hello depolama hesabı anahtarlarını erişemiyor hello özelliği tooaccess hello depolama hesabı anahtarları, belirli kullanıcılara verebilirsiniz.</p>|

## <a id="rooting-detection"></a>Örtük kaçış veya algılama kök dizini değiştirme uygulanması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Mobil istemci | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Uygulama kendi yapılandırması ve kullanıcı verilerini telefon kökü varsa durum ya da işletim sistemi engellemeleri korunması. Kök dizini değiştirme/çiğnemekten kısıtlamaları yetkisiz erişim, normal hangi kullanıcıların kendi telefonlarda olmaz anlamına gelir. Bu nedenle, uygulama başlatma, hello telefon kökü ise toodetect örtük algılama mantığı uygulama olması gerekir.</p><p>Merhaba algılama mantığı yalnızca normal olarak, yalnızca kök kullanıcı, örneğin erişebilir dosyalara erişme:</p><ul><li>/System/App/Superuser.apk</li><li>/ sbin/su</li><li>/System/bin/su</li><li>/System/xbin/su</li><li>/Data/Local/xbin/su</li><li>/Data/local/bin/su</li><li>/System/SD/xbin/su</li><li>/System/bin/failsafe/su</li><li>/Data/Local/su</li></ul><p>Merhaba uygulaması bu dosyalar erişebiliyorsa hello uygulama kök kullanıcı olarak çalıştığını gösterir.</p>|

## <a id="weak-class-wcf"></a>WCF'de zayıf sınıf başvurusu

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | <p>Merhaba sistem yetkisiz tooexecute kod bir saldırganın zayıf sınıf başvurusu kullanır. Merhaba program benzersiz olarak tanımlanmadığı kullanıcı tanımlı bir sınıf başvurur. Merhaba CLR türü yükleyicisi hello konumlarda aşağıdaki hello hello sınıfında arar zayıf tanımlanan bu sınıf .NET yüklediğinde sipariş belirtilen:</p><ol><li>Merhaba derleme hello türü biliniyorsa hello yükleyicisi aramalar yapılandırma dosyanın yeniden yönlendirme konumları, GAC, hello geçerli derleme yapılandırma bilgilerini kullanarak hello ve uygulamanın ana dizin hello</li><li>Hello derleme bilinmiyorsa hello yükleyicisi aramaları geçerli derleme, mscorlib ve hello TypeResolve olay işleyicisi tarafından döndürülen hello konumu hello</li><li>Bu CLR arama sırası hello tür iletme mekanizması gibi kancaları ve hello AppDomain.TypeResolve olay ile değiştirilebilir</li></ol><p>Bir saldırgan oluşturarak hello CLR arama sırası yararlanırsa alternatif bir sınıf Merhaba aynı ad ve CLR ilk yükleme bu hello alternatif bir konuma yerleştirerek, hello CLR istemeden hello saldırgan tarafından sağlanan kod yürütülmez.</p>|

### <a name="example"></a>Örnek
Merhaba `<behaviorExtensions/>` hello WCF yapılandırma dosyasının aşağıdaki öğesinin WCF tooadd özel davranış sınıfı tooa belirli WCF uzantısı bildirir.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
Tam (tanımlayıcı) adlarının benzersiz olarak kullanarak bir türü tanımlar ve daha da sisteminizin güvenliğini artırır. Merhaba machine.config ve app.config dosya türlerini kaydetme tam nitelikli derleme adları kullanın.

### <a name="example"></a>Örnek
Merhaba `<behaviorExtensions/>` hello WCF yapılandırma dosyasının aşağıdaki öğesinin WCF tooadd kesinlikle başvurulan özel davranış sınıfı tooa belirli WCF uzantısı bildirir.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF uygulayan yetkilendirme denetimi

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | <p>Bu hizmet bir yetkilendirme denetimini kullanmaz. Bir istemci belirli bir WCF Hizmeti aradığında, WCF bu hello çağıran izni tooexecute hello hizmet yöntemi hello sunucuda doğrulayın çeşitli yetkilendirme düzenleri sağlar. Kimliği doğrulanmış bir kullanıcı, yetkilendirme denetimleri için WCF hizmetleri etkinleştirilmezse ayrıcalık yükseltme elde edebilirsiniz.</p>|

### <a name="example"></a>Örnek
yapılandırma aşağıdaki hello WCF toonot onay hello yetkilendirme düzeyini hello istemci hello hizmet yürütülürken bildirir:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Merhaba hello hizmet yöntemini çağıran bir hizmet Yetkilendirme düzeni tooverify yetkili toodo şekilde kullanılır. WCF iki mod sağlar ve bir özel Yetkilendirme düzeni hello tanımlanmasına olanak tanır. Merhaba UseWindowsGroups modu Windows rolleri ve kullanıcıların ve SQL Server, tooauthenticate gibi bir ASP.NET rol sağlayıcıyı hello UseAspNetRoles modu kullanır.

### <a name="example"></a>Örnek
Merhaba aşağıdaki yapılandırma WCF toomake hello Ekle hizmet yürütmeden önce o hello istemci hello Administrators grubunun bir parçası olduğundan emin bildirir:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Merhaba hizmet ardından hello aşağıdaki gibi bildirilmiş:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>ASP.NET Web API'de uygun yetkilendirme mekanizması uygulayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, MVC5 |
| **Öznitelikleri**              | Yok, kimlik sağlayıcısı - ADFS, kimlik sağlayıcısı - Azure AD |
| **Başvuruları**              | [Kimlik doğrulama ve yetkilendirme ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Adımları** | <p>Merhaba uygulaması üzerlerinde kimlik sağlayıcısı olarak kullanır veya hello uygulamanın kendisinin olabilir, ADFS talepleri, sağlanan veya hello uygulama kullanıcıları için rol bilgileri Azure AD'den elde edilebilir. Bu durumların hiçbirinde hello özel yetkilendirme uygulama hello kullanıcı rolü bilgilerini doğrulamalıdır.</p><p>Merhaba uygulaması üzerlerinde kimlik sağlayıcısı olarak kullanır veya hello uygulamanın kendisinin olabilir, ADFS talepleri, sağlanan veya hello uygulama kullanıcıları için rol bilgileri Azure AD'den elde edilebilir. Bu durumların hiçbirinde hello özel yetkilendirme uygulama hello kullanıcı rolü bilgilerini doğrulamalıdır.</p>

### <a name="example"></a>Örnek
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Tüm denetleyicileri hello ve tooprotected gereken eylem yöntemleri ile öznitelik donatılmış.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Farklı izin düzeyleri gereken çeşitli eylemler destekliyorsa hello Aygıt yetkilendirme denetimleri gerçekleştirin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT cihaz | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Merhaba arayan istenen hello gerekli izinleri tooperform hello eylem varsa hello aygıt hello arayan toocheck yetkilendirmeniz. Örneğin sağlar için deyin hello hello buluttan izlenebilir akıllı bir kapısını kilitleme aygıttır artı uzaktan hello kapısını kilitleme gibi işlevler sağlar.</p><p>yalnızca birisi fiziksel olarak hello kapı bir kart ile geldiğinde hello akıllı kapısını kilitleme kilidini açma işlevselliği sağlar. Bu durumda, hello hello uzaktan komut ve denetim uyarlamasını hello bulut ağ geçidi yetkili toosend komutu toounlock hello kapı olmadığından, hiçbir işlevsellik toounlock hello kapı sağlamaz şekilde yapılmalıdır.</p>|

## <a id="field-permission"></a>Farklı izin düzeyleri gereken çeşitli eylemler destekliyorsa hello alan ağ geçidi yetkilendirme denetimleri gerçekleştirin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Merhaba arayan istenen hello gerekli izinleri tooperform hello eylem varsa hello alan ağ geçidi hello arayan toocheck yetkilendirmeniz. Örneğin olmamalıdır için farklı bir yönetici kullanıcının izinlerini arabirimi/API tooconfigure tooit bağlanan bir alan ağ geçidi v/s aygıtları kullanılır.|
