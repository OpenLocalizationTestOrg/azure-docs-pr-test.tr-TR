---
title: "aaaMigrate etkin bir DNS adı tooAzure App Service | Microsoft Docs"
description: "Nasıl toomigrate tooa zaten atanmış olan özel bir DNS etki alanı adı Canlı herhangi kesinti olmadan site tooAzure uygulama hizmeti hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Etkin bir DNS adı tooAzure uygulama hizmeti geçirme

Bu makalede toomigrate etkin bir DNS adı çok nasıl gösterilmektedir[Azure App Service](../app-service/app-service-value-prop-what-is.md) herhangi kesinti olmadan.

Canlı site ve kendi DNS etki alanı adı tooApp hizmeti geçirdiğinizde, o DNS adını dinamik trafik zaten hizmet veriyor. Merhaba etkin DNS adı tooyour App Service uygulaması erken önlem bağlayarak hello geçiş sırasında kapalı kalma süresi DNS çözümlemesi ile önleyebilirsiniz.

Kapalı kalma süresi DNS çözümlemesi ile ilgili endişeleniyoruz değil, bkz: [bir var olan özel DNS adı tooAzure Web Apps eşleme](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Ön koşullar

toocomplete bu nasıl yapılır:

- [Uygulama hizmeti uygulamanızı ücretsiz katmanında olmadığından emin olun](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Merhaba etki alanı adı erken önlem bağlama

Özel bir etki alanı erken önlem bağladığınızda, hem de DNS kayıtlarınızı herhangi bir değişiklik yapmadan önce hello aşağıdakileri gerçekleştirirsiniz:

- Etki alanı sahipliğini doğrulayın
- Merhaba etki alanı adını, uygulamanız için etkinleştir

Merhaba eski site toohello App Service uygulaması son olarak, özel DNS adı geçirdiğinizde, DNS çözümlemesi kapalı kalma süresi olacaktır.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Etki alanı doğrulama kaydı oluşturma

tooverify etki alanı sahipliğini Ekle bir TXT kaydı. Merhaba TXT kaydı eşlemeleri _awverify.&lt; alt etki alanı >_ too_&lt;uygulamaadı >. azurewebsites.net_. 

Merhaba ihtiyacınız TXT kaydı toomigrate istediğiniz DNS kaydı hello üzerinde bağlıdır. Örnekler için aşağıdaki tablonun hello bakın (`@` genellikle temsil kök etki alanı hello):  

| DNS kaydı örneği | TXT ana bilgisayar | TXT değeri |
| - | - | - |
| @ (root) | _awverify_ | _&lt;uygulamaadı >. azurewebsites.net_ |
| www (alt) | _awverify.www_ | _&lt;uygulamaadı >. azurewebsites.net_ |
| \*(joker karakterler) | _awverify.\*_ | _&lt;uygulamaadı >. azurewebsites.net_ |

DNS kayıtları sayfasında hello toomigrate istediğiniz DNS ad kayıt türü hello unutmayın. Uygulama hizmeti CNAME ve A kayıtlarını eşlemelerini destekler.

### <a name="enable-hello-domain-for-your-app"></a>Uygulamanız için Hello etki alanı etkinleştir

Merhaba, [Azure portal](https://portal.azure.com), buna hello hello uygulama sayfasının sol gezinti bölmesinde, seçin **özel etki alanları**. 

![Özel etki alanı menüsü](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Merhaba, **özel etki alanları** sayfası, select hello  **+**  simgesi sonraki çok**ana bilgisayar adını eklemek**.

![Ana bilgisayar adı ekleyin](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Hello tam etki alanı adını yazın, hello TXT kaydı gibi eklenen `www.contoso.com`. Bir joker karakter etki alanı için (gibi \*. contoso.com), hello joker karakter etki alanıyla eşleşen herhangi bir DNS adı kullanabilirsiniz. 

Seçin **doğrulamak**.

Merhaba **ana bilgisayar adını eklemek** düğmesi etkinleştirilir. 

Olduğundan emin olun **ana bilgisayar adı kayıt türü** toomigrate istediğiniz toohello DNS kaydı türünü ayarlayın.

Seçin **ana bilgisayar adını eklemek**.

![DNS adı toohello uygulama Ekle](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Merhaba uygulamanın içinde yansıtılan hello yeni ana bilgisayar adı toobe için biraz zaman alabilir **özel etki alanları** sayfası. Merhaba tarayıcı tooupdate hello verileri yenilemeyi deneyin.

![CNAME kaydı eklendi](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Özel DNS adınızı Azure uygulamanızı şimdi etkinleştirildi. 

## <a name="remap-hello-active-dns-name"></a>Merhaba active DNS adı yeniden eşleme

Merhaba yalnızca şey sol toodo, etkin DNS kaydı toopoint tooApp hizmeti yeniden eşleme. Sağ şimdi onu hala tooyour eski site işaret eder.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Merhaba uygulamanın IP adresini (yalnızca bir kayıt) kopyalayın

Bir CNAME kaydı yeniden eşleme, bu bölümü atlayabilirsiniz. 

tooremap bir A kaydı hello gösterilen hello uygulama hizmeti uygulamanın dış IP adresine gereksinim **özel etki alanları** sayfası.

Kapat hello **ana bilgisayar adını eklemek** seçerek sayfa **X** hello sağ üst köşedeki. 

Merhaba, **özel etki alanları** sayfasında, hello uygulamanın IP adresini kopyalayın.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Merhaba DNS kaydını güncelleştirin

Geri hello DNS kayıtları sayfasında, etki alanı sağlayıcısının hello DNS kaydı tooremap seçin.

Hello için `contoso.com` kök etki alanı örneği, aşağıdaki tablonun hello hello örneklerde gibi hello A veya CNAME kaydı yeniden eşleyin: 

| FQDN örneği | Kayıt türü | Host | Değer |
| - | - | - | - |
| contoso.com (root) | A | `@` | IP adresinden [kopyalama hello uygulamanın IP adresi](#info) |
| www.contoso.com (alt) | CNAME | `www` | _&lt;uygulamaadı >. azurewebsites.net_ |
| \*. contoso.com (joker karakterler) | CNAME | _\*_ | _&lt;uygulamaadı >. azurewebsites.net_ |

Ayarlarınızı kaydedin.

DNS sorguları hemen DNS'ye yayma işlemi gerçekleştikten sonra tooyour App Service uygulaması çözme başlamanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toobind özel bir SSL sertifikası tooApp hizmeti hakkında bilgi edinin.

> [!div class="nextstepaction"]
> [Bir var olan özel SSL sertifika tooAzure Web Apps bağlama](app-service-web-tutorial-custom-ssl.md)
