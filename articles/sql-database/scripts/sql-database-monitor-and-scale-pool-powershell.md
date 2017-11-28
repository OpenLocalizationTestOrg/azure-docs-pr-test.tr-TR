---
title: "aaaPowerShell örnek İzleyici ölçek SQL esnek havuzu Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği toomonitor ve ölçek Azure SQL veritabanındaki bir SQL esnek havuzu"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="bad99-103">PowerShell toomonitor kullanın ve Azure SQL veritabanı bir SQL esnek havuzda ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bad99-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="bad99-104">Performans ölçümlerini bir esnek havuz izleyicileri hello bu PowerShell Betiği örneği tooa daha yüksek performans düzeyi ölçeklendirir ve hello performans ölçümleri birinde bir uyarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bad99-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="bad99-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="bad99-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bad99-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="bad99-106">Clean up deployment</span></span>

<span data-ttu-id="bad99-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad99-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="bad99-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="bad99-108">Script explanation</span></span>

<span data-ttu-id="bad99-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="bad99-109">This script uses hello following commands.</span></span> <span data-ttu-id="bad99-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="bad99-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bad99-111">Komut</span><span class="sxs-lookup"><span data-stu-id="bad99-111">Command</span></span> | <span data-ttu-id="bad99-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="bad99-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="bad99-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bad99-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bad99-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bad99-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bad99-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="bad99-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="bad99-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bad99-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="bad99-117">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="bad99-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="bad99-118">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bad99-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="bad99-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="bad99-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="bad99-120">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bad99-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="bad99-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="bad99-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="bad99-122">Merhaba veritabanı Hello boyutu kullanım bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bad99-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="bad99-123">Ekleme AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="bad99-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="bad99-124">Ekler veya ölçüm tabanlı uyarı kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bad99-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="bad99-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="bad99-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="bad99-126">Esnek havuz özelliklerini güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="bad99-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="bad99-127">Ekleme AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="bad99-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="bad99-128">Bir uyarı kuralı tooautomatically İzleyici Dtu'lar hello gelecekteki ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bad99-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="bad99-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bad99-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="bad99-130">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="bad99-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="bad99-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bad99-131">Next steps</span></span>

<span data-ttu-id="bad99-132">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bad99-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bad99-133">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bad99-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
