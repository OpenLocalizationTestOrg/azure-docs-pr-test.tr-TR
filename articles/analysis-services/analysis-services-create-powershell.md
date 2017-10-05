---
title: "PowerShell kullanarak bir Azure Analysis Services sunucusu oluşturma | Microsoft Docs"
description: "PowerShell kullanarak bir Azure Analysis Services sunucusu oluşturma hakkında bilgi edinin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="906c4-103">PowerShell kullanarak bir Azure Analysis Services sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="906c4-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="906c4-104">Bu hızlı başlangıç, Azure aboneliğinizde bir [Azure kaynak grubunda](../azure-resource-manager/resource-group-overview.md) Azure Analysis Services sunucusu oluşturmak için komut satırından PowerShell kullanmayı anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="906c4-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="906c4-105">Bu görev için Azure PowerShell modülünün 4.0 veya daha sonraki bir sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="906c4-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="906c4-106">Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="906c4-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="906c4-107">Yüklemek veya yükseltmek için bkz. [Azure PowerShell Modülü yükleme](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="906c4-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="906c4-108">Sunucu oluşturulması ek hizmet ücretlerine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="906c4-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="906c4-109">Daha fazla bilgi için bkz. [Analysis Services fiyatlandırması](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="906c4-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="906c4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="906c4-110">Prerequisites</span></span>
<span data-ttu-id="906c4-111">Bu hızlı başlangıcı tamamlamak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="906c4-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="906c4-112">**Azure aboneliği**: Hesap oluşturmak için [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/offers/ms-azr-0044p/)’nü ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="906c4-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="906c4-113">**Azure Active Directory**: Aboneliğinizin bir Azure Active Directory Kiracısı ile ilişkilendirilmiş olması ve ilgili dizinde bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="906c4-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="906c4-114">Daha fazla bilgi edinmek için bkz. [Kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="906c4-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="906c4-115">AzureRm.AnalysisServices modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="906c4-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="906c4-116">Aboneliğinizde bir sunucu oluşturmak için [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) bileşen modülünü kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="906c4-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="906c4-117">AzureRm.AnalysisServices modülünü PowerShell oturumunuza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="906c4-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="906c4-118">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="906c4-118">Sign in to Azure</span></span>

<span data-ttu-id="906c4-119">[Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komutunu kullanarak Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="906c4-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="906c4-120">Ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="906c4-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="906c4-121">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="906c4-121">Create a resource group</span></span>
 
<span data-ttu-id="906c4-122">[Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md), Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="906c4-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="906c4-123">Sunucunuzu oluşturduğunuzda, aboneliğinizde bir kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="906c4-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="906c4-124">Zaten bir kaynak grubunuz yoksa [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutunu çalıştırarak bir kaynak grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="906c4-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="906c4-125">Aşağıdaki örnekte Batı ABD bölgesinde `myResourceGroup` adında bir kaynak grubu oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="906c4-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="906c4-126">Sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="906c4-126">Create a server</span></span>

<span data-ttu-id="906c4-127">[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutunu kullanarak yeni bir sunucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="906c4-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="906c4-128">Aşağıdaki örnek, Batı ABD bölgesinde D1 katmanında myResourceGroup’ta myServer adlı bir sunucu oluşturur ve sunucu yöneticisi olarak philipc@adventureworks.com adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="906c4-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="906c4-129">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="906c4-129">Clean up resources</span></span>

<span data-ttu-id="906c4-130">[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutunu kullanarak sunucuyu aboneliğinizden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="906c4-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="906c4-131">Bu koleksiyondaki diğer hızlı başlangıçları ve öğreticileri kullanacaksanız sunucunuzu kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="906c4-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="906c4-132">Aşağıdaki örnekte önceki adımda oluşturduğunuz sunucu kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="906c4-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="906c4-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="906c4-133">Next steps</span></span>
<span data-ttu-id="906c4-134">[Azure Analysis Services’ı PowerShell ile yönetme](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="906c4-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="906c4-135">[SSDT’den model dağıtma](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="906c4-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="906c4-136">Azure portalında bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="906c4-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)