---
title: "aaaAuthentication - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Güvenlik çerçevesi: Kimlik doğrulaması | Azaltıcı Etkenler 
| Ürün/hizmet | Makale |
| --------------- | ------- |
| **Web uygulaması**    | <ul><li>[Standart kimlik doğrulama mekanizması tooauthenticate tooWeb uygulama kullanmayı deneyin](#standard-authn-web-app)</li><li>[Uygulamalar başarısız kimlik doğrulama senaryoları güvenli bir şekilde işlemesi gerekir](#handle-failed-authn)</li><li>[Etkinleştirme adım veya uyarlamalı kimlik doğrulaması](#step-up-adaptive-authn)</li><li>[Yönetim arabirimleri uygun şekilde kilitlendiğini emin olun](#admin-interface-lockdown)</li><li>[Uygulama parolası işlevler güvenli bir şekilde unuttum](#forgot-pword-fxn)</li><li>[Parola ve hesap ilkesi uygulanır emin olun](#pword-account-policy)</li><li>[Uygulama denetimleri tooprevent kullanıcıadı numaralandırması](#controls-username-enum)</li></ul> |
| **Veritabanı** | <ul><li>[Mümkün olduğunda, Windows kimlik doğrulaması tooSQL sunucusuna bağlanmak için kullanın](#win-authn-sql)</li><li>[Mümkün olduğunda bağlanma tooSQL veritabanı için Azure Active Directory kimlik doğrulaması kullanın.](#aad-authn-sql)</li><li>[SQL kimlik doğrulama modu kullanıldığında, hesap ve parola ilke SQL Server'da zorunlu emin olun](#authn-account-pword)</li><li>[SQL kimlik doğrulaması kapsanan veritabanlarında kullanmayın](#autn-contained-db)</li></ul> |
| **Azure Event hub'ı** | <ul><li>[SaS belirteci kullanarak cihaz kimlik doğrulaması kimlik bilgilerini kullanın](#authn-sas-tokens)</li></ul> |
| **Azure güven sınırı** | <ul><li>[Azure yöneticileri Azure çok faktörlü kimlik doğrulamasını etkinleştir](#multi-factor-azure-admin)</li></ul> |
| **Service Fabric güven sınırı** | <ul><li>[Anonim erişim tooService Fabric kümesi kısıtla](#anon-access-cluster)</li><li>[Service Fabric istemcisi düğümü sertifikanın düğümü düğümü sertifikadan farklı olduğundan emin olun](#fabric-cn-nn)</li><li>[AAD tooauthenticate istemcileri tooservice yapı kümeleri kullanın](#aad-client-fabric)</li><li>[Service fabric sertifikaları bir onaylanmış sertifika yetkilisinden (CA) aldığınız emin olun](#fabric-cert-ca)</li></ul> |
| **Kimlik sunucusu** | <ul><li>[Kimlik sunucusu tarafından desteklenen standart kimlik doğrulama senaryoları kullanın](#standard-authn-id)</li><li>[Merhaba varsayılan kimlik sunucusunu belirteç önbelleği ile ölçeklenebilir bir alternatif geçersiz kıl](#override-token)</li></ul> |
| **Makine güven sınırı** | <ul><li>[Dağıtılan uygulamanın ikili dosyaları dijital olarak imzalandığından emin olun](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[WCF tooMSMQ kuyruklarda bağlanırken kimlik doğrulamasını etkinleştirin](#msmq-queues)</li><li>[WCF ileti clientCredentialType toonone ayarlanmadı](#message-none)</li><li>[WCF aktarım clientCredentialType toonone ayarlanmadı](#transport-none)</li></ul> |
| **Web API** | <ul><li>[Standart kimlik doğrulama teknikleri kullanılan toosecure Web API'leri olduğundan emin olun](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Azure Active Directory tarafından desteklenen standart kimlik doğrulama senaryoları kullanın](#authn-aad)</li><li>[Merhaba varsayılan ADAL belirteç önbelleği ile ölçeklenebilir bir alternatif geçersiz kıl](#adal-scalable)</li><li>[TokenReplayCache kullanılan tooprevent hello yeniden yürütme ADAL kimlik doğrulaması belirteçlerinin olduğundan emin olun](#tokenreplaycache-adal)</li><li>[Toomanage belirteci OAuth2 istemcileri tooAAD istekleri (veya şirket içi AD) ADAL kitaplıklarını kullanma](#adal-oauth2)</li></ul> |
| **IOT alan ağ geçidi** | <ul><li>[Toohello alan ağ geçidi bağlanan cihazları kimlik doğrulaması](#authn-devices-field)</li></ul> |
| **IOT bulut ağ geçidi** | <ul><li>[TooCloud ağ geçidi bağlanan cihazları doğrulanır emin olun](#authn-devices-cloud)</li><li>[Cihaz başına kimlik doğrulama kimlik bilgilerini kullan](#authn-cred)</li></ul> |
| **Azure Depolama** | <ul><li>[Bu yalnızca Merhaba kapsayıcılara ve blob'lara anonim okuma erişimi verilir gerekli olun](#req-containers-anon)</li><li>[Sınırlı erişim tooobjects SAS veya SAP kullanarak Azure depolama alanında verin](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Standart kimlik doğrulama mekanizması tooauthenticate tooWeb uygulama kullanmayı deneyin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | <p>Kimlik doğrulama, burada bir varlık genellikle bir kullanıcı adı ve parola gibi kimlik bilgilerini aracılığıyla kendi kimliklerini kanıtlayan hello işlemidir. Düşünülebilecek birden çok kimlik doğrulama protokolleri kullanılabilir vardır. Bunlardan bazıları aşağıda listelenmiştir:</p><ul><li>İstemci sertifikaları</li><li>Windows tabanlı</li><li>Formlara</li><li>Federasyon - ADFS</li><li>Federasyon - Azure AD</li><li>Federasyon - kimlik sunucusu</li></ul><p>Bir standart kimlik doğrulama mekanizması tooidentify hello kaynak işlemi kullanmayı düşünün</p>|

## <a id="handle-failed-authn"></a>Uygulamalar başarısız kimlik doğrulama senaryoları güvenli bir şekilde işlemesi gerekir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | <p>Açıkça kullanıcıların kimliğini doğrulayan uygulamalar securely.hello kimlik doğrulama mekanizması gerekir başarısız kimlik doğrulama senaryoları işlemesi gerekir:</p><ul><li>Kimlik doğrulama başarısız olduğunda tooprivileged kaynaklara erişimi reddetme</li><li>Genel hata iletisini başarısız kimlik doğrulamasından sonra görüntüler ve erişim reddedildi gerçekleşir</li></ul><p>İçin test edin:</p><ul><li>Başarısız oturum açmalar sonra ayrıcalıklı kaynakların koruma</li><li>Başarısız kimlik doğrulaması genel bir hata iletisi görüntülenir ve olay erişim reddedildi</li><li>Hesapları aşırı sayıda başarısız girişimden sonra devre dışı bırakılır</li><ul>|

## <a id="step-up-adaptive-authn"></a>Etkinleştirme adım veya uyarlamalı kimlik doğrulaması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | <p>Merhaba uygulaması ek yetkilendirme (adım yukarı gibi ya da OTP SMS, e-posta vb. veya yeniden kimlik doğrulaması için isteyen gönderme gibi çok faktörlü kimlik doğrulaması aracılığıyla Uyarlamalı kimlik doğrulaması) olduğunu doğrulayın hello kullanıcı erişim verilmeden önce kimlik doğrulaması için toosensitive bilgileri. Bu kural önemli değişiklikler tooan hesabı veya eylem yapmak için de geçerlidir</p><p>Bu da kimlik doğrulama hello uyarlama gibi içinde uygulanan toobe sahip anlamına gelir Merhaba uygulaması doğru bağlama duyarlı yetkilendirme zorlayan bir şekilde toonot olarak şekilde izin yoluyla yetkisiz işleme örnekte parametre oynama</p>|

## <a id="admin-interface-lockdown"></a>Yönetim arabirimleri uygun şekilde kilitlendiğini emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | Merhaba ilk toogrant erişim yalnızca arabiriminden bir belirli kaynak IP aralığı toohello yönetim çözümüdür. Bu çözüm her zaman daha mümkün olmayacaktır hello Yönetim arabirimine oturum açma için geçmeksizin veya uyarlamalı bir kimlik doğrulaması tooenforce önerilen |

## <a id="forgot-pword-fxn"></a>Uygulama parolası işlevler güvenli bir şekilde unuttum

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | <p>Merhaba, parola ve diğer kurtarma yolları zaman sınırlı etkinleştirme hello yerine belirteci parola kendisi de dahil olmak üzere bağlantısı Gönder unuttunuz tooverify ilk şey olur. Merhaba bağlantı üzerinden gönderilmeden önce ek kimlik doğrulama soft-belirteçleri (örn. SMS belirteci, yerel mobil uygulamalar, vb.) göre de gerekli olabilir. Hello yeni bir parola alma işlemi devam ediyor adımında ikinci olarak, size hello kullanıcıların hesabını kilitlemek değil.</p><p>Bir saldırgan otomatik bir saldırı hello kullanıcılarla toointentionally kilitlenme karar olduğunda bu tooa hizmet reddi saldırısına neden olabilir. Üçüncü Hello yeni parola isteği ediyor kümesi olduğunda, görüntü selamlama iletisine sipariş tooprevent kullanıcıadı numaralandırmada genelleştirilmiş. Dördüncü, her zaman hello eski parolaların kullanımına izin verme ve güçlü bir parola ilkesi uygulayın.</p> |

## <a id="pword-account-policy"></a>Parola ve hesap ilkesi uygulanır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| Ayrıntılar | <p>Parola ve hesap ilkesiyle uyumlu kuruluş ilkesi ve en iyi yöntemler uygulanmalıdır.</p><p>toodefend yanılma ve sözlük karşı göre tahmin: güçlü bir parola ilkesi kullanıcıların karmaşık parola (örn., 12 karakter en az uzunluk, alfasayısal ve özel karakterler) oluşturma uygulanan tooensure olması gerekir.</p><p>Hesap kilitleme ilkeleri aşağıdaki şekilde hello uygulanabilir:</p><ul><li>**Yazılım kilidi genişletme:** bu kullanıcılarınızın deneme yanılma saldırılarına karşı korumak için iyi bir seçenek olabilir. Hello kullanıcının girdiği her Örneğin, yanlış parola üç kez Merhaba uygulaması hello hesabı için bir dakika içinde sipariş tooslow hello saldırgan tooproceed için daha az karlı yapmadan parolasını zorlama kaba hello işlemi aşağı kilitlenemedi. Bu örnek elde etmek için Sabit kilitleme önlemler tooimplement olsaydı "kalıcı olarak hesapları kilitleme tarafından Dos" a. Alternatif olarak, uygulama bir OTP (bir saat parola) oluşturma ve bant dışı Gönder (e-posta, aracılığıyla sms vb.) toohello kullanıcı. Başarısız girişim sayısı eşiği sayısını ulaşıldıktan sonra başka bir yaklaşım tooimplement CAPTCHA olabilir.</li><li>**Sabit kilitleme:** uygulamanızı saldırmak kullanıcı algılamak ve onu bir yanıt takım zaman toodo kendi hukuk vardı kadar kalıcı olarak kendi hesabını kilitlemek yoluyla sayaç kilitleme bu tür uygulanmalıdır. Bu işlem toogive hello geri kullanıcı hesabının karar ya da ona karşı daha fazla yasal eylemleri gerçekleştirin. Bu tür bir yaklaşım, daha fazla uygulama ve altyapı penetrating gelen hello saldırganın engeller.</li></ul><p>Varsayılan ve tahmin edilebilir hesapları saldırılarına karşı toodefend tüm anahtarları ve parolaları değiştirilebilir, ve oluşturulan veya yükleme süresini sonra değiştirilen olduğunu doğrulayın.</p><p>Merhaba uygulaması tooauto varsa-parolaları oluşturmak, oluşturulan hello parolaları rastgele ve yüksek entropi sahip olduğundan emin olun.</p>|

## <a id="controls-username-enum"></a>Uygulama denetimleri tooprevent kullanıcıadı numaralandırması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web Uygulaması | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Tüm hata iletileri, sipariş tooprevent kullanıcıadı numaralandırmada genelleştirilmiş. Ayrıca bazen bir kayıt sayfasına gibi işlevler sızmasını bilgi kaçının olamaz. Burada toouse hız sınırlaması yöntemler CAPTCHA tooprevent otomatik bir saldırı bir saldırganın gibi gerekir. |

## <a id="win-authn-sql"></a>Mümkün olduğunda, Windows kimlik doğrulaması tooSQL sunucusuna bağlanmak için kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | OnPrem |
| **Öznitelikleri**              | SQL sürümü - tüm |
| **Başvuruları**              | [SQL Server - bir kimlik doğrulama modu seçin](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Adımları** | Windows kimlik doğrulaması, Kerberos güvenlik protokolünü kullanır, parola ilkesi zorlama şekilde toocomplexity doğrulama için güçlü parolalar, hesap kilitleme için destek sağlar ve parola süre aşımını destekler sağlar.|

## <a id="aad-authn-sql"></a>Mümkün olduğunda bağlanma tooSQL veritabanı için Azure Active Directory kimlik doğrulaması kullanın.

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | SQL Azure |
| **Öznitelikleri**              | SQL sürümü - V12 |
| **Başvuruları**              | [Bağlantı tooSQL veritabanı tarafından kullanarak Azure Active Directory kimlik doğrulaması](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Adımları** | **En düşük sürüm:** Azure SQL Database V12 hello Microsoft Directory karşı tooallow Azure SQL veritabanı toouse AAD kimlik doğrulaması gerekli |

## <a id="authn-account-pword"></a>SQL kimlik doğrulama modu kullanıldığında, hesap ve parola ilke SQL Server'da zorunlu emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [SQL Server Parola İlkesi](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Adımları** | SQL Server kimlik doğrulaması kullanırken, Windows kullanıcı hesaplarına dayalı olmayan SQL Server oturumları oluşturulur. Merhaba kullanıcı adı ve hello parola SQL Server kullanarak oluşturulur ve SQL Server içinde depolanır. SQL Server, Windows parola ilkesi mekanizmaları kullanabilirsiniz. SQL Server içinde kullanılan Windows toopasswords aynı karmaşıklık ve sona erme tarihi ilkeleri kullanılan hello uygulayabilirsiniz. |

## <a id="autn-contained-db"></a>SQL kimlik doğrulaması kapsanan veritabanlarında kullanmayın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Database | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | OnPrem, SQL Azure |
| **Öznitelikleri**              | SQL sürüm - MSSQL2012, SQL sürümü - V12 |
| **Başvuruları**              | [Kapsanan veritabanları ile en iyi güvenlik uygulamaları](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Adımları** | zorlanan parola ilkesi Hello yokluğu kapsanan bir veritabanında kuruldu zayıf bir kimlik bilgisi hello olasılığını artırabilir. Windows kimlik doğrulaması yararlanın. |

## <a id="authn-sas-tokens"></a>SaS belirteci kullanarak cihaz kimlik doğrulaması kimlik bilgilerini kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Event hub'ı | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Olay hub'ları kimlik doğrulaması ve güvenlik modeline genel bakış](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Adımları** | <p>Merhaba olay hub'ları güvenlik modelini birleşimi paylaşılan erişim imzası (SAS) belirteçleri ve olay yayımcıları üzerinde temel alır. Merhaba Yayımcı adı hello hello belirteç alan DeviceID temsil eder. Bu hello belirteçleri ile ilgili cihazları hello oluşturulan ilişkilendirmenize yardımcı.</p><p>Tüm iletileri gönderen hizmet tarafında algılama denemeleri yanıltma yükü kaynak izin verme ile etiketlenir. Cihaz kimlik doğrulamasını yaparken, Oluştur bir aygıt SaS belirteci kapsamlı tooa benzersiz yayımcı başına.</p>|

## <a id="multi-factor-azure-admin"></a>Azure yöneticileri Azure çok faktörlü kimlik doğrulamasını etkinleştir

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure Multi-Factor Authentication nedir?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Adımları** | <p>Çok faktörlü kimlik doğrulaması (MFA), birden fazla doğrulama yöntemi gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir. Her iki veya daha fazla doğrulama yöntemlerini aşağıdaki hello isteyerek çalışır:</p><ul><li>(Genellikle parola) bildiğiniz bir şey</li><li>(Kolayca, bir telefon gibi yineleniyor değil güvenilir bir cihaz) sahip olduğunuz şey</li><li>(Biyometri) olan bir şey</li><ul>|

## <a id="anon-access-cluster"></a>Anonim erişim tooService Fabric kümesi kısıtla

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure  |
| **Başvuruları**              | [Service Fabric kümesi güvenlik senaryoları](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Adımları** | <p>Kümeler, özellikle üretim iş yükleri üzerinde çalıştırılan olduğunda tooyour küme bağlanma güvenli tooprevent yetkisiz kullanıcıların her zaman olmalıdır.</p><p>Service fabric kümesi oluştururken bu hello güvenlik modunu "güvenli" çok ayarlandığından emin olun ve gerekli hello X.509 sunucu sertifikası yapılandırın. "Güvenli olmayan" bir küme oluşturma izni verdiği herhangi bir anonim kullanıcı tooconnect tooit yönetim uç noktaları toohello gösterir, genel Internet.</p>|

## <a id="fabric-cn-nn"></a>Service Fabric istemcisi düğümü sertifikanın düğümü düğümü sertifikadan farklı olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure, ortam - tek başına |
| **Başvuruları**              | [Service Fabric istemcisi düğümü sertifika güvenliği](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [Bağlan tooa güvenli küme istemci sertifikası kullanarak](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Adımları** | <p>İstemci düğüm sertifika güvenliği hello küme hello Azure portal aracılığıyla, Resource Manager şablonları ya da tek başına JSON şablonunu yönetici istemci sertifikası ve/veya bir kullanıcı istemci sertifikası belirterek oluşturulurken yapılandırılır.</p><p>Belirttiğiniz hello yönetici istemci ve kullanıcı istemci sertifikası düğümü düğümü güvenlik için belirttiğiniz hello birincil ve ikincil sertifikaları farklı olmalıdır.</p>|

## <a id="aad-client-fabric"></a>AAD tooauthenticate istemcileri tooservice yapı kümeleri kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure |
| **Başvuruları**              | [Kümesi güvenlik senaryolarını - güvenlik önerileri](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Adımları** | Azure üzerinde çalışan kümelerle toohello yönetim uç noktalarının Azure Active Directory (AAD), istemci sertifikalarını dışında kullanarak erişim güvenliğini sağlayabilirsiniz. Azure kümeler için düğümü düğümü güvenlik için AAD güvenlik tooauthenticate istemcileri ve sertifikalar kullanmanız önerilir.|

## <a id="fabric-cert-ca"></a>Service fabric sertifikaları bir onaylanmış sertifika yetkilisinden (CA) aldığınız emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Service Fabric güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ortam - Azure |
| **Başvuruları**              | [X.509 sertifikaları ve Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Adımları** | <p>Service Fabric, kimlik doğrulama, düğümlerin ve istemciler için X.509 sertifikaları kullanır.</p><p>Hizmet fabrics'e sertifikalar kullanırken bazı önemli noktalar tooconsider:</p><ul><li>Üretim iş yükleri çalıştıran kümelerde kullanılan sertifikaları doğru yapılandırılmış bir Windows Server sertifika hizmeti kullanılarak oluşturulan veya bir onaylanmış sertifika yetkilisinden (CA) edinilen. Merhaba CA onaylanmış bir dış CA veya bir düzgün yönetilen iç ortak anahtar altyapısı (PKI) olabilir</li><li>Hiçbir zaman hiçbir geçici kullanın veya MakeCert.exe gibi araçları ile oluşturulmuş üretim sertifikaları test et</li><li>Kendinden imzalı bir sertifika kullanabilirsiniz, ancak yalnızca test kümeleri için alan ve üretim bunu</li></ul>|

## <a id="standard-authn-id"></a>Kimlik sunucusu tarafından desteklenen standart kimlik doğrulama senaryoları kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [IdentityServer3 - hello büyük resmi](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Adımları** | <p>Aşağıda hello kimlik sunucusu tarafından desteklenen tipik etkileşimler şunlardır:</p><ul><li>Tarayıcılar web uygulamaları ile iletişim</li><li>Web uygulamalarını web API'leri (bazen üzerinde kendi, bazen bir kullanıcı adına) ile iletişim</li><li>Tarayıcı tabanlı uygulamalar, web API'leri ile iletişim</li><li>Yerel uygulamalar, web API ile iletişim</li><li>Sunucu tabanlı uygulamalar, web API'leri ile iletişim</li><li>Web API web API'leri (bazen üzerinde kendi, bazen bir kullanıcı adına) ile iletişim</li></ul>|

## <a id="override-token"></a>Merhaba varsayılan kimlik sunucusunu belirteç önbelleği ile ölçeklenebilir bir alternatif geçersiz kıl

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Kimlik sunucusu | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Kimlik sunucusu dağıtım - önbelleğe alma](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Adımları** | <p>IdentityServer basit, yerleşik bir bellek içi önbellek bulunur. Bu küçük ölçekli yerel uygulamalar için iyi olmakla birlikte, aşağıdaki nedenlerden hello için orta katman ve arka uç uygulamaların ölçeklenmez:</p><ul><li>Bu uygulamaları aynı anda birden çok kullanıcı tarafından erişilir. Tüm erişim belirteçleri aynı depolama yalıtım sorunlar oluşturur ve ölçekte çalışırken zorluklar sunar hello kaydetme: hello kaynakları şirket adına, uygulama erişimleri hello gibi çok sayıda kullanıcı, her sayıda belirteçleri ile büyük sayılar ve çok pahalı arama gelebilir işlemleri</li><li>Bu uygulamalar genellikle birden çok düğüm gerekir sahip olduğu erişim toohello dağıtılmış topolojileri dağıtılan aynı önbellek</li><li>Önbelleğe alınan belirteçleri, işlem dönüştürür ve deactivations varlığını sürdürmesini gerekir</li><li>Web uygulamaları, uygulama yüklenirken nedeniyle, yukarıdaki tüm hello için toooverride hello varsayılan kimlik sunucunun belirteç önbelleği ile Azure Redis önbelleği gibi ölçeklenebilir bir alternatif önerilir.</li></ul>|

## <a id="binaries-signed"></a>Dağıtılan uygulamanın ikili dosyaları dijital olarak imzalandığından emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Makine güven sınırı | 
| **SDL aşaması**               | Dağıtım |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Böylece hello ikili dosyaları Hello bütünlüğünü doğrulanabilir dağıtılan uygulamanın ikili dosyaları dijital olarak imzalandığından emin olun|

## <a id="msmq-queues"></a>WCF tooMSMQ kuyruklarda bağlanırken kimlik doğrulamasını etkinleştirin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, NET Framework 3 |
| **Öznitelikleri**              | Yok |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Adımları** | Program tooMSMQ sıraları bağlanırken tooenable kimlik doğrulama başarısız olursa, bir saldırganın anonim olarak işleme iletileri toohello sırası gönderebilirsiniz. Kimlik doğrulaması kullanılan tooconnect tooan MSMQ kullanılan sırasının toodeliver bir ileti tooanother program değilse, bir saldırgan kötü amaçlı bir anonim iletisi gönder.|

### <a name="example"></a>Örnek
Merhaba `<netMsmqBinding/>` hello WCF yapılandırma dosyasının aşağıdaki öğesinin WCF toodisable kimlik doğrulama ileti teslimi tooan MSMQ sırası bağlanırken bildirir.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Gelen veya giden iletiler için her zaman MSMQ toorequire Windows etki alanı veya sertifika kimlik doğrulamasını yapılandırın.

### <a name="example"></a>Örnek
Merhaba `<netMsmqBinding/>` hello WCF yapılandırma dosyasının aşağıdaki öğesinin tooan MSMQ sırası bağlanırken WCF tooenable sertifika kimlik doğrulaması talimatı verir. Merhaba istemci X.509 sertifikalarını kullanarak kimlik doğrulaması yapılır. Merhaba istemci sertifikası hello sunucusunun sertifika deposuna hello mevcut olması gerekir.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>WCF ileti clientCredentialType toonone ayarlanmadı

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | .NET framework 3 |
| **Öznitelikleri**              | İstemci kimlik bilgisi türü - yok |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | kimlik doğrulama Hello yokluğu herkes anlamına gelir mümkün tooaccess bu hizmetidir. İstemcilerinden kimlik doğrulama kullanmaz bir hizmet tooall kullanıcıların erişim sağlar. İstemci kimlik bilgileri karşı Hello uygulama tooauthenticate yapılandırın. Bu, hello ileti clientCredentialType tooWindows ya da sertifika ayarlayarak yapılabilir. |

### <a name="example"></a>Örnek
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>WCF aktarım clientCredentialType toonone ayarlanmadı

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | WCF | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, .NET Framework 3 |
| **Öznitelikleri**              | İstemci kimlik bilgisi türü - yok |
| **Başvuruları**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Adımları** | kimlik doğrulama Hello yokluğu herkes anlamına gelir mümkün tooaccess bu hizmetidir. İstemcilerinden kimlik doğrulama kullanmaz bir hizmetin tüm kullanıcıların tooaccess işlevselliği sağlar. İstemci kimlik bilgileri karşı Hello uygulama tooauthenticate yapılandırın. Bu, hello aktarım clientCredentialType tooWindows ya da sertifika ayarlayarak yapılabilir. |

### <a name="example"></a>Örnek
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Standart kimlik doğrulama teknikleri kullanılan toosecure Web API'leri olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Web API | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Kimlik doğrulama ve yetkilendirme ASP.NET Web API'de](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), [ASP.NET Web API ile dış kimlik doğrulama hizmeti (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **Adımları** | <p>Kimlik doğrulama, burada bir varlık genellikle bir kullanıcı adı ve parola gibi kimlik bilgilerini aracılığıyla kendi kimliklerini kanıtlayan hello işlemidir. Düşünülebilecek birden çok kimlik doğrulama protokolleri kullanılabilir vardır. Bunlardan bazıları aşağıda listelenmiştir:</p><ul><li>İstemci sertifikaları</li><li>Windows tabanlı</li><li>Formlara</li><li>Federasyon - ADFS</li><li>Federasyon - Azure AD</li><li>Federasyon - kimlik sunucusu</li></ul><p>Her hello kimlik doğrulama şemasını nasıl olabilir üzerinde alt düzey ayrıntıların toosecure bir Web API uygulanan hello başvuruları bölümdeki bağlantılar sağlar.</p>|

## <a id="authn-aad"></a>Azure Active Directory tarafından desteklenen standart kimlik doğrulama senaryoları kullanın

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure AD | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Azure AD için kimlik doğrulama senaryoları](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory kod örnekleri](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Azure Active Directory Geliştirici Kılavuzu](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Adımları** | <p>Azure Active Directory (Azure AD), OAuth 2.0 ve Openıd Connect gibi endüstri standardı protokoller desteği olan bir hizmet olarak kimlik sağlayarak geliştiriciler için kimlik doğrulama basitleştirir. Aşağıda Azure AD tarafından desteklenen beş birincil uygulama senaryoları hello şunlardır:</p><ul><li>Web tarayıcısı tooWeb uygulama: bir kullanıcı Azure AD tarafından güvenli hale getirilen tooa web uygulamasında toosign gerekiyor</li><li>Tek sayfa uygulama (SPA): Bir kullanıcının Azure AD tarafından güvenli hale getirilen tooa tek sayfa uygulamada toosign gerekir.</li><li>Yerel uygulama tooWeb API: Azure AD tarafından güvenli hale getirilen telefon, tablet veya PC gereksinimlerini tooauthenticate kullanıcı tooget kaynakları bir web API çalışan bir yerel uygulaması</li><li>Web uygulama tooWeb API: tooget kaynaklardan bir web API'sini Azure AD tarafından güvenliği sağlanan bir web uygulaması gerekiyor</li><li>Arka plan programı veya sunucu uygulaması tooWeb API: arka plan programı uygulamanın veya bir sunucu uygulaması web kullanıcı arabirimi ile bir web API'sini Azure AD tarafından güvenli hale getirilmiş tooget kaynaklardan gerekiyor</li></ul><p>Hello başvurular bölümüne toohello bağlantıları alt düzey uygulama ayrıntıları için lütfen bakın</p>|

## <a id="adal-scalable"></a>Merhaba varsayılan ADAL belirteç önbelleği ile ölçeklenebilir bir alternatif geçersiz kıl

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure AD | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Web uygulamaları için Azure Active Directory ile modern kimlik doğrulaması](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/), [kullanarak Redis ADAL belirteç önbelleği olarak](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)  |
| **Adımları** | <p>ADAL (Active Directory Authentication Library) kullanımdır işlem genelinde kullanılabilir bir statik depolamaya dayanır bir bellek içi önbellek hello varsayılan önbellek. Bu yerel uygulamalar için çalışırken, aşağıdaki nedenlerden hello için orta katman ve arka uç uygulamaların ölçeklenmez:</p><ul><li>Bu uygulamaları aynı anda birden çok kullanıcı tarafından erişilir. Tüm erişim belirteçleri aynı depolama yalıtım sorunlar oluşturur ve ölçekte çalışırken zorluklar sunar hello kaydetme: hello kaynakları şirket adına, uygulama erişimleri hello gibi çok sayıda kullanıcı, her sayıda belirteçleri ile büyük sayılar ve çok pahalı arama gelebilir işlemleri</li><li>Bu uygulamalar genellikle birden çok düğüm gerekir sahip olduğu erişim toohello dağıtılmış topolojileri dağıtılan aynı önbellek</li><li>Önbelleğe alınan belirteçleri, işlem dönüştürür ve deactivations varlığını sürdürmesini gerekir</li></ul><p>Web uygulamaları, uygulama yüklenirken nedeniyle, yukarıdaki tüm hello için toooverride hello varsayılan ADAL belirteç önbelleği ile Azure Redis önbelleği gibi ölçeklenebilir bir alternatif önerilir.</p>|

## <a id="tokenreplaycache-adal"></a>TokenReplayCache kullanılan tooprevent hello yeniden yürütme ADAL kimlik doğrulaması belirteçlerinin olduğundan emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure AD | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [Web uygulamaları için Azure Active Directory ile modern kimlik doğrulaması](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) |
| **Adımları** | <p>Geliştiriciler toodefine belirteç yeniden yürütme önbellek, herhangi bir belirteci belirteçleri hello amacı, doğrulama için kaydetmek için kullanılan bir mağaza birden çok kez kullanılabilir Hello TokenReplayCache özelliği sağlar.</p><p>Bu ortak saldırılara karşı bir ölçü hello aptly belirteç yeniden yürütme saldırı çağrılmaz: oturum açma sırasında gönderilen hello belirteci kesintiye uğratan bir saldırganın toosend deneyebilirsiniz onu yeniden toohello uygulama ("yeni bir oturum oluşturmak için anlayamazsanız"). Örn., içinde OIDC kodu-verme akışı başarılı kullanıcı kimlik doğrulamasının ardından, bir istek çok "/ signin-oidc" Merhaba bağlı olan taraf uç nokta "id_token" ile "code" ve "Durum" parametreleri yapılan.</p><p>bağlı olan taraf hello bu isteği doğrular ve yeni bir oturum oluşturur. Bir saldırganın bu isteği yakalar ve bunu başlayarak yeniden oynatılır, klasöründe başarılı bir oturum ve sızma hello kullanıcı kurabilirsiniz. Openıd Connect içinde hello nonce Hello varlığını sınırlamak ancak tam olarak hangi hello saldırı başarıyla kamulaştırılmış hello durumlarda ortadan kaldırmak. Geliştiriciler uygulamalarını tooprotect bir ITokenReplayCache belirtin ve bir örnek tooTokenReplayCache atayın.</p>|

### <a name="example"></a>Örnek
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Örnek
Burada, örnek uygulama hello ITokenReplayCache arabiriminin verilmiştir. (Lütfen özelleştirmek ve projeye özgü önbelleğe alma framework'ünüzün uygulama)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
uygulanan hello önbelleğe hello "Tokenvalidationparameters değerini" özelliği aracılığıyla OIDC seçeneklerini aşağıdaki gibi başvurulan toobe sahiptir.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Lütfen, bu yapılandırma, oturum açma uygulamanıza yerel OIDC korumalı tootest hello verimliliğini unutmayın ve hello isteği çok yakalama`"/signin-oidc"` fiddler'da uç noktası. Merhaba koruma yerinde olmadığı durumlarda, bu istek fiddler'da yeniden oynatmak yeni bir oturum tanımlama ayarlayın. Merhaba TokenReplayCache koruma eklendikten sonra hello isteği tekrarlanır, Merhaba uygulaması gibi bir özel durum oluşturur:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Toomanage belirteci OAuth2 istemcileri tooAAD istekleri (veya şirket içi AD) ADAL kitaplıklarını kullanma

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure AD | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Adımları** | <p>Hello Azure AD authentication Library (ADAL) etkinleştirir istemci uygulama geliştiricilerin tooeasily kullanıcılar toocloud kimlik doğrulaması veya şirket içi Active Directory (AD) ve API çağrıları güvenliğini sağlamak için erişim belirteci alın.</p><p>ADAL sahip birçok özellik yapma kimlik doğrulamanın daha kolay zaman uyumsuz desteği, erişim belirteçleri ve yenileme belirteçleri, bir erişim belirtecinin süresi ve yenileme belirteci kullanılabilir olduğunda otomatik belirteci yenileme depolar yapılandırılabilir bir belirteç önbelleği gibi geliştiriciler için ve Daha fazla.</p><p>Çoğu hello karmaşıklık işleyerek ADAL kendi iş mantığı Geliştirici odaklanmanıza yardımcı olmak ve kolayca kaynakları güvenlik uzmanı olmadan güvenli hale getirme. Ayrı kitaplıklar, .NET, JavaScript (istemci ve Node.js), iOS, Android ve Java için kullanılabilir.</p>|

## <a id="authn-devices-field"></a>Toohello alan ağ geçidi bağlanan cihazları kimlik doğrulaması

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT alan ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok  |
| **Başvuruları**              | Yok  |
| **Adımları** | Her cihaz bunları verileri kabul etmek ve hello bulut ağ geçidi Yukarı Akış iletişimlerinizde kolaylaştırmanın önce hello alan ağ geçidi tarafından doğrulandıktan emin olun. Ayrıca, aygıtlar ile bağlanmasını sağlamak bir aygıt başına tek bir cihazı benzersiz olarak tanımlanabilir böylece kimlik bilgisi.|

## <a id="authn-devices-cloud"></a>TooCloud ağ geçidi bağlanan cihazları doğrulanır emin olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel, C#, Node.JS,  |
| **Öznitelikleri**              | Yok, ağ geçidi seçim - Azure IOT Hub |
| **Başvuruları**              | Yok, [.NET ile Azure IOT hub](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [olan IOT hub'ı kullanmaya başlama ve düğüm JS](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [SAS ve sertifikaları ile güvenli hale getirme IOT](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Git deposu](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Adımları** | <ul><li>**Genel:** Aktarım Katmanı Güvenliği (TLS) veya IPSec kullanarak kimlik doğrulaması yap hello cihazı. Altyapı önceden paylaşılan anahtar (PSK) kullanarak tam asimetrik şifreleme işleyemiyor bu cihazlarda desteklemelidir. Azure AD, Oauth yararlanın.</li><li>**C# ' ta:** DeviceClient örneği oluşturulurken varsayılan olarak hello oluşturma yöntemi IOT Hub ile Merhaba AMQP protokolünü toocommunicate kullanan bir DeviceClient örneği oluşturur. toouse hello HTTPS protokolünü toospecify hello Protokolü sağlayan hello oluşturma yönteminin hello geçersiz kılma kullanın. Merhaba HTTPS protokolünü kullanıyorsanız hello de eklemeniz gerekir `Microsoft.AspNet.WebApi.Client` NuGet paketi tooyour proje tooinclude hello `System.Net.Http.Formatting` ad alanı.</li></ul>|

### <a name="example"></a>Örnek
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Örnek
**Node.JS: kimlik doğrulaması**
#### <a name="symmetric-key"></a>Simetrik anahtar
* Azure üzerinde bir IOT hub oluşturma
* Merhaba cihaz kimlik kayıt defterinde bir giriş oluşturun
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Sanal bir cihaz oluşturma
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>SAS belirteci
* Kullanırken, simetrik anahtar ancak dahili olarak oluşturulan oluşturabilir ve açıkça de kullanın
* Bir protokol tanımlayın:`var Http = require('azure-iot-device-http').Http;`
* Bir sas belirteci oluşturun:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* SAS belirteci kullanarak bağlan: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Sertifikalar
* Kendi imzalı X509 Oluştur kullanarak sertifika OpenSSL toogenerate gibi sırasıyla bir .cert ve .key dosyaları toostore hello sertifika ve başlangıç anahtarı aracı
* Sertifikaları kullanarak güvenli bir bağlantı kabul eden bir cihaz hazırlayın.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Bir sertifika kullanarak bir aygıtı bağlayın
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Cihaz başına kimlik doğrulama kimlik bilgilerini kullan

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | IOT bulut ağ geçidi  | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Ağ geçidi seçim - Azure IOT Hub |
| **Başvuruları**              | [Azure IOT Hub güvenlik belirteçleri](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Adımları** | SaS belirteci kullanarak cihaz kimlik doğrulaması kimlik bilgilerini başına kullanım aygıt anahtarı veya istemci sertifikası göre IOT Hub düzeyi yerine paylaşılan erişim ilkeleri. Bu bir başkası tarafından bir aygıt veya alan ağ geçidi'nin kimlik doğrulama belirteçleri hello kullanılmasını engeller |

## <a id="req-containers-anon"></a>Bu yalnızca Merhaba kapsayıcılara ve blob'lara anonim okuma erişimi verilir gerekli olun

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | StorageType - Blob |
| **Başvuruları**              | [Anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [paylaşılan erişim imzaları, 1. Bölüm: Merhaba SAS modelini anlama](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Adımları** | <p>Varsayılan olarak, bir kapsayıcı ve içindeki tüm BLOB'ları yalnızca hello hello depolama hesabının sahibi tarafından erişilebilir. toogive anonim kullanıcıların Okuma izinleri tooa kapsayıcı ve bloblarını, bir hello kapsayıcı izinleri tooallow genel erişim ayarlayabilirsiniz. Anonim kullanıcılar genel olarak erişilebilir bir kapsayıcıdaki blobları hello isteği doğrulanmadan okuyabilir.</p><p>Kapsayıcılar kapsayıcı erişimi yönetmek için seçenekler aşağıdaki hello sağlar:</p><ul><li>Tam herkese okuma erişimi: kapsayıcı ve blob verilerini anonim istek okunabilir. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.</li><li>Ortak okuma erişiminin yalnızca BLOB'lar için: Bu kapsayıcı içindeki Blob verilerini anonim istek okunabilir ancak kapsayıcı verileri kullanılabilir değil. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları numaralandırılamıyor</li><li>Hiçbir public okuma erişimi: kapsayıcı ve blob verilerini yalnızca hello hesap sahibi tarafından okunabilir</li></ul><p>Anonim erişim burada belirli BLOB'lar her zaman için anonim okuma erişimini kullanılabilir olmalıdır senaryoları için en iyisidir. Geçirmiş denetim için bir farklı izinleri kullanarak toodelegate kısıtlı erişim sağlayan bir paylaşılan erişim imzası oluşturabilirsiniz ve belirli bir zaman aralığı içinde. Kapsayıcılar ve olası hassas verileri içerebilir, bloblar anonim erişim yanlışlıkla verilmez emin olun</p>|

## <a id="limited-access-sas"></a>Sınırlı erişim tooobjects SAS veya SAP kullanarak Azure depolama alanında verin

| Başlık                   | Ayrıntılar      |
| ----------------------- | ------------ |
| **Bileşen**               | Azure Storage | 
| **SDL aşaması**               | Oluşturma |  
| **İlgili teknolojiler** | Genel |
| **Öznitelikleri**              | Yok |
| **Başvuruları**              | [Paylaşılan erişim imzalar, 1. Bölüm: Merhaba SAS modelini anlama](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [paylaşılan erişim imzaları, bölüm 2: oluşturma ve bir SAS Blob storage'ı kullanma](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [nasıl toodelegate erişim hesabı kullanarak tooobjects Paylaşılan erişim imzaları ve saklı erişim ilkeleri](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Adımları** | <p>Güçlü şekilde toogrant sınırlı erişim tooobjects tooexpose hesap erişim tuşu sahip olmayan bir depolama hesabı tooother istemcileri, paylaşılan erişim imzası (SAS) kullanmaktır. Merhaba SAS kendi sorgu parametrelerini kapsayan bir URI değil tüm kimlik doğrulaması için gerekli olan hello bilgileri tooa depolama kaynağı erişebilirsiniz. tooaccess depolama kaynaklarını hello SAS ile Merhaba istemci hello SAS toohello uygun Oluşturucusu veya yöntemi toopass yeterlidir.</p><p>Merhaba hesap anahtarı ile güvenilemez, depolama hesabı tooa istemcisinde tooprovide erişim tooresources istediğinizde bir SAS kullanabilirsiniz. Depolama hesabı anahtarlarını hem her ikisi de yönetimsel erişim tooyour hesabı ve tüm hello kaynaklarında vermek birincil ve ikincil bir anahtar içerir. Hesap anahtarlarınızı birini gösterme, kötü amaçlı ya da ihmalkar kullanım hesap toohello olasılığını açılır. Paylaşılan erişim imzaları diğer tooread, yazma ve silme verilerini verilen toohello izinler göre depolama hesabınızda ve hello hesap anahtarı için gerek kalmadan istemcilerin güvenli bir alternatif sunar.</p><p>Bir mantıksal parametrelerinin her zaman benzer varsa, depolanan erişim ilkesi (SAP) kullanarak daha iyi bir fikirdir. Depolanan bir erişim ilkesi tarafından türetilmiş SAS kullanarak verdiğinden SAS hemen, bu en iyi yöntem tooalways hello önerilen olduğunu hello özelliği toorevoke depolanan erişim ilkeleri mümkün olduğunda kullanın.</p>|
