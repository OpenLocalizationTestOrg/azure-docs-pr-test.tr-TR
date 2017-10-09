---
title: "aaaPoint bir şirketin Internet etki alanı tooa trafik yöneticisi etki alanı adı | Microsoft Docs"
description: "Bu makalede, şirket etki alanı adı tooa trafik yöneticisi etki alanı adı noktası yardımcı olur."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Bir şirketin Internet etki alanı tooan Azure Traffic Manager etki noktası

Traffic Manager profili oluşturduğunuzda, Azure bu profil için otomatik olarak bir DNS adı atar. DNS bölgenizi adından toouse toohello etki alanı adını Traffic Manager profilinize eşleyen bir CNAME DNS kaydı oluşturun. Merhaba trafik yöneticisi etki alanı adı hello bulabilirsiniz **genel** hello trafik Yöneticisi profili hello yapılandırma sayfasında bölümü.

Örneğin, toopoint adı www.contoso.com toohello trafik Yöneticisi DNS adı olan contoso.trafficmanager.NET'e, DNS kaynak kaydını aşağıdaki hello oluşturursunuz:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Tüm trafik istekleri çok*www.contoso.com* çok yönlendirilmiş*contoso.trafficmanager.net*.

> [!IMPORTANT]
> İkinci düzey etki alanı gibi işaret edemez *contoso.com*, toohello trafik yöneticisi etki alanı. DNS protokolü standartları, ikinci düzey etki alanı adları için CNAME kayıtlarına izin vermez.

## <a name="next-steps"></a>Sonraki adımlar

* [Traffic Manager yönlendirme yöntemleri](traffic-manager-routing-methods.md)
* [Traffic Manager - Bir profili devre dışı bırakma, etkinleştirme veya silme](disable-enable-or-delete-a-profile.md)
* [Traffic Manager - Bir uç noktayı devre dışı bırakma veya etkinleştirme](disable-or-enable-an-endpoint.md)
