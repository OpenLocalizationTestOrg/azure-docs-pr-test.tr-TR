---
title: "aaaAzure DNS temsilci genel bakış | Microsoft Docs"
description: "Nasıl toochange etki alanı temsilcisi kullanımı Azure DNS etki alanı tooprovide barındıran sunucu adı ve anlayın."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Azure DNS ile DNS bölgelerinin temsilciliği

Azure DNS toohost bir DNS bölgesi sağlar ve azure'de bir etki alanı için DNS kayıtlarını hello yönetin. Bir etki alanı tooreach Azure DNS için DNS sorgularını sırayla hello etki alanı toobe sahip hello üst etki alanından tooAzure DNS temsilcisi. Azure DNS unutmayın hello etki alanı kayıt değil. Bu makalede nasıl etki alanı temsilcisi çalışır ve nasıl açıklanmaktadır toodelegate etki alanları tooAzure DNS.

## <a name="how-dns-delegation-works"></a>DNS temsilcisi seçme nasıl çalışır?

### <a name="domains-and-zones"></a>Etki alanları ve bölgeler

Merhaba etki alanı adı sistemi, etki alanları hiyerarşisidir. Merhaba hiyerarşi adı olan basitçe hello 'kök' etki alanından başlar '**.**'.  Bunun altında "com", "net", "org", "uk" veya "jp" gibi en üst düzey etki alanları bulunur.  Bu üst düzey etki alanlarının altında ‘org.uk’ veya ‘co.jp’ gibi ikinci düzey etki alanları bulunur.  Etki alanları bu hiyerarşi sıralamasıyla devam eder. Merhaba DNS hiyerarşi Hello etki alanlarında, ayrı DNS bölgeleri kullanılarak barındırılır. Bu bölgeler Global, Merhaba dünya genelindeki DNS ad sunucuları tarafından barındırılan dağıtılır.

**DNS bölgesi** -bir etki alanında benzersiz bir etki alanı adı sistemi, örneğin "contoso.com" Merhaba addır. Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Örneğin, hello etki alanı "contoso.com", "mail.contoso.com" (bir posta sunucusu için) ve 'www.contoso.com' (bir Web sitesi) gibi birçok DNS kayıtlarını içerebilir.

**Etki alanı kayıt şirketi** - Etki alanı kayıt şirketi, İnternet etki alanı adlarını sağlayabilen bir şirkettir. Merhaba Internet etki alanını istiyorsanız toouse kullanılabilir ve toopurchase izin doğrulayın. Merhaba etki alanı adı kaydedildiğinde, hello etki alanı adı için hello yasal sahibi olursunuz. Zaten bir Internet etki alanınız varsa, hello geçerli etki alanı kayıt şirketi toodelegate tooAzure DNS kullanır.

