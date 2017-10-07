---
title: "aaaMap Azure CDN içerik tooa özel etki alanı | Microsoft Docs"
description: "Nasıl toomap Azure CDN içerik tooa özel etki alanı öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Harita Azure CDN içerik tooa özel etki alanı
Özel etki alanı tooa CDN uç noktası sipariş toouse içinde URL'leri toocached azureedge.net bir alt etki alanı kullanmak yerine içerik, kendi etki alanı adı eşleyebilirsiniz.

Özel etki alanı tooa CDN uç noktanız iki yolu toomap vardır:

1. [Etki alanı kayıt şirketinizle bir CNAME kaydı oluşturun ve özel etki alanı ve alt etki alanı toohello CDN uç noktanız eşleyin](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Bir CNAME kaydı, bir kaynak etki alanı gibi eşleyen bir DNS özelliğidir `www.contosocdn.com` veya `cdn.contoso.com`, tooa hedef etki alanı. Bu durumda, özel etki alanı ve alt etki alanı hello kaynak etki alanıdır (bir alt etki alanı gibi **www** veya **cdn** her zaman gereklidir). CDN uç noktanız Hello hedef etki alanıdır.  
   
    hello Azure Portal hello etki alanı kaydettirirken özel etki alanı tooyour CDN uç noktanız eşleme hello işlem ancak, kapalı kalma süresi hello etki alanı için kısa bir süre neden olabilir.
2. [Bir ara kayıt adımıyla eklemek **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Özel etki alanınız var olması kapalı kalma süresi gerektiren bir hizmet düzeyi sözleşmesi (SLA) sahip bir uygulama şu anda destekleme sonra hello Azure kullanabilirsiniz **cdnverify** alt etki alanı tooprovide bir ara kaydı Adım kullanıcılar mümkün tooaccess sırasında etki alanınızın olması gerçekleşmesi eşleme DNS hello.  

Yukarıdaki yordamları hello birini kullanarak özel etki alanınızı kaydettikten sonra çok isteyeceksiniz[bu hello özel alt etki alanı başvuran CDN uç noktanız doğrulayın](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Etki alanı toohello CDN uç noktanız, etki alanı kayıt şirketi toomap ile bir CNAME kaydı oluşturmanız gerekir. CNAME kayıtları eşleme belirli bir alt etki alanları gibi `www.contoso.com` veya `cdn.contoso.com`. Bu olası toomap bir CNAME kaydı tooa kök etki alanı gibi değil `contoso.com`.
> 
> Bir alt etki alanı yalnızca bir CDN uç noktasıyla ilişkili olabilir. Merhaba, oluşturduğunuz CNAME kaydı tüm trafiği yönlendirmek toohello alt etki alanı toohello belirtilen bitiş noktası.  Örneğin, ilişkilendirirseniz `www.contoso.com` , CDN uç noktasıyla sonra onu bir depolama hesabı uç noktası veya bir bulut Hizmeti uç noktası gibi diğer Azure uç noktaları ile ilişkilendiremezsiniz. Ancak, farklı alt etki alanından hello kullanabilirsiniz farklı hizmet uç noktaları için aynı etki alanı. Ayrıca farklı bir alt etki alanları toohello eşleştirebilirsiniz aynı CDN uç noktası.
> 
> İçin **verizon'dan Azure CDN** (standart ve Premium) uç noktaları, Not çok kapladığı olduğunu**90 dakika** toopropagate tooCDN kenar düğümleri özel etki alanı değişiklikleri için.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Bir Azure CDN uç noktası için özel bir etki alanı kaydetme
1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).
2. Tıklatın **Gözat**, ardından **CDN profili**, CDN profili hello hello noktayla istediğiniz toomap tooa özel etki alanı.  
3. Merhaba, **CDN profili** dikey penceresinde hello CDN uç noktası tooassociate hello alt etki alanı ile istediğiniz'ı tıklatın.
4. Merhaba hello uç nokta dikey penceresinde Hello üstünde tıklatın **özel etki alanı Ekle** düğmesi.  Merhaba, **özel bir etki alanı ekleme** dikey penceresinde hello uç noktası ana bilgisayar adı, CDN uç noktanız, yeni bir CNAME kaydı oluşturma toouse türetilmiş göreceksiniz. Merhaba ana bilgisayar adı adresinin Hello biçimi olarak görünür  **&lt;EndpointName >. azureedge.net**.  Bu ana bilgisayar adı toouse hello CNAME kaydı oluşturmada kopyalayabilirsiniz.  
5. Tooyour etki alanı kayıt şirketinizin web sitesine gidin ve DNS kayıtları oluşturmak için hello bölümünü bulun. Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.
6. Merhaba bölümü CNAME'ler yönetmek için bulunamıyor. CNAME, diğer ad veya alt etki alanları hello sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz.
7. Seçilen alt eşleşen yeni bir CNAME kaydı oluşturun (örneğin, **www** veya **cdn**) hello sağlanan toohello ana bilgisayar adı **özel bir etki alanı ekleme** dikey. 
8. Toohello iade **özel bir etki alanı ekleme** dikey penceresinde ve hello alt etki alanı, hello iletişim kutusunda dahil olmak üzere, özel etki alanı adı girin. Örneğin, hello biçiminde hello etki alanı adı girin `www.contoso.com` veya `cdn.contoso.com`.   
   
   Azure hello CNAME kaydı girdiğiniz hello etki alanı adı için mevcut doğrular. Merhaba CNAME doğru ise, özel etki alanınız doğrulandı.  İçin **verizon'dan Azure CDN** (standart ve Premium) uç noktaları, sürebilir özel etki alanı ayarları toopropagate tooall CDN kenar düğümü, too90 dakika yukarı ancak.  
   
   Bu durumlarda, bazı Not hello Internet üzerinde hello CNAME kaydı toopropagate tooname sunucuları için zaman alabilir. Etki alanınızı hemen doğrulanmaz ve hello CNAME kaydı doğru olduğunu düşünüyorsanız, birkaç dakika bekleyin ve yeniden deneyin.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Merhaba Ara cdnverify alt etki alanı kullanarak bir Azure CDN uç noktası için özel bir etki alanı kaydetme
1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).
2. Tıklatın **Gözat**, ardından **CDN profili**, CDN profili hello hello noktayla istediğiniz toomap tooa özel etki alanı.  
3. Merhaba, **CDN profili** dikey penceresinde hello CDN uç noktası tooassociate hello alt etki alanı ile istediğiniz'ı tıklatın.
4. Merhaba hello uç nokta dikey penceresinde Hello üstünde tıklatın **özel etki alanı Ekle** düğmesi.  Merhaba, **özel bir etki alanı ekleme** dikey penceresinde hello uç noktası ana bilgisayar adı, CDN uç noktanız, yeni bir CNAME kaydı oluşturma toouse türetilmiş göreceksiniz. Merhaba ana bilgisayar adı adresinin Hello biçimi olarak görünür  **&lt;EndpointName >. azureedge.net**.  Bu ana bilgisayar adı toouse hello CNAME kaydı oluşturmada kopyalayabilirsiniz.
5. Tooyour etki alanı kayıt şirketinizin web sitesine gidin ve DNS kayıtları oluşturmak için hello bölümünü bulun. Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.
6. Merhaba bölümü CNAME'ler yönetmek için bulunamıyor. Merhaba sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz **CNAME**, **diğer**, veya **alt etki alanları**.
7. Yeni bir CNAME kaydı oluşturun ve hello içeren bir alt etki alanı diğer adı sağlayın **cdnverify** alt etki alanı. Örneğin, belirttiğiniz hello alt hello biçimde olacaktır **cdnverify.www** veya **cdnverify.cdn**. Merhaba biçiminde, CDN uç noktası hello ana bilgisayar adı sağlayın **cdnverify.&lt; EndpointName >. azureedge.net**. DNS eşleştirme gibi görünmelidir:`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Toohello iade **özel bir etki alanı ekleme** dikey penceresinde ve hello alt etki alanı, hello iletişim kutusunda dahil olmak üzere, özel etki alanı adı girin. Örneğin, hello biçiminde hello etki alanı adı girin `www.contoso.com` veya `cdn.contoso.com`. Bu adımda, toopreface hello alt etki alanı ile gerekmediği Not **cdnverify**.  
   
    Azure hello CNAME kaydı için hello cdnverify etki alanı adı girdiğiniz var olduğunu doğrular.
9. Bu noktada, özel etki alanınızı Azure tarafından doğrulandı, ancak trafik tooyour etki alanı yönlendirilmiş tooyour CDN uç noktası henüz alınmıyor. Yeterince uzun tooallow hello özel etki alanı ayarları toopropagate bekledikten sonra toohello CDN kenar düğümleri (90 dakika **verizon'dan Azure CDN**, 1-2 dakika **akamai'den Azure CDN**), tooyour DNS Döndür Kayıt şirketinizin web sitesi ve alt etki alanı tooyour CDN uç noktanız eşlemeleri başka bir CNAME kaydı oluşturun. Örneğin, hello alt etki alanı olarak belirtmeniz **www** veya **cdn**, ve ana bilgisayar adı olarak hello  **&lt;EndpointName >. azureedge.net**. Bu adımda, özel etki alanınızı hello kaydı tamamlanır.
10. Son olarak, hello CNAME kaydı kullanılarak oluşturulan silebilirsiniz **cdnverify**, yalnızca bir ara adım olarak gerekli olduğu gibi.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>CDN uç noktanız bu hello özel alt etki alanı başvuran doğrulayın
* Özel etki alanınızı hello kaydı tamamladıktan sonra hello özel etki alanını kullanan CDN uç noktanız önbelleğe alınmış içeriğe erişebilir.
  İlk olarak, hello uç noktada önbelleğe alınan bir ortak içeriğe olduğundan emin olun. Örneğin, CDN uç noktanız bir depolama hesabı ile ilişkili ise, hello CDN ortak blob kapsayıcıları içeriği önbelleğe alır. tootest hello özel etki alanı, kapsayıcı tooallow genel erişim ayarlanır ve en az bir blob içerdiğinden emin olun.
* Tarayıcınızda, hello özel etki alanını kullanan hello blob toohello adresini gidin. Örneğin, özel etki alanınız varsa `cdn.contoso.com`, hello URL tooa önbelleğe alınmış blobu benzer toohello URL aşağıdaki gibi: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Ayrıca Bkz.
[Nasıl tooEnable hello Azure içerik teslim ağı (CDN)](cdn-create-new-endpoint.md)  

