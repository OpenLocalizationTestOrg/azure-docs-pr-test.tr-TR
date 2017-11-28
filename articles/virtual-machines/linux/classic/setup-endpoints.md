---
title: "uç noktaları klasik bir Linux VM üzerinde yukarı aaaSet | Microsoft Docs"
description: "Hello Azure Klasik portalı tooallow iletişimi azure'da bir Linux sanal makine ile bir Linux VM için uç noktalar yukarı tooset öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="f01ed-103">Nasıl tooset bir Linux Klasik sanal makinede Azure uç noktaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="f01ed-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="f01ed-104">Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz tüm Linux sanal makineleri otomatik olarak hello içindeki diğer sanal makinelerle özel ağ kanalı üzerinden aynı hizmet veya sanal ağ bulut iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="f01ed-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="f01ed-105">Ancak, hello Internet veya diğer sanal ağlardaki bilgisayarlar uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f01ed-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="f01ed-106">Bu makalede ayrıca kullanılabilir [Windows sanal makineleri](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f01ed-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f01ed-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f01ed-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f01ed-108">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f01ed-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f01ed-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="f01ed-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f01ed-110">Merhaba, **Resource Manager** dağıtım modeli, uç noktalar kullanılarak yapılandırılmış olan **ağ güvenlik grupları (Nsg'ler)**.</span><span class="sxs-lookup"><span data-stu-id="f01ed-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="f01ed-111">Daha fazla bilgi için bkz: [bağlantı noktalarını ve uç noktaları açmadan](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f01ed-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f01ed-112">Hello Azure portal Linux sanal makine oluşturduğunuzda, bir uç nokta için güvenli Kabuk (SSH) genellikle sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f01ed-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="f01ed-113">Merhaba sanal makine oluşturulurken veya daha sonra gerektikçe ek uç noktaları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f01ed-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="f01ed-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f01ed-114">Next steps</span></span>
* <span data-ttu-id="f01ed-115">Hello kullanarak bir VM uç noktası oluşturabilirsiniz [Azure komut satırı arabirimi](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f01ed-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="f01ed-116">Merhaba çalıştırmak **azure vm uç noktası oluşturma** komutu.</span><span class="sxs-lookup"><span data-stu-id="f01ed-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="f01ed-117">Merhaba Resource Manager dağıtım modelinde bir sanal makine oluşturduysanız, Resource Manager moduna hello Azure CLI kullanabileceğine[ağ güvenlik grupları oluşturma](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol trafiği toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f01ed-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
