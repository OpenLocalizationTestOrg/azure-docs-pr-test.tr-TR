---
title: "bir Azure sanal ağ (Klasik) bir benzeşim grubu tooa bölgesinden aaaMigrate | Microsoft Docs"
description: "Nasıl toomigrate sanal ağ (Klasik) üzerinden benzeşim grubunda tooa bölge öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="2a5f8-103">Bir benzeşim grubu tooa bölgesindeki bir sanal ağ (Klasik) geçirme</span><span class="sxs-lookup"><span data-stu-id="2a5f8-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a5f8-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a5f8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="2a5f8-105">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2a5f8-106">Microsoft, en yeni dağıtımların hello Resource Manager dağıtım modeli kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="2a5f8-107">Benzeşim grupları, kaynaklar aynı benzeşim grubu fiziksel olarak, bu kaynakları toocommunicate daha hızlı etkinleştirme birbirine yakın sunucuları tarafından barındırılan hello içinde oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="2a5f8-108">Geçmiş Hello benzeşim grupları sanal ağları (Klasik) oluşturmak için bir gereksinim yoktu.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="2a5f8-109">O anda sanal ağları (Klasik) yönetilen hello Ağ Yöneticisi hizmeti yalnızca fiziksel sunucularda veya ölçek birimi kümesinde işe yarayabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="2a5f8-110">Mimari geliştirmeleri ağ yönetimi tooa bölge hello kapsamını artırmıştır.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="2a5f8-111">Bu mimari geliştirmeler sonucunda benzeşim grupları artık önerilen veya sanal ağları (Klasik) için gerekli.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="2a5f8-112">benzeşim grupları Hello kullanımını sanal ağları (Klasik) bölgeleri değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="2a5f8-113">(Klasik) bölgeleri ile ilişkilendirilmiş sanal ağları bölgesel sanal ağ adı verilir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="2a5f8-114">Benzeşim grupları genel kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="2a5f8-115">Merhaba sanal ağ gereksinimi yanı sıra benzeşim grupları da önemli toouse işlem (Klasik) ve depolama (Klasik) gibi tooensure kaynaklar, diğer yerleştirildi.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="2a5f8-116">Ancak, hello geçerli Azure ağ mimarisiyle bu yerleştirme gereksinimleri artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a5f8-117">Hala teknik olarak mümkün toocreate bir benzeşim grubu ile ilişkili bir sanal ağ olmasına karşın, yoktur ilgi çekici herhangi bir nedenle toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="2a5f8-118">Ağ güvenlik grupları gibi birçok sanal ağ özellikleri bölgesel bir sanal ağ kullanırken yalnızca kullanılabilir ve benzeşim gruplarıyla ilişkili sanal ağlar için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="2a5f8-119">Merhaba ağ yapılandırma dosyasını düzenleyin</span><span class="sxs-lookup"><span data-stu-id="2a5f8-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="2a5f8-120">Merhaba ağ yapılandırma dosyasını dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-120">Export hello network configuration file.</span></span> <span data-ttu-id="2a5f8-121">nasıl tooexport bir ağ yapılandırması PowerShell kullanarak dosya veya Azure komut satırı arabirimi (CLI) 1.0, hello toolearn bkz [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="2a5f8-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="2a5f8-122">Merhaba ağ yapılandırma dosyasını düzenlemenize değiştirme **AffinityGroup** ile **konumu**.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="2a5f8-123">Bir Azure belirttiğiniz [bölge](https://azure.microsoft.com/regions) için **konumu**.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2a5f8-124">Merhaba **konumu** , sanal ağ (Klasik) ile ilişkili hello benzeşim grubu için belirtilen hello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="2a5f8-125">Örneğin, sanal ağ (Klasik) geçirdiğinizde, Batı ABD içinde bulunan bir benzeşim grubu ile ilişkili ise, **konumu** tooWest ABD işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="2a5f8-126">Ağ yapılandırma dosyanızda izleyerek, hello değerleri kendi değerlerinizle değiştirerek hello düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="2a5f8-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="2a5f8-127">**Eski değer:** \<VirtualNetworkSitename "VNetUSWest" AffinityGroup = "VNetDemoAG" =\></span><span class="sxs-lookup"><span data-stu-id="2a5f8-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="2a5f8-128">**Yeni değer:** \<VirtualNetworkSitename = "VNetUSWest" Konum "Batı ABD" =\></span><span class="sxs-lookup"><span data-stu-id="2a5f8-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="2a5f8-129">Değişikliklerinizi kaydetmek ve [alma](virtual-networks-using-network-configuration-file.md#import) ağ yapılandırması tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="2a5f8-130">Bu geçiş kapalı kalma süresi tooyour Hizmetleri neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="2a5f8-131">Bir benzeşim grubunda bir VM'ye (Klasik) varsa, hangi toodo</span><span class="sxs-lookup"><span data-stu-id="2a5f8-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="2a5f8-132">(Klasik), şu anda bir benzeşim grubunda yer alan VM'ler hello benzeşim grubundan kaldırılmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="2a5f8-133">Bir VM dağıtıldığında, dağıtılan tooa tek ölçek birimi değil.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="2a5f8-134">Benzeşim grupları, kullanılabilir VM boyutları için yeni bir VM dağıtımı hello kümesi kısıtlayabilir ancak dağıtılan var olan VM zaten kısıtlı toohello kümesi VM boyutları hello ölçek birimi hangi hello VM dağıtılırken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="2a5f8-135">Tooa ölçek birimi hello VM zaten dağıtılmış olduğundan, bir VM bir benzeşim grubundan kaldırma hello VM üzerinde etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="2a5f8-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
