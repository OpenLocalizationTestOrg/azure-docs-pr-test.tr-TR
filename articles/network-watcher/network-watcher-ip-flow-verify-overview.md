---
title: "IP akış giriş doğrulayın Azure Ağ İzleyicisi | Microsoft Docs"
description: "Bu sayfada bir genel bakış sunulmaktadır Ağ İzleyicisi IP'si akış özelliği doğrulayın"
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
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="1ee59-103">IP akış giriş Azure Ağ İzleyicisi doğrulayın</span><span class="sxs-lookup"><span data-stu-id="1ee59-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="1ee59-104">IP akışı, bir paket izin verilen veya için veya 5-tanımlama bilgilerine dayalı bir sanal makineden reddedildi denetimleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1ee59-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="1ee59-105">Bu bilgiler yönü, protokol, yerel IP, uzak IP, yerel bağlantı noktası ve uzak bağlantı noktası oluşur.</span><span class="sxs-lookup"><span data-stu-id="1ee59-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="1ee59-106">Paket bir güvenlik grubu tarafından engellenirse Paket reddedildi kuralının adı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1ee59-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="1ee59-107">Kaynak veya hedef IP seçilebilir olsa da, bu özellik hızla gelen veya Internet ve gelen veya şirket içi ortamına bağlantı sorunları tanılamak yöneticilerin yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1ee59-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="1ee59-108">IP akış doğrulayın hedefleyen bir sanal makinenin ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="1ee59-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="1ee59-109">Trafik akışı için ya da bu ağ arabirimini yapılandırılan ayarlara göre doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="1ee59-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="1ee59-110">Bu özellik, bir ağ güvenlik grubu kural giriş ve çıkış trafiği için veya bir sanal makineden durumunda engelliyor onaylayan yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1ee59-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="1ee59-111">Ağ İzleyicisi IP akış çalıştırmayı planladığınız tüm bölgelerde oluşturulması gerekiyor örneği doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1ee59-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="1ee59-112">Ağ İzleyicisi bölgesel bir hizmettir ve yalnızca olması çalıştırılmıştır aynı bölgede kaynaklara karşı.</span><span class="sxs-lookup"><span data-stu-id="1ee59-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="1ee59-113">Bu mu NIC ile ilişkili yol hala döndürülen IP akış sonuçlarını doğrulamak etkiler.</span><span class="sxs-lookup"><span data-stu-id="1ee59-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="1ee59-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ee59-115">Next steps</span></span>

<span data-ttu-id="1ee59-116">Bir paket izin verilen veya portal aracılığıyla belirli bir sanal makine için reddedildi, yapacağınızı öğrenmek için aşağıdaki makaleyi ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="1ee59-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="1ee59-117">Trafik akışı IP doğrulayın'yle bir VM'yi Portalı'nı kullanarak izin verilip verilmediğini denetleme</span><span class="sxs-lookup"><span data-stu-id="1ee59-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












