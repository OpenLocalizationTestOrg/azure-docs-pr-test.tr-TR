---
title: "Azure CDN uç aaaPurge | Microsoft Docs"
description: "Tüm toopurge nasıl önbelleğe öğrenin Azure CDN uç noktasından içerik."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Bir Azure CDN uç noktasını temizleme
## <a name="overview"></a>Genel Bakış
Merhaba varlığın yaşam süresi (TTL) süresi doluncaya kadar azure CDN uç düğümleri varlıklar önbelleğe alır.  Bir istemci hello kenar düğümden hello varlık istediğinde hello varlığın TTL dolduktan sonra hello kenar düğümüne hello varlık tooserve hello istemci isteği yeni güncelleştirilmiş bir kopyasını almak ve yenileme hello önbellek depolamak.

varlıklarınızı her güncelleştirin ve bunları yeni URL'ler olarak yayımlamak tooversion Hello en iyi yöntem toomake kullanıcılarınızın her zaman en yeni kopyasını varlıklarınızı hello Al emin olur.  CDN hemen hello sonraki istemci istekleri için yeni varlıklar hello alır.  Bazen toopurge önbelleğe alınmış içeriği tüm kenar düğümlerinden ve tüm tooretrieve yeni güncelleştirilmiş varlıklar zorlamak isteyebilirsiniz.  Bu tooupdates tooyour web uygulaması veya yanlış bilgiler içeren tooquickly güncelleştirme varlıklar olabilir.

> [!TIP]
> Temizleme, hello yalnızca temizler, Not önbelleğe alınmış içeriği hello CDN uç sunucularda.  Proxy sunucuları ve yerel tarayıcı önbellekleri gibi tüm aşağı akış önbellekleri önbelleğe alınmış kopyasını hello dosyasının hala tutabilir.  Önemli tooremember olduğundan bu yaşam süresi bir dosyanın ayarlandığında.  Bir aşağı akış istemci toorequest hello en son sürümünü dosyanızı güncelleştirmeniz her zaman benzersiz bir ad verip tarafından ya da yararlanarak zorlayabilirsiniz [sorgu dizesi önbelleğe alma](cdn-query-string.md).  
> 
> 

Bu öğreticide, bir uç nokta tüm kenar düğümlerinden varlıklar temizleme aracılığıyla açıklanmaktadır.

## <a name="walkthrough"></a>Kılavuz
1. Merhaba, [Azure Portal](https://portal.azure.com), toopurge istediğiniz hello bitiş noktası içeren toohello CDN profili göz atın.
2. Merhaba CDN profili dikey penceresinden hello Temizleme düğmesini tıklatın.
   
    ![CDN profili dikey penceresi](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    Merhaba temizleme dikey pencere açılır.
   
    ![CDN temizleme dikey penceresi](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Dikey penceresinde Hello üzerinde temizlemek, hello URL açılır gelen toopurge istediğiniz hello hizmeti adresi seçin.
   
    ![Form Temizle](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > Merhaba tıklayarak da toohello temizleme dikey alabilirsiniz **Temizleme** hello CDN uç noktası dikey düğmesi.  Bu durumda, hello **URL** alan hello hizmeti adresi bu belirli uç ile önceden doldurulmuş haldedir olacaktır.
   > 
   > 
4. Hangi varlıkları kenar düğümleri hello gelen toopurge istediğiniz seçin.  Tüm varlıklar tooclear isterseniz hello tıklatın **Tümünü Temizle** onay kutusu.  Aksi takdirde, her varlık türü hello yolunu toopurge hello istediğiniz **yolu** metin kutusu. Merhaba yolunda aşağıdaki biçimleri desteklenir.
    1. **Tek URL Temizleme**: temizleme tek varlığı ile veya olmadan hello dosya uzantısı, örneğin, hello tam URL belirterek`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Joker Temizleme**: yıldız işareti (\*) joker karakter olarak kullanılabilir. Tüm klasörleri, alt klasörler ve dosyaları bir uç nokta altında Temizleme `/*` hello yolu veya arkasından hello klasörünü belirterek tüm alt klasörleri ve belirli bir klasör altındaki dosyalar Temizleme `/*`, örn.,`/pictures/*`.  Bu joker temizleme akamai'den Azure CDN tarafından şu anda desteklenmiyor unutmayın. 
    3. **Kök etki alanı Temizleme**: hello endpoint hello yolundaki "/" ile temizleme hello kökü.
   
   > [!TIP]
   > Yollar için temizleme belirtilmeli ve hello şunları sığacak göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx). **Tümünü Temizle** ve **joker Temizleme** tarafından desteklenmeyen **akamai'den Azure CDN** şu anda.
   > > Tek URL temizleme`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Sorgu dizesi`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Joker Temizleme `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Daha fazla **yolu** kutularındaki metin tooallow girdikten sonra görünür toobuild birden çok varlıkların listesi.  Merhaba üç nokta (...) düğmesini tıklatarak varlıklar hello listesinden silebilirsiniz.
   > 
5. Merhaba tıklatın **Temizleme** düğmesi.
   
    ![Düğme Temizle](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Temizleme istekleri almak yaklaşık 2-3 dakika tooprocess ile **verizon'dan Azure CDN** (standart ve Premium) ve yaklaşık 7 dakika ile **akamai'den Azure CDN**.  Azure CDN 50 eş zamanlı istekleri herhangi bir anda temizleme bir sınıra sahiptir. 
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure CDN uç noktasında varlıkları önceden yükleme](cdn-preload-endpoint.md)
* [Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme](https://msdn.microsoft.com/library/mt634451.aspx)

