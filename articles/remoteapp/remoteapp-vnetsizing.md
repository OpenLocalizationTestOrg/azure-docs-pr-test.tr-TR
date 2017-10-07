---
title: "Azure remoteapp'te bir VNET için aaaSizing bilgi | Microsoft Docs"
description: "Bir VNET ile birlikte çalışan Azure RemoteApp için başlangıç IP adresi gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="10f5a-103">Boyutlandırma bilgileri Azure remoteapp'te bir VNET için</span><span class="sxs-lookup"><span data-stu-id="10f5a-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="10f5a-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="10f5a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="10f5a-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="10f5a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="10f5a-106">Bir sanal ağ (VNET) ile Azure RemoteApp kullandığınızda, RemoteApp hello alt ağ içindeki IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="10f5a-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="10f5a-107">RemoteApp hizmetinizi Hello ölçeğini bağlı olarak, alt ağınızı RemoteApp sanal makineler için kullanılabilir yeterli IP adresine sahip tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="10f5a-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="10f5a-108">Bu boyutlandırma kılavuzluğu nasıl RemoteApp dinamik olarak yukarı döner ve sanal makineleri bir koleksiyon içinde aşağı döner verilen kusursuz olmasa da, alt ağ aralığınızı tahmin etmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="10f5a-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="10f5a-109">Sanal ağ içinde bir RemoteApp hizmete sonra RemoteApp kaldırmadan hello alt ağ boyutunu artırılamıyor gibi bu özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="10f5a-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="10f5a-110">En büyük kapasitesini toorun istediğiniz her RemoteApp koleksiyonu için kullanılabilir 100 IP adresleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10f5a-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="10f5a-111">Örneğin, bir RemoteApp koleksiyonu hello standart planda varsa ve toohave hello en fazla 500 kullanıcıya istediğiniz, bu koleksiyon için 100 IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="10f5a-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="10f5a-112">Benzer şekilde, 100 IP adreslerini 800 kullanıcısı olan hello temel planda bir RemoteApp koleksiyonu için gerekir.</span><span class="sxs-lookup"><span data-stu-id="10f5a-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="10f5a-113">(Küçüktür hello maksimum) daha az kullanıcı toohave planlıyorsanız, koleksiyon gerekli hello IP adreslerini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="10f5a-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="10f5a-114">Merhaba en düşük alt ağ boyutu gereksinimdir, 30 IP adresleri (/ 27).</span><span class="sxs-lookup"><span data-stu-id="10f5a-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="10f5a-115">Bilgi toomake ağınızı yapılandırıldığından emin izleyen ve propertly çalışma hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="10f5a-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="10f5a-116">Kişisel VNET tooan Azure VNET geçirme</span><span class="sxs-lookup"><span data-stu-id="10f5a-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="10f5a-117">Azure RemoteApp ile Hello Azure VNET toouse doğrula</span><span class="sxs-lookup"><span data-stu-id="10f5a-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

