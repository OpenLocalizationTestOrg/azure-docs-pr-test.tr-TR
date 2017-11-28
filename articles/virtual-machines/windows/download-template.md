---
title: "bir Azure VM için aaaDownload hello şablonu | Microsoft Docs"
description: "Merhaba templatefor hello Resource Manager dağıtım modeli dağıtımlarda otomatikleştirmede VM toohelp indirin"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="d3f4b-103">Bir VM için Hello şablonunu yükle</span><span class="sxs-lookup"><span data-stu-id="d3f4b-103">Download hello template for a VM</span></span>
<span data-ttu-id="d3f4b-104">Azure'da VM oluşturduğunuzda hello portalı veya bir Resource Manager PowerShell kullanarak şablonu otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="d3f4b-105">Bu şablon tooquickly yinelenen bir dağıtım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="d3f4b-106">Merhaba şablonu bir kaynak grubunda hello kaynakların tümünü hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="d3f4b-107">Bir sanal makine için bu hello şablonu hello VM hello ağ kaynaklarını dahil olmak üzere bu kaynak grubundaki desteklenmesi amacıyla oluşturulan her şeyi içeren anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="d3f4b-108">Merhaba portal kullanarak hello şablonunu yükle</span><span class="sxs-lookup"><span data-stu-id="d3f4b-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="d3f4b-109">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d3f4b-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d3f4b-110">Bir hello hub menüsünde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="d3f4b-111">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="d3f4b-112">Seçin **Otomasyon betiğini**.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="d3f4b-113">Seçin **karşıdan** ve hello .zip dosya tooyour yerel bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="d3f4b-114">Merhaba .zip dosyasını açın ve hello dosyaları tooa klasörüne ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="d3f4b-115">Merhaba .zip dosyası içerir:</span><span class="sxs-lookup"><span data-stu-id="d3f4b-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="d3f4b-116">Deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="d3f4b-116">deploy.ps1</span></span>
   * <span data-ttu-id="d3f4b-117">Deploy.sh</span><span class="sxs-lookup"><span data-stu-id="d3f4b-117">deploy.sh</span></span> 
   * <span data-ttu-id="d3f4b-118">deployer.RB</span><span class="sxs-lookup"><span data-stu-id="d3f4b-118">deployer.rb</span></span>
   * <span data-ttu-id="d3f4b-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="d3f4b-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="d3f4b-120">Parameters.JSON</span><span class="sxs-lookup"><span data-stu-id="d3f4b-120">parameters.json</span></span>
   * <span data-ttu-id="d3f4b-121">Template.JSON</span><span class="sxs-lookup"><span data-stu-id="d3f4b-121">template.json</span></span>

<span data-ttu-id="d3f4b-122">Merhaba template.json dosyasını hello şablonudur.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="d3f4b-123">PowerShell kullanarak hello şablonunu yükle</span><span class="sxs-lookup"><span data-stu-id="d3f4b-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="d3f4b-124">Ayrıca hello kullanarak hello .json şablon dosyası indirebilirsiniz [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="d3f4b-125">Merhaba kullanabilirsiniz `-path` tooprovide hello filename parametresi ve hello .json dosyası için yol.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="d3f4b-126">Bu örnek nasıl hello kaynak grubu için toodownload hello şablonu adlı gösterir **myResourceGroup** toohello **C:\users\public\downloads** klasör, yerel bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="d3f4b-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="d3f4b-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3f4b-127">Next steps</span></span>
<span data-ttu-id="d3f4b-128">şablonları kullanarak kaynakları dağıtma hakkında daha fazla toolearn bkz [Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d3f4b-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

