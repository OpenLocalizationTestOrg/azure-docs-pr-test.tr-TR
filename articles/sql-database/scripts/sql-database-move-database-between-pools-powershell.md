---
title: "aaaPowerShell örnek taşıma Azure SQL veritabanı SQL esnek havuzu | Microsoft Docs"
description: "Azure PowerShell örnek betiği toomove PowerShell kullanarak esnek havuzları arasında bir SQL veritabanı"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="b4920-103">PowerShell toocreate esnek havuzlar kullanın ve esnek havuzlar arasında veritabanlarını taşıma</span><span class="sxs-lookup"><span data-stu-id="b4920-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="b4920-104">Bu PowerShell Betiği örneği iki esnek havuzlar oluşturur ve bir veritabanı bir esnek havuzdan başka bir esnek havuza ve ardından bir veritabanını bir esnek havuz tooa tek veritabanı performans düzeyi dışında taşır.</span><span class="sxs-lookup"><span data-stu-id="b4920-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b4920-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b4920-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b4920-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="b4920-106">Clean up deployment</span></span>

<span data-ttu-id="b4920-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4920-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b4920-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b4920-108">Script explanation</span></span>

<span data-ttu-id="b4920-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="b4920-109">This script uses hello following commands.</span></span> <span data-ttu-id="b4920-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="b4920-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4920-111">Komut</span><span class="sxs-lookup"><span data-stu-id="b4920-111">Command</span></span> | <span data-ttu-id="b4920-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="b4920-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4920-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4920-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b4920-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4920-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4920-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="b4920-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b4920-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4920-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b4920-117">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b4920-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b4920-118">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4920-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b4920-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4920-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b4920-120">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b4920-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b4920-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4920-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="b4920-122">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="b4920-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b4920-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4920-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b4920-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="b4920-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b4920-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4920-125">Next steps</span></span>

<span data-ttu-id="b4920-126">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4920-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b4920-127">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b4920-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
