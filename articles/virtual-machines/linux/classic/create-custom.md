---
title: kullanarak bir Linux VM Klasik aaaCreate hello Azure CLI 1.0 | Microsoft Docs
description: "Nasıl toocreate hello Azure CLI 1.0 kullanarak Linux sanal makine hello Klasik dağıtım modeli öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="7c160-103">Nasıl tooCreate klasik bir Linux VM ile bir hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7c160-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7c160-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7c160-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7c160-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c160-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7c160-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="7c160-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7c160-107">Merhaba Resource Manager sürümü için bkz: [burada](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c160-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7c160-108">Bu konuda nasıl toocreate Linux sanal hello Azure CLI 1.0 kullanarak makine (VM) hello Klasik dağıtım modeli açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c160-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="7c160-109">Merhaba kullanılabilir Linux görüntüden kullanırız **GÖRÜNTÜLERİ** Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="7c160-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="7c160-110">Hello Azure CLI 1.0 komutları diğerlerinin yanı sıra yapılandırma seçeneklerinin aşağıdaki hello verin:</span><span class="sxs-lookup"><span data-stu-id="7c160-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="7c160-111">Merhaba VM tooa sanal ağa bağlanma</span><span class="sxs-lookup"><span data-stu-id="7c160-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="7c160-112">Merhaba VM tooan mevcut bulut hizmeti ekleme</span><span class="sxs-lookup"><span data-stu-id="7c160-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="7c160-113">Merhaba VM tooan var olan depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="7c160-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="7c160-114">Merhaba VM tooan kullanılabilirlik kümesi veya Konum ekleme</span><span class="sxs-lookup"><span data-stu-id="7c160-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c160-115">Ana bilgisayar adı veya şirket içi bağlantılar kurma tarafından doğrudan tooit bağlanabilmesi için bir sanal ağ, VM toouse istiyorsanız, hello VM oluşturduğunuzda hello sanal ağ belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7c160-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="7c160-116">Yalnızca hello VM oluşturduğunuzda bir VM yapılandırılmış toojoin sanal bir ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c160-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="7c160-117">Sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Virtual Network'e genel bakış](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="7c160-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="7c160-118">Nasıl toocreate kullanarak Linux VM bir hello Klasik dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="7c160-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

