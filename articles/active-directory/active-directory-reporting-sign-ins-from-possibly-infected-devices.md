---
title: "Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri"
description: "Bazı kötü amaçlı yazılım (kötü amaçlı yazılım) çalışmıyor olabilir aygıtlardan yürütülen deneme işareti içeren bir rapor."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="3fa02-103">Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="3fa02-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="3fa02-104">Bu rapor, etkilenen haline gelir ve şimdi bir botnet parçası olan kullanıcıların cihazları tanımlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="3fa02-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="3fa02-105">Kullanıcıların oturum açtığını botnet sunucusu iletişim kurmayan gibi biliyoruz IP adresleri IP adreslerini aralarındaki ilişkileri belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="3fa02-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="3fa02-106">Öneri: Bu rapor, IP adresleri, kullanıcı aygıtları işaretler.</span><span class="sxs-lookup"><span data-stu-id="3fa02-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="3fa02-107">Kullanıcıyla iletişime geçin ve emin olmak için tüm kullanıcı aygıtları tarama öneririz.</span><span class="sxs-lookup"><span data-stu-id="3fa02-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="3fa02-108">Ayrıca bir kullanıcının kişisel cihaz bulaşmış ya da aynı IP adresi kullanıcı tarafından kullanılan, kullanıcının başka birisi etkilenen bir aygıt olduğunu mümkündür.</span><span class="sxs-lookup"><span data-stu-id="3fa02-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="3fa02-109">Adres kötü amaçlı yazılımların yayılmasını kullanma hakkında daha fazla bilgi için bkz: [kötü amaçlı yazılımdan koruma Merkezi](http://go.microsoft.com/fwlink/?linkid=335773).</span><span class="sxs-lookup"><span data-stu-id="3fa02-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

