---
title: "aaaCreate bir ASP.NET web uygulamasına | Microsoft Docs"
description: "Nasıl hello varsayılan ASP.NET dağıtarak toorun web uygulamaları Azure App Service'te web uygulaması hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Azure’da ASP.NET web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.  Bu hızlı başlangıç gösterir nasıl toodeploy ilk ASP.NET web uygulaması tooAzure Web uygulamaları. İşlemi tamamladığınızda bir App Service planı ve dağıtılmış web uygulaması ile Azure web uygulamasından oluşan kaynak grubunuz olacaktır.

Bu hızlı başlangıç eylem Hello video toosee izleyin ve ardından izleyin hello adımları kendiniz toopublish ilk .NET uygulamanızı Azure üzerinde.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

* Yükleme [Visual Studio 2017](https://www.visualstudio.com/downloads/) iş yükleri aşağıdaki hello ile:
    - **ASP.NET ve web geliştirme**
    - **Azure geliştirme**

    ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>ASP.NET web uygulaması oluşturma

Visual Studio'da **Dosya > Yeni > Proje**’yi seçerek bir proje oluşturun. 

Merhaba, **yeni proje** iletişim kutusunda **Visual C# > Web > ASP.NET Web uygulaması (.NET Framework)**.

Ad Merhaba uygulaması _myFirstAzureWebApp_ve ardından **Tamam**.
   
![Yeni Proje iletişim kutusu](./media/app-service-web-get-started-dotnet/new-project.png)

ASP.NET web uygulaması tooAzure herhangi bir türde dağıtabilirsiniz. Bu Hızlı Başlangıç için hello seçin **MVC** şablonu ve kimlik doğrulama çok ayarlandığından emin olun**doğrulaması yok**.
      
**Tamam**’ı seçin.

![Yeni ASP.NET Projesi iletişim kutusu](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Başlangıç menüsünden seçin **hata ayıklama > hata ayıklama olmadan Başlat** toorun hello web uygulamasını yerel olarak.

![Uygulamayı yerel olarak çalıştırma](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>TooAzure yayımlama

Merhaba, **Çözüm Gezgini**, sağ hello **myFirstAzureWebApp** proje ve seçin **Yayımla**.

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’yı seçin.

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Merhaba açılır **App Service Oluştur** iletişim kutusu, Azure'da tüm hello gerekli Azure kaynaklarını toorun hello ASP.NET web uygulaması oluşturmanıza yardımcı olur.

## <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Merhaba, **App Service Oluştur** iletişim kutusunda **Hesap Ekle**ve tooyour Azure aboneliği oturum açın. Zaten oturum açtınız, hello içeren select hello hesabı hello açılır abonelikten istenen.

> [!NOTE]
> Zaten oturum açtıysanız **Oluştur** öğesini henüz seçmeyin.
>
>
   
![İçinde tooAzure oturum](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Sonraki çok**kaynak grubu**seçin **yeni**.

Ad hello kaynak grubu **myResourceGroup** seçip **Tamam**.

## <a name="create-an-app-service-plan"></a>App Service planı oluşturma

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Sonraki çok**App Service planı**seçin **yeni**. 

Merhaba, **App Service planı Yapılandır** iletişim kutusunda, hello ekran aşağıdaki hello tablosundaki hello ayarları kullanın.

![App Service planı oluşturma](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Ayar | Önerilen Değer | Açıklama |
|-|-|-|
|App Service Planı| myAppServicePlan | Merhaba uygulama hizmeti plan adı. |
| Konum | Batı Avrupa | Merhaba veri merkezi başlangıç web uygulaması barındırıldığı. |
| Boyut | Ücretsiz | [Fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/app-service/), barındırma özelliklerini belirler. |

**Tamam**’ı seçin.

## <a name="create-and-publish-hello-web-app"></a>Oluşturma ve yayımlama hello web uygulaması

İçinde **Web uygulaması adı**, benzersiz uygulama adını yazın (geçerli karakterler `a-z`, `0-9`, ve `-`), veya hello otomatik olarak oluşturulan benzersiz adı kabul edin. Merhaba web uygulaması Hello URL'sidir `http://<app_name>.azurewebsites.net`, burada `<app_name>` web uygulaması adı.

Seçin **oluşturma** toostart hello Azure kaynakları oluşturma.

![Web uygulaması adını yapılandırma](./media/app-service-web-get-started-dotnet/web-app-name.png)

Merhaba Sihirbaz tamamlandıktan sonra hello ASP.NET web uygulaması tooAzure yayımlar ve ardından başlatır hello varsayılan tarayıcıda uygulama hello.

![Azure’da yayımlanmış ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

Hello belirtilen hello web uygulaması adı [oluşturma ve yayımlama adım](#create-and-publish-the-web-app) URL öneki hello biçiminde hello olarak kullanılan `http://<app_name>.azurewebsites.net`.

Tebrikler, ASP.NET web uygulamanız Azure App Service’te çalışıyor.

## <a name="update-hello-app-and-redeploy"></a>Güncelleştirme hello uygulama ve yeniden dağıtın

Merhaba gelen **Çözüm Gezgini**, açık _Views\Home\Index.cshtml_.

Hello bulur `<div class="jumbotron">` HTML etiketi hello yukarıya yakın ve koddan hello ile Merhaba tüm öğeyi değiştirin:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, sağ hello **myFirstAzureWebApp** proje **Çözüm Gezgini** seçip **Yayımla**.

Merhaba, yayımlama sayfası, seçin **Yayımla**.

Yayımlama tamamlandığında Visual Studio Başlangıç web uygulaması bir tarayıcı toohello URL başlatır.

![Azure’da güncelleştirilmiş ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Hello Azure web uygulaması yönetme

Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web uygulaması.

Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adı seçin.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-dotnet/access-portal.png)

Web uygulamanızın Genel Bakış sayfasını görürsünüz. Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. 

![Azure portalında App Service dikey penceresi](./media/app-service-web-get-started-dotnet/web-app-blade.png)

Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [SQL Veritabanı ile ASP.NET](app-service-web-tutorial-dotnet-sqldatabase.md)
