---
title: "aaaPowerShell İzleyici ölçek tek örnek Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği toomonitor ve ölçek tek bir Azure SQL veritabanı"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="967e6-103">PowerShell toomonitor kullanın ve tek bir SQL veritabanı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="967e6-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="967e6-104">Bir veritabanı performans ölçümlerini izleyiciler hello bu PowerShell Betiği örneği tooa daha yüksek performans düzeyi ölçeklendirir ve bir uyarı kuralı hello performans ölçümleri birinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="967e6-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="967e6-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="967e6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="967e6-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="967e6-106">Clean up deployment</span></span>

<span data-ttu-id="967e6-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="967e6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="967e6-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="967e6-108">Script explanation</span></span>

<span data-ttu-id="967e6-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="967e6-109">This script uses hello following commands.</span></span> <span data-ttu-id="967e6-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="967e6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="967e6-111">Komut</span><span class="sxs-lookup"><span data-stu-id="967e6-111">Command</span></span> | <span data-ttu-id="967e6-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="967e6-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="967e6-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="967e6-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="967e6-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="967e6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="967e6-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="967e6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="967e6-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="967e6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="967e6-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="967e6-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="967e6-118">Merhaba veritabanı Hello boyutu kullanım bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="967e6-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="967e6-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="967e6-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="967e6-120">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="967e6-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="967e6-121">Ekleme AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="967e6-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="967e6-122">Bir uyarı kuralı tooautomatically İzleyici Dtu'lar hello gelecekteki ayarlar.</span><span class="sxs-lookup"><span data-stu-id="967e6-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="967e6-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="967e6-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="967e6-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="967e6-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="967e6-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="967e6-125">Next steps</span></span>

<span data-ttu-id="967e6-126">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="967e6-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="967e6-127">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="967e6-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
