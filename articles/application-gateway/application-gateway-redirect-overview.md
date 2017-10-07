---
title: "Azure uygulama ağ geçidi için aaaRedirect genel bakış | Microsoft Docs"
description: "Azure uygulama ağ geçidi hello yeniden yönlendirme özelliği hakkında bilgi edinin"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Uygulama ağ geçidi yeniden yönlendirmeye genel bakış

Birçok web uygulamaları için yaygın bir senaryo toosupport otomatik HTTP tooHTTPS yeniden yönlendirme tooensure tüm uygulama ve onun kullanıcıları arasında şifrelenmiş bir yolu üzerinden iletişimin ' dir. Hello geçmişte, müşteriler üzerinde HTTP tooHTTPS aldığı tooredirect istekleri tek amacı olan bir adanmış arka uç havuzu oluşturma gibi teknikler kullandınız.  Uygulama ağ geçidi artık hello uygulama ağ geçidi üzerinde özelliği tooredirect trafiğini destekler. Bu uygulama yapılandırmasını basitleştirir, hello kaynak kullanımı en iyi duruma getirir ve genel ve yol tabanlı yönlendirme dahil olmak üzere yeni yeniden yönlendirme senaryoları destekler. Uygulama ağ geçidi yeniden yönlendirme desteği sınırlı değildir tooHTTP HTTPS yeniden yönlendirmesi tek başına ->. Uygulama ağ geçidi tooanother dinleyicisinde bir dinleyici adresindeki alınan trafik yeniden yönlendirilmesine izin veren bir genel yönlendirme mekanizması budur. Ayrıca, yeniden yönlendirme tooan dış site de destekler. Uygulama ağ geçidi yeniden yönlendirme desteği hello aşağıdaki özellikleri sunmaktadır:

1. Genel Yönlendirme hello ağ geçidi tooanother dinleyicisinde bir dinleyici gelen. Bu, bir sitede HTTP tooHTTPS yönlendirme sağlar.
2. Yol tabanlı yönlendirmesi. Örneğin bir alışveriş sepeti alanı/Sepeti/belirtilen HTTP tooHTTPS yeniden yönlendirme yalnızca belirli site alanına bu tür bir yeniden yönlendirme sağlar *.
3. Yeniden yönlendirme tooexternal sitesi.

![yeniden yönlendirme](./media/application-gateway-redirect-overview/redirect.png)

Bu değişiklik müşteriler toocreate hello hedef dinleyici belirten yeni bir yeniden yönlendirme yapılandırma nesnesi gerekir ya da dış site toowhich yeniden yönlendirme istenen. Merhaba yapılandırma öğesi seçenekleri tooenable hello URI yolu ve sorgu dizesi toohello URL'ye yeniden yönlendirilen ekleyerek de destekler. Müşteriler, yeniden yönlendirme geçici (HTTP durum kodu 302) ya da kalıcı bir yeniden yönlendirme (HTTP durum kodu 301) olup olmadığını da tercih edebilirsiniz. Bu yeniden yönlendirme yapılandırması oluşturulduktan sonra yeni bir kural aracılığıyla ekli toohello kaynak dinleyicisi buradadır. Temel bir kural kullanırken hello yeniden yönlendirme yapılandırma kaynağı dinleyicisi ile ilişkili ve genel bir yeniden yönlendirme. Yol tabanlı bir kural kullanıldığında, hello yeniden yönlendirme yapılandırması hello URL yolu haritada tanımlanır ve bu nedenle toohello belirli yol alanını bir sitenin yalnızca uygulanır.

### <a name="next-steps"></a>Sonraki adımlar

[Bir uygulama ağ geçidinde URL yeniden yönlendirmeyi yapılandırma](application-gateway-configure-redirect-powershell.md)
