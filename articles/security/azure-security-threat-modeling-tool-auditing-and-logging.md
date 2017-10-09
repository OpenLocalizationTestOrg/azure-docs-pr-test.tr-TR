---
title: "aaaAuditing ve günlüğe kaydetme - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Güvenlik çerçevesi: Denetim ve günlük | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Çözümünüzdeki hassas varlıkları tanımlamak ve değişiklik denetimi uygulama](#sensitive-entities)</li></ul> |
| **Web uygulaması** | <ul><li>[Denetim ve günlük, hello uygulamada zorlanan emin olun](#auditing)</li><li>[Günlük rotasyonunun ve ayırma yerinde olduğundan emin olun](#log-rotation)</li><li>[Merhaba uygulaması hassas kullanıcı verilerini günlüğe kaydetmez emin olun](#log-sensitive-data)</li><li>[Denetim ve günlük dosyalarını sınırlı erişimi olduğundan emin olun](#log-restricted-access)</li><li>[Kullanıcı Yönetimi olayları oturum açtığınızdan emin olun](#user-management)</li><li>[Merhaba sistemi olduğundan emin olun kötüye karşı yerleşik savunma](#inbuilt-defenses)</li><li>[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](#diagnostics-logging)</li></ul> |
| **Veritabanı** | <ul><li>[SQL Server'da oturum açma denetimi etkin olduğundan emin olun](#identify-sensitive-entities)</li><li>[Azure SQL tehdit algılamayı etkinleştir](#threat-detection)</li></ul> |
| **Azure Depolama** | <ul><li>[Azure Storage, Azure depolama çözümlemeleri tooaudit erişimi kullanın.](#analytics)</li></ul> |
| **WCF** | <ul><li>[Yeterli günlük kaydı uygulayın](#sufficient-logging)</li><li>[Uygulama yeterli denetim hata işleme](#audit-failure-handling)</li></ul> |
| **Web API** | <ul><li>[Denetim ve günlük, Web API uygulanmasını sağlamak](#logging-web-api)</li></ul> |
| **IOT alan ağ geçidi** | <ul><li>[Uygun denetim ve günlük alan ağ geçidinde zorlanır emin olun](#logging-field-gateway)</li></ul> |
| **IOT bulut ağ geçidi** | <ul><li>[Uygun denetim ve günlük bulut ağ geçidinde zorlanır emin olun](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Çözümünüzdeki hassas varlıkları tanımlamak ve değişiklik denetimi uygulama

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Dynamics CRM | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | Hassas veri içeren çözümünüzdeki varlıkları tanımlamak ve o varlıklar ile alanları değişikliğini denetleme uygulamak |

## <a id="auditing"></a>Denetim ve günlük, hello uygulamada zorlanan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | Denetim ve tüm bileşenlerini günlük etkinleştirin. Denetim günlüklerini kullanıcı bağlamı yakalama. Tüm önemli olayları belirleyin ve bu olayları günlüğe kaydedin. Merkezi günlük kaydı uygulayın |

## <a id="log-rotation"></a>Günlük rotasyonunun ve ayırma yerinde olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | <p>Günlük rotasyonunun tarihli günlük dosyalarını arşivlenmiş sistem yönetiminde kullanılan otomatik bir işlemdir. Büyük uygulamalar genellikle çalıştırdığı sunucuları oturum her istek: hantal günlüklerinin hello karşılaştıkları yolu toolimit hello günlük rotasyonunun olan toplam boyutu hello günlüklerinin hala son olayların analizini verirken. </p><p>Günlük dosyalarınızın işletim sistemi/uygulama sipariş tooavert bir hizmet reddi çalıştığı olarak farklı bir bölüme saldırı veya uygulamanızın performansını eski sürüme düşürmeyi hello toostore sahip günlük ayrımı temelde anlamına gelir</p>|

## <a id="log-sensitive-data"></a>Merhaba uygulaması hassas kullanıcı verilerini günlüğe kaydetmez emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | <p>Bir kullanıcı tooyour site gönderen herhangi bir duyarlı veri günlük tutma denetleyin. Tasarım sorunları neden yan etkileri yanı sıra kasıtlı günlüğünü denetleyin. Gizli verilerin örnekleri şunlardır:</p><ul><li>Kullanıcı kimlik bilgileri</li><li>Sosyal Güvenlik numarası veya başka tanımlayıcı bilgiler</li><li>Kredi kartı numaraları veya diğer finansal bilgileri</li><li>Sistem durumu bilgileri</li><li>Özel anahtarlar veya şifrelenmiş kullanılan toodecrypt bilgiler olabilir diğer verileri</li><li>Kullanılabilir sistem veya uygulama bilgilerini toomore etkili bir şekilde hello uygulama saldırısı</li></ul>|

## <a id="log-restricted-access"></a>Denetim ve günlük dosyalarını sınırlı erişimi olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | <p>Tooensure erişim hakları toolog dosyaları uygun şekilde ayarlanmış denetleyin. Uygulama hesapları yalnızca yazma erişimi ve işleçler olması gerekir ve destek personeli, gerektiği gibi salt okunur erişimi olması gerekir.</p><p>Yöneticiler hesapları tam erişimi olan hello yalnızca hesaplarıdır. Düzgün şekilde kısıtlanır tooensure Windows ACL günlük dosyaları denetleyin:</p><ul><li>Uygulama hesapları yalnızca yazma erişimi olması gerekir</li><li>İşleçler ve destek personeli salt okunur erişim gerektiğinde olmalıdır</li><li>Yöneticiler tam erişime sahip olması gereken hello yalnızca hesaplardır</li></ul>|

## <a id="user-management"></a>Kullanıcı Yönetimi olayları oturum açtığınızdan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | <p>Merhaba uygulaması başarılı ve başarısız bir kullanıcı oturum açma bilgileri gibi kullanıcı yönetimi olayları izler, parolasını sıfırlar, parola değişiklikleri, hesap kilitleme, kullanıcı kaydı emin olun. Bunun yapılması, fotoğraflar ve toopotentially şüpheli davranış tepki toodetect yardımcı olur. Ayrıca, toogather işlemleri veri sağlar; Örneğin, hello uygulamaya erişmeyi tootrack</p>|

## <a id="inbuilt-defenses"></a>Merhaba sistemi olduğundan emin olun kötüye karşı yerleşik savunma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları**                   | <p>Denetimler, uygulama kötüye kullanılması durumunda güvenlik özel durum yerinde olmalıdır. Örneğin, giriş doğrulaması yerinde olduğundan ve bir saldırgan hello regex eşleşmiyor tooinject kötü amaçlı kod çalışır, bir güvenlik özel durumu, sistemin kötüye kullanımı bir vurgulayan olabilen atılabilen</p><p>Örneğin, oturum açmış toohave güvenlik özel durumları ve sorunları aşağıdaki hello için yapılan eylemler önerilir:</p><ul><li>Giriş doğrulaması</li><li>CSRF ihlalleri</li><li>Deneme yanılma saldırısı (kullanıcı kaynak başına istek sayısı için üst sınır)</li><li>Dosya karşıya yükleme ihlalleri</li><ul>|

## <a id="diagnostics-logging"></a>Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | EnvironmentType - Azure |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Azure web uygulaması bir uygulama hizmeti ayıklama yerleşik tanılama tooassist sağlar. TooAPI uygulamaları ve mobil uygulamalara da uygulanır. App Service web apps hello web sunucusu ve hello web uygulamasının içinden bilgileri günlüğe kaydetme için tanılama işlevsellik sağlar.</p><p>Bu web sunucusu tanılama ve uygulama tanılama mantıksal olarak ayrılır</p>|

## <a id="identify-sensitive-entities"></a>SQL Server'da oturum açma denetimi etkin olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Oturum açma denetimi yapılandırma](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Adımları** | <p>Veritabanı sunucusu oturum açma denetimi saldırıları tahmin etkin toodetect/parolayı olması gerekir. Toocapture başarısız oturum açma denemeleri önemlidir. Hem başarılı ve başarısız oturum açma denemesi yakalama sırasında adli incelemelere ek bir fayda sağlar</p>|

## <a id="threat-detection"></a>Azure SQL tehdit algılamayı etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure |
| **Öznitelikleri**              | SQL sürümü - V12 |
| **Başvuruları**              | [SQL veritabanı tehdit algılama ile çalışmaya başlama](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Adımları** |<p>Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar. Yeni bir katman müşterileri toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği sağlar.</p><p>Kullanıcıları, Azure SQL veritabanı bir girişim tooaccess sağlamazsa toodetermine ihlal denetimi kullanarak hello şüpheli olayları keşfedin veya hello veritabanındaki verileri yararlanma.</p><p>Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan yapan veya sistemleri izleme Gelişmiş Güvenlik yönetme</p>|

## <a id="analytics"></a>Azure Storage, Azure depolama çözümlemeleri tooaudit erişimi kullanın.

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok |
| **Başvuruları**              | [Storage Analytics toomonitor yetkilendirme türünü kullanma](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Adımları** | <p>Her Depolama hesabı için bir Azure depolama çözümlemeleri tooperform günlüğe yazılmasını etkinleştirmek ve ölçüm verilerini depolar. Merhaba depolama analytics günlükleri depolama eriştiklerinde birisi tarafından kullanılan kimlik doğrulama yöntemi gibi önemli bilgileri sağlar.</p><p>Bu erişim toostorage sıkı bir şekilde kullanılan koruyarak gerçekten yardımcı olabilir. Örneğin, Blob depolama alanına Merhaba kapsayıcılara tooprivate tümünün ayarlayın ve uygulamalarınızı hello hizmeti kullanımı için bir SAS uygulamak. Ardından hello düzenli olarak bloblarınızın bir güvenlik açığını gösterebilir, hello depolama hesabı anahtarları kullanılarak erişilir veya hello BLOB'lar ortak ancak bunlar olmamalıdır toosee günlüklerini denetleyin.</p>|

## <a id="sufficient-logging"></a>Yeterli günlük kaydı uygulayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | <p>bir güvenlik olayı sonra uygun denetim izi Hello eksikliği adli çaba engel olabilir. Windows Communication Foundation (WCF) hello özelliği toolog başarılı ve/veya başarısız kimlik doğrulama girişimlerini sunar.</p><p>Başarısız kimlik doğrulama girişimlerini günlüğe olası kaba kuvvet saldırıları yöneticileri uyarır. Yasal bir hesap güvenliği aşıldığında benzer şekilde, başarılı kimlik doğrulama olaylarını günlüğe yararlı denetim izi sağlayabilir. WCF'ın hizmeti güvenlik denetim özelliğini etkinleştir |

### <a name="example"></a>Örnek
Denetim etkin olan bir örnek yapılandırma Hello aşağıda verilmiştir
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Uygulama yeterli denetim hata işleme

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Krallık Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | <p>Geliştirilmiş çözüm yapılandırılmış toogenerate toowrite tooan denetim günlüğü başarısız olduğunda bir özel durum. WCF yapılandırılmışsa toothrow oluşturulamıyor toowrite tooan denetim günlüğü olduğunda, hello program hello başarısızlığını değil bildirilir ve kritik güvenlik olaylarının denetlenmesi algılanamayabilir bir özel durum.</p>|

### <a name="example"></a>Örnek
Merhaba `<behavior/>` hello WCF yapılandırma dosyasının aşağıdaki öğesinin bildirir WCF toonot Merhaba uygulaması WCF toowrite tooan denetim günlüğü başarısız olduğunda bildir.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
%S toowrite tooan denetim günlüğü olduğunda WCF toonotify hello programı yapılandırın. Merhaba program bir alternatif bildirim düzeni denetim izleri tutulan değil yer tooalert hello kuruluşta olması gerekir. 

## <a id="logging-web-api"></a>Denetim ve günlük, Web API uygulanmasını sağlamak

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Denetim ve günlük Web API'leri etkinleştirin. Denetim günlüklerini kullanıcı bağlamı yakalama. Tüm önemli olayları belirleyin ve bu olayları günlüğe kaydedin. Merkezi günlük kaydı uygulayın |

## <a id="logging-field-gateway"></a>Uygun denetim ve günlük alan ağ geçidinde zorlanır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | <p>Birden çok aygıt tooa alan ağ geçidi bağladığınızda, bağlantı denemeleri ve bireysel aygıtlar için kimlik doğrulama durumu (başarı veya başarısızlık) oturum açmış ve hello alan ağ geçidi üzerinde tutulan emin olun.</p><p>Ayrıca, alan ağ geçidi hello sorumlu olduğu durumlarda IOT hub'ı bireysel aygıtlar için kimlik bilgileri, bu kimlik bilgileri alınırken denetim özelliğinin gerçekleştirildiğinden emin olun. Bir işlem tooperiodically karşıya yükleme hello günlükleri tooAzure IOT hub'ı / depolama uzun vadeli bekletme için geliştirin.</p> |

## <a id="logging-cloud-gateway"></a>Uygun denetim ve günlük bulut ağ geçidinde zorlanır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Giriş tooIoT Hub işlemlerini izleme](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Adımları** | <p>Toplama ve IOT Hub işlemlerini izleme ile toplanan denetim verilerini depolamak için tasarlayın. İzleme kategorisi aşağıdaki hello etkinleştirin:</p><ul><li>Aygıt Kimliği işlemleri</li><li>Cihaz bulut iletişimleri</li><li>Bulut-cihaz iletişimi</li><li>Bağlantılar</li><li>Dosya yüklemeleri</li></ul>|
