---
title: "Azure üzerinde bir Windows VM oluşturmanın farklı yolları | Microsoft Docs"
description: "Resource Manager ile Windows sanal makine oluşturmanın farklı yollarını listeler."
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a><span data-ttu-id="ef590-103">Windows sanal makine oluşturmanın farklı yolları</span><span class="sxs-lookup"><span data-stu-id="ef590-103">Different ways to create a Windows virtual machine</span></span>

<span data-ttu-id="ef590-104">Azure sanal makineleri farklı kullanıcılar ve amaçlar için uygundur çünkü bir sanal makine oluşturmanın farklı yollarını sunar.</span><span class="sxs-lookup"><span data-stu-id="ef590-104">Azure offers different ways to create a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="ef590-105">Başka bir deyişle, sanal makine ve nasıl oluşturulduğu hakkında bazı seçim yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef590-105">This means that you need to make some choices about the virtual machine and how to create it.</span></span> <span data-ttu-id="ef590-106">Bu makale için yönergeler bu seçimlere ve bağlantıları bir özetini verir.</span><span class="sxs-lookup"><span data-stu-id="ef590-106">This article gives you a summary of these choices and links to instructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="ef590-107">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="ef590-107">Azure portal</span></span>
<span data-ttu-id="ef590-108">Özellikle, yalnızca Azure ile başlıyorsanız Azure portalını kullanarak bir sanal makine denemek için basit bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="ef590-108">Using the Azure portal is a simple way to try out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="ef590-109">Portalı kullanarak Windows çalıştıran sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef590-109">Create a virtual machine running Windows using the portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="ef590-110">Şablon</span><span class="sxs-lookup"><span data-stu-id="ef590-110">Template</span></span>
<span data-ttu-id="ef590-111">Sanal makinelerin, kaynakların bileşimini gerekir (bir kullanılabilirlik gibi ayarlar ve depolama hesapları).</span><span class="sxs-lookup"><span data-stu-id="ef590-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="ef590-112">Dağıtma ve her bir kaynağın ayrı ayrı yönetmek yerine, dağıtır ve tüm kaynakları tek ve eşgüdümlü bir işlemle sağlayan bir Azure Resource Manager şablonu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef590-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of the resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="ef590-113">Resource Manager şablonu kullanarak Windows sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef590-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="ef590-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef590-114">Azure PowerShell</span></span>
<span data-ttu-id="ef590-115">Bir komut kabuğunda çalışma tercih ederseniz, Azure PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef590-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="ef590-116">PowerShell kullanarak Windows VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef590-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="ef590-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ef590-117">Visual Studio</span></span>
<span data-ttu-id="ef590-118">Visual Studio oluşturmak, yönetmek ve Visual Studio ve Azure SDK'sı için Azure Araçları ile sanal makineleri dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef590-118">Use Visual Studio to build, manage, and deploy VMs with the Azure Tools for Visual Studio and the Azure SDK.</span></span>

[<span data-ttu-id="ef590-119">Visual Studio için Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="ef590-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

