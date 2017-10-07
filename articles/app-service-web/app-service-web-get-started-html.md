---
title: "Azure web uygulamasında aaaCreate statik HTML | Microsoft Docs"
description: "Bir statik HTML dağıtarak toorun web uygulamaları Azure App Service'deki uygulama nasıl örnek öğrenin."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Azure'da statik bir HTML web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.  Bu hızlı başlangıç nasıl toodeploy temel HTML + CSS site tooAzure Web uygulamaları gösterir. Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek HTML içerik toohello web uygulaması kullanın.

![Örnek uygulamanın giriş sayfası](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz. Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç:

- [Git'i yükleyin](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Merhaba örnek indirme

Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.

## <a name="view-hello-html"></a>Görünüm başlangıç HTML

Merhaba örnek HTML içeren toohello dizinine gidin. Açık hello *index.html* dosyayı tarayıcınızda.

![Örnek uygulama ana sayfası](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-html/app-service-web-service-created.png)

Azure'da yeni bir boş uygulama oluşturdunuz.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello uygulama Gözat

Bir tarayıcıda toohello Azure web uygulaması URL'si gidin:

```
http://<app_name>.azurewebsites.net
```

Başlangıç sayfası, bir Azure App Service web uygulaması çalışıyor.

![Örnek uygulama ana sayfası](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Tebrikler!** İlk, HTML Uygulama tooApp hizmeti dağıttıktan sonra.

## <a name="update-and-redeploy-hello-app"></a>Güncelleştirme ve hello uygulama yeniden dağıtın

Açık hello *index.html* dosyasını bir metin düzenleyicisinde ve değişiklik toohello biçimlendirme yapın. Örneğin, "Azure uygulama hizmeti – örnek statik HTML Site" toojust hello H1 başlığını değiştirme "Azure uygulama hizmeti '.

Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.

```bash
git commit -am "updated HTML"
git push azure master
```

Dağıtım tamamlandıktan sonra tarayıcı toosee hello değişikliklerinizi yenileyin.

![Güncelleştirilen örnek uygulama giriş sayfası](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Yeni Azure web uygulamanızı yönetme

Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-html/portal1.png)

Web uygulamanızın Genel Bakış sayfasını görürsünüz. Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. 

![Azure portalında App Service dikey penceresi](./media/app-service-web-get-started-html/portal2.png)

Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Özel etki alanı eşleme](app-service-web-tutorial-custom-domain.md)
