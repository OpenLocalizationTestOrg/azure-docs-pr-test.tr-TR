---
title: "Klasik Windows VM üzerindeki uç noktaları yukarı aaaSet | Microsoft Docs"
description: "Hello Azure Klasik portalı tooallow iletişimi azure'da Windows sanal makine ile bir Windows VM için uç noktalar yukarı tooset öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="0d948-103">Nasıl tooset azure'da klasik bir Windows sanal makine üzerindeki uç noktaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="0d948-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="0d948-104">Tüm Windows Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz sanal makine otomatik olarak diğer sanal makineler ile özel ağ kanalı üzerinden iletişim kurabilir aynı bulut hizmeti ya da sanal ağ hello.</span><span class="sxs-lookup"><span data-stu-id="0d948-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="0d948-105">Ancak, hello Internet veya diğer sanal ağlardaki bilgisayarlar uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0d948-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="0d948-106">Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="0d948-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d948-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0d948-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d948-108">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d948-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0d948-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="0d948-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="0d948-110">Merhaba, **Resource Manager** dağıtım modeli, uç noktalar kullanılarak yapılandırılmış olan **ağ güvenlik grupları (Nsg'ler)**.</span><span class="sxs-lookup"><span data-stu-id="0d948-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="0d948-111">Daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d948-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0d948-112">Hello Azure portalında Windows sanal makine oluşturduğunuzda, Uzak Masaüstü ve Windows PowerShell uzaktan iletişim için olanlar gibi ortak uç noktaları genellikle sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0d948-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="0d948-113">Merhaba sanal makine oluşturulurken veya daha sonra gerektikçe ek uç noktaları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d948-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="0d948-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d948-114">Next steps</span></span>
* <span data-ttu-id="0d948-115">toouse bir Azure PowerShell cmdlet tooset bir VM uç noktası yukarı bkz [Ekle AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d948-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="0d948-116">toouse Azure PowerShell cmdlet toomanage bir uç noktasındaki ACL bkz [yönetme erişim denetim listeleri (ACL'ler) uç noktaları için PowerShell kullanarak](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0d948-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="0d948-117">Merhaba Resource Manager dağıtım modelinde bir sanal makine oluşturduysanız, Azure PowerShell kullanabileceğine[ağ güvenlik grupları oluşturma](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol trafiği toohello VM.</span><span class="sxs-lookup"><span data-stu-id="0d948-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
