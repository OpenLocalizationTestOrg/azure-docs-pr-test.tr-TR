---
title: Mobile Services tooan mobil uygulama hizmeti gelen aaaMigrate
description: "Nasıl tooeasily geçirmek, Mobile Services uygulama tooan mobil uygulama hizmeti öğrenin"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Var olan Azure mobil hizmeti tooAzure uygulama hizmeti geçirme
Merhaba ile [Azure uygulama hizmeti genel kullanılabilirliğini], Azure Mobile Services'ın siteleri kolayca olabilir geçirilen yerinde tootake özelliğinden tüm hello Azure uygulama hizmeti.  Bu belge, sitenizi Azure Mobile Services tooAzure App Service ' geçiş sırasında hangi tooexpect açıklar.

## <a name="what-does-migration-do"></a>Geçiş tooyour site ne yapar
Azure Mobile hizmetinizi geçişini kapatır mobil hizmetiniz bir [Azure App Service] hello kodunu etkilemeden uygulama.  Bildirim hub'ları, SQL veri bağlantısı, kimlik doğrulama ayarları, zamanlanmış işler ve etki alanı adı değişmeden kalır.  Azure mobil hizmeti kullanarak mobil istemciler toooperate normal şekilde devam eder.  Aktarılan tooAzure uygulama hizmeti başladıktan sonra geçiş hizmetinizi yeniden başlatır.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Sitenizi neden geçirmelisiniz
Microsoft, Azure mobil hizmeti tootake özelliğinden hello Azure uygulama hizmeti geçirmek öneren:

* Yeni ana bilgisayara özellikleri [WebJobs] ve [özel etki alanı adlarını].
* Bağlantı tooyour şirket içi kullanarak kaynakları [VNet] ayrıca çok[karma bağlantılar].
* İzleme ve sorun giderme ile New Relic veya [Application Insights].
* Yerleşik DevOps araçları dahil olmak üzere [yuvaları hazırlama], geri alma ve üretim sınama.
* [Otomatik ölçek], Yük Dengeleme, ve [performans izleme].

Azure uygulama hizmeti hello avantajları hakkında daha fazla bilgi için bkz: Merhaba [Mobile Services vs. Uygulama hizmeti] konu.

## <a name="before-you-begin"></a>Başlamadan önce
Sitenizde herhangi bir ana iş başlamadan önce SQL veritabanı ve mobil hizmeti betikleri yedeklemeniz gerekir.

## <a name="migrating-site"></a>Sitelerinizin geçirme
Merhaba geçiş işlemi, tek bir Azure bölge içindeki tüm siteleri geçirir.

toomigrate sitenizi:

1. İçinde toohello oturum [Klasik Azure portalı].
2. Bir mobil hizmeti seçin hello bölgede toomigrate istiyor.
3. Merhaba tıklatın **tooApp hizmet geçirmek** düğmesi.

   ![Merhaba geçirme düğmesi][0]
4. Merhaba geçirme tooApp hizmet iletişim okuyun.
5. Mobil hizmetinizi Hello adını sağlanan hello kutusuna girin.  Örneğin, etki alanı adınızı contoso.azure mobile.net ise, enter *contoso* hello kutusunda sağlanan.
6. Merhaba onay düğmesine tıklayın.

Merhaba geçiş hello etkinlik İzleyicisi'nde Hello durumunu izleyin. Siteniz olarak listelenen *geçirme* hello Klasik Azure Portalı'nda.

  ![Geçiş etkinliğini izleme][1]

Her geçiş herhangi bir yere Geçirilmekte olan mobil hizmeti başına 3 too15 dakika sürebilir.  Sitenizi hello geçiş sırasında kullanılabilir olarak kalır.
Sitenizi hello hello geçiş işleminin sonunda yeniden başlatılır.  Merhaba site birkaç saniye sürebilir hello yeniden başlatma işlemi sırasında kullanılamıyor.

