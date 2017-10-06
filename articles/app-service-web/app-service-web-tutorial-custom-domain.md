---
title: "aaaMap var olan bir özel DNS ad tooAzure Web Apps | Microsoft Docs"
description: "Nasıl tooadd var olan bir özel DNS etki alanı adı (gösterim etki alanında) tooa web uygulaması, mobil uygulama arka ucu veya Azure App Service'teki API uygulamasına öğrenin."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Harita bir var olan özel DNS adı tooAzure Web uygulamaları

[Azure Web Apps](app-service-web-overview.md) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar. Bu öğretici nasıl toomap var olan bir özel DNS ad tooAzure Web uygulamaları gösterir.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bir alt etki alanı eşleme (örneğin, `www.contoso.com`) bir CNAME kaydı kullanılarak
> * Kök etki alanını eşlemek (örneğin, `contoso.com`) kullanarak bir A kaydı
> * Joker karakter etki alanını eşlemek (örneğin, `*.contoso.com`) bir CNAME kaydı kullanılarak
> * Etki alanı eşlemesi komut dosyaları ile otomatikleştirme

Kullanabilirsiniz bir **CNAME kaydı** veya bir **kayıt** toomap özel DNS tooApp hizmet adı. 

> [!NOTE]
> Bir kök etki alanı dışındaki tüm özel DNS adları için CNAME kullanmanızı öneririz (örneğin, `contoso.com`).

