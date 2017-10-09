---
title: "aaaCreate veya PowerShell ile otomatik olarak Azure Resource Manager şablonları kullanarak labs değiştirme | Microsoft Docs"
description: "Öğrenin nasıl toouse Azure Resource Manager şablonları PowerShell toocreate ile veya otomatik olarak DevTest lab labs değiştirme"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="e1d18-103">Oluşturun veya Azure Resource Manager şablonları ve PowerShell kullanılarak otomatik olarak labs değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1d18-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="e1d18-104">DevTest Labs birçok Azure Resource Manager şablonları ve hızlı bir şekilde Yardım ve otomatik olarak yeni labs oluşturmak veya var olan Laboratuarları değiştirebilir ve ardından bu kaynakları dağıtabilirsiniz PowerShell komut dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1d18-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="e1d18-105">Bu makalede, bu şablonları ve komut dosyaları tooautomate hello oluşturulması, değiştirilmesi ve, labs dağıtımını kullanarak hello işleminde size kılavuzluk yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1d18-105">This article helps guide you through hello process of using these templates and scripts tooautomate hello creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="e1d18-106">Bu makalede ayrıca nasıl toouse PowerShell tooperform DevTest Labs'de bazı ortak görevler hakkında daha fazla bilgi bulabileceği yerler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e1d18-106">This article also shows you where you can find more information about how toouse PowerShell tooperform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="e1d18-107">Adım 1: şablonları ve komut dosyaları toplama</span><span class="sxs-lookup"><span data-stu-id="e1d18-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="e1d18-108">Önceden yapılan bulabilir [Azure Resource Manager şablonları](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) ve [PowerShell komut dosyalarını](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) ortak adresindeki [Github deposunu](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="e1d18-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="e1d18-109">Bunları kullanın-olan veya gereksinimlerinize göre özelleştirmek ve bunları kendi içinde depolamak [özel Git deposuna](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e1d18-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="e1d18-110">2. adım: Azure Resource Manager şablonunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="e1d18-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="e1d18-111">Merhaba adımları izleyin [, ilk Azure Resource Manager şablonu oluşturma](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) hiçbir zaman önce bir şablon oluşturduysanız.</span><span class="sxs-lookup"><span data-stu-id="e1d18-111">You can follow hello steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="e1d18-112">Ayrıca, [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) birçok kılavuzları ve önerileri toohelp sunar güvenilir ve kolay toouse olan Azure Resource Manager şablonları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1d18-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions toohelp you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="e1d18-113">Genellikle, bir çeşitlemesi hello yaklaşımlardan birini kullanın veya örnekler sağlanan ve şablonunuzu gereksinimleriniz için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1d18-113">Typically, you will use a variation of one of hello approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="e1d18-114">Adım 3: PowerShell kaynaklarla dağıtma</span><span class="sxs-lookup"><span data-stu-id="e1d18-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="e1d18-115">Şablonlar ve komut dosyalarınız özelleştirdikten sonra hello gerekli çok adımları[Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e1d18-115">After you have customized your templates and scripts, follow hello steps necessary too[deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="e1d18-116">Merhaba makale kaynakları tooAzure Azure Resource Manager şablonları toodeploy ile Azure PowerShell'i kullanma hakkında genel bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1d18-116">hello article provides general information about using Azure PowerShell with Azure Resource Manager templates toodeploy your resources tooAzure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="e1d18-117">PowerShell kullanarak DevTest Labs'de gerçekleştirdiğiniz ortak görevler</span><span class="sxs-lookup"><span data-stu-id="e1d18-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="e1d18-118">PowerShell kullanarak otomatikleştirebilirsiniz birçok diğer ortak görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="e1d18-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="e1d18-119">Merhaba aşağıdaki bölümlerde hello belgelerin hello adımları gerekli tooperform bu görevler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1d18-119">hello following sections of hello documentation outline hello steps required tooperform these tasks.</span></span>

* [<span data-ttu-id="e1d18-120">PowerShell kullanarak bir VHD'yi dosyasından özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="e1d18-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="e1d18-121">PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e1d18-121">Upload VHD file toolab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="e1d18-122">PowerShell kullanarak bir dış kullanıcı tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="e1d18-122">Add an external user tooa lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="e1d18-123">PowerShell kullanarak bir lab özel rolü oluşturun</span><span class="sxs-lookup"><span data-stu-id="e1d18-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="e1d18-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1d18-124">Next steps</span></span>
* <span data-ttu-id="e1d18-125">Bilgi nasıl toocreate bir [özel Git deposu](devtest-lab-add-artifact-repo.md) depolayacağınız özelleştirilmiş şablonları veya komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e1d18-125">Learn how toocreate a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="e1d18-126">Merhaba keşfedin [Azure Resource Manager şablonları Azure hızlı başlangıç Şablon Galerisinden](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e1d18-126">Explore hello [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
