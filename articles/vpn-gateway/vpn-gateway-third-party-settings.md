---
title: "Topluluk önerilen üçüncü taraf VPN veya güvenlik duvarı için cihaz ayarları Azure VPN ağ geçidi | Microsoft Docs"
description: "Topluluk önerilen üçüncü taraf VPN veya güvenlik duvarı için cihaz ayarları Azure VPN ağ geçidi hakkında bilgi edinin."
services: vpn-gateway
documentationcenter: 
author: chadmath
manager: cshepard
editor: 
tags: azure-vpn-gateway
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: delhan
ms.openlocfilehash: 79df187c9093eb01f18b3dfdc25d1d19a2f63c62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="community-suggested-third-party-vpn-or-firewall-device-settings-for-azure-vpn-gateway"></a><span data-ttu-id="a448b-103">Topluluk önerilen üçüncü taraf VPN veya güvenlik duvarı için cihaz ayarları Azure VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="a448b-103">Community-suggested third-party VPN or firewall device settings for Azure VPN gateway</span></span>

<span data-ttu-id="a448b-104">Bu makalede, üçüncü taraf VPN veya Azure VPN ağ geçidi ile kullanılan güvenlik duvarı aygıtları için birkaç önerilen çözümler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a448b-104">This article provides several suggested solutions for third-party VPN or firewall devices that are used with Azure VPN gateway.</span></span>

> [!Note]
> <span data-ttu-id="a448b-105">Üçüncü taraf VPN veya güvenlik duvarı aygıtları için teknik destek aygıt satıcısı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a448b-105">Technical support for third-party VPN or firewall devices is provided by the device vendor.</span></span> 

## <a name="more-information"></a><span data-ttu-id="a448b-106">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a448b-106">More information</span></span>

<span data-ttu-id="a448b-107">Aşağıdaki tabloda birçok yaygın aygıtları ve ilgili Yardım listeler:</span><span class="sxs-lookup"><span data-stu-id="a448b-107">The following table lists several common devices and related help:</span></span>

|<span data-ttu-id="a448b-108">Ürün</span><span class="sxs-lookup"><span data-stu-id="a448b-108">Product</span></span>    |<span data-ttu-id="a448b-109">Başvuru</span><span class="sxs-lookup"><span data-stu-id="a448b-109">Reference</span></span>                                                |
|-----------|-----------------------------------------------------------|
|<span data-ttu-id="a448b-110">Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="a448b-110">Cisco ASA</span></span>  |[<span data-ttu-id="a448b-111">Cisco ASA Azure VPN üzerinde için çözümleri topluluk önerilen</span><span class="sxs-lookup"><span data-stu-id="a448b-111">Community suggested solutions for Cisco ASA on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ASA&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="a448b-112">Cisco ISR</span><span class="sxs-lookup"><span data-stu-id="a448b-112">Cisco ISR</span></span>  |[<span data-ttu-id="a448b-113">Topluluk çözümleri Azure VPN üzerinde Cisco ISR için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-113">Community suggested solutions for Cisco ISR on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ISR&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="a448b-114">Cisco ASR</span><span class="sxs-lookup"><span data-stu-id="a448b-114">Cisco ASR</span></span>  |[<span data-ttu-id="a448b-115">Topluluk çözümleri Azure VPN üzerinde Cisco ASR için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-115">Community suggested solutions for Cisco ASR on Azure VPN</span></span>](https://search.cisco.com/search?query=%22Azure%20VPN%22%20ASR&locale=enUS&tab=Cisco)   |
|<span data-ttu-id="a448b-116">SonicWALL</span><span class="sxs-lookup"><span data-stu-id="a448b-116">Sonicwall</span></span> |<span data-ttu-id="a448b-117">Arama **Azure VPN** üzerinde [Sonicwall site](https://support.sonicwall.com/search)</span><span class="sxs-lookup"><span data-stu-id="a448b-117">Search for **Azure VPN** on [Sonicwall site](https://support.sonicwall.com/search)</span></span> |
| <span data-ttu-id="a448b-118">Denetim noktası</span><span class="sxs-lookup"><span data-stu-id="a448b-118">Checkpoint</span></span>    |<span data-ttu-id="a448b-119">Arama **Azure VPN** üzerinde [denetim noktası sitesi](https://supportcenter.checkpoint.com/supportcenter/portal)</span><span class="sxs-lookup"><span data-stu-id="a448b-119">Search for **Azure VPN** on [Checkpoint site](https://supportcenter.checkpoint.com/supportcenter/portal)</span></span> |
|<span data-ttu-id="a448b-120">Juniper</span><span class="sxs-lookup"><span data-stu-id="a448b-120">Juniper</span></span> |<span data-ttu-id="a448b-121">Arama **Azure VPN** üzerinde [Juniper site]( http://www.juniper.net/search/public/)</span><span class="sxs-lookup"><span data-stu-id="a448b-121">Search for **Azure VPN** on [Juniper site]( http://www.juniper.net/search/public/)</span></span>|
|<span data-ttu-id="a448b-122">Barracuda</span><span class="sxs-lookup"><span data-stu-id="a448b-122">Barracuda</span></span>  |[<span data-ttu-id="a448b-123">Topluluk çözümleri Azure VPN üzerinde Barracuda için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-123">Community suggested solutions for Barracuda on Azure VPN</span></span>](https://campus.barracuda.com/search/?q=%22Azure+VPN%22&x=0&y=0)   |
|<span data-ttu-id="a448b-124">F5</span><span class="sxs-lookup"><span data-stu-id="a448b-124">F5</span></span>         |[<span data-ttu-id="a448b-125">Topluluk çözümleri Azure VPN üzerinde F5 için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-125">Community suggested solutions for F5 on Azure VPN</span></span>](https://support.f5.com/csp/#/federated-search?q=%22Azure%20VPN%22&source=support)          |
|<span data-ttu-id="a448b-126">Palo</span><span class="sxs-lookup"><span data-stu-id="a448b-126">Palo</span></span>       |[<span data-ttu-id="a448b-127">Topluluk çözümleri Azure VPN üzerinde Palo için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-127">Community suggested solutions for Palo on Azure VPN</span></span>](https://live.paloaltonetworks.com/t5/forums/searchpage/tab/message?q=Azure+VPN)        |
|<span data-ttu-id="a448b-128">Watchguard</span><span class="sxs-lookup"><span data-stu-id="a448b-128">Watchguard</span></span> |[<span data-ttu-id="a448b-129">Topluluk çözümleri Azure VPN yükleyeceğiniz için önerilen.</span><span class="sxs-lookup"><span data-stu-id="a448b-129">Community suggested solutions for Watchguard on Azure VPN</span></span>](http://watchguardsupport.force.com/SupportSearch#q=Azure%20VPN&t=All&sort=relevancy)  |

## <a name="next-step"></a><span data-ttu-id="a448b-130">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a448b-130">Next step</span></span>

[<span data-ttu-id="a448b-131">Azure ağ geçitleri ayarları</span><span class="sxs-lookup"><span data-stu-id="a448b-131">Azure Gateways settings</span></span>](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#a-nameipsecaipsecike-parameters)

[<span data-ttu-id="a448b-132">Bilinen uyumlu cihazlar</span><span class="sxs-lookup"><span data-stu-id="a448b-132">Known compatible devices</span></span>](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#validated-vpn-devices)