## <a name="finalizing-migration"></a>Merhaba geçiş Tamamlanıyor
Tootest hello sonuç hello geçiş işleminin mobil bir istemcide sitenizden planlayın.  Değişiklikleri toohello mobil istemcisi olmayan tüm ortak istemci eylemleri gerçekleştirebilir emin olun.  

### <a name="update-app-service-tier"></a>Uygun bir uygulama hizmeti fiyatlandırma katmanı seçin
Uygulama hizmeti tooAzure geçirdikten sonra fiyatlandırma daha fazla esneklik bulunur.

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **App Service planı** hello ayarları menüsünde.
5. Merhaba tıklatın **fiyatlandırma katmanı** döşeme.
6. Merhaba döşeme uygun tooyour gereksinimleri tıklayın ve ardından **seçin**.  TooClick gerekebilir **tüm görüntüle** toosee hello fiyatlandırma katmanlarına kullanılabilir.

Bir başlangıç noktası olarak katmanlar izleyerek hello öneririz:

| Mobil hizmet fiyatlandırma katmanı | Uygulama hizmeti fiyatlandırma katmanı |
|:--- |:--- |
| Ücretsiz |F1 Ücretsiz |
| Temel |B1 Basic |
| Standart |S1 Standart |

Sağ fiyatlandırma katmanı, uygulamanız için hello seçerken büyük oranda esneklik yoktur.  Çok başvuran[App Service fiyatlandırması] Merhaba yeni App Service fiyatlandırması hakkında tam bilgi.

> [!TIP]
> Merhaba App Service standart katmanını içeren toouse, isteyebilirsiniz toomany özelliklere erişim dahil olmak üzere [yuvaları hazırlama], otomatik yedeklemeler ve otomatik ölçeklendirme.  Varken hello yeni özelliklerini kullanıma bakın!
>
>

### <a name="review-migration-scheduler-jobs"></a>Merhaba geçirilen zamanlayıcı işlerinin gözden geçirin
Zamanlayıcı işlerinin geçişten sonra yaklaşık 30 dakika kadar görünür olmaz.  Zamanlanan işler toorun hello arka planda devam eder.
tooview yeniden görünür sonra zamanlanan işleriniz:

1. İçinde toohello oturum [Azure portal].
2. Seçin **Gözat >**, girin **zamanlama** hello içinde *filtre* kutusuna ve ardından **Zamanlayıcı koleksiyonları**.

Ücretsiz zamanlayıcı işleri kullanılabilir geçiş sonrası sınırlı sayıda vardır.  Kullanım ve hello gözden [Azure Zamanlayıcı planları].

### <a name="configure-cors"></a>Gerekirse CORS'yi yapılandırın
Çıkış noktaları arası kaynak paylaşma teknik tooallow bir Web sitesi tooaccess farklı bir etki alanındaki bir Web API ' dir.  İlişkili bir Web sitesi ile Azure Mobile Services kullanıyorsanız, tooconfigure hello geçiş işleminin parçası olarak CORS gerekir.  Yalnızca mobil aygıtlardan Azure Mobile Services erişiyorsanız, CORS dışında nadir durumlarda yapılandırılmış toobe gerekmez.

Geçirilen CORS ayarlarınızı hello kullanılabilir **MS_CrossDomainWhitelist** uygulama ayarı.  toomigrate, site toohello App Service CORS tesis:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **CORS** hello API menüsünde.
5. Sağlanan hello kutusuna her birinden sonra Enter tuşuna basarak tüm izin verilen çıkış noktası girin.
6. İzin verilen çıkış noktası listesini doğru olduğunda hello Kaydet düğmesine tıklayın.

> [!TIP]
> Bir Azure uygulama hizmeti kullanmanın yararları hello biri üzerinde hello web siteniz ve mobil hizmet çalıştırabilirsiniz aynı site.  Daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.
>
>

### <a name="download-publish-profile"></a>Yeni bir yayımlama profili indirin
Yayımlama Hello profili sitenizin tooAzure uygulama hizmeti geçiş sırasında değiştirilir.  Visual Studio içinde sitenizden toopublish düşünüyorsanız, yeni bir yayımlama profili gerekir.  toodownload hello yeni yayımlama profili:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Tıklatın **Get yayımlama profili**.

