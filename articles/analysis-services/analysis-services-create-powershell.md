---
title: PowerShell kullanarak bir Azure Analysis Services sunucusuna aaaCreate | Microsoft Docs
description: "Toocreate Azure Analiz Hizmetleri nasıl öğrenin PowerShell kullanarak sunucu"
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
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="eb4b2-103">PowerShell kullanarak bir Azure Analysis Services sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb4b2-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="eb4b2-104">Bir Azure Analysis Services sunucusuna hello komut satırı toocreate PowerShell kullanarak bu hızlı başlangıç açıklar bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="eb4b2-105">Bu görev için Azure PowerShell modülünün 4.0 veya daha sonraki bir sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="eb4b2-106">çalıştırma toofind hello sürüm ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="eb4b2-107">bkz: tooinstall veya yükseltme, [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="eb4b2-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="eb4b2-108">Sunucu oluşturulması ek hizmet ücretlerine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="eb4b2-109">toolearn daha, fazla [Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="eb4b2-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb4b2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eb4b2-110">Prerequisites</span></span>
<span data-ttu-id="eb4b2-111">toocomplete Bu Hızlı Başlangıç, gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb4b2-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="eb4b2-112">**Azure aboneliği**: ziyaret [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate bir hesap.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="eb4b2-113">**Azure Active Directory**: Aboneliğinizin bir Azure Active Directory Kiracısı ile ilişkilendirilmiş olması ve ilgili dizinde bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="eb4b2-114">toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="eb4b2-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="eb4b2-115">AzureRm.AnalysisServices modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="eb4b2-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="eb4b2-116">toocreate aboneliğinizde bir sunucu, kullandığınız hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) Bileşen Modülü.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="eb4b2-117">Merhaba AzureRm.AnalysisServices modülü PowerShell oturumunuza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="eb4b2-118">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="eb4b2-118">Sign in tooAzure</span></span>

<span data-ttu-id="eb4b2-119">Tooyour Azure aboneliği hello kullanarak oturum [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="eb4b2-120">Merhaba ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="eb4b2-121">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb4b2-121">Create a resource group</span></span>
 
<span data-ttu-id="eb4b2-122">[Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md), Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="eb4b2-123">Sunucunuzu oluşturduğunuzda, aboneliğinizde bir kaynak grubu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="eb4b2-124">Bir kaynak grubu zaten yoksa, hello kullanarak yeni bir tane oluşturabilirsiniz [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="eb4b2-125">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello Batı ABD bölgesindeki.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="eb4b2-126">Sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb4b2-126">Create a server</span></span>

<span data-ttu-id="eb4b2-127">Hello kullanarak yeni bir sunucu oluşturmak [yeni AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="eb4b2-128">Merhaba aşağıdaki örnek hello D1 katmanı adresindeki hello Batı ABD bölgesindeki myResourceGroup myServer adlı bir sunucu oluşturur ve belirtir philipc@adventureworks.com sunucu yöneticisi olarak.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="eb4b2-129">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="eb4b2-129">Clean up resources</span></span>

<span data-ttu-id="eb4b2-130">Hello kullanarak aboneliğinizden hello sunucu kaldırabilirsiniz [Kaldır AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutu.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="eb4b2-131">Bu koleksiyondaki diğer hızlı başlangıçları ve öğreticileri kullanacaksanız sunucunuzu kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="eb4b2-132">Merhaba aşağıdaki örnek hello önceki adımda oluşturduğunuz hello sunucusunu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="eb4b2-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="eb4b2-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb4b2-133">Next steps</span></span>
<span data-ttu-id="eb4b2-134">[Azure Analysis Services’ı PowerShell ile yönetme](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="eb4b2-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="eb4b2-135">[SSDT’den model dağıtma](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="eb4b2-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="eb4b2-136">Azure portalında bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb4b2-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)