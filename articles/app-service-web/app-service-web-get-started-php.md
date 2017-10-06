---
title: "aaaCreate bir PHP web uygulamasına | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk PHP Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Azure’da PHP web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.  Bu hızlı başlangıç Öğreticisi gösterir nasıl toodeploy bir PHP uygulaması tooAzure Web uygulamaları. Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) içinde bulut kabuk ve Git toodeploy örnek PHP kodunu toohello web uygulaması kullanın.

![Azure'da çalışan örnek uygulama]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz. Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç:

* [Git'i yükleyin](https://git-scm.com/)
* [PHP'yi yükleyin](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Merhaba örnek yerel olarak indir

Bir terminal penceresi hello aşağıdaki komutları çalıştırın. Bu hello örnek uygulama tooyour yerel makine ve toohello directory içeren hello örnek kod gidin.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Merhaba uygulamayı yerel olarak çalıştırma

Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `php` komutu toolaunch hello yerleşik PHP web sunucusu.

```bash
php -S localhost:8080
```

Bir web tarayıcısı açın ve http://localhost: 8080 toohello örnek uygulamaya gidin.

Merhaba gördüğünüz **Merhaba Dünya!** ileti hello örnek uygulamadan hello sayfasında görüntülenir.

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Boş web uygulaması sayfası](media/app-service-web-get-started-php/app-service-web-service-created.png)

Azure'da yeni bir boş uygulama oluşturdunuz.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>Yerel olarak toohello uygulama Gözat

Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.

```bash
http://<app_name>.azurewebsites.net
```

Merhaba PHP örnek kod bir Azure App Service web uygulaması çalışıyor.

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Tebrikler!** İlk, PHP uygulaması tooApp hizmeti dağıttıktan sonra.

## <a name="update-locally-and-redeploy-hello-code"></a>Yerel olarak güncelleştirin ve hello kodu yeniden dağıtın

Bir yerel metin düzenleyicisi kullanarak hello açmak `index.php` dosya hello PHP uygulama içinde ve küçük değişiklikler toohello metin hello dizesindeki sonraki çok olun`echo`:

```php
echo "Hello Azure!";
```

Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.

```bash
git commit -am "updated output"
git push azure master
```

Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün **Gözat toohello uygulama** adım ve yenileme hello sayfası.

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Yeni Azure web uygulamanızı yönetme

Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Web uygulamanızın Genel Bakış sayfasını görürsünüz. Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [MySQL ile PHP](app-service-web-tutorial-php-mysql.md)