bir etki alanı adının Kime veya hakkında bilgi için daha fazla bilgiyi toofind toobuy bir etki alanı bkz [Azure AD'de Internet etki alanı yönetimi](https://msdn.microsoft.com/library/azure/hh969248.aspx).

### <a name="resolution-and-delegation"></a>Çözümleme ve temsilci seçme

İki tür DNS sunucusu bulunur:

* *Yetkili* DNS sunucusu DNS bölgelerini barındırır. Bu sunucu, yalnızca bu bölgelerdeki kayıtlar için DNS sorgularını yanıtlar.
* *Özyinelemeli* DNS sunucusu DNS bölgelerini barındırmaz. Tüm DNS sorgularını gereksinim duyduğu yetkili DNS sunucularının toogather hello veri çağırarak yanıtlar.

Azure DNS, bir yetkili DNS hizmeti sağlar.  Bir özyinelemeli DNS hizmeti sağlamaz. Bulut Hizmetleri ve VM'ler için Azure'da otomatik olarak yapılandırılan toouse ayrıca Azure'nın alt yapısının bir parçası sağlanan bir yinelemeli DNS hizmeti markalarıdır. Toochange şu DNS ayarlarını nasıl görürüm hakkında bilgi için [Azure ad çözümleme](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

Bilgisayarlar veya mobil cihazlarda bulunan DNS istemcileri, yinelemeli DNS sunucusu tooperform hello istemci uygulamaları için gereken tüm DNS sorguları genellikle çağırın.

Yinelemeli bir DNS sunucusu "www.contoso.com" gibi bir DNS kaydı için bir sorgu aldığında, hello "contoso.com" etki alanı için ilk toofind hello adı sunucu barındırma hello bölgesi gerekir. toofind hello ad sunucusu, onu hello kök adı sunucularından başlar ve buradan hello "com" bölgesini barındıran hello ad sunucularını bulur. Ardından, hello "com" ad sunucuları toofind hello ad sunucuları hello "contoso.com" bölgesini barındıran sorgular.  Son olarak, bu ad sunucuları için mümkün tooquery olduğundan 'www.contoso.com'.

Bu yordamı hello DNS adını çözümleme olarak adlandırılır. NET olarak söylemek DNS çözümlemesi Cname'leri izleme gibi ek adımları içerir ancak DNS temsilcisi seçme nasıl çalışır önemli toounderstanding değil.

Nasıl bir üst bölge 'toohello ad sunucuları bir alt bölgenin işaret eder"? Bunu, NS kaydı olarak adlandırılan (NS "ad sunucusu" anlamına gelir) özel bir DNS kaydı türünü kullanarak yapar. Örneğin, hello kök bölgesi "com" için NS kayıtları içerir ve hello hello "com" bölgesi için ad sunucularını gösterir. Buna karşılık, hello "com" bölgesi hello hello "contoso.com" bölgesi için ad sunucularını gösteren "contoso.com" için NS kayıtları içerir. Bir üst bölge içindeki bir alt bölgenin hello NS kayıtlarını ayarlama temsilci hello etki alanı adı verilir.

Görüntü aşağıdaki hello örnek bir DNS sorgu gösterir. Merhaba contoso.net ve partners.contoso.net Azure DNS bölgeleri ' dir.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. Merhaba istemci isteklerini `www.partners.contoso.net` kendi yerel DNS sunucusundan.
1. bir istek tootheir kök ad sunucusu yapar şekilde hello yerel DNS sunucusu hello kaydı yok.
1. Merhaba kök ad sunucusu hello kaydının yok ancak hello hello adresini bilir `.net` ad sunucusu, bu adres toohello DNS sunucusu sağlar
1. Merhaba DNS gönderir hello isteği toohello `.net` ad sunucusu onu yok ancak hello contoso.net ad sunucusu hello adresini bildiğinizden hello kaydı. Bu durumda, Azure DNS’de barındırılan bir DNS bölgesidir.
1. Merhaba bölge `contoso.net` hello kaydının yok ancak hello ad sunucusu için bilir `partners.contoso.net` ve ile yanıt verir. Bu durumda, Azure DNS’de barındırılan bir DNS bölgesidir.
1. Merhaba DNS sunucusu ister hello IP adresini `partners.contoso.net` hello gelen `partners.contoso.net` bölgesi. Merhaba A kaydı içerir ve hello IP adresiyle yanıt verir.
1. Başlangıç IP adresi toohello istemci Hello DNS sunucusu sağlar
1. Merhaba istemci toohello Web sitesine bağlanır `www.partners.contoso.net`.

Her temsilci seçimi aslında hello NS kayıtlarının iki kopyasını sahiptir; bir hello üst bölgedeki toohello alt ve hello alt bölgenin kendisi de başka bir işaret ediyor. Merhaba 'contoso.net' bölge 'contoso.net' hello NS kayıtlarını (toplama toohello NS kayıtlarında 'net') içerir. Bu kayıtları yetkili NS kayıtları olarak adlandırılır ve hello hello alt bölgenin tepesinde sit.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok bilgi[, etki alanı tooAzure DNS temsilci seçme](dns-delegate-domain-azure-dns.md)

