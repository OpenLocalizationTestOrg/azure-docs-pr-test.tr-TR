---
title: "aaaIntroduction tooIP akış doğrulayın Azure Ağ İzleyicisi | Microsoft Docs"
description: "Bu sayfada bir genel bakış sunulmaktadır Ağ İzleyicisi IP Merhaba akış özelliği doğrulayın"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Giriş tooIP akış Azure Ağ İzleyicisi doğrulayın

IP akışı, bir paket izin verilen ya da 5-tanımlama bilgilerine dayalı bir sanal makineden tooor reddedildi denetimleri doğrulayın. Bu bilgiler yönü, protokol, yerel IP, uzak IP, yerel bağlantı noktası ve uzak bağlantı noktası oluşur. Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello Paket reddedildi hello kuralının hello adı döndürülür. Bu özellik, kaynak veya hedef IP seçilebilir durumdayken, yöneticilerin gelen bağlantı sorunları veya toohello bulmanıza yardımcı olur Internet ve veya toohello şirket içi ortamda.

IP akış doğrulayın hedefleyen bir sanal makinenin ağ arabirimi. Trafik akışı yapılandırılmış hello ayarları tooor bu ağ arabiriminden göre doğrulanır. Bu özellik, bir ağ güvenlik grubu kural bir sanal makineden giriş ve çıkış trafiği tooor durumunda engelliyor onaylayan yararlıdır.

Ağ İzleyicisi gereksinimlerini toobe toorun IP akış planladığınız tüm bölgelerde oluşturulan örneği doğrulayın. Ağ İzleyicisi bölgesel bir hizmettir ve yalnızca olması çalıştırılmıştır hello kaynaklara karşı aynı bölgede. Bu hello rota NIC hala döndürülecek hello ile ilişkili olarak IP akış sonuçlarını doğrulama hello etkilemez.

![1][1]

## <a name="next-steps"></a>Sonraki adımlar

Bir paket izin verilen ya da hello Portalı aracılığıyla belirli bir sanal makine için reddedildi makale toolearn aşağıdaki hello ziyaret edin. [Trafik akışı IP doğrulayın'yle bir VM'yi hello portal kullanarak izin verilip verilmediğini denetleme](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