Canlı site ve kendi DNS etki alanı adı tooApp hizmeti toomigrate bkz [etkin bir DNS adı tooAzure uygulama hizmeti geçirmek](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

* [Bir App Service uygulaması oluşturma](/azure/app-service/), veya başka bir öğretici için oluşturduğunuz bir uygulama kullanın.
* Bir etki alanı adı satın alın ve etki alanı sağlayıcınızın (örneğin, GoDaddy) erişim toohello DNS kayıt defteri sahip olduğunuzdan emin olun.

  Örneğin, için DNS girişleri tooadd `contoso.com` ve `www.contoso.com`, mümkün tooconfigure hello DNS ayarlarını hello olmalıdır `contoso.com` kök etki alanı.

  > [!NOTE]
  > Ad, göz önünde bulundurun var olan bir etki alanı yoksa [hello Azure portal kullanarak bir etki alanı satın alma](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Merhaba uygulamasını hazırlama

bir özel DNS adı tooa web uygulamanızın, hello web uygulaması toomap [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) Ücretli katmanı olmalıdır (**paylaşılan**, **temel**, **standart**, veya  **Premium**). Bu adımda, fiyatlandırma katmanı bu hello uygulama hello uygulamadır hizmeti desteklenen emin olun.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Açık hello [Azure portal](https://portal.azure.com) ve Azure hesabınızla oturum açın.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Toohello uygulamada hello Azure portalına gidin

Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından hello uygulamasının hello adı seçin.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/select-app.png)

Merhaba App Service uygulaması hello Yönetimi sayfasında bakın.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Fiyatlandırma katmanı hello denetleyin

Sol gezinti hello uygulama sayfasının hello toohello kaydırma **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.

![Büyütme menüsü](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

Merhaba uygulamanın geçerli katmanı mavi kenarlığı ile vurgulanır. Bu hello uygulama hello olmadığından emin toomake denetleyin **serbest** katmanı. Özel DNS hello desteklenmiyor **serbest** katmanı. 

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Merhaba uygulama hizmeti planı değilse **serbest**, Kapat hello **fiyatlandırma katmanınızı seçin** sayfasında ve çok atla[bir CNAME kaydı eşleme](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Uygulama hizmeti planı Hello ölçeklendirme

Merhaba boş olmayan katmanları birini seçin (**paylaşılan**, **temel**, **standart**, veya **Premium**). 

**Seç**'e tıklayın.

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Bildirim aşağıdaki hello gördüğünüzde, hello ölçeklendirme işlemi tamamlanır.

![Ölçek işlemi onayı](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Harita bir CNAME kaydı

Başlangıç Öğreticisi örnekte hello için bir CNAME kaydı ekleyin `www` alt etki alanı (örneğin, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Merhaba CNAME kaydı oluşturun.

Bir alt etki alanı toohello uygulamanın varsayılan ana bilgisayar adı bir CNAME kaydı toomap ekleyin (`<app_name>.azurewebsites.net`).

Hello için `www.contoso.com` etki alanı örneği hello adı eşleyen bir CNAME kaydı ekleyin `www` çok`<app_name>.azurewebsites.net`.

Merhaba CNAME ekledikten sonra aşağıdaki örneğine hello gibi hello DNS kayıtları sayfasında görünür:

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Azure'da Hello CNAME kaydı eşleştirmeyi etkinleştir

Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**. 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Merhaba, **özel etki alanları** sayfa hello özel DNS adını tam hello uygulama Ekle (`www.contoso.com`) toohello listesi.

Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Merhaba tam etki alanı adını yazın, için bir CNAME kaydı gibi eklenen `www.contoso.com`. 

Seçin **doğrulamak**.

Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir. 

Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**CNAME (www.example.com veya herhangi bir alt etki alanı)**.

Seçin **ana bilgisayar adını eklemek**.

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası. Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Bir adımı eksik veya herhangi bir yerde yazmış hello sayfa hello altındaki bir doğrulama hatası daha önce bkz.

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Bir A kaydı eşleme

Başlangıç Öğreticisi örnekte hello kök etki alanı için bir A kaydı ekleyin (örneğin, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Merhaba uygulamanın IP adresini kopyalayın

toomap bir A kaydı hello uygulamanın dış IP adresi gerekir. Bu IP adresi hello uygulamanın içinde bulabilirsiniz **özel etki alanları** hello Azure portal sayfasında.

Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**. 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Merhaba, **özel etki alanları** sayfasında, hello uygulamanın IP adresini kopyalayın.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Merhaba A kaydını oluşturun

toomap bir A kaydı tooan uygulama, uygulama hizmeti gerekiyor. **iki** DNS kayıtları:

- Bir **A** toomap toohello uygulamanın IP adresini kaydedin.
- A **TXT** toomap toohello uygulamanın varsayılan ana bilgisayar adı kayıt `<app_name>.azurewebsites.net`. Uygulama hizmeti bu kaydı yalnızca yapılandırması sırasında hello özel etki alanı kendi tooverify kullanır. Özel etki alanınız doğrulandı ve App Service'te yapılandırdıktan sonra bu TXT kaydı silebilirsiniz. 

Hello için `contoso.com` etki alanı örneği, aşağıdaki tablonun toohello göre hello A ve TXT kayıtlarını oluşturun (`@` genellikle temsil kök etki alanı hello). 

| Kayıt türü | Host | Değer |
| - | - | - |
| A | `@` | IP adresinden [kopyalama hello uygulamanın IP adresi](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Merhaba kayıtları eklendiğinde, hello DNS kayıtları sayfasında hello örnek aşağıdaki gibi görünür:

![DNS kayıtları sayfasında](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Merhaba hello uygulama kaydı eşlemesindeki etkinleştir

Merhaba uygulamanın edilene **özel etki alanları** sayfasında hello Azure portal, hello özel DNS adını tam ekleyin (örneğin, `contoso.com`) toohello listesi.

Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Merhaba A kaydı, aşağıdaki gibi yapılandırılmış türü hello tam etki alanı adı `contoso.com`.

Seçin **doğrulamak**.

Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir. 

Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**bir kayıt (example.com)**.

Seçin **ana bilgisayar adını eklemek**.

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası. Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.

![Bir kayıt eklendi](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Bir adımı eksik veya herhangi bir yerde yazmış hello sayfa hello altındaki bir doğrulama hatası daha önce bkz.

![Doğrulama hatası](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Bir joker karakter etki alanına Eşle

Hello öğretici örnekte, eşleme bir [joker DNS adına](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (örneğin, `*.contoso.com`) toohello bir CNAME kaydı ekleyerek App Service uygulaması. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Merhaba CNAME kaydı oluşturun.

Bir joker karakter adı toohello uygulamanın varsayılan ana bilgisayar adı bir CNAME kaydı toomap ekleyin (`<app_name>.azurewebsites.net`).

Hello için `*.contoso.com` etki alanı örneği hello CNAME kaydı hello adı eşleme `*` çok`<app_name>.azurewebsites.net`.

Merhaba CNAME eklendiğinde hello DNS kayıtları sayfasında hello örnek aşağıdaki gibi görünür:

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Merhaba uygulamasında Hello CNAME kaydı eşleştirmeyi etkinleştir

Merhaba joker adı toohello uygulama eşleşen alt etki alanı artık ekleyebilirsiniz (örneğin, `sub1.contoso.com` ve `sub2.contoso.com` eşleşen `*.contoso.com`). 

Hello Azure portalında sol gezinti hello uygulama sayfasının hello seçin **özel etki alanları**. 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Merhaba joker karakter etki alanıyla eşleşen bir tam etki alanı adı yazın (örneğin, `sub1.contoso.com`) ve ardından **doğrulama**.

Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir. 

Olduğundan emin olun **ana bilgisayar adı kayıt türü** çok ayarlanır**CNAME kaydı (www.example.com veya herhangi bir alt etki alanı)**.

Seçin **ana bilgisayar adını eklemek**.

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası. Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.

Select hello  **+**  simge tekrar tooadd hello joker karakter etki alanıyla eşleşen başka bir ana bilgisayar adı. Örneğin, ekleyin `sub2.contoso.com`.

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Tarayıcıda test

Daha önce yapılandırılmış toohello DNS adları göz atın (örneğin, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, ve `sub2.contoso.com`).

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Komut dosyalarıyla otomatikleştirme

Hello kullanarak yönetim komut dosyaları ile özel etki alanlarının otomatik hale getirebilirsiniz [Azure CLI](/cli/azure/install-azure-cli) veya [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Azure CLI 

komutu aşağıdaki hello bir yapılandırılmış özel DNS adı tooan App Service uygulaması ekler. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Daha fazla bilgi için bkz: [bir özel etki alanı tooa web uygulaması eşleme](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

komutu aşağıdaki hello bir yapılandırılmış özel DNS adı tooan App Service uygulaması ekler. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Daha fazla bilgi için bkz: [bir özel etki alanı tooa web uygulaması atamak](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Bir alt etki alanı CNAME kaydı kullanılarak eşleme
> * Bir A kaydı kullanarak bir kök etki alanına Eşle
> * Bir CNAME kaydı kullanılarak bir joker karakter etki alanına Eşle
> * Etki alanı eşlemesi komut dosyaları ile otomatikleştirme

İlerlemek toohello sonraki öğretici toolearn nasıl toobind özel bir SSL sertifikası tooa web uygulaması.

> [!div class="nextstepaction"]
> [Bir var olan özel SSL sertifika tooAzure Web Apps bağlama](app-service-web-tutorial-custom-ssl.md)
