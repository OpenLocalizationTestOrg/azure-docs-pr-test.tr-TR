---
title: "Azure Marketi’nde bir web uygulaması oluşturma | Microsoft Belgeleri"
description: "Azure Portal'ı kullanarak Azure Marketi'nde yeni bir WordPress web uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: 16951ac0fcc350b7176747a7ad4e0bc8e186ab17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-from-the-azure-marketplace"></a>Azure Marketi’nde bir web uygulaması oluşturma
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Azure Market çok çeşitli popüler web uygulamalarını açık kaynaklı yazılım topluluklar, örneğin WordPress ve Umbraco CMS tarafından geliştirilen sağlar. Bu öğreticide, WordPress uygulaması Azure Marketi'nden oluşturmayı öğrenin.
bir Azure Web uygulaması ve MySQL veritabanı oluşturur. 

![Örnek WordPress web app Panosu](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Başlamadan önce 

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

## <a name="deploy-from-azure-marketplace"></a>Azure Marketi'nden dağıtma
Azure Marketi'nden WordPress dağıtmak için aşağıdaki adımları izleyin.

### <a name="sign-in-to-azure"></a>Azure'da oturum açma
[Azure Portal](https://portal.azure.com)’da oturum açın.

### <a name="deploy-wordpress-template"></a>WordPress şablonu dağıtma
Şablonları Azure Market sunar kaynaklarını ayarlama için Kurulum [WordPress](https://portal.azure.com/#create/WordPress.WordPress) başlamak için şablon.
   
WordPress uygulama ve kaynaklarına dağıtmak için aşağıdaki bilgileri girin.

  ![WordPress akışı oluştur](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Alan         | Önerilen Değer           | Açıklama  |
| ------------- |-------------------------|-------------|
| Uygulama adı      | mywordpressapp          | Bir benzersiz uygulama adı, **Web uygulaması adı**. Bu ad, uygulamanız için varsayılan DNS adının bir parçası olarak kullanılır `<app_name>.azurewebsites.net`, azure'daki tüm uygulamalar arasında benzersiz olması gerekir. Kullanıcılarınız için kullanıma önce uygulamanız için bir özel etki alanı adı daha sonra eşleyebilirsiniz |
| Abonelik  | Kullandıkça Öde             | Bir **Abonelik** seçin. Birden çok aboneliğiniz varsa, uygun abonelik seçin. |
| Kaynak Grubu| mywordpressappgroup                 |    Girin bir **kaynak grubu**. Bir kaynak grubu, web uygulamaları, dağıtılan ve yönetilen veritabanları gibi Azure kaynakları içine mantıksal bir kapsayıcısıdır. Bir kaynak grubu oluşturmak veya mevcut bir kullanın |
| App Service Planı | myappplan          | Uygulama hizmeti planları, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları koleksiyonunu temsil eder. Seçin **konumu** ve **fiyatlandırma katmanı**. Fiyatlandırma hakkında daha fazla bilgi için bkz: [fiyatlandırma katmanı uygulama hizmeti](https://azure.microsoft.com/pricing/details/app-service/) |
| Database      | mywordpressapp          | MySQL için uygun veritabanı sağlayıcısı seçin. Web uygulamaları destekler **ClearDB**, **Azure veritabanı için MySQL** ve **uygulama MySQL**. Daha fazla ayrıntı için bkz: [veritabanı yapılandırması](#database-config) bölümüne bakın. |
| Application Insights | AÇIK veya kapalı          | Bu isteğe bağlıdır. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) tıklatarak web uygulamanız için izleme hizmetleri sağlayan **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Veritabanı yapılandırması
MySQL veritabanı sağlayıcısı, tercihine bağlı aşağıdaki adımları izleyin.  Bu Web uygulaması ve MySQL veritabanını aynı konumda olması önerilir.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) Azure üzerinde tam olarak tümleşik bir MySQL hizmeti için bir üçüncü taraf çözümüdür. ClearDB veritabanı kullanmak için bir kredi kartı ilişkilendirmek gerekir, [Azure hesabı](http://account.windowsazure.com/subscriptions). ClearDB veritabanı sağlayıcısı seçtiyseniz, aşağıdakilerden birini seçin veya var olan veritabanlarının listesini görüntüleyebileceğiniz **Yeni Oluştur** bir veritabanı oluşturmak için düğmesi.

![ClearDB oluşturma](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Azure veritabanı için MySQL (Önizleme)
[Azure veritabanı için MySQL](https://azure.microsoft.com/en-us/services/mysql) uygulama geliştirme ve bir MySQL veritabanını dakika bekleyin ve kolay bir şekilde buluta ölçeği olanak sağlayan dağıtım çoğu güven için bir yönetilen veritabanı hizmeti sağlar. Yüksek kullanılabilirlik, güvenlik ve kurtarma, Hayır yerleşik – gibi istediğiniz tüm işlevlerini edinecek dahil fiyatlandırma modelleriyle ekstra maliyet. Tıklatın **fiyatlandırma katmanı** farklı bir seçmek için [fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/mysql). Varolan bir veritabanına veya varolan bir MySQL sunucusu kullanmak için sunucunun bulunduğu varolan bir kaynak grubu kullanın. 

![Web uygulaması için veritabanı ayarlarını yapılandırma](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure veritabanı MySQL (Önizleme) ve Linux (Önizleme) üzerinde Web uygulaması için kullanılabilir değil tüm bölgelerde. Daha fazla bilgi edinmek için [Azure veritabanı için MySQL (Önizleme)](https://docs.microsoft.com/en-us/azure/mysql) ve [Linux üzerinde Web uygulaması](./app-service-linux-intro.md) sınırlamaları. 

#### <a name="mysql-in-app"></a>Uygulama MySQL
[Uygulama MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) MySql platformu üzerinde yerel olarak çalışan sağlayan bir uygulama hizmeti özelliğidir. Özellik sürümünde desteklenen çekirdek işlevselliğini:

- Siteyi barındıran web sunucunuz ile aynı örneğinde yan yana çalıştıran MySQL sunucu. Bu, uygulamanızın performansını artırır.
- Depolama, MySQL ve web uygulama dosyalarınızı arasında paylaşılır. Not site kullanarak eylemleri, temel bizim kota sınırına ulaşıp ücretsiz ve paylaşılan planları ile gerçekleştirin. Kullanıma [kota sınırlamalarını](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) ücretsiz ve paylaşılan planları.
- Yavaş sorgu günlüğü ve MySQL için genel günlük kaydını etkinleştirebilirsiniz. Bu site performansını etkileyebilir ve her zaman açık unutmayın. Günlüğe kaydetme özelliği, uygulama sorunları araştırma yardımcı olur. 

Daha fazla bilgi için bu denetleyin [makale](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![MySQL uygulama yönetimi](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

WordPress uygulaması dağıtılırken portal sayfasının üst zil simgesine tıklayarak ilerleme durumunu izleyebilirsiniz.    
![İlerleme göstergesi](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Yeni Azure web uygulamanızı yönetme

Azure portalına giderek yeni oluşturduğunuz web uygulamasına göz atın.

Bunu yapmak için [https://portal.azure.com](https://portal.azure.com) sayfasında oturum açın.

Sol menüden **Uygulama Hizmetleri**’ne ve ardından Azure web uygulamanızın adına tıklayın.

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Web uygulamanızın _dikey penceresini_ açtınız (yatay yönde açılan portal sayfası).

Varsayılan olarak, web uygulamanızın dikey penceresinde **Genel Bakış** sayfası gösterilir. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Dikey pencerenin sol tarafındaki sekmeler, açabileceğiniz farklı yapılandırma sayfalarını gösterir.

![Azure portalında App Service dikey penceresi](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Dikey penceredeki bu sekmelerde web uygulamanıza ekleyebileceğiniz çok sayıda harika özellik gösterilir. Aşağıdaki listede yalnızca birkaç olasılık sunulmaktadır:

* Özel bir DNS adı eşleme
* Özel bir SSL sertifikası bağlama
* Sürekli dağıtımı yapılandırma
* Ölçeği artırma ve genişletme
* Kullanıcı kimlik doğrulaması ekleme

WordPress uygulaması çalışır olması için 5 dakikalık WordPress Yükleme Sihirbazı'nı tamamlayın. Kullanıma [Wordpress belgelerine](https://codex.WordPress.org/) web uygulamanızı geliştirilir.

![Wordpress Yükleme Sihirbazı](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Uygulamanızı yapılandırma 
WordPress uygulamanızı üretim kullanımı için hazır hale gelmeden önce yönetilmesindeki ilgili birden çok adım vardır. Yapılandırmak ve WordPress uygulamanızı yönetmek için aşağıdaki adımları izleyin:

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Büyük dosyaları depolamak ya da karşıya yükle** |[WordPress eklentisini Blob storage kullanma](https://wordpress.org/plugins/windows-azure-storage/)|
| **E-posta Gönder** |Satın alma [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) kullanın ve hizmet e-posta [SendGrid kullanmak için WordPress eklentisini](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) yapılandırmak için|
| **Özel etki alanı adları** |[Azure App Service'te özel etki alanı adını yapılandırma](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir](app-service-web-tutorial-custom-ssl.md) |
| **Üretim öncesi doğrulama** |[Azure App Service'deki web uygulamaları için hazırlama ve geliştirme ortamlarını ayarlama](web-sites-staged-publishing.md)|
| **İzleme ve sorun giderme** |[Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](web-sites-enable-diagnostic-log.md) ve [Azure App Service'te Web uygulamalarını izleme](app-service-web-tutorial-monitoring.md) |
| **Sitenizi dağıtma** |[Azure App Service'te bir web uygulaması dağıtma](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Uygulamanızı güvenli 
WordPress uygulamanızı üretim kullanımı için hazır hale gelmeden önce yönetilmesindeki ilgili birden çok adım vardır. Yapılandırmak ve WordPress uygulamanızı yönetmek için aşağıdaki adımları izleyin:

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Güçlü kullanıcı adı ve parola**|  Sık parolayı değiştirin. Değil yaygın olarak kullanılan kullanım kullanıcı adları beğendiniz mi *yönetici* veya *wordpress* vs. Tüm WordPress kullanıcıları benzersiz kullanıcı adı ve güçlü parolalar kullanmaya zorlar. |
| **Güncel kalın** | WordPress çekirdek, temalar, eklenti güncel tutun. Azure App Service'te kullanılabilen en son PHP çalışma kullanın |
| **WordPress güvenlik anahtarlarını güncelleştirin** | Güncelleştirme [WordPress güvenlik anahtarı](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tanımlama bilgilerinde depolanan şifreleme artırmak için|

## <a name="improve-performance"></a>Performansı
Bulutta performans temelde önbelleğe alma ve ölçeklendirme elde edilir. Ancak, bellek, bant genişliği ve Web uygulamalarını barındırma diğer öznitelikleri dikkate alınmalıdır.

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **App Service örneği özelliklerini anlama** |[Uygulama hizmet katmanları yeteneklerini de dahil olmak üzere fiyatlandırma ayrıntıları](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Önbelleği kaynakları** |Kullanım [Azure Redis önbelleği](https://azure.microsoft.com/en-us/services/cache/), veya diğer önbelleğe alma tekliflerini [Azure depolama](https://azuremarketplace.microsoft.com) |
| **Uygulamanızı ölçeklendirme** |Ölçeklendirme gerek [Azure App Service'in web uygulamasında](web-sites-scale.md) ve/veya MySQL veritabanı. Uygulama MySQL genişleme desteği yok, bu nedenle ClearDB veya Azure veritabanı için MySQL (Önizleme) seçin. [MySQL (Önizleme) Azure veritabanı ölçeklendirme](https://azure.microsoft.com/en-us/pricing/details/mysql/) veya kullanıyorsanız [ClearDB yüksek kullanılabilirlik yönlendirme](http://w2.cleardb.net/faqs/) veritabanınızı ölçeklendirme |

## <a name="availability-and-disaster-recovery"></a>Kullanılabilirlik ve olağanüstü durum kurtarma
Yüksek kullanılabilirlik özelliği iş sürekliliği sağlamak için olağanüstü durum kurtarma, içerir. Hataları ve olağanüstü durumları bulutta planlama hataları kolayca tanımak gerektirir. Bu çözümler, yüksek kullanılabilirlik için bir strateji uygulamaya yardımcı olur.

| Bunu yapmak için... | Bunu kullanın... |
| --- | --- |
| **Yük Dengeleme siteleri** veya **coğrafi-siteler dağıtın** |[Azure Traffic Manager ile trafiği yönlendirme](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Yedekleme ve geri yükleme** |[Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md) ve [Azure App Service'in web uygulamasında geri yükleme](web-sites-restore.md) |

## <a name="next-steps"></a>Sonraki adımlar
Çeşitli özellikleri hakkında bilgi edinin [geliştirmek ve ölçeklendirmek için uygulama hizmeti](/app-service-web/).