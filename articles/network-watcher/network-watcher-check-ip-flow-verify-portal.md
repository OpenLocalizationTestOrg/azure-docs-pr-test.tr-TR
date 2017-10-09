---
title: "Azure Ağ İzleyicisi IP akış ile aaaVerify trafiği doğrulama - Azure portalı | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya reddedilen varsa toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Trafik izin veya tooor VM IP akış doğrulayın ile Azure Ağ İzleyicisi bileşeni reddedildi olmadığını denetleyin

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API'si](network-watcher-check-ip-flow-verify-rest.md)


IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir. Merhaba doğrulama gelen veya giden trafiği için çalıştırılabilir. Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak ya da başka bir kaynak iletişim kurabilirsiniz, geçerli bir durumda olur. IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme. IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu senaryo akış IP doğrulayın tooverify kullanıyorsa bir sanal makine tooanother makine 443 numaralı bağlantı noktası iletişim kurabilirsiniz. Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür. IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Çalışma IP akış doğrulayın

Ağ İzleyicisi tooyour gidin ve tıklayın **IP akış doğrulayın**. Tooverify trafiğinden istediğiniz Hello sanal makine ve ağ arabirimi seçin. Ek filtreleme bilgileri girin ve tıklayın **denetleyin**.

Tıkladığınızda **denetleyin**, sağladığınız hello ölçütlere göre hello akışı denetlenir. Merhaba sonucu olan ya da **izin verilen erişim** veya **erişim reddedildi**. Erişimi reddedilirse, ağ güvenlik grubu (NSG) hello ve trafiği engellemek güvenlik kuralı sağlanır. Trafik Hello reddi beklenen davranıştır, hello kuralı başarılı oldu.

> [!NOTE]
> IP akış doğrulayın gerektirir hello VM kaynak ayrılır.

Görüntü aşağıdaki hello görebileceğiniz gibi hello giden HTTPS trafiğine izin.

![IP akış doğrulayın genel bakış][1]

Görüntü aşağıdaki hello görülen trafiği değiştirilir tooinbound ve hello gelen bağlantı noktası değiştirilen too123. Trafik şimdi engellendi, selamlama iletisine "erişim engellendi" Merhaba trafiği reddetmeye hello ağ güvenlik grubu ve güvenlik kuralı ile birlikte sağlanır.

![IP akış sonuçları][2]

## <a name="next-steps"></a>Sonraki adımlar

Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













