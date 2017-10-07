---
title: "Azure CDN aaaTroubleshooting dosya sıkıştırmasını | Microsoft Docs"
description: "Azure CDN dosya sıkıştırma ile ilgili sorunları giderin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>CDN dosya sıkıştırma sorunlarını giderme
Bu makale ile ilgili sorunları gidermenize yardımcı [CDN dosya sıkıştırma](cdn-improve-performance.md).

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **destek alın**.

## <a name="symptom"></a>Belirti
Uç noktanız için sıkıştırma etkin, ancak dosyalar sıkıştırılmamış döndürülen.

> [!TIP]
> toocheck dosyalarınızı sıkıştırılmış döndürülen olsun, bir aracı gibi toouse gerek [Fiddler](http://www.telerik.com/fiddler) veya tarayıcınızın [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Onay hello HTTP yanıt üstbilgilerini, önbelleğe alınan CDN içerik döndürdü.  Adlı bir üst bilgi olup olmadığını `Content-Encoding` değerini **gzip**, **bzıp2**, veya **deflate**, içeriğinizi sıkıştırılır.
> 
> ![İçerik Kodlama üstbilgisi](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Nedeni
Dahil birkaç olası nedenleri şunlardır:

* Merhaba, içerik sıkıştırma için uygun değil istedi.
* Sıkıştırma hello için etkin değil istenen dosya türü.
* Merhaba HTTP isteği, geçerli sıkıştırma türünü isteyen bir üst bilgisi içermiyordu.

## <a name="troubleshooting-steps"></a>Sorun giderme adımları
> [!TIP]
> Yeni uç nokta dağıtırken olduğu gibi ile bazı zaman toopropagate hello ağ üzerinden CDN yapılandırma değişiklikleri gerçekleştirin.  Genellikle, değişiklikler 90 dakika içinde uygulanır.  Bu hello sıkıştırmayı ayarlama, CDN uç noktası için ayarladığınız ilk kez kullanıyorsanız, 1-2 saat toobe hello sıkıştırma ayarları toohello POP dağıtıldıktan emin bekleyen düşünmelisiniz. 
> 
> 

### <a name="verify-hello-request"></a>Merhaba isteği doğrulayın
İlk olarak, biz hello istek üzerinde bir hızlı sağlamlık denetimi yapmanız gerekir.  Tarayıcınızın kullanabilirsiniz [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello istekleri yapılan.

* Tooyour uç nokta URL'si Hello isteği gönderiliyor doğrulayın `<endpointname>.azureedge.net`ve kaynağınıza değil.
* Merhaba isteği içerdiğini doğrulayın bir **Accept-Encoding** üstbilgi ve hello değer bu üst bilgiyi içeren için **gzip**, **deflate**, veya **bzıp2** .

> [!NOTE]
> **Akamai'den Azure CDN** yalnızca destek profilleri **gzip** kodlama.
> 
> 

![CDN istek üstbilgileri](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Sıkıştırma ayarları (standart CDN profili) doğrulayın
> [!NOTE]
> CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN standart** veya **akamai'den Azure CDN standart** profili. 
> 
> 

Merhaba tooyour uç gidin [Azure portal](https://portal.azure.com) hello tıklatıp **yapılandırma** düğmesi.

* Sıkıştırma etkin doğrulayın.
* Merhaba hello sıkıştırılmış toobe sıkıştırılmış biçimleri hello listesinde yer içerik için MIME türünü doğrulayın.

![CDN sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Sıkıştırma ayarları (Premium CDN profili) doğrulayın
> [!NOTE]
> CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN Premium** profili.
> 
> 

Merhaba tooyour uç gidin [Azure portal](https://portal.azure.com) hello tıklatıp **Yönet** düğmesi.  Merhaba ek portalı açar.  Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.  Tıklatın **sıkıştırma**. 

* Sıkıştırma etkin doğrulayın.
* Merhaba doğrulayın **dosya türlerini** listesini içeren bir virgülle ayrılmış listesi (boşluksuz) MIME türleri.
* Merhaba hello sıkıştırılmış toobe sıkıştırılmış biçimleri hello listesinde yer içerik için MIME türünü doğrulayın.

![CDN premium sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Merhaba içerik önbelleğe doğrulayın
> [!NOTE]
> CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).
> 
> 

Tarayıcınızın Geliştirici Araçları'nı kullanarak hello yanıt üstbilgileri tooensure hello dosyası burada istenmektedir hello bölgede önbelleğe denetleyin.

* Merhaba denetleyin **Server** yanıtı üstbilgisi.  Merhaba üstbilgi hello biçiminde olması gerektiğini **Platform (POP/sunucu kimliği)**hello aşağıdaki örnekte görüldüğü gibi.
* Merhaba denetleyin **X önbellek** yanıtı üstbilgisi.  Merhaba üstbilgi kimler **İSABET**.  

![CDN yanıt üstbilgileri](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Merhaba dosyası başlangıç boyutu gereksinimlerini karşıladığını doğrulayın
> [!NOTE]
> CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).
> 
> 

sıkıştırma için uygun toobe, bir dosya boyutu gereksinimleri aşağıdaki hello karşılaması gerekir:

* 128 bayt daha büyük.
* 1 MB'tan küçük.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Merhaba kaynak sunucu için Hello isteğiyle denetleyin bir **aracılığıyla** üstbilgisi
Merhaba **aracılığıyla** HTTP üstbilgisi gösterir isteği hello toohello web sunucusu bir proxy sunucusu tarafından geçirilen.  Varsayılan olarak Microsoft IIS web sunucuları sıkıştırma yanıtları hello istek içerdiğinde bir **aracılığıyla** üstbilgi.  toooverride Bu davranış hello aşağıdakileri yapın:

* **IIS 6**: [ayarlamak HcNoCompressionForProxies hello IIS metatabanı özelliklerinde = "FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 ve en fazla**: [ayarlanacağı **noCompressionForHttp10** ve **noCompressionForProxies** tooFalse hello sunucu yapılandırması](http://www.iis.net/configreference/system.webserver/httpcompression)

