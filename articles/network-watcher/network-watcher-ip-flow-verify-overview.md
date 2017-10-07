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
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="2c83f-103">Giriş tooIP akış Azure Ağ İzleyicisi doğrulayın</span><span class="sxs-lookup"><span data-stu-id="2c83f-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="2c83f-104">IP akışı, bir paket izin verilen ya da 5-tanımlama bilgilerine dayalı bir sanal makineden tooor reddedildi denetimleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2c83f-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="2c83f-105">Bu bilgiler yönü, protokol, yerel IP, uzak IP, yerel bağlantı noktası ve uzak bağlantı noktası oluşur.</span><span class="sxs-lookup"><span data-stu-id="2c83f-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="2c83f-106">Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello Paket reddedildi hello kuralının hello adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2c83f-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="2c83f-107">Bu özellik, kaynak veya hedef IP seçilebilir durumdayken, yöneticilerin gelen bağlantı sorunları veya toohello bulmanıza yardımcı olur Internet ve veya toohello şirket içi ortamda.</span><span class="sxs-lookup"><span data-stu-id="2c83f-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="2c83f-108">IP akış doğrulayın hedefleyen bir sanal makinenin ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="2c83f-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="2c83f-109">Trafik akışı yapılandırılmış hello ayarları tooor bu ağ arabiriminden göre doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="2c83f-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="2c83f-110">Bu özellik, bir ağ güvenlik grubu kural bir sanal makineden giriş ve çıkış trafiği tooor durumunda engelliyor onaylayan yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="2c83f-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="2c83f-111">Ağ İzleyicisi gereksinimlerini toobe toorun IP akış planladığınız tüm bölgelerde oluşturulan örneği doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2c83f-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="2c83f-112">Ağ İzleyicisi bölgesel bir hizmettir ve yalnızca olması çalıştırılmıştır hello kaynaklara karşı aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="2c83f-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="2c83f-113">Bu hello rota NIC hala döndürülecek hello ile ilişkili olarak IP akış sonuçlarını doğrulama hello etkilemez.</span><span class="sxs-lookup"><span data-stu-id="2c83f-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="2c83f-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c83f-115">Next steps</span></span>

<span data-ttu-id="2c83f-116">Bir paket izin verilen ya da hello Portalı aracılığıyla belirli bir sanal makine için reddedildi makale toolearn aşağıdaki hello ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="2c83f-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="2c83f-117">Trafik akışı IP doğrulayın'yle bir VM'yi hello portal kullanarak izin verilip verilmediğini denetleme</span><span class="sxs-lookup"><span data-stu-id="2c83f-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












