---
title: "aaaDeploy hello beş dakikada Azure portalında WordPress uygulamasında | Microsoft Docs"
description: "Ne kadar kolay toorun web uygulamaları App Service'te bir WordPress uygulaması dağıtarak olduğunu öğrenin. Sonuçları anında görün."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Hello Azure portal WordPress uygulamasında beş dakika içinde dağıtma

Bu öğretici şunların nasıl yapıldığını gösterir toodeploy ilk [WordPress](https://wordpress.org/) çok web uygulaması[Azure App Service](../app-service/app-service-value-prop-what-is.md) dakika.

![WordPress sitesi](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Ön koşullar
Bir Microsoft Azure hesabınızın olması gerekir. Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)

> [!NOTE]
> Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/). Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Merhaba WordPress uygulaması dağıtma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress) adresini açın.

    Bu bir kısayol tooimmediately hello Azure portalında yeni bir WordPress uygulaması yapılandırma bağlantıdır.

3. **Uygulama adı** bölümünde bir web uygulaması adı girin. Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `azurewebsites.net` etki alanı.
   
5. İçinde **kaynak grubu**, tıklatın **Yeni Oluştur** yeni bir toocreate [kaynak grubu](../azure-resource-manager/resource-group-overview.md), bir ad verin.

6. **Veritabanı Sağlayıcısı**'nda **CleaDB**'yi seçin.

7. **App Service planı/Konum** > **Yeni Oluştur**'a tıklayın. Merhaba yapılandırma [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) gösterildiği gibi:

    - İçinde **uygulama hizmeti planı**, türü hello istenen adı.
    - İçinde **konumu**, bir konum toohost planınızı seçin.
    - **Fiyatlandırma katmanı**'na tıklayıp **F1 Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.
    - **Tamam** düğmesine tıklayın.

8. **Veritabanı** > **Yeni Oluştur**'a tıklayın. SQL veritabanı Hello gösterildiği gibi yapılandırın:

    - **Veritabanı Adı** alanına bir veritabanı adı yazın. 
    - İçinde **konumu**, seçin hello hello uygulama hizmeti planı aynı konumda.
    - **Fiyatlandırma katmanı**'na tıklayıp **Mercury** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.
    - **Yasal Koşullar**'a ve **Satın Al**'a tıklayın.
    - **Tamam** düğmesine tıklayın.

9. **Oluştur**’a tıklayın.

    Azure şimdi yapılandırmanızı temel alarak WordPress uygulamanızı oluşturur. **Dağıtım başlatıldı...** bildirimini görmeniz gerekir.

    ![Dağıtım başladı - Azure App Service’teki ilk WordPress uygulaması](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>WordPress web uygulamanızı başlatma ve yönetme

Azure uygulama dağıtımını tamamladığında başka bir bildirim daha göreceksiniz.

![Dağıtım başarılı - Azure App Service’teki ilk WordPress uygulaması](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Merhaba bildirime tıklayın. Bu eksik, her zaman hello bildirim zil tıklayarak erişebildiğinizi (![bildirim aşağıdaki - Azure App Service'te ilk WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Şimdi web uygulamasının yönetim [dikey penceresini](../azure-resource-manager/resource-group-portal.md#manage-resources) (*dikey pencere*: dikey olarak açılan portal sayfası) görmeniz gerekir.

3. Merhaba genel bakış sayfası Hello üst tıklatın **Gözat**.
   
    ![Göz at - Azure App Service’teki ilk WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    Merhaba WordPress gördüğünüz artık **Hoş Geldiniz** sayfası. Merhaba WordPress yüklemesini yapılandırmak ve onunla yürütmeye başlayın!

    ![WordPress yapılandırması - Azure App Service’teki ilk WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Sonraki adımlar
* [Oluşturma, yapılandırma ve Laravel web uygulama tooAzure dağıtma](app-service-web-php-get-started.md) -ihtiyacınız toorun Azure, herhangi bir PHP web uygulamasına gibi hello temel becerileri öğrenin:

    * Azure’da PowerShell/Bash uygulamaları oluşturma ve yapılandırma.
    * PHP sürümünü ayarlama.
    * Merhaba kök uygulama dizininde değil bir başlangıç dosyasını kullanın.
    * Composer otomasyonunu etkinleştirme.
    * Ortama özel değişkenlere erişme.
    * Sık karşılaşılan hataları giderme.

* [Kod tooAzure uygulama hizmeti dağıtmak](web-sites-deploy.md)-toodeploy FTP ya da kaynak havuzları nasıl kontrol öğrenin.
* [İşlevselliği tooyour ilk web uygulamanız eklemek](app-service-web-get-started-2.md) -Azure uygulaması toohello sonraki düzeye taşıyın. Kullanıcılarınızın kimliklerini doğrulayın. Talebe göre ölçeklendirin. Performans uyarıları ayarlayın. Tümünü birkaç tıklamayla gerçekleştirin.
