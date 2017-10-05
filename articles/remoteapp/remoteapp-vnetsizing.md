---
title: "Boyutlandırma bilgileri için bir VNET Azure remoteapp'te | Microsoft Docs"
description: "Bir VNET ile birlikte çalışan Azure RemoteApp için IP adresi gereksinimleri hakkında bilgi edinin"
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="0c7fa-103">Boyutlandırma bilgileri Azure remoteapp'te bir VNET için</span><span class="sxs-lookup"><span data-stu-id="0c7fa-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c7fa-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0c7fa-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0c7fa-106">Bir sanal ağ (VNET) ile Azure RemoteApp kullandığınızda, RemoteApp alt ağ içindeki IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="0c7fa-107">RemoteApp hizmetinizi ölçekte alt ağınızı RemoteApp sanal makineler için kullanılabilir yeterli IP adresine sahip olduğundan emin olun gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="0c7fa-108">Bu boyutlandırma kılavuzluğu nasıl RemoteApp dinamik olarak yukarı döner ve sanal makineleri bir koleksiyon içinde aşağı döner verilen kusursuz olmasa da, alt ağ aralığınızı tahmin etmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="0c7fa-109">Sanal ağ içinde bir RemoteApp hizmete sonra RemoteApp kaldırmadan alt ağ boyutunu artırılamıyor gibi bu özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="0c7fa-110">Maksimum kapasitede çalıştırmak istediğiniz her RemoteApp koleksiyonu için kullanılabilir 100 IP adresleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="0c7fa-111">Örneğin, standart plana bir RemoteApp koleksiyonu vardır ve en fazla 500 kullanıcıya olmasını istiyorsanız, bu koleksiyon için 100 IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="0c7fa-112">Benzer şekilde, 100 IP adreslerini 800 kullanıcılara temel planda bir RemoteApp koleksiyonu için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="0c7fa-113">Az sayıda kullanıcıyla (en büyük değerinden) oluşturmayı planlıyorsanız, koleksiyon gerekli IP adreslerini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="0c7fa-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="0c7fa-114">En düşük alt ağ boyutu gereksinimdir 30 IP adresleri (/ 27).</span><span class="sxs-lookup"><span data-stu-id="0c7fa-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="0c7fa-115">Yapılandırılmış ve çalışıyor propertly VNET'İNİZİ emin olmak için aşağıdaki bilgileri kullanıma:</span><span class="sxs-lookup"><span data-stu-id="0c7fa-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="0c7fa-116">Kişisel Sanal ağdan bir Azure sanal ağına geçiş</span><span class="sxs-lookup"><span data-stu-id="0c7fa-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="0c7fa-117">Azure RemoteApp ile kullanmak için Azure VNET doğrula</span><span class="sxs-lookup"><span data-stu-id="0c7fa-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

