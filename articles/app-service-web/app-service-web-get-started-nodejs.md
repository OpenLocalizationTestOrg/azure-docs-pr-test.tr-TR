---
title: "aaaCreate azure'da Node.js web uygulamasına | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk Node.js Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Azure App Service'te Node.js web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.  Bu hızlı başlangıç gösterir nasıl toodeploy bir Node.js uygulaması tooAzure Web uygulamaları. Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek Node.js kodu toohello web uygulaması kullanın.

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz. Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç:

* [Git'i yükleyin](https://git-scm.com/)
* [Node.js ve NPM'yi yükleyin](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Merhaba örnek indirme

Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.

Merhaba örnek kod içeren toohello dizini değiştirin.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Merhaba uygulamayı yerel olarak çalıştırma

Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `npm start` betik toolaunch hello Node.js HTTP sunucusu kurulur.

```bash
npm start
```

Bir web tarayıcısı açın ve http://localhost: 1337 toohello örnek uygulamaya gidin.

Merhaba gördüğünüz **Hello World** hello örnek uygulamadan hello sayfasında görüntülenen ileti.

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-php/app-service-web-service-created.png)

Azure'da yeni bir boş uygulama oluşturdunuz.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello uygulama Gözat

Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.

```bash
http://<app_name>.azurewebsites.net
```

Merhaba Node.js örnek kod bir Azure App Service web uygulaması çalışıyor.

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Tebrikler!** İlk Node.js uygulaması tooApp hizmeti dağıttıktan sonra.

## <a name="update-and-redeploy-hello-code"></a>Güncelleştirme ve hello kodu yeniden dağıtın

Bir metin düzenleyicisi kullanarak hello açın `index.js` dosya hello Node.js uygulamasında ve küçük değişiklikler toohello metin hello çağrıda çok olun`response.end`:

```nodejs
response.end("Hello Azure!");
```

Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.

```bash
git commit -am "updated output"
git push azure master
```

Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün **Gözat toohello uygulama** adım ve yenileme basın.

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Yeni Azure web uygulamanızı yönetme

Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Web uygulamanızın Genel Bakış sayfasını görürsünüz. Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. 

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [MongoDB ile Node.js](app-service-web-tutorial-nodejs-mongodb-app.md)
