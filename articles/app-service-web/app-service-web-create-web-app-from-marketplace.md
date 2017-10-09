---
title: "aaaCreate hello Azure Marketi'nde bir web uygulamasından | Microsoft Docs"
description: "Nasıl toocreate kullanarak Azure Marketi hello yeni bir WordPress web uygulamasından hello Azure Portal hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Azure Market hello bir web uygulaması oluşturma
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketi çok çeşitli popüler web uygulamalarını açık kaynaklı yazılım topluluklar, örneğin WordPress ve Umbraco CMS tarafından geliştirilen sağlar. Bu öğreticide, bilgi nasıl toocreate WordPress uygulaması Azure Marketi'nden.
bir Azure Web uygulaması ve MySQL veritabanı oluşturur. 

![Örnek WordPress web app Panosu](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Başlamadan önce 

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

## <a name="deploy-from-azure-marketplace"></a>Azure Marketi'nden dağıtma
Azure Marketi'nden toodeploy WordPress Hello adımları izleyin.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum
İçinde toohello oturum [Azure portal](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>WordPress şablonu dağıtma
Hello Azure Marketi kaynakları, Kurulum hello ayarlama için şablonlar sağlar [WordPress](https://portal.azure.com/#create/WordPress.WordPress) şablonu tooget başlatıldı.
   
Merhaba aşağıdakileri girin bilgi toodeploy hello WordPress uygulama ve kaynaklarına.

  ![WordPress akışı oluştur](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Alan         | Önerilen Değer           | Açıklama  |
| ------------- |-------------------------|-------------|
| Uygulama adı      | mywordpressapp          | Bir benzersiz uygulama adı, **Web uygulaması adı**. Bu ad hello varsayılan DNS adını, uygulamanız için bir parçası olarak kullanılır `<app_name>.azurewebsites.net`, onu toobe benzersiz tüm uygulamalarında Azure nedenle gerekir. Daha sonra tooyour kullanıcılar kullanıma önce bir özel etki alanı adı tooyour uygulaması eşleyebilirsiniz |
| Abonelik  | Kullandıkça Öde             | Bir **Abonelik** seçin. Birden çok aboneliğiniz varsa, hello uygun abonelik seçin. |
| Kaynak Grubu| mywordpressappgroup                 |    Girin bir **kaynak grubu**. Bir kaynak grubu, web uygulamaları, dağıtılan ve yönetilen veritabanları gibi Azure kaynakları içine mantıksal bir kapsayıcısıdır. Bir kaynak grubu oluşturmak veya mevcut bir kullanın |
| App Service Planı | myappplan          | Uygulama hizmeti planları, uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder. Select hello **konumu** ve hello **fiyatlandırma katmanı**. Fiyatlandırma hakkında daha fazla bilgi için bkz: [fiyatlandırma katmanı uygulama hizmeti](https://azure.microsoft.com/pricing/details/app-service/) |
| Database      | mywordpressapp          | MySQL için Hello uygun veritabanı sağlayıcısı seçin. Web uygulamaları destekler **ClearDB**, **Azure veritabanı için MySQL** ve **uygulama MySQL**. Daha fazla ayrıntı için bkz: [veritabanı yapılandırması](#database-config) bölümüne bakın. |
| Application Insights | AÇIK veya kapalı          | Bu isteğe bağlıdır. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) tıklatarak web uygulamanız için izleme hizmetleri sağlayan **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Veritabanı yapılandırması
MySQL veritabanı sağlayıcısı, tercihine bağlı hello adımları izleyin.  Bu Web uygulaması ve MySQL veritabanının hello olması önerilir konumda.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) Azure üzerinde tam olarak tümleşik bir MySQL hizmeti için bir üçüncü taraf çözümüdür. Sipariş toouse ClearDB veritabanlarında tooassociate bir kredi kartı tooyour gerekir [Azure hesabı](http://account.windowsazure.com/subscriptions). ClearDB veritabanı sağlayıcısı seçtiyseniz, var olan veritabanlarını toochoose bir listesini görüntülemek veya tıklatın **Yeni Oluştur** düğmesini toocreate bir veritabanı.

![ClearDB oluşturma](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Azure veritabanı için MySQL (Önizleme)
[Azure veritabanı için MySQL](https://azure.microsoft.com/en-us/services/mysql) en güvendiğiniz hello bulutta uçarak uygulama geliştirme ve dakika ve hello ölçekte bir MySQL veritabanını toostand sağlayan dağıtım için bir yönetilen veritabanı hizmeti sağlar. Yüksek kullanılabilirlik, güvenlik ve kurtarma, Hayır yerleşik – gibi istediğiniz tüm hello özelliklerini al dahil fiyatlandırma modelleriyle ekstra maliyet. Tıklatın **fiyatlandırma katmanı** toochoose farklı bir [fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/mysql). toouse varolan bir veritabanı veya MySQL server varolan hangi hello sunucusunun bulunduğu varolan bir kaynak grubunu kullanın. 

![Merhaba web uygulaması için Hello veritabanı ayarlarını yapılandırma](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure veritabanı MySQL (Önizleme) ve Linux (Önizleme) üzerinde Web uygulaması için kullanılabilir değil tüm bölgelerde. toolearn hakkında daha fazla [Azure veritabanı için MySQL (Önizleme)](https://docs.microsoft.com/en-us/azure/mysql) ve [Linux üzerinde Web uygulaması](./app-service-linux-intro.md) sınırlamaları. 

#### <a name="mysql-in-app"></a>Uygulama MySQL
[Uygulama MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) MySql hello platformu üzerinde yerel olarak çalışan sağlayan bir uygulama hizmeti özelliğidir. Merhaba çekirdek işlevselliğini Hello hello özelliği sürümünde desteklenir:

- Aynı hello siteyi barındıran web sunucunuz yan yana örnek hello çalışan MySQL sunucu. Bu, uygulamanızın performansını artırır.
- Depolama, MySQL ve web uygulama dosyalarınızı arasında paylaşılır. Not hello sitesini kullanarak hello eylemleri, temel bizim kota sınırına ulaşıp ücretsiz ve paylaşılan planları ile gerçekleştirin. Kullanıma [kota sınırlamalarını](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) ücretsiz ve paylaşılan planları.
- Yavaş sorgu günlüğü ve MySQL için genel günlük kaydını etkinleştirebilirsiniz. Bu hello site performansını etkileyebilir ve her zaman açık unutmayın. Merhaba günlüğe kaydetme özelliği, uygulama sorunları araştırma yardımcı olur. 

Daha fazla bilgi için bu denetleyin [makale](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![MySQL uygulama yönetimi](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Merhaba sayfanın üst kısmındaki hello portal WordPress uygulaması dağıtılan hello sırasında hello zil simgesine tıklayarak hello ilerleme durumunu izleyebilirsiniz.    
![İlerleme göstergesi](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Yeni Azure web uygulamanızı yönetme

Azure portal tootake göz atın, yeni oluşturduğunuz hello web uygulaması toohello gidin.

toodo Bu, çok oturum[https://portal.azure.com](https://portal.azure.com).

Merhaba sol menüden **uygulama hizmetleri**, Azure web uygulamanızın hello adını tıklatın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Web uygulamanızın _dikey penceresini_ açtınız (yatay yönde açılan portal sayfası).

Varsayılan olarak, web uygulamanızın dikey penceresinde hello gösterir **genel bakış** sayfası. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Merhaba sol tarafındaki hello dikey penceresinde Hello sekmeleri açabilirsiniz hello farklı yapılandırma sayfaları gösterir.

![Azure portalında App Service dikey penceresi](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Bu sekme hello dikey penceresinde hello tooyour web uygulama eklemek için birçok harika özellikler gösterir. liste aşağıdaki hello birkaçı hello olasılıklar sunar:

* Özel bir DNS adı eşleme
* Özel bir SSL sertifikası bağlama
* Sürekli dağıtımı yapılandırma
* Ölçeği artırma ve genişletme
* Kullanıcı kimlik doğrulaması ekleme

Merhaba 5 dakikalık WordPress Yükleme Sihirbazı'nı toohave WordPress uygulaması çalışır tamamlayın. Kullanıma [Wordpress belgelerine](https://codex.WordPress.org/) toodevelop web uygulamanızı.

![Wordpress Yükleme Sihirbazı](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Uygulamanızı yapılandırma 
WordPress uygulamanızı üretim kullanımı için hazır hale gelmeden önce yönetilmesindeki ilgili birden çok adım vardır. Bu adımları tooconfigure izleyin ve WordPress uygulamanızı yönetebilirsiniz:

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Büyük dosyaları depolamak ya da karşıya yükle** |[WordPress eklentisini Blob storage kullanma](https://wordpress.org/plugins/windows-azure-storage/)|
| **E-posta Gönder** |Satın alma [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) hello kullanın ve hizmet e-posta [SendGrid kullanmak için WordPress eklentisini](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure,|
| **Özel etki alanı adları** |[Azure App Service'te özel etki alanı adını yapılandırma](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir](app-service-web-tutorial-custom-ssl.md) |
| **Üretim öncesi doğrulama** |[Azure App Service'deki web uygulamaları için hazırlama ve geliştirme ortamlarını ayarlama](web-sites-staged-publishing.md)|
| **İzleme ve sorun giderme** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](web-sites-enable-diagnostic-log.md) ve [Azure App Service'te Web uygulamalarını izleme](app-service-web-tutorial-monitoring.md) |
| **Sitenizi dağıtma** |[Azure App Service'te bir web uygulaması dağıtma](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Uygulamanızı güvenli 
WordPress uygulamanızı üretim kullanımı için hazır hale gelmeden önce yönetilmesindeki ilgili birden çok adım vardır. Bu adımları tooconfigure izleyin ve WordPress uygulamanızı yönetebilirsiniz:

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Güçlü kullanıcı adı ve parola**|  Sık parolayı değiştirin. Değil yaygın olarak kullanılan kullanım kullanıcı adları beğendiniz mi *yönetici* veya *wordpress* vs. Tüm WordPress kullanıcıları toouse benzersiz kullanıcı adı ve güçlü parolalar zorlar. |
| **Güncel kalın** | WordPress çekirdek, temalar, eklenti toodate yukarı tutun. Merhaba son PHP çalışma zamanı Azure App Service'te kullanılabilir kullanın |
| **WordPress güvenlik anahtarlarını güncelleştirin** | Güncelleştirme [WordPress güvenlik anahtarı](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tanımlama bilgilerinde depolanan tooimprove şifreleme|

## <a name="improve-performance"></a>Performansı
Merhaba bulutta performans temelde önbelleğe alma ve ölçeklendirme elde edilir. Ancak, hello bellek, bant genişliği ve Web uygulamalarını barındırma diğer öznitelikleri dikkate alınmalıdır.

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **App Service örneği özelliklerini anlama** |[Uygulama hizmet katmanları yeteneklerini de dahil olmak üzere fiyatlandırma ayrıntıları](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Önbelleği kaynakları** |Kullanım [Azure Redis önbelleği](https://azure.microsoft.com/en-us/services/cache/), veya diğer önbelleğe alma tekliflerini hello hello biri [Azure depolama](https://azuremarketplace.microsoft.com) |
| **Uygulamanızı ölçeklendirme** |Tooscale gerek [hello web uygulamasını Azure App Service'te](web-sites-scale.md) ve/veya MySQL veritabanı. Uygulama MySQL genişleme desteği yok, bu nedenle ClearDB veya Azure veritabanı için MySQL (Önizleme) seçin. [MySQL (Önizleme) Azure veritabanı ölçeklendirme](https://azure.microsoft.com/en-us/pricing/details/mysql/) veya kullanıyorsanız [ClearDB yüksek kullanılabilirlik yönlendirme](http://w2.cleardb.net/faqs/) tooscale veritabanınızı ayarlama |

## <a name="availability-and-disaster-recovery"></a>Kullanılabilirlik ve olağanüstü durum kurtarma
Yüksek kullanılabilirlik, olağanüstü durum kurtarma toomaintain iş sürekliliği hello yönünü içerir. Hataları ve olağanüstü durumları hello bulutta planlama toorecognize hello hataları hızla gerektirir. Bu çözümler, yüksek kullanılabilirlik için bir strateji uygulamaya yardımcı olur.

| toodo bu... | Bunu kullanın... |
| --- | --- |
| **Yük Dengeleme siteleri** veya **coğrafi-siteler dağıtın** |[Azure Traffic Manager ile trafiği yönlendirme](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Yedekleme ve geri yükleme** |[Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md) ve [Azure App Service'in web uygulamasında geri yükleme](web-sites-restore.md) |

## <a name="next-steps"></a>Sonraki adımlar
Çeşitli özellikleri hakkında bilgi edinin [uygulama hizmeti toodevelop ve ölçek](/app-service-web/).
