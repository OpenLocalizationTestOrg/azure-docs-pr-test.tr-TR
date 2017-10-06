---
title: "aaaCreate bir Ruby uygulaması Linux üzerinde Web uygulamalarıyla | Microsoft Docs"
description: "Toocreate Ruby öğrenin Linux Azure web wpp uygulamalarla."
keywords: Azure uygulama hizmeti, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Linux üzerinde Web uygulamaları ile Söyleniş bir uygulama oluşturun. 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar. Bu hızlı başlangıç toocreate rayları uygulama üzerinde temel bir Ruby sonra dağıtma gösterir tooAzure Linux üzerinde bir Web uygulaması olarak.

![Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Ön koşullar

* [Ruby 2.4.1 ya da daha yüksek](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Bir [etkin Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Merhaba örnek indirme

Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma

Merhaba uygulama toowork sırada Hello rayları sunucu çalıştırın. Değiştirme toohello *Merhaba Dünya* dizin ve hello `rails server` başlatır hello sunucu komutu.

```bash
cd hello-world\bin
rails server
```
    
Web tarayıcınız üzerinden gidin çok`http://localhost:3000` tootest hello uygulamasını yerel olarak.  

![Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Uygulama toodisplay Hoş Geldiniz iletisi değiştirme

Hoş Geldiniz iletisi görüntüler şekilde hello uygulama değiştirin. Merhaba uygulamanın denetleyicisini selamlama iletisine HTML toohello tarayıcı olarak döndürecek şekilde değiştirin. 

Açık *~/workspace/hello-world/app/controllers/application_controller.rb* düzenlemek için. Merhaba değiştirme `ApplicationController` sınıfı toolook hello kodu örneği aşağıdaki gibi:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Uygulamanız şimdi yapılandırıldı. Web tarayıcınız üzerinden gidin çok`http://localhost:3000` tooconfirm hello kök giriş sayfası.

![Yapılandırılmış Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Azure üzerinde bir Söyleniş web uygulaması oluşturma

Kullanım hello [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) komutu toocreate web uygulamanız için bir app service planı. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Ardından, hello sorun [az webapp oluşturmak](https://docs.microsoft.com/cli/azure/webapp) yeni oluşturulan hello hizmet planı kullanan komut toocreate hello web uygulaması. Bu hello çalışma zamanı çok ayarlamak fark`ruby|2.3`. Tooreplace unutmayın `<app name>` benzersiz bir uygulama adına sahip.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Merhaba web uygulaması oluşturulduktan sonra bir **genel bakış** kullanılabilir tooview sayfasıdır. Tooit gidin. Giriş sayfası aşağıdaki hello görüntülenir:

![Giriş sayfası](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Uygulamanızı dağıtmak

Git toodeploy hello Ruby uygulaması tooAzure kullanın. yapılandırılmış bir Git dağıtımı Hello web uygulaması zaten var. Vererek hello dağıtım URL'si alabilir bir [az webapp dağıtım](https://docs.microsoft.com/cli/azure/webapp/deployment) komutu.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Git URL'si hello dikkat edin, web uygulaması adınıza göre form aşağıdaki hello sahiptir:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Komutları toodeploy hello yerel uygulama tooyour Azure Web sitesinde aşağıdaki hello çalıştırın:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Merhaba uzak dağıtım işlemlerini Başarı Raporu onaylayın. Merhaba komutları ürettiği benzer toohello metin aşağıdaki çıktı:

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Merhaba dağıtım tamamlandıktan sonra web uygulamanız için hello dağıtım tootake etkisi hello kullanarak yeniden [az webapp yeniden](https://docs.microsoft.com/cli/azure/webapp#restart) aşağıda gösterildiği gibi komut:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Tooyour site gidin ve hello sonuçlarını doğrulayın.

```bash
http://<your web app name>.azurewebsites.net
```
![güncelleştirilmiş web uygulaması](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Merhaba uygulama yeniden başlatılırken bir HTTP durum kodu toobrowse hello site sonuçlarında çalışırken `Error 503 Server unavailable`. Birkaç dakika sürebilir toofully yeniden başlatın.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Sonraki adımlar

[Azure App Service Web uygulaması Linux SSS](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)