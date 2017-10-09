---
title: "aaaPowerShell örnek etkin coğrafi çoğaltmalı-çoğaltma-tek Azure SQL Database | Microsoft Docs"
description: "Azure PowerShell örnek betiği tooset etkin coğrafi çoğaltma tek bir Azure SQL veritabanı için ayarlama"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="d6ed4-103">PowerShell tooconfigure etkin coğrafi çoğaltma için tek bir Azure SQL veritabanına kullanın</span><span class="sxs-lookup"><span data-stu-id="d6ed4-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="d6ed4-104">Bu PowerShell Betiği örneği tek bir Azure SQL veritabanı için etkin coğrafi çoğaltma yapılandırır ve tooa hello Azure SQL veritabanı'nın ikincil çoğaltma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="d6ed4-105">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="d6ed4-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d6ed4-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="d6ed4-106">Clean up deployment</span></span>

<span data-ttu-id="d6ed4-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d6ed4-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="d6ed4-108">Script explanation</span></span>

<span data-ttu-id="d6ed4-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-109">This script uses hello following commands.</span></span> <span data-ttu-id="d6ed4-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d6ed4-111">Komut</span><span class="sxs-lookup"><span data-stu-id="d6ed4-111">Command</span></span> | <span data-ttu-id="d6ed4-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="d6ed4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6ed4-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6ed4-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d6ed4-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d6ed4-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="d6ed4-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d6ed4-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d6ed4-117">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="d6ed4-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="d6ed4-118">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="d6ed4-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d6ed4-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="d6ed4-120">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="d6ed4-121">AzureRmSqlDatabaseSecondary yeni</span><span class="sxs-lookup"><span data-stu-id="d6ed4-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="d6ed4-122">Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="d6ed4-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d6ed4-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="d6ed4-124">Bir veya daha fazla veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="d6ed4-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d6ed4-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="d6ed4-126">Bir ikincil veritabanı toobe birincil tooinitiate yük devretme geçer.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="d6ed4-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="d6ed4-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="d6ed4-128">Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki Hello coğrafi Çoğaltma bağlantılarını alır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="d6ed4-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d6ed4-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="d6ed4-130">Bir SQL veritabanı ve hello belirtilen ikincil veritabanı arasında veri kopyalama sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="d6ed4-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6ed4-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d6ed4-132">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="d6ed4-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d6ed4-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6ed4-133">Next steps</span></span>

<span data-ttu-id="d6ed4-134">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6ed4-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6ed4-135">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d6ed4-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
