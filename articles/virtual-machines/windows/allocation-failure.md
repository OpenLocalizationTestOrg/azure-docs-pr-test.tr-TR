---
title: "Windows VM ayırma hatalarının sorunlarını giderme | Microsoft Docs"
description: "Oluşturduğunuzda, yeniden başlatın veya Windows VM Azure ile yeniden boyutlandırın ayırma hatalarını giderme"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: 57925b5a75fd8bcf2a9450025b5dc51eb552353f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="f892c-103">Oluşturduğunuzda, yeniden başlatın veya Windows VM'ler için Azure'da yeniden boyutlandırma ayırma hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="f892c-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="f892c-104">Bir VM oluşturun, durduruldu (serbest bırakıldığında) sanal makineleri yeniden başlatın veya bir VM'yi yeniden boyutlandırın, Microsoft Azure aboneliğinize işlem kaynakları ayırır.</span><span class="sxs-lookup"><span data-stu-id="f892c-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="f892c-105">Zaman zaman bile Azure abonelik limitleri düşmeden önce bu işlemleri--yaparken hatalar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f892c-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="f892c-106">Bu makalede, bazı ortak ayırma hatalarının nedenlerini açıklar ve olası düzeltme önerir.</span><span class="sxs-lookup"><span data-stu-id="f892c-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="f892c-107">Hizmetlerinizin dağıtımını planlarken bilgiler de yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f892c-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="f892c-108">Ayrıca [oluşturduğunuzda, yeniden başlatın veya Linux VM'ler için Azure'da yeniden boyutlandırma ayırma hatalarını giderme](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f892c-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

