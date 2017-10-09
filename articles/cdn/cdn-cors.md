---
title: aaaUsing CORS ile Azure CDN | Microsoft Docs
description: "Nasıl toouse hello Azure içerik teslim ağı (CDN) toowith çıkış noktaları arası kaynak paylaşımı (CORS) hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>CORS'yi Azure CDN kullanma
## <a name="what-is-cors"></a>CORS nedir?
CORS (arası kaynak kaynak paylaşımı) altında bir etki alanı tooaccess kaynakları başka bir etki alanında çalışan bir web uygulaması sağlayan bir HTTP özelliğidir. Sipariş tooreduce hello olasılığını siteler arası komut dosyası saldırıları içinde tüm modern web tarayıcıları olarak bilinen bir güvenlik kısıtlama uygulamak [kaynak aynı ilke](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Bu arama API'ları farklı bir etki alanındaki bir web sayfasından önler.  CORS bir güvenli şekilde tooallow bir kaynağı (Merhaba kaynak etki alanı) toocall API'leri başka bir kaynak olarak sağlar.

## <a name="how-it-works"></a>Nasıl çalışır?
CORS isteklerini, iki tür vardır *basit istekleri* ve *karmaşık istekleri.*

### <a name="for-simple-requests"></a>Basit istekleri için:

1. Merhaba tarayıcı gönderir hello CORS istekle ek bir **kaynak** HTTP isteği üstbilgisi. Merhaba Bu üstbilgi değeri hello birleşimi tanımlanan hello üst sayfa sunulan hello kaynak *protokolü,* *etki alanı,* ve *bağlantı noktası.*  Https://www.contoso.com sayfasından hello fabrikam.com kaynak kullanıcının verileri tooaccess çalıştığında, istek üstbilgisi aşağıdaki hello toofabrikam.com gönderilir:

   `Origin: https://www.contoso.com`

2. Merhaba sunucusu aşağıdakilerden herhangi birini hello ile yanıt verebilir:

   * Bir **Access-Control-Allow-Origin** hangi kaynak site izin verilen gösteren yanıt üstbilgisi. Örneğin:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Bir HTTP hata kodu 403 gibi hello sunucu hello çıkış noktaları arası istek hello kaynak üstbilgisi denetledikten sonra izin vermiyorsa

   * Bir **Access-Control-Allow-Origin** tüm kaynaklara izin veren bir joker karakter üstbilgiyle:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Karmaşık istekleri için:

Karmaşık bir istek CORS istek hello tarayıcı gerekli toosend olduğu bir *denetim öncesi isteği* (yani ön bir araştırma) hello fiili CORS isteğini göndermeden önce. Merhaba denetim öncesi isteği hello sunucu izni hello özgün CORS isteğini devam edebilirsiniz ve olup olmadığını soran bir `OPTIONS` toohello isteği aynı URL.

> [!TIP]
> CORS akışları ve ortak Tuzaklar hakkında daha fazla ayrıntı için hello görüntülemek [tooCORS için REST API'leri Kılavuzu](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Joker karakter ya da tek kaynak senaryoları
CORS'yi Azure CDN üzerinde ek bir yapılandırma olmadan hello olduğunda otomatik olarak çalışır **Access-Control-Allow-Origin** toowildcard (*) veya tek bir kaynak üstbilgisi ayarlandı.  Merhaba CDN önbelleğe alınması hello ilk yanıt ve sonraki istekleri hello kullanacağınız aynı üstbilgi.

İstekleri toohello CDN önceki tooCORS üzerinde hello kaynağınıza ayarlanan yapılmışsa, toopurge içerik, uç nokta içerik tooreload hello hello ile içerik ihtiyacınız olacak **Access-Control-Allow-Origin** üstbilgi.

## <a name="multiple-origin-scenarios"></a>Birden çok kaynak senaryoları
Tooallow belirli CORS için izin verilen çıkış noktası toobe listesini gerekiyorsa, biraz daha karmaşık işlerinizi. Merhaba sorun oluşuyor hello CDN hello önbelleğe **Access-Control-Allow-Origin** hello ilk CORS çıkış üstbilgisi.  Farklı bir CORS kaynaktan bir sonraki istekte bulunduğunda hello CDN önbelleğe hello görecek **Access-Control-Allow-Origin** eşleşmeyecektir üstbilgi.  Vardır birkaç yolu toocorrect bu.

### <a name="azure-cdn-premium-from-verizon"></a>Verizon’dan Azure CDN Premium
en iyi şekilde tooenable hello toouse budur **verizon'dan Azure CDN Premium**, gelişmiş işlevselliği, bazı kullanıma sunar. 

Çok gerekir[bir kural oluşturmak](cdn-rules-engine.md) toocheck hello **kaynak** hello isteği üstbilgisi.  Geçerli bir kaynak varsa, kural hello ayarlar **Access-Control-Allow-Origin** üstbilgi hello isteğinde sağlanan hello kaynağına sahip.  Merhaba kaynak hello belirtilmişse **kaynak** üstbilgi izin verilmez, kuralınız hello atlayın **Access-Control-Allow-Origin** hello tarayıcı tooreject hello isteğini neden olacak üstbilgi. 

Vardır iki yolu toodo bu hello kurallar altyapısı ile.  Her iki durumda da hello **Access-Control-Allow-Origin** hello dosyanın kaynak sunucu başlığından tamamen göz ardı, hello CDN'ın kurallar altyapısı tamamen CORS çıkış noktası izin verilen hello yönetir.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Tüm geçerli kaynaklara sahip bir normal ifade
Bu durumda, tüm hello kaynakları içeren bir normal ifade oluşturacaksınız tooallow istiyor: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **Verizon'dan Azure CDN** kullanan [Perl uyumlu normal ifadeler](http://pcre.org/) normal ifadeler için kendi altyapısı olarak bulunabilir.  Gibi bir araç kullanabilirsiniz [normal ifadeler 101](https://regex101.com/) toovalidate, normal ifade.  Merhaba "/" karakterini unutmayın normal ifadelerde geçerli değil ve kaçışlı toobe gerek yoktur, ancak bu karakteri kaçış ve en iyi yöntem olarak kabul edilir bazı regex doğrulayıcıları tarafından beklenen.
> 
> 

Merhaba normal ifadeyle eşleşen, kuralınız hello değiştirir **Access-Control-Allow-Origin** hello isteği gönderen hello kaynağına sahip hello kaynaktan üstbilgi (varsa).  Ek CORS üstbilgilerini gibi ekleyebilirsiniz **erişim-denetim-Allow-Methods**.

![Normal ifade ile kurallar örneği](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Her kaynak için istek üstbilgisi kuralı.
Normal ifadeler yerine, bunun yerine ayrı bir oluşturabileceğiniz hello kullanarak tooallow istediğiniz her kaynak için kural **istek üstbilgisi joker** [eşleşen koşulu](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Hello normal ifade yöntemiyle olarak tek başına kümeleri hello CORS üstbilgilerini hello kurallar altyapısı. 

![Normal ifade olmadan kuralları örneği](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> Merhaba yukarıdaki örnekte, hello joker karakter kullanımı hello * hello kurallar altyapısı toomatch söyler hem HTTP hem de HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Azure CDN standart
Toouse mekanizması tooallow hello joker kaynak hello kullanmadan birden çok kaynaklar için yalnızca Azure CDN standart profilleri hello [sorgu dizesi önbelleğe alma](cdn-query-string.md).  İzin verilen her etki alanı gelen istekleri için bir benzersiz sorgu dizesi kullanın ve tooenable sorgu dizesi ayarı hello CDN uç noktası için gerekir. Bunun yapılması hello her benzersiz sorgu dizesi için ayrı bir nesne önbelleği CDN neden olur. Bu yaklaşım uygun değildir, ancak aynı dosyayı önbelleğe alınmış hello CDN hello birden çok kopyasını neden.  

