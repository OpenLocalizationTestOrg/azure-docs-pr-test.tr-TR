---
title: "PowerShell örnek İzleyici ölçek SQL esnek havuzu Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanındaki bir SQL esnek havuzu ölçekleme ve izlemek için azure PowerShell örnek betiği"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="dfd86-103">İzleme ve Azure SQL veritabanındaki bir SQL esnek havuzu ölçeklendirmek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="dfd86-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="dfd86-104">Bu PowerShell Betiği örneği bir esnek havuz performans ölçümlerini izler, daha yüksek bir performans düzeyine ölçeklendirir ve performans ölçümleri birinde bir uyarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfd86-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="dfd86-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="dfd86-105">Sample script</span></span>

<span data-ttu-id="dfd86-106">[!code-powershell[Ana](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "İzleyici ve ölçek tek SQL veritabanı")]</span><span class="sxs-lookup"><span data-stu-id="dfd86-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dfd86-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="dfd86-107">Clean up deployment</span></span>

<span data-ttu-id="dfd86-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dfd86-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="dfd86-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="dfd86-109">Script explanation</span></span>

<span data-ttu-id="dfd86-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="dfd86-110">This script uses the following commands.</span></span> <span data-ttu-id="dfd86-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="dfd86-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dfd86-112">Komut</span><span class="sxs-lookup"><span data-stu-id="dfd86-112">Command</span></span> | <span data-ttu-id="dfd86-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="dfd86-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="dfd86-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfd86-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dfd86-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfd86-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dfd86-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="dfd86-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="dfd86-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfd86-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="dfd86-118">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="dfd86-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="dfd86-119">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfd86-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="dfd86-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="dfd86-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="dfd86-121">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dfd86-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="dfd86-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="dfd86-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="dfd86-123">Veritabanı boyutu kullanım bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="dfd86-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="dfd86-124">Ekleme AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="dfd86-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="dfd86-125">Ekler veya ölçüm tabanlı uyarı kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dfd86-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="dfd86-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="dfd86-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="dfd86-127">Esnek havuz özelliklerini güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="dfd86-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="dfd86-128">Ekleme AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="dfd86-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="dfd86-129">Otomatik olarak Dtu'lar gelecekte izlemek için bir uyarı kuralı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dfd86-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="dfd86-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfd86-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dfd86-131">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="dfd86-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="dfd86-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dfd86-132">Next steps</span></span>

<span data-ttu-id="dfd86-133">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfd86-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dfd86-134">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dfd86-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
