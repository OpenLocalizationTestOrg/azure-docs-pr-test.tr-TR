---
title: "Azure App Service'te bir WordPress web uygulaması aaaCreate | Microsoft Docs"
description: "Nasıl toocreate yeni bir Azure web uygulaması hello Azure Portal'ı kullanarak WordPress blogu için öğrenin."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Azure App Service’te bir WordPress web uygulaması oluşturma
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Bu öğretici nasıl toodeploy bir WordPress blog sitesi hello Azure Marketi gösterir.

Merhaba Bu öğreticiyi tamamladığınızda ve hello bulutta çalışan kendi WordPress blog sitenize sahip olacaksınız.

![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Şunları öğreneceksiniz:

* Nasıl toofind hello Azure Marketi'nde bir uygulama şablonunda.
* Nasıl toocreate bir web uygulamasını Azure App Service, hello şablonunu temel alır.
* Nasıl tooconfigure Azure App Service ayarlarını hello yeni uygulama ve veritabanı web.

Hello Azure Marketi çok çeşitli popüler web uygulamalarını Microsoft, üçüncü taraf şirketler ve açık kaynak yazılım girişimleri tarafından geliştirilen kullanılabilir hale getirir. Merhaba web uygulamaları dahili çok çeşitli popüler uygulamayı üzerinde gibi [PHP](/develop/nodejs/) bu WordPress örneğinde [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), ve [Python](/develop/python/), az bir tooname. toocreate hello Azure Marketi hello Merhaba hello tarayıcının gereksinim duyduğunuz yazılım, yalnızca web uygulamasından [Azure Portal](https://portal.azure.com/). 

Bu öğreticide dağıttığınız WordPress sitesi hello hello veritabanı için MySQL kullanır. Merhaba veritabanı için SQL veritabanı tooinstead kullanmak istiyorsanız, bkz: [proje Nami](http://projectnami.org/). **Proje Nami** hello Market de kullanılabilir.

> [!NOTE]
> toocomplete Bu öğreticide, bir Microsoft Azure hesabınızın olması gerekir. Bir hesabınız yoksa, [Visual Studio abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) veya [ücretsiz deneme için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/). Burada, App Service'te hemen bir kısa süreli başlangıç web uygulaması oluşturabilirsiniz; kredi kartı gerekmez ve hiçbir taahhüt yoktur.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>WordPress’i seçme ve Azure App Service için yapılandırma
1. İçinde toohello oturum [Azure Portal](https://portal.azure.com/).
2. **Yeni**’ye tıklayın.
   
    ![Yeni Oluştur][5]
3. **WordPress**’i arayın ve ardından **WordPress**’e tıklayın. Toouse MySQL yerine SQL Database istiyorsanız, arama **proje Nami**.
   
    ![Listede WordPress][7]
4. Merhaba hello WordPress uygulaması açıklamasını okuduktan sonra tıklatın **oluşturma**.
   
    ![Oluştur](./media/web-sites-php-web-site-gallery/create.png)
5. Hello hello web uygulaması için bir ad girin **Web uygulaması** kutusu.
   
    Hello web uygulamasının Hello URL'si {ad} olacağı için bu ad hello azurewebsites.net etki alanında benzersiz olmalıdır. azurewebsites.net. Girdiğiniz hello ad benzersiz değilse, hello metin kutusunda kırmızı bir ünlem işareti görüntülenir.
6. Merhaba seçin, birden fazla aboneliğiniz varsa bir istediğiniz toouse. 
7. Bir **Kaynak Grubu** seçin veya yeni bir tane oluşturun.
   
    Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).
8. Bir **App Service planı/Konum** seçin veya yeni bir tane oluşturun.
   
    App Service planları hakkında daha fazla bilgi için bkz. [Azure App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. Tıklatın **veritabanı**ve ardından hello **yeni MySQL veritabanı** dikey penceresinde, MySQL veritabanınızı yapılandırmak için gerekli hello değerleri belirtin.
   
    a. Yeni bir ad girin veya hello varsayılan adı bırakın.
   
    b. Merhaba bırakın **veritabanı türü** çok ayarlamak**paylaşılan**.
   
    c. Hello gibi bir hello aynı konuma hello web uygulaması için seçtiğiniz seçin.
   
    d. Bir fiyatlandırma katmanı seçin. Minimum izin verilen bağlantı ve disk alanıyla ücretsiz olan Mercury bu öğretici için uygundur.
10. Merhaba, **yeni MySQL veritabanı** dikey penceresinde tıklatın **Tamam**. 
11. Merhaba, **WordPress** dikey penceresinde hello yasal koşulları kabul edin ve ardından **oluşturma**. 
    
     ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/configure.png)
    
     Azure uygulama hizmeti hello web uygulamasını, genellikle bir dakikadan oluşturur. Merhaba sayfanın üst kısmındaki hello portal hello zil simgesine tıklayarak hello ilerleme durumunu izleyebilirsiniz.
    
     ![İlerleme göstergesi](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>WordPress web uygulamanızı başlatma ve yönetme
1. Merhaba web uygulaması oluşturma tamamlandığında, hello uygulama oluşturulan ve hello web app ve hello veritabanı görebilirsiniz hello Azure Portal toohello kaynak grubuna gidin.
   
    Merhaba hello ampul simgeli ek kaynak olan [Application Insights](/services/application-insights/), web uygulamanız için izleme hizmetleri sağlar.
2. Merhaba, **kaynak grubu** dikey penceresinde hello web uygulaması satırına tıklayın.
   
    ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. Merhaba Web uygulaması dikey penceresinde tıklatın **Gözat**.
   
    ![site URL][browse]
4. Merhaba WordPress içinde **Hoş Geldiniz** sayfasında, WordPress için gereken hello yapılandırma bilgilerini girin ve ardından **Wordpress'i Yükle**.
   
    ![WordPress’i yapılandırma](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Merhaba üzerinde oluşturulan hello kimlik bilgilerini kullanarak oturum **Hoş Geldiniz** sayfası.  
6. Sitenizin Pano sayfası açılır.    
   
    ![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Sonraki adımlar
Gördüğünüz nasıl toocreate ve hello Galeriden bir PHP web uygulamasını dağıtın. Azure'da PHP kullanma hakkında daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

Hakkında daha fazla bilgi için App Service Web Apps ile toowork yan (geniş tarayıcı pencereleri için için) başlangıç sayfasının sol hello hello bağlantılar bakın veya hello sayfanın üst kısmındaki hello (için dar tarayıcı pencereleri için). 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet gelen bir kılavuzu toohello değişiklik için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
