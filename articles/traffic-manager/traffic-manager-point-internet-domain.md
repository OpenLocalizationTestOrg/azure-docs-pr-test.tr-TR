---
title: "Bir şirketin İnternet etki alanını Traffic Manager etki alanı adına yönlendirme | Microsoft Belgeleri"
description: "Bu makale, şirketinizin etki alanı adını Traffic Manager etki alanı adına yönlendirmenize yardımcı olacaktır."
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
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a>Bir şirketin İnternet etki alanını Azure Traffic Manager etki alanına yönlendirme

Traffic Manager profili oluşturduğunuzda, Azure bu profil için otomatik olarak bir DNS adı atar. DNS bölgenizdeki bir adı kullanmak için Traffic Manager profilinizin etki alanı adıyla eşleşen bir CNAME DNS kaydı oluşturun. Traffic Manager etki alanı adını, Traffic Manager profilinin Yapılandırma sayfasındaki **Genel** bölümünde bulabilirsiniz.

Örneğin, www.contoso.com adını Traffic Manager DNS adı olan contoso.trafficmanager.net'e yönlendirmek için aşağıdaki DNS kaynağı kaydını oluşturmanız gerekir:

    www.contoso.com IN CNAME contoso.trafficmanager.net

*www.contoso.com* adresi için yapılan tüm trafik istekleri *contoso.trafficmanager.net* adresine yönlendirilir.

> [!IMPORTANT]
> *contoso.com* gibi ikinci düzey bir etki alanını Traffic Manager etki alanına yönlendiremezsiniz. DNS protokolü standartları, ikinci düzey etki alanı adları için CNAME kayıtlarına izin vermez.

## <a name="next-steps"></a>Sonraki adımlar

* [Traffic Manager yönlendirme yöntemleri](traffic-manager-routing-methods.md)
* [Traffic Manager - Bir profili devre dışı bırakma, etkinleştirme veya silme](disable-enable-or-delete-a-profile.md)
* [Traffic Manager - Bir uç noktayı devre dışı bırakma veya etkinleştirme](disable-or-enable-an-endpoint.md)
