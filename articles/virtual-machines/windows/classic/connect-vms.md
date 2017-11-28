---
title: bir bulut hizmetinde Windows VM'ler aaaConnect | Microsoft Docs
description: "Merhaba Klasik dağıtım modeli tooan Azure bulut hizmeti veya sanal ağ ile oluşturulan Windows sanal makineleri bağlayın."
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
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="93431-103">Bir sanal ağ veya Bulut hizmeti ile Merhaba Klasik dağıtım modeliyle oluşturulan Windows sanal makineleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="93431-103">Connect Windows virtual machines created with hello classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93431-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="93431-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="93431-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="93431-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="93431-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="93431-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="93431-107">Merhaba Klasik dağıtım modeliyle oluşturulan Windows sanal makinelerin her zaman bir bulut hizmetinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="93431-107">Windows virtual machines created with hello classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="93431-108">Merhaba bulut hizmeti, bir kapsayıcı gibi davranır ve benzersiz bir genel DNS adı, bir ortak IP adresi ve bitiş noktaları tooaccess hello sanal makine kümesi hello Internet sağlar.</span><span class="sxs-lookup"><span data-stu-id="93431-108">hello cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints tooaccess hello virtual machine over hello Internet.</span></span> <span data-ttu-id="93431-109">Merhaba bulut hizmeti sanal bir ağa olabilir, ancak bu zorunlu değildir.</span><span class="sxs-lookup"><span data-stu-id="93431-109">hello cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="93431-110">Ayrıca [Linux sanal makineleri bir sanal ağ veya Bulut hizmetiyle bağlantı](../../linux/classic/connect-vms.md).</span><span class="sxs-lookup"><span data-stu-id="93431-110">You can also [connect Linux virtual machines with a virtual network or cloud service](../../linux/classic/connect-vms.md).</span></span>

<span data-ttu-id="93431-111">Bir bulut hizmeti bir sanal ağ içinde değilse, adlı bir *tek başına* bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="93431-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="93431-112">bir tek başına bulut hizmeti Hello sanal makinelerin diğer sanal makinelerle kullanarak diğer sanal makinelerin Genel DNS adlarını hello ve hello trafiği hello Internet geçen iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="93431-112">hello virtual machines in a standalone cloud service communicate with other virtual machines by using hello other virtual machines’ public DNS names, and hello traffic travels over hello Internet.</span></span> <span data-ttu-id="93431-113">Bulut hizmeti ile Merhaba sanal ağdaki diğer tüm sanal makineler hello Internet herhangi bir trafik göndermeden iletişim kurabilir, bir sanal ağ içinde hello sanal makineler bir bulut hizmeti ise.</span><span class="sxs-lookup"><span data-stu-id="93431-113">If a cloud service is in a virtual network, hello virtual machines in that cloud service can communicate with all other virtual machines in hello virtual network without sending any traffic over hello Internet.</span></span>

<span data-ttu-id="93431-114">Yerleştirdiğiniz varsa aynı tek başına bulut hizmeti sanal makinelerinizi Merhaba, Yük Dengeleme kullanmaya devam edebilirsiniz ve kullanılabilirlik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="93431-114">If you place your virtual machines in hello same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="93431-115">Ayrıntılar için bkz [Yük Dengeleme sanal makineleri](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [hello sanal makinelerin kullanılabilirliğini yönetme](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93431-115">For details, see [Load balancing virtual machines](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Manage hello availability of virtual machines](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="93431-116">Ancak, alt ağlar hello sanal makinelerde düzenlemek veya tek başına bulut hizmeti tooyour şirket içi ağ bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93431-116">However, you can't organize hello virtual machines on subnets or connect a standalone cloud service tooyour on-premises network.</span></span> <span data-ttu-id="93431-117">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="93431-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="93431-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93431-118">Next steps</span></span>
<span data-ttu-id="93431-119">Bir sanal makineyi oluşturduktan sonra bir çok fikirdir[bir veri diski Ekle](attach-disk.md) Hizmetleri ve iş yükleri bir konum toostore verileri alacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="93431-119">After you create a virtual machine, it's a good idea too[add a data disk](attach-disk.md) so your services and workloads have a location toostore data.</span></span>
