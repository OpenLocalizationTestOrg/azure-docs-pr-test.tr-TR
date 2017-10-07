---
title: "aaaDeploy hello beş dakikada Azure portalında bir Umbraco web uygulamasında | Microsoft Docs"
description: "Ne kadar kolay toorun App Service'te web uygulamalarını örnek bir ASP.NET uygulaması dağıtarak olduğunu öğrenin. Sonuçları anında görün."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Beş dakika içinde bir hello Azure portal Umbraco web uygulamasında dağıtma

Bu öğretici n dağıtmanıza yardımcı olan [Umbraco](https://our.umbraco.org/) çok web uygulaması[Azure App Service](../app-service/app-service-value-prop-what-is.md) dakika.

![Umbraco uygulaması](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Ön koşullar
Bir Microsoft Azure hesabınızın olması gerekir. Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)

> [!NOTE]
> Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/). Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Merhaba ASP.NET uygulamasını dağıtma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS) adresini açın.

    Bu bir kısayol tooimmediately hello Azure portalında yeni bir Umbraco uygulaması yapılandırma bağlantıdır.

3. **Uygulama adı** bölümünde bir web uygulaması adı girin. Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `azurewebsites.net` etki alanı.
   
5. İçinde **kaynak grubu**, tıklatın **Yeni Oluştur** yeni bir toocreate [kaynak grubu](../azure-resource-manager/resource-group-overview.md), bir ad verin.

7. **App Service planı/Konum** > **Yeni Oluştur**'a tıklayın. Merhaba yapılandırma [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) gösterildiği gibi:

    - İçinde **uygulama hizmeti planı**, türü hello istenen adı.
    - İçinde **konumu**, bir konum toohost planınızı seçin.
    - **Fiyatlandırma katmanı**'na tıklayıp **F1 Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.
    - **Tamam** düğmesine tıklayın.

    Umbraco CMS yapılandırmanızı hello ekran aşağıdaki gibi görünmelidir:

    ![Yapılandırma devam ediyor - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. **SQL Veritabanı** > **Yeni veritabanı oluştur**'a tıklayın. SQL veritabanı Hello gösterildiği gibi yapılandırın:

    - **Ad** alanına **myDB** gibi bir ad girin.
    - **Fiyatlandırma katmanı**'na tıklayıp **F Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.
    - **Hedef sunucu** > **Yeni sunucu oluştur**'a tıklayın. Merhaba veritabanı sunucusu gösterildiği gibi yapılandırın:

        - **Sunucu adı** alanına bir sunucu adı yazın. Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `.database.windows.net` etki alanı.
        - İçinde **Sunucu Yöneticisi oturum açma**, türü hello istenen yöneticinin kullanıcı adı.
        - İçinde **parola** ve **parolayı onayla**, hello istediğiniz parolayı girin.
        - Konumunda, select hello web uygulaması için kullandığınız aynı konuma hello.
        - Emin olun **izin azure Hizmetleri tooaccess sunucusu** seçilir.
        - **Seç**'e tıklayın.
    
    - **Seç**'e tıklayın.

13. Tıklatın **Web uygulaması ayarları**hello veritabanı kullanıcı adı ve parola belirtin ve tıklatın **Tamam**.

    Umbraco CMS yapılandırmanızı hello ekran aşağıdaki gibi görünmelidir:

    ![Yapılandırma tamamlandı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. **Oluştur**’a tıklayın.
    
    Azure şimdi yapılandırmanızı temel alarak Umbraco uygulamanızı oluşturur. **Dağıtım başlatıldı...** bildirimini görmeniz gerekir.

    ![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Umrbaco web uygulamanızı başlatma ve yönetme

Azure uygulama dağıtımını tamamladığında başka bir bildirim daha göreceksiniz.

![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Merhaba bildirime tıklayın. Bu eksik, her zaman hello bildirim zil tıklayarak erişebildiğinizi (![bildirim aşağıdaki - Azure App Service'te ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Şimdi web uygulamasının yönetim [dikey penceresini](../azure-resource-manager/resource-group-portal.md#manage-resources) (*dikey pencere*: dikey olarak açılan portal sayfası) görmeniz gerekir.

3. Merhaba genel bakış sayfası Hello üst tıklatın **Gözat**.
   
    ![Göz at - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Merhaba Umbraco gördüğünüz artık **Hoş Geldiniz** sayfası. Merhaba Umbraco yükleme yapılandırmak ve onunla yürütmeye başlayın!

    ![Umbraco yapılandırması - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Sonraki adımlar
* [Bir ASP.NET web uygulaması tooAzure App Service, Visual Studio kullanarak dağıtmak](app-service-web-get-started-dotnet.md) -toocreate hello herhangi birini kullanarak Visual Studio'da yeni bir Azure web uygulaması uygulama şablonları nasıl dahil öğrenin.
* [Kod tooAzure uygulama hizmeti dağıtmak](web-sites-deploy.md)-toodeploy FTP ya da kaynak havuzları nasıl kontrol öğrenin.
* [İşlevselliği tooyour ilk web uygulamanız eklemek](app-service-web-get-started-2.md) -Azure uygulaması toohello sonraki düzeye taşıyın. Kullanıcılarınızın kimliklerini doğrulayın. Talebe göre ölçeklendirin. Performans uyarıları ayarlayın. Tümünü birkaç tıklamayla gerçekleştirin.
