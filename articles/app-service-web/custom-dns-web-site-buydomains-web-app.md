---
title: "aaaBuy Azure Web uygulamaları için özel etki alanı adı"
description: "Nasıl toobuy özel bir etki alanı adını Azure App Service'te bir web uygulaması ile bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Azure Web uygulamaları için özel etki alanı adı satın alma

Uygulama hizmeti etki alanları (Önizleme) doğrudan Azure içinde yönetilen en üst düzey etki alanlarıdır. Bunlar, kolay toomanage özel etki alanları oluşturmak için [Azure Web Apps](app-service-web-overview.md). Bu öğretici nasıl toobuy bir uygulama hizmeti etki alanı Ata DNS adları ve tooAzure Web uygulamaları gösterir.

Bu makalede Azure uygulama hizmeti (Web Apps, API Apps, Mobile Apps, Logic Apps) içindir. Azure VM veya Azure Storage için bkz: [atamak uygulama hizmeti etki alanı tooAzure VM veya Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Bulut Hizmetleri için bkz: [bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

* [Bir App Service uygulaması oluşturma](/azure/app-service/), veya başka bir öğretici için oluşturduğunuz bir uygulama kullanın.

## <a name="prepare-hello-app"></a>Merhaba uygulamasını hazırlama

Azure Web uygulamaları, web uygulaması'nın özel etki alanlarında toouse [uygulama hizmeti planı](https://azure.microsoft.com/pricing/details/app-service/) Ücretli katmanı olmalıdır (**paylaşılan**, **temel**, **standart**, veya **Premium**). Bu adımda, bu hello web uygulaması fiyatlandırma katmanı hello desteklenir emin olun.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Açık hello [Azure portal](https://portal.azure.com) ve Azure hesabınızla oturum açın.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Toohello uygulamada hello Azure portalına gidin

Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından hello uygulamasının hello adı seçin.

![Portal Gezinti tooAzure uygulama](./media/app-service-web-tutorial-custom-domain/select-app.png)

Merhaba App Service uygulaması hello Yönetimi sayfasında bakın.  

### <a name="check-hello-pricing-tier"></a>Fiyatlandırma katmanı hello denetleyin

Sol gezinti hello uygulama sayfasının hello toohello kaydırma **ayarları** bölümünde ve seçin **(uygulama hizmeti planı) ölçeklendirme**.

![Büyütme menüsü](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

Merhaba uygulamanın geçerli katmanı mavi kenarlığı ile vurgulanır. Bu hello uygulama hello olmadığından emin toomake denetleyin **serbest** katmanı. Özel DNS hello desteklenmiyor **serbest** katmanı. 

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Merhaba uygulama hizmeti planı değilse **serbest**, Kapat hello **fiyatlandırma katmanınızı seçin** sayfasında ve çok atla[satınalma hello etki alanı](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Uygulama hizmeti planı Hello ölçeklendirme

Merhaba boş olmayan katmanları birini seçin (**paylaşılan**, **temel**, **standart**, veya **Premium**). 

**Seç**'e tıklayın.

![Fiyatlandırma katmanı denetleyin](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Bildirim aşağıdaki hello gördüğünüzde, hello ölçeklendirme işlemi tamamlanır.

![Ölçek işlemi onayı](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Merhaba etki alanı satın alma

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum
Açık hello [Azure portal](https://portal.azure.com/) ve Azure hesabınızla oturum açın.

### <a name="launch-buy-domains"></a>Satınalma etki alanları başlatma
Merhaba, **Web Apps** sekmesini seçin, web uygulamanızın hello adını tıklatın, **ayarları**ve ardından **özel etki alanları**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Merhaba, **özel etki alanları** sayfasında, **satın etki alanları**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Merhaba etki alanı satın alma yapılandırın

Merhaba, **uygulama hizmeti etki alanı** sayfasında hello **etki alanı Ara** kutusu, hello etki alanı adını yazın, istediğiniz toobuy ve türü `Enter`. Merhaba önerilen kullanılabilir etki alanlarının hemen altındaki metin kutusuna hello gösterilir. Toobuy istediğiniz bir veya daha fazla etki alanı seçin. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Merhaba tıklatın **iletişim bilgileri** ve hello etki alanının kişi bilgilerini formu doldurun. Tamamlandığında tıklatarak **Tamam** tooreturn toohello uygulama hizmeti etki alanı sayfası.
   
Mümkün olduğunca doğruluğu ile tüm gerekli alanları doldurun önemlidir. İletişim bilgileri için yanlış veri hatası toopurchase alanlarında neden olabilir. 

Ardından, etki alanınız için istenen hello seçenekleri seçin. Aşağıdaki tablonun açıklamalarını hello bakın:

| Ayar | Önerilen Değer | Açıklama |
|-|-|-|
|Otomatik yenileme | **Etkinleştirme** | Uygulama hizmeti etki alanınızın her yıl otomatik olarak yeniler. Kredi kartınızdan ücret yenileme hello aynı anda aynı satın alma ücretinin hello. |
|Gizlilik Koruması | Etkinleştirme | Çok kabul "Merhaba satın alma fiyatına dahil gizlilik korumasını" _ücretsiz_ (kayıt defterine desteklemediği gizlilik korumasını gibi üst düzey etki alanları dışında _. co.in_, _. co.uk_, vb.). |
| Varsayılan ana bilgisayar adları atama | **www** ve**@** | Select hello konak adı bağlamaları isterseniz istenen. Merhaba etki alanı satın alma işlemi tamamlandığında, web uygulamanızı seçili hello ana bilgisayar adları erişilebilir. Merhaba web uygulaması arkasında ise [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), hello seçeneği tooassign hello kök etki alanı görmüyorum (@), çünkü destek A kayıtlarını trafik Yöneticisi yapar. Merhaba etki alanı satın alma işlemi tamamlandıktan sonra toohello hostname atamaları değişiklik yapabilirsiniz. |

### <a name="accept-terms-and-purchase"></a>Koşulları kabul etmek ve satın alma

Tıklatın **yasal koşulları** tooreview hello koşulları ve hello ücretleri, ardından **satın**.

> [!NOTE]
> Uygulama hizmeti etki alanlarının Azure DNS'ye toohost hello etki alanları kullanın. Ayrıca toohello etki alanı kayıt ücreti, kullanım ücretleri Azure DNS için geçerlidir. Bilgi için bkz: [Azure DNS fiyatlandırma](https://azure.microsoft.com/pricing/details/dns/).
>
>

Merhaba edilene **uygulama hizmeti etki alanı** sayfasında, **Tamam**. Merhaba işlemi sürerken bildirimleri aşağıdaki hello bakın:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Test hello ana bilgisayar adları

Varsayılan ana bilgisayar adları tooyour web uygulaması atanmışsa, seçilen her ana bilgisayar adı için bir başarı bildirimi de görebilirsiniz. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Merhaba hello seçili konak adları Ayrıca bkz: **özel etki alanları** sayfasında hello **ana bilgisayar adları** bölümü. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

tootest hello ana bilgisayar adı, listelenen toohello ana bilgisayar adları hello tarayıcıda gidin. Merhaba hello örnekte ekran, önceki deneyin too_kontoso.net_ gezinme ve _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Ana bilgisayar adları tooweb uygulama atama

Değil tooassign birini seçin veya daha fazla varsayılan ana bilgisayar adları tooyour web uygulaması hello sırasında satın alma işlemi ya da tooassign bir ana bilgisayar adı değil gerekiyorsa listelenen bir ana bilgisayar adı zaman atayabilirsiniz.

Ayrıca, diğer web uygulaması hello uygulama hizmeti etki alanı tooany konak adları atayabilirsiniz. Merhaba adımları olup olmadığını hello uygulama hizmeti etki alanı ve hello web uygulaması toohello ait üzerinde bağımlı aynı abonelik.

- Farklı bir abonelik: eşleme hello uygulama hizmeti etki alanı toohello web uygulamasından harici olarak satın alınan bir etki alanı gibi özel DNS kaydı. Ekleme özel DNS hakkında bilgi tooan uygulama hizmeti etki alanı adları için bkz: [özel DNS kayıtlarını yönetme](#custom). toomap bir dış satın alınan etki alanı tooa web uygulaması bkz [bir var olan özel DNS adı tooAzure Web Apps eşleme](app-service-web-tutorial-custom-domain.md). 
- Aynı abonelik: aşağıdaki adımları kullanın hello.

### <a name="launch-add-hostname"></a>Başlatma ana bilgisayar adı ekleyin
Merhaba, **uygulama hizmetleri** sayfası, web uygulamanızın tooassign konak seçmek için istediğiniz select hello adı **ayarları**ve ardından **özel etki alanları**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Satın alınan etki alanınızın hello listelendiğinden emin olun **uygulama hizmet alanları** bölümünde, ancak bunu seçmeyin. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Tüm uygulama hizmeti etki alanlarında aynı abonelik hello web uygulamanızın içinde gösterilen hello **özel etki alanları** sayfası. Merhaba web uygulamanızın abonelikte etki alanınızda olan ancak hello web uygulamanızın içinde göremiyorum **özel etki alanları** sayfasında, hello yeniden açmayı deneyin **özel etki alanları** sayfasında veya hello Web sayfasını yenileyin. Ayrıca, ilerleme durumunu veya oluşturma hataları için hello Azure portal hello üstündeki hello bildirim zil kontrol edin.
>
>

Seçin **ana bilgisayar adını eklemek**.

### <a name="configure-hostname"></a>Ana bilgisayar adı yapılandırma
Merhaba, **ana bilgisayar adını eklemek** iletişim kutusunda, uygulama hizmeti etki alanı veya herhangi bir alt etki alanı hello tam olarak nitelenmiş etki alanı adını yazın. Örneğin:

- kontoso.NET
- www.kontoso.NET
- ABC.kontoso.NET

Tamamlandığında, seçin **doğrulama**. Merhaba ana bilgisayar adı kayıt türü sizin için otomatik olarak seçilir.

Seçin **ana bilgisayar adını eklemek**.

Merhaba işlemi tamamlandığında, ana bilgisayar adı atanmış hello yönelik bir başarı bildirimi görürsünüz.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Ana bilgisayar adı Kapat ekleme
Merhaba, **ana bilgisayar adını eklemek** sayfasında, tüm diğer ana bilgisayar adı tooyour web uygulaması, istenen olarak atayın. Tamamlandığında, hello kapatmak **ana bilgisayar adını eklemek** sayfası.

Yeni atanan hello hostname(s), uygulamanızın içinde görmelisiniz **özel etki alanları** sayfası.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Test hello ana bilgisayar adları

Listelenen toohello ana bilgisayar adları hello tarayıcıda gidin. Ekran görüntüsü önceki hello Hello örnekte, too_abc.kontoso.net_ gezinme deneyin.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Özel DNS kayıtlarını yönetme

Azure üzerinde bir uygulama hizmeti etki alanı için DNS kayıtlarını kullanılarak yönetilen [Azure DNS](https://azure.microsoft.com/services/dns/). Ekleyebilir, kaldırabilir, ve DNS kayıtlarını güncelleştirmek, harici olarak satın alınan bir etki alanı için olduğu gibi.

### <a name="open-app-service-domain"></a>Açık uygulama hizmeti etki alanı

Merhaba hello sol menüden Azure portal seçin **daha Hizmetleri** > **uygulama hizmet alanları**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Merhaba etki alanı toomanage seçin. 

### <a name="access-dns-zone"></a>Erişim DNS bölgesi

Merhaba etki alanının soldaki menüde seçin **DNS bölgesi**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Bu eylemin hello açılır [DNS bölgesi](../dns/dns-zones-records.md) Azure DNS App Service etki alanınızda sayfası. Hakkında bilgi için bkz: tooedit DNS kayıtları, [nasıl toomanage DNS bölgelerini Azure portal hello](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>İptal satın alma (delete etki alanı)

Merhaba uygulama hizmeti etki alanı satın aldıktan sonra satın alma işleminiz tam iade için beş gün toocancel sahip. Beş gün sonra hello uygulama hizmeti etki alanı silebilir ancak para iadesi alamazsınız.

### <a name="open-app-service-domain"></a>Açık uygulama hizmeti etki alanı

Merhaba hello sol menüden Azure portal seçin **daha Hizmetleri** > **uygulama hizmet alanları**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Merhaba etki alanı tooyou istediğiniz toocancel seçin veya silebilirsiniz. 

### <a name="delete-hostname-bindings"></a>Konak adı bağlamaları Sil

Merhaba etki alanının soldaki menüde seçin **konak adı bağlamaları**. Tüm Azure hizmetlerinden Hello konak adı bağlamaları burada listelenir.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

Tüm konak adı bağlamaları silinene kadar hello uygulama hizmeti etki alanı silinemiyor.

Her ana bilgisayar adı bağlama seçerek silme **...**   >  **Silmek**. Tüm hello bağlamaları silindikten sonra Seç **kaydetmek**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>İptal veya silme

Merhaba etki alanının soldaki menüde seçin **genel bakış**. 

Merhaba iptal süresi satın hello etki alanında değil dolmuşsa, seçin **iptal satın alma**. Aksi takdirde, gördüğünüz bir **silmek** yerine düğme. para iadesi, select olmadan toodelete hello etki alanına **silmek**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Seçin **Tamam** tooconfirm hello işlemi. Tooproceed istemiyorsanız, hello onay iletişim dışında herhangi bir yere tıklayın.

Merhaba işlemi tamamlandıktan sonra aboneliğiniz yayımlanan ve herkes için kullanılabilir hello etki alanıdır yeniden toopurchase. 
