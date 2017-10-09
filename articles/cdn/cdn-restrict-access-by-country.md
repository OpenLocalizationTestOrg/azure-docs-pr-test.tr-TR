---
title: "Azure CDN içeriğini ülkeye göre aaaRestrict | Microsoft Docs"
description: "Nasıl toorestrict tooyour Azure CDN içerik kullanarak erişimini izin ver hello coğrafi filtreleme özelliği hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Azure CDN içeriğini ülkeye göre kısıtla

## <a name="overview"></a>Genel Bakış
Kullanıcı varsayılan olarak, içerik istediğinde, hello içerik hello kullanıcı bu istekten burada yapılan bağımsız olarak sunulur. Bazı durumlarda, toorestrict erişim tooyour içerik ülkeye göre isteyebilirsiniz. Bu konuda açıklanmaktadır nasıl toouse hello **coğrafi filtreleme** sipariş tooconfigure hello hizmeti tooallow veya blok erişimini ülkeye göre özelliği.

> [!IMPORTANT]
> Merhaba Verizon ve Akamai ürünleri sağlamak hello aynı coğrafi filtreleme işlevselliği ancak destekledikleri arı ülke kodlarına küçük bir fark vardır. Adım 3'için bir bağlantı toohello farkları bakın.


Kısıtlama, bu tür tooconfiguring dikkat edilecek noktalar hakkında bilgi için hello bkz [konuları](cdn-restrict-access-by-country.md#considerations) hello konu hello sonunda bölüm.  

![Ülke filtreleme](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>1. adım: hello dizin yolu tanımlama
Uç noktanız hello portalındaki seçin ve bu özellik hello coğrafi filtreleme sekmesinde hello sol gezinti toofind bulun.

Bir ülke filtresi yapılandırırken hello göreli yol toohello konumu toowhich kullanıcılar izin verilen veya erişimi reddedilen belirtmeniz gerekir. Tüm dosyaları ile coğrafi filtreleme uygulayabilirsiniz "/" veya seçili klasörler dizin yolu "/ resimler /" belirterek. Ayrıca coğrafi filtreleme tooa tek dosyalı hello dosya belirterek uygulayabilirsiniz ve bırakarak hello eğik "/ resimler/şehir.PNG silebilir".

Örnek dizin yolu Filtresi:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>2. adım: hello eylem tanımlama: Engelle veya izin ver
**Engelle:** hello kullanıcılardan belirtilen ülkeler bu özyinelemeli yolundan istenen erişim tooassets izni verilmez. Bu konumda hiçbir diğer ülke filtreleme seçenekleri yapılandırıldıysa diğer tüm kullanıcıların erişim verilmez.

**İzin ver:** hello kullanıcılardan yalnızca belirtilen ülkeler bu özyinelemeli yolundan istenen erişim tooassets izin verilir.

## <a name="step-3-define-hello-countries"></a>3. adım: hello ülkelerde tanımlama
Tooblock istediğiniz veya hello yolu için izin hello ülke seçin. 

Örneğin, /Photos/Strasbourg/engelleme hello kural dosyaları dahil süzer:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Ülke kodu
Merhaba **coğrafi filtreleme** özelliği için güvenli bir dizin, bir istek izin verilen ya da engellenen ülke kodları toodefine hello ülkelerde kullanır. Ülke kodu hello bulacaksınız [Azure CDN ülke kodlarına](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Dikkat edilecek noktalar
* Verizon too90 dakika veya değişiklikleri tooyour ülke filtreleme yapılandırması tootake etkisi Akamai ile birkaç dakika sürebilir.
* Bu özellik joker karakterleri desteklemez (örneğin, ' *').
* Merhaba göreli yol ile ilişkili hello coğrafi filtreleme yapılandırması uygulanan yinelemeli olarak toothat yol olacaktır.
* Yalnızca bir kural uygulanan toohello olabilir aynı göreli yol (Bu noktası toohello birden fazla ülke filtre oluşturulamıyor aynı göreli yolu. Bununla birlikte, bir klasör birden fazla ülke filtre olabilir. Ülke filtreleri toohello özyinelemeli yapısı budur. Diğer bir deyişle, önceden yapılandırılmış bir klasörün bir alt farklı ülke filtre atanabilir.

