---
title: "Windows sanal makineleri bir bulut hizmetine bağlanmak | Microsoft Docs"
description: "Bir Azure bulut hizmeti veya sanal ağı Klasik dağıtım modeliyle oluşturulan Windows sanal makineleri bağlayın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 0c7a21461e5bb111c4359df8e949d48382b591c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="8b584-103">Bir sanal ağ veya Bulut hizmeti ile klasik dağıtım modeliyle oluşturulan Windows sanal makineleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="8b584-103">Connect Windows virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8b584-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8b584-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8b584-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8b584-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8b584-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="8b584-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="8b584-107">Klasik dağıtım modeliyle oluşturulan Windows sanal makinelerin her zaman bir bulut hizmetinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b584-107">Windows virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="8b584-108">Bulut hizmeti bir kapsayıcı gibi davranır ve benzersiz bir genel DNS adı, bir ortak IP adresi ve sanal makine Internet üzerinden erişmek için uç noktalar kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b584-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="8b584-109">Bulut hizmeti sanal bir ağa olabilir, ancak bu zorunlu değildir.</span><span class="sxs-lookup"><span data-stu-id="8b584-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="8b584-110">Ayrıca [Linux sanal makineleri bir sanal ağ veya Bulut hizmetiyle bağlantı](../../linux/classic/connect-vms.md).</span><span class="sxs-lookup"><span data-stu-id="8b584-110">You can also [connect Linux virtual machines with a virtual network or cloud service](../../linux/classic/connect-vms.md).</span></span>

<span data-ttu-id="8b584-111">Bir bulut hizmeti bir sanal ağ içinde değilse, adlı bir *tek başına* bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8b584-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="8b584-112">Sanal makine bir tek başına bulut hizmeti, diğer sanal makineler ortak DNS adlarını kullanarak diğer sanal makinelerle iletişim kurmak ve trafik Internet üzerinden geçen.</span><span class="sxs-lookup"><span data-stu-id="8b584-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="8b584-113">Bir bulut hizmeti sanal bir ağda ise, bulut hizmetinin'nde sanal makinelerin sanal ağdaki diğer tüm sanal makinelerin tüm trafik Internet üzerinden göndermeden iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="8b584-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="8b584-114">Sanal makinelerinizi aynı tek başına bulut hizmeti yerleştirirseniz, Yük Dengeleme ve kullanılabilirlik kümelerini kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b584-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="8b584-115">Ayrıntılar için bkz [Yük Dengeleme sanal makineleri](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [sanal makinelerin kullanılabilirliğini yönetme](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b584-115">For details, see [Load balancing virtual machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Manage the availability of virtual machines](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8b584-116">Ancak, alt ağlar sanal makinelerde düzenlemek veya tek başına bulut hizmeti şirket içi ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8b584-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="8b584-117">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8b584-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="8b584-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b584-118">Next steps</span></span>
<span data-ttu-id="8b584-119">Bir sanal makine oluşturduktan sonra iyi bir fikir olduğu [bir veri diski Ekle](attach-disk.md) böylece Hizmetleri ve iş yüklerini veri depolamak için bir konum.</span><span class="sxs-lookup"><span data-stu-id="8b584-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
