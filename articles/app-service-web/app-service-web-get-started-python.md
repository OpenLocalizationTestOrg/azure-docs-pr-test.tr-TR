---
title: "aaaCreate bir Python web uygulamasını Azure | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk Python Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a>Azure’da Python web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.  Bu hızlı başlangıç nasıl anlatılmaktadır toodevelop ve Python uygulama tooAzure Web uygulamaları dağıtın. Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek Python kodu toohello web uygulaması kullanın.

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz. Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.
## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

1. [Git'i yükleyin](https://git-scm.com/)
1. [Python'ı yükleyin](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Merhaba örnek indirme

Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.

Merhaba örnek kod içeren toohello dizini değiştirin.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Merhaba uygulamayı yerel olarak çalıştırma

Kullanarak hello gerekli paketleri yüklemek `pip`.

```bash
pip install -r requirements.txt
```

Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `Python` komutu toolaunch hello yerleşik Python web sunucusu.

```bash
python main.py
```

Bir web tarayıcısı açın ve http://localhost: 5000 toohello örnek uygulamaya gidin.

Merhaba görebilirsiniz **Hello World** hello örnek uygulamadan hello sayfasında görüntülenen ileti.

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-python/app-service-web-service-created.png)

Azure'da yeni bir boş uygulama oluşturdunuz.

## <a name="configure-toouse-python"></a>Toouse Python yapılandırın

Kullanım hello [az webapp yapılandırma kümesi](/cli/azure/webapp/config#set) komutu tooconfigure hello web uygulama toouse Python sürümü `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Bu şekilde Hello Python sürümü ayarı hello platform tarafından sağlanan varsayılan kapsayıcı kullanır. toouse kendi kapsayıcı bkz hello hello için CLI başvurusu [az webapp config kapsayıcı kümesi](/cli/azure/webapp/config/container#set) komutu.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Toohello uygulama Gözat

Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.

```bash
http://<app_name>.azurewebsites.net
```

Merhaba Python örnek kod bir Azure App Service web uygulaması çalışıyor.

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Tebrikler!** İlk Python uygulaması tooApp hizmeti dağıttıktan sonra.

## <a name="update-and-redeploy-hello-code"></a>Güncelleştirme ve hello kodu yeniden dağıtın

Bir yerel metin düzenleyicisi kullanarak hello açmak `main.py` dosya hello Python uygulamada ve küçük değişiklikler toohello metin sonraki toohello olun `return` deyimi:

```python
return 'Hello, Azure!'
```

Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.

```bash
git commit -am "updated output"
git push azure master
```

Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün [Gözat toohello uygulama](#browse-to-the-app) adım ve yenileme hello sayfası.

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-python/hello-azure-in-browser.png)

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
> [PostgreSQL ile Python](app-service-web-tutorial-docker-python-postgresql-app.md)