Merhaba PublishSettings dosyasını karşıdan yüklenen tooyour bilgisayardır.  Normalde adlı *sitename*. PublishSettings.  Yayımlama ayarları varolan projenize alma hello:

1. Visual Studio ve Azure mobil hizmet projenizi açın.
2. Merhaba, projenize sağ tıklayıp **Çözüm Gezgini** seçip **Yayımla...**
3. Tıklatın **alma**
4. Tıklatın **Gözat** ve seçin, indirilen yayımlama ayarları dosyası.  **Tamam**’a tıklayın.
5. Tıklatın **bağlantıyı doğrula** tooensure hello ayarları iş yayımlayın.
6. Tıklatın **Yayımla** toopublish sitenizi.

## <a name="working-with-your-site"></a>Site geçiş sonrası ile çalışma
Yeni uygulama hizmetiniz hello ile çalışmaya başlamak [Azure portal] geçiş sonrası.  Merhaba hello tooperform kullanılan bazı notlar belirli işlemlerini şunlardır [Klasik Azure portalı], kendi uygulama hizmeti eşdeğer birlikte.

### <a name="publishing-your-site"></a>İndirme ve geçirilen sitenizi yayımlama
Sitenizin git veya ftp aracılığıyla kullanılabilir ve WebDeploy, TFS, Mercurial, GitHub ve FTP dahil olmak üzere çeşitli farklı mekanizmaları ile yeniden.  Merhaba dağıtım kimlik bilgileri hello sitenizi kalanıyla geçirilir.  Dağıtım kimlik bilgilerinizi ayarlamamış veya bunları hatırlamıyorsanız, bunları sıfırlayabilirsiniz:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **dağıtım kimlik bilgileri** menü yayımlama hello içinde.
5. Merhaba yeni dağıtım kimlik bilgileri hello kutulara girin, sonra hello Kaydet düğmesine tıklayın.

Bu kimlik bilgileri tooclone hello site git ile kullanın veya otomatik dağıtımları GitHub, TFS veya Mercurial ayarlayın.  Daha fazla bilgi için bkz: Merhaba [Azure uygulama hizmeti dağıtım belgeleri].

### <a name="appsettings"></a>Uygulama ayarları
Geçirilen bir mobil hizmet için çoğu ayarları aracılığıyla uygulama ayarlarını kullanılabilir.  Hello hello uygulama ayarları listesi elde edebilirsiniz [Azure portal].
tooview veya uygulama ayarlarınızı değiştirin:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **uygulama ayarları** hello genel menüsünde.
5. Toohello uygulama ayarları bölümüne kaydırın ve uygulama ayarını bulun.
6. Merhaba değerini hello uygulama ayarı tooedit hello'ı tıklatın.  Tıklatın **kaydetmek** toosave hello değeri.

Merhaba birden çok uygulama ayarlarını güncelleştirebilirsiniz aynı anda.

> [!TIP]
> İki uygulama ayarları hello ile aynı değer.  Örneğin, görebileceğiniz *ApplicationKey* ve *MS\_ApplicationKey*.  Merhaba, hem uygulama ayarlarını güncelleştirme aynı anda.
>
>

### <a name="authentication"></a>Kimlik doğrulaması
Tüm kimlik doğrulama ayarları, uygulama ayarları geçirilen siteniz olarak kullanılabilir.  tooupdate kimlik doğrulama ayarlarınızı uygun uygulama ayarları değiştirmeniz gerekir.  Merhaba aşağıdaki tabloda, kimlik doğrulama sağlayıcısı için hello uygun uygulaması ayarları gösterilmektedir:

| Sağlayıcı | İstemci kimliği | İstemci parolası | Diğer ayarları |
|:--- |:--- |:--- |:--- |
| Microsoft Hesabı |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_Aadclientıd** | |**MS\_AadTenants** |

