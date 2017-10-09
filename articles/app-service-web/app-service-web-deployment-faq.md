---
title: "Azure web uygulamaları için aaaDeployment sık sorulan sorular | Microsoft Docs"
description: "Azure App Service Web Apps özelliğini hello için dağıtımı hakkında sorular yanıtlar toofrequently alın."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Azure Web uygulamalarının dağıtımını SSS

Bu makalede Merhaba dağıtım sorunları hakkında sorulan sorular (SSS) yanıtlar toofrequently sahip [Azure App Service Web Apps özelliğini](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>I yalnızca App Service web apps ile çalışmaya başlama. Kodumu nasıl yayımlanacak?

Web uygulama kodunuzda yayımlamak için bazı seçenekler şunlardır:

*   Visual Studio kullanarak dağıtın. Merhaba Visual Studio çözümünüz varsa hello web uygulama projesine sağ tıklayın ve ardından **Yayımla**.
*   Bir FTP istemcisi kullanarak dağıtın. Hello Azure portal, indirme hello yayımlama hello web uygulaması için profil kodunuzu toodeploy istiyor. Ardından, hello dosyaları too\site\wwwroot karşıya hello kullanarak aynı profili FTP kimlik yayımlayın.

Daha fazla bilgi için bkz: [, uygulama tooApp hizmet dağıtma](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Visual Studio'dan toodeploy çalıştığınızda hata iletisine bakın. Bu nasıl giderebilirim?

İletiden hello görürseniz, hello SDK eski bir sürümünü kullanıyor olabilirsiniz: "'YourResourceGroup' kaynak grubundaki 'YourResourceName' kaynağının dağıtımı sırasında bir hata oluştu: MissingRegistrationForLocation: hello abonelik için kayıtlı değil Merhaba kaynak 'Orta ABD' hello konumda 'Bileşenleri' yazın. Lütfen sıra toohave erişim toothis konumda bu sağlayıcı için yeniden kaydedin." 

tooresolve bu hata, yükseltme toohello [son SDK](https://azure.microsoft.com/downloads/). Bu iletiyi görürseniz ve en yeni SDK'ya hello sahip bir destek isteği gönderin.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Visual Studio tooApp Service ASP.NET uygulamasından nasıl dağıtırım?
<a id="deployasp"></a>

Başlangıç Öğreticisi [beş dakika içinde ilk ASP.NET web uygulamanızı oluşturma](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) nasıl toodeploy bir ASP.NET web uygulaması App Service'in web uygulamasında tooa Visual Studio 2015 kullanarak gösterir.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Dağıtım kimlik bilgileri hello farklı türleri nelerdir?

Uygulama hizmeti yerel Git dağıtımı ve FTP/S dağıtımı için iki kimlik bilgisi türlerinin kullanılmasını destekler. Hakkında daha fazla bilgi için bkz tooconfigure dağıtım kimlik bilgileri, [dağıtım kimlik bilgileri App Service için yapılandırma](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Merhaba dosya veya dizin yapısını my App Service web uygulaması nedir?

Uygulama hizmeti uygulamanızı hello dosya yapısı hakkında daha fazla bilgi için bkz: [dosya yapısı Azure'da](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Ne giderebilirim "FTP hata 550 - orada hello disk üzerinde yeterli alan yok" dosyalarımı tooFTP çalıştığınızda miyim?

Bu iletiyi görürseniz, disk kotası web uygulamanız için hello hizmeti planında çalıştırıyorsanız olasıdır. Disk alanı gereksinimlerinize göre tooa daha yüksek hizmet katmanı oluşturan tooscale gerekebilir. Fiyatlandırma planları ve kaynak sınırları hakkında daha fazla bilgi için bkz: [uygulama hizmeti fiyatlandırma](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>My App Service web uygulaması için sürekli dağıtım nasıl ayarlarım?

Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox ve diğer Git depoları gibi çeşitli kaynaklardan sürekli dağıtım ayarlayabilirsiniz. Bu seçenekler hello Portalı'nda kullanılabilir. [Sürekli dağıtım tooApp hizmet](app-service-continuous-deployment.md) açıklayan yararlı bir öğreticidir nasıl tooset sürekli dağıtım.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>GitHub ve Bitbucket sürekli dağıtım sorunlarını giderme nasıl?

GitHub veya Bitbucket sürekli dağıtım sorunları incelemeye Yardım için bkz. [sürekli dağıtım araştırma](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>I edemiyor toomy site FTP ve kodumu yayımlayın. Bu nasıl giderebilirim?

tooresolve FTP sorunlar:

1. Merhaba doğru ana bilgisayar adı ve kimlik bilgilerini girme olduğunu doğrulayın. Farklı kimlik bilgileri hakkında ayrıntılı bilgi için ve nasıl toouse, görebileceği [dağıtım kimlik bilgileri](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Merhaba FTP bağlantı noktalarını güvenlik duvarı tarafından engellenmeyen olduğunu doğrulayın. Merhaba bağlantı noktalarını bu ayarlara sahip olmalıdır:
    * FTP denetim bağlantı noktası: 21
    * FTP veri bağlantı noktası: 989, 10001 10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>My kod tooApp hizmeti nasıl yayımlanacak?

Hello Azure hızlı başlangıç hello dağıtım yığını ve tercih ettiğiniz yöntemi kullanarak uygulamanızı dağıtma tasarlanmış toohelp ' dir. toouse hello hızlı başlangıç, hello Azure portal, Git çok**ayarları** > **uygulama dağıtımı**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Neden Uygulamam bazen dağıtım tooApp sonra hizmeti yeniden?

toolearn hello koşullar altında bir uygulama dağıtımının neden olabilir bir yeniden başlatma hakkında bkz [dağıtım çalışma zamanı sorunlarına karşılaştırması](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Merhaba makalede gibi uygulama hizmeti dosyaları toohello wwwroot klasörüne dağıtır. Bunu doğrudan uygulamanızı yeniden başlatmaz.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Uygulama hizmeti ile nasıl Visual Studio Team Services kod tümleşik mu?

Visual Studio Team Services ile kullanarak sürekli dağıtımı için iki seçeneğiniz vardır:

*   Git proje kullanın. Uygulama hizmeti bu depo için hello dağıtım seçenekleri kullanarak bağlanın.
*   Team Foundation sürüm denetimi (TFVC'yi) proje kullanın. Uygulama hizmeti için Hello yapı aracısını kullanarak dağıtın.

Bu her iki seçenek için sürekli kod dağıtım varolan geliştirici iş akışları ve iade etme yordamları bağlıdır. Daha fazla bilgi için bu makalelere bakın: 

*   [Sürekli dağıtımı, uygulama tooan Azure Web uygulaması](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Tooa web uygulaması dağıtabilmek için bir Visual Studio Team Services hesabı ayarlamanız](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>FTP veya FTPS toodeploy my uygulama tooApp hizmet nasıl kullanabilirim?

Web uygulaması tooApp hizmeti, FTP veya FTPS toodeploy kullanma hakkında bilgi için bkz: [FTP/S kullanarak, uygulama tooApp hizmet dağıtma](app-service-deploy-ftp.md).
