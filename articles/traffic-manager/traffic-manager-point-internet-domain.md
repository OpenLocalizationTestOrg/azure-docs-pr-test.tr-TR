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
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="0d55a-103">Bir şirketin Internet etki alanı tooan Azure Traffic Manager etki noktası</span><span class="sxs-lookup"><span data-stu-id="0d55a-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="0d55a-104">Traffic Manager profili oluşturduğunuzda, Azure bu profil için otomatik olarak bir DNS adı atar.</span><span class="sxs-lookup"><span data-stu-id="0d55a-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="0d55a-105">DNS bölgenizi adından toouse toohello etki alanı adını Traffic Manager profilinize eşleyen bir CNAME DNS kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d55a-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="0d55a-106">Merhaba trafik yöneticisi etki alanı adı hello bulabilirsiniz **genel** hello trafik Yöneticisi profili hello yapılandırma sayfasında bölümü.</span><span class="sxs-lookup"><span data-stu-id="0d55a-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="0d55a-107">Örneğin, toopoint adı www.contoso.com toohello trafik Yöneticisi DNS adı olan contoso.trafficmanager.NET'e, DNS kaynak kaydını aşağıdaki hello oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="0d55a-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="0d55a-108">Tüm trafik istekleri çok*www.contoso.com* çok yönlendirilmiş*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="0d55a-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d55a-109">İkinci düzey etki alanı gibi işaret edemez *contoso.com*, toohello trafik yöneticisi etki alanı.</span><span class="sxs-lookup"><span data-stu-id="0d55a-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="0d55a-110">DNS protokolü standartları, ikinci düzey etki alanı adları için CNAME kayıtlarına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="0d55a-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d55a-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d55a-111">Next steps</span></span>

* [<span data-ttu-id="0d55a-112">Traffic Manager yönlendirme yöntemleri</span><span class="sxs-lookup"><span data-stu-id="0d55a-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="0d55a-113">Traffic Manager - Bir profili devre dışı bırakma, etkinleştirme veya silme</span><span class="sxs-lookup"><span data-stu-id="0d55a-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="0d55a-114">Traffic Manager - Bir uç noktayı devre dışı bırakma veya etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0d55a-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