Not: **MS\_AadTenants** Kiracı etki alanları (Merhaba "İzin verilen kiracılar" alanları hello Mobile Services Portalı'nda) virgülle ayrılmış bir listesi olarak depolanır.

> [!WARNING]
> **Merhaba kimlik doğrulama mekanizmaları hello ayarlar menüsünde kullanmayın**
>
> Azure uygulama hizmeti sağlayan ayrı bir "kod yok" kimlik doğrulama ve yetkilendirme sistemi hello altında *kimlik doğrulama / yetkilendirme* ayarlar menüsünü ve (kullanım dışı) hello *Mobil kimlik doğrulaması* hello ayarları menüsündeki seçeneği.  Bu seçenekleri geçirilen bir Azure mobil hizmeti ile uyumlu değil.  Yapabilecekleriniz [sitenizi yükseltme](app-service-mobile-net-upgrading-from-mobile-services.md) tootake avantajı hello Azure App Service kimlik doğrulama.
>
>

### <a name="easytables"></a>Veri
Merhaba *veri* Mobile Services sekmesinde tarafından değiştirildi *kolay tabloları* hello Azure portalı içinde.  tooaccess kolay tabloları:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **kolay tabloları** hello mobil menüsünde.

Merhaba tıklayarak bir tablo ekleyebilirsiniz **Ekle** düğmesini veya bir tablo adı tıklayarak mevcut tablolarınızı erişim.  Bu dikey pencereden yapabileceğiniz çeşitli işlemler vardır dahil olmak üzere:

* Tablo izinleri değiştirme
* Merhaba işletimsel komut dosyalarını düzenleme
* Merhaba tablo şemasını yönetme
* Merhaba tablo silme
* Merhaba tablo içeriğini temizleme
* Merhaba tablonun belirli satırları silme

### <a name="easyapis"></a>API
Merhaba *API* Mobile Services sekmesinde tarafından değiştirildi *kolay API'leri* hello Azure portalı içinde.  tooaccess kolay API'leri:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Tıklatın **kolay API'leri** hello mobil menüsünde.

Geçirilen Apı'lerinizi zaten hello dikey penceresinde listelenir.  Bu dikey pencereden bir API de ekleyebilirsiniz.  belirli bir API toomanage hello API'ı tıklatın.
Merhaba yeni dikey penceresinden hello izinleri ayarlama ve hello betikler hello API için düzenleyin.

### <a name="on-demand-jobs"></a>Zamanlayıcı işleri
Tüm zamanlayıcı işlerinin Zamanlayıcı İş koleksiyonları bölüm hello kullanılabilir.  tooaccess zamanlayıcı işlerinin:

1. İçinde toohello oturum [Azure portal].
2. Seçin **Gözat >**, girin **zamanlama** hello içinde *filtre* kutusuna ve ardından **Zamanlayıcı koleksiyonları**.
3. Siteniz için Hello iş koleksiyonu seçin.  Bu adlı *sitename*-işler.
4. Tıklatın **ayarları**.
5. Tıklatın **zamanlayıcı işlerinin** Yönet altında.

Zamanlanan işler geçişten önce belirtilen hello sıklığı birlikte listelenmiştir.  İsteğe bağlı işleri devre dışı bırakılır.  bir isteğe bağlı iş toorun:

1. Toorun istediğiniz hello işi seçin.
2. Gerekirse, **etkinleştirmek** tooenable hello işi.
3. Tıklatın **ayarları**, ardından **zamanlama**.
4. Bir yinelenmesini seçin **kez**, ardından **Kaydet**

İsteğe bağlı işleriniz bulunan `App_Data/config/scripts/scheduler post-migration`.  Tüm isteğe bağlı işleri çok Dönüştür öneririz[WebJobs] veya [işlevler].  Yeni zamanlayıcı işlerinin olarak yazma [WebJobs] veya [işlevler].

### <a name="notification-hubs"></a>Bildirim hub'ları
Mobile Services anında iletme bildirimleri için Notification Hubs'ı kullanır.  Uygulama ayarları aşağıdaki hello kullanılan toolink hello bildirim hub'ı tooyour mobil hizmeti geçişten sonra şunlardır:

| Uygulama ayarı | Açıklama |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Merhaba bildirim hub'ı Namespace |
| **MS\_NotificationHubName** |Merhaba bildirim hub'ı adı |
| **MS\_NotificationHubConnectionString** |Merhaba bildirim hub'ı bağlantı dizesi |
| **MS\_NamespaceName** |MS_PushEntityNamespace için diğer ad |

Bildirim Hub'ınız hello yönetilen [Azure portal].  (Bu hello uygulama ayarlarını kullanarak bulabilirsiniz) hello bildirim hub'ı adını not edin:

1. İçinde toohello oturum [Azure portal].
2. Seçin **Gözat**> seçeneğini belirleyip **bildirim hub'ları**
3. Hello mobil hizmetle ilişkili hello bildirim hub'ı adını tıklatın.

> [!NOTE]
> Bildirim HUb'ınızı "Karma" türü ise, görünür değil.  Bildirim hub'ları bildirim hub'ları ve eski Service Bus özelliklerini kullanma "Karma" yazın.  [Karma alanlarınızın Dönüştür] devam etmeden önce.  Merhaba dönüştürme işlemi tamamlandıktan sonra bildirim hub'ınızı hello görünür [Azure portal].
>
>

Daha fazla bilgi için hello gözden [bildirim hub'ları] belgeleri.

> [!TIP]
> Bildirim hub'ları yönetimi özelliklerine hello [Azure portal] olan hala önizlemede.  Merhaba [Klasik Azure portalı] tüm bildirim hub'ı yönetmek için kullanılabilir durumda kalır.
>
>

### <a name="legacy-push"></a>Eski itme ayarları
Anında iletme, mobil hizmetinize hello giriş bildirim hub'ları üzerinde önce yapılandırdıysanız, kullanmakta olduğunuz *eski itme*.  Anında iletme kullanıyorsanız ve bir bildirim hub'ı yapılandırmanızda listelenen görüyor musunuz durumunda kullanmakta olduğunuz olasıdır *eski itme*.  Bu özellik ile diğer tüm özelliklerini geçirilir.  Ancak, yakında hello geçiş tamamlandıktan sonra tooNotification hub yükseltmenizi öneririz.

Hello Ara, tüm hello eski itme ayarlarla (Merhaba önemli özel durum hello APNS sertifikasının) uygulama ayarlarında kullanılabilir.  Merhaba APNS sertifikasını hello filesystem hello uygun dosyayı değiştirerek güncelleştirin.

### <a name="app-settings"></a>Diğer uygulama ayarları
ek uygulama ayarları aşağıdaki hello mobil hizmetinizden geçirilen ve altında kullanılabilir *ayarları* > *uygulama ayarları*:

| Uygulama ayarı | Açıklama |
|:--- |:--- |
| **MS\_MobileServiceName** |Uygulamanızı Hello adı |
| **MS\_MobileServiceDomainSuffix** |Merhaba etki alanı öneki. yani Azure mobile.net |
| **MS\_ApplicationKey** |Uygulama anahtarı |
| **MS\_MasterKey** |Uygulama ana anahtarı |

Merhaba uygulama anahtarı ve ana anahtar özgün mobil hizmetiniz aynı toohello uygulama anahtarları yok.  Özellikle, hello uygulama anahtarı kullanımları hello mobil API tarafından mobil istemcilerin toovalidate gönderilir.

### <a name="cliequivalents"></a>Komut satırı eşdeğerleri
Merhaba artık kullanabileceğiniz *azure mobil* toomanage Azure Mobile Services sitenizi komutu.  Bunun yerine, birçok işlevini hello ile değiştirilmiştir *azure site* komutu.  Sık kullanılan komutlar için tablo toofind eşdeğerleri aşağıdaki hello kullan:

| *Azure Mobile* komutu | Eşdeğer *Azure Site* komutu |
|:--- |:--- |
| Mobil konumları |site konumu listesi |
| Mobil listesi |site listesi |
| Mobil Göster *adı* |Site Göster *adı* |
| Mobil yeniden *adı* |Site yeniden *adı* |
| Mobil dağıtın *adı* |Site dağıtım dağıtın *commitId* *adı* |
| Mobil anahtar kümesi *adı* *türü* *değeri* |Site appsetting silme *anahtar* *adı* <br/> Site appsetting eklemek *anahtar*=*değeri* *adı* |
| Mobil config listesi *adı* |Site appsetting listesinin *adı* |
| Mobil config alma *adı* *anahtarı* |Site appsetting Göster *anahtar* *adı* |
| Mobil yapılandırma kümesi *adı* *anahtarı* |Site appsetting silme *anahtar* *adı* <br/> Site appsetting eklemek *anahtar*=*değeri* *adı* |
| Mobil etki alanı listesi *adı* |site etki alanı listesi *adı* |
| Mobil etki alanı ekleme *adı* *etki alanı* |Site, etki alanı ekleme *etki alanı* *adı* |
| Mobil etki alanı delete *adı* |site etki alanı delete *etki alanı* *adı* |
| Mobil ölçek Göster *adı* |Site Göster *adı* |
| Mobil ölçek değişiklik *adı* |Site ölçek modu *modu* *adı* <br /> Site ölçek örnekleri *örnekleri* *adı* |
| Mobil appsetting listesi *adı* |Site appsetting listesinin *adı* |
| Mobil appsetting eklemek *adı* *anahtar* *değeri* |Site appsetting eklemek *anahtar*=*değeri* *adı* |
| Mobil appsetting silme *adı* *anahtarı* |Site appsetting silme *anahtar* *adı* |
| Mobil appsetting Göster *adı* *anahtarı* |Site appsetting silme *anahtar* *adı* |

Kimlik doğrulama veya anında iletme bildirimi güncelleştirerek ayarları uygun uygulama ayarı hello güncelleştirin.
Dosyaları düzenleyebilir ve sitenizi ftp veya git üzerinden yayımlayın.

### <a name="diagnostics"></a>Tanılama ve günlüğe kaydetme
Tanılama günlük normalde bir Azure App Service'te devre dışıdır.  tooenable tanılama günlük:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Varsayılan olarak Hello ayarları dikey penceresini açar.
4. Seçin **tanılama günlüklerini** hello Özellikler menüsü altında.
5. Tıklatın **ON** günlükleri aşağıdaki hello için: **uygulama günlüğü (dosya sistemi)**, **ayrıntılı hata iletileri**, ve **başarısız istek izleme**
6. Tıklatın **dosya sistemi** için Web sunucusu günlüğü
7. Tıklatın **Kaydet**

tooview hello günlükleri:

1. İçinde toohello oturum [Azure portal].
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** geçirilen mobil hizmetiniz hello adını tıklatın.
3. Merhaba tıklatın **Araçları** düğmesi
4. Seçin **günlük akışı** hello GÖZLEMLE menüsü altında.

Bunlar oluşturulduğunda günlükleri hello penceresinde görüntülenir.  Dağıtım kimlik bilgilerinizi kullanarak daha sonraki analizler için hello günlüklerini de indirebilirsiniz. Daha fazla bilgi için bkz: Merhaba [günlüğü] belgeleri.

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>Geçirilen mobil uygulama kopya silme site kesintiye neden olur
Azure PowerShell sonra Sil hello kopya kullanarak geçirilen mobil hizmetinizi kopyalarsanız, hello üretim hizmetiniz için DNS girişi kaldırılır.  Sitenizi olduğu artık Internet hello erişilebilir.  

Çözüm: sitenizi tooclone isterseniz hello portalı üzerinden bunu.

### <a name="changing-webconfig-does-not-work"></a>Web.config değiştirme çalışmıyor
Bir ASP.NET sitesi varsa, toohello değişiklikleri `Web.config` dosya uygulanmaz.  Hello Azure uygulama hizmeti uygun bir derlemeler `Web.config` başlangıç toosupport hello Mobile Services çalışma zamanı sırasında dosya.  Bir XML dönüştürme dosyası kullanarak (örneğin, özel üstbilgiler) belirli ayarları geçersiz kılabilirsiniz.  Bir dosya oluşturun olarak adlandırılan `applicationHost.xdt` -bu dosyanın hello bitmelidir `D:\home\site` hello Azure hizmeti üzerinde dizin.  Karşıya yükleme `applicationHost.xdt` dosya aracılığıyla özel dağıtım komut dosyası veya Kudu kullanarak doğrudan.  Merhaba aşağıdaki örnek bir belgeyi gösterir:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Merhaba daha fazla bilgi için bkz: [XDT dönüştürme örnekleri] belgeler GitHub üzerinde.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Geçirilen Mobile Services tooTraffic Yöneticisi eklenemez.
Bir Traffic Manager profili oluşturduğunuzda, doğrudan geçirilen mobil hizmet toohello profili seçemezsiniz.  "Dış uç noktası." kullanın  Dış uç noktası yalnızca PowerShell aracılığıyla eklenebilir.  Daha fazla bilgi için bkz: [trafik Yöneticisi Öğreticisi](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Sonraki Adımlar
Uygulamanızı geçirilen tooApp hizmeti olduğundan, kullanabileceğiniz daha da fazla özellikleri vardır:

* Dağıtım [yuvaları hazırlama] toostage değişiklikleri tooyour sitesine izin ver ve gerçekleştirmenizi / B testi.
* [WebJobs] isteğe bağlı zamanlanan işleri için yenileme sağlayın.
* Yapabilecekleriniz [sürekli olarak dağıtma] site tooGitHub, TFS veya Mercurial bağlayarak sitenizi.
* Kullanabileceğiniz [Application Insights] toomonitor sitenizi.
* Web sitesi bir hizmet vermemesini ve mobil API'SİNDEN aynı kodu hello.

### <a name="upgrading-your-site"></a>Mobile Services site tooAzure Mobile Apps SDK'sı yükseltme
* Node.js tabanlı sunucu projeleri için yeni hello [Mobile Apps Node.js SDK'sı] birçok yeni özellik sağlar. Örneğin, artık yerel geliştirme ve hata ayıklama yapın, 0,10 yukarıda herhangi bir Node.js sürümünü kullanın ve Express.js Ara yazılımların ile özelleştirme.
* İçin. NET tabanlı sunucu projeleri hello yeni [Mobile Apps SDK NuGet paketlerini](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) NuGet bağımlılıklar hakkında daha fazla esneklik bulunur.  Bu paketleri hello yeni uygulama hizmeti kimlik doğrulamayı desteklemek ve ile tüm ASP.NET projesi oluşturun. Yükseltme hakkında daha fazla bilgi edinmek için [varolan .NET Mobil hizmeti tooApp hizmet yükseltme](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Uygulama hizmeti fiyatlandırması]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Otomatik ölçek]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Azure uygulama hizmeti dağıtım belgeleri]: ../app-service-web/web-sites-deploy.md
[Klasik Azure portalı]: https://manage.windowsazure.com
[Azure portal]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure Zamanlayıcı planları]: ../scheduler/scheduler-plans-billing.md
[sürekli olarak dağıtma]: ../app-service-web/app-service-continuous-deployment.md
[Karma alanlarınızın Dönüştür]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[özel etki alanı adlarını]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[Azure uygulama hizmeti genel kullanılabilirliğini]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[karma bağlantılar]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[günlüğü]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Mobile Apps Node.js SDK'sı]: https://github.com/azure/azure-mobile-apps-node
[Mobile Services vs. Uygulama hizmeti]: app-service-mobile-value-prop-migration-from-mobile-services.md
[bildirim hub'ları]: ../notification-hubs/notification-hubs-push-notification-overview.md
[performans izleme]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[yuvaları hazırlama]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT dönüştürme örnekleri]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[işlevler]: ../azure-functions/functions-overview.md
