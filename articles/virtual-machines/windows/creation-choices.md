---
title: "aaaDifferent yolları toocreate Azure Windows VM | Microsoft Docs"
description: "Merhaba farklı şekillerde toocreate Resource Manager ile Windows sanal makine listeler."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="51c49-103">Farklı şekillerde toocreate Windows sanal makine</span><span class="sxs-lookup"><span data-stu-id="51c49-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="51c49-104">Sanal makineler farklı kullanıcılar ve amaçlar için uygundur çünkü azure sanal makine farklı şekillerde toocreate sunar.</span><span class="sxs-lookup"><span data-stu-id="51c49-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="51c49-105">Bu hello sanal makine hakkında bazı seçenekler toomake gerektiği anlamına gelir ve nasıl toocreate onu.</span><span class="sxs-lookup"><span data-stu-id="51c49-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="51c49-106">Bu makalede, bu seçenek bir özetini verir ve tooinstructions bağlar.</span><span class="sxs-lookup"><span data-stu-id="51c49-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="51c49-107">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="51c49-107">Azure portal</span></span>
<span data-ttu-id="51c49-108">Özellikle, yalnızca Azure ile başlıyorsanız hello Azure portal kullanarak basit bir yol tootry bir sanal makine çıkışı değildir.</span><span class="sxs-lookup"><span data-stu-id="51c49-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="51c49-109">Hello portal kullanarak Windows çalıştıran bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="51c49-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="51c49-110">Şablon</span><span class="sxs-lookup"><span data-stu-id="51c49-110">Template</span></span>
<span data-ttu-id="51c49-111">Sanal makinelerin, kaynakların bileşimini gerekir (bir kullanılabilirlik gibi ayarlar ve depolama hesapları).</span><span class="sxs-lookup"><span data-stu-id="51c49-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="51c49-112">Dağıtma ve her bir kaynağın ayrı ayrı yönetmek yerine, dağıtır ve tüm hello kaynakları tek ve eşgüdümlü bir işlemle sağlayan bir Azure Resource Manager şablonu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51c49-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="51c49-113">Resource Manager şablonu kullanarak Windows sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="51c49-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="51c49-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51c49-114">Azure PowerShell</span></span>
<span data-ttu-id="51c49-115">Bir komut kabuğunda çalışma tercih ederseniz, Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51c49-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="51c49-116">PowerShell kullanarak Windows VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="51c49-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="51c49-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51c49-117">Visual Studio</span></span>
<span data-ttu-id="51c49-118">Visual Studio toobuild kullanın, Yönet'i ve VM'ler hello Azure Araçları ile Visual Studio için dağıtmak ve Azure SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="51c49-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="51c49-119">Visual Studio için Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="51c49-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

