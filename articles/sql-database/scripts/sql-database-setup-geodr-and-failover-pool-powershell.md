---
title: "aaaPowerShell örnek etkin coğrafi çoğaltma havuza Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği tooset havuza alınmış bir Azure SQL veritabanı için etkin coğrafi çoğaltma ayarlama"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="0f24a-103">Havuza alınmış bir Azure SQL veritabanı için PowerShell tooconfigure etkin coğrafi çoğaltma kullanın</span><span class="sxs-lookup"><span data-stu-id="0f24a-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="0f24a-104">Bu PowerShell Betiği örneği etkin coğrafi çoğaltma için bir Azure SQL veritabanını bir esnek havuz yapılandırır ve toohello hello Azure SQL veritabanı'nın ikincil çoğaltma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0f24a-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="0f24a-105">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="0f24a-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0f24a-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="0f24a-106">Clean up deployment</span></span>

<span data-ttu-id="0f24a-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f24a-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0f24a-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0f24a-108">Script explanation</span></span>

<span data-ttu-id="0f24a-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="0f24a-109">This script uses hello following commands.</span></span> <span data-ttu-id="0f24a-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="0f24a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0f24a-111">Komut</span><span class="sxs-lookup"><span data-stu-id="0f24a-111">Command</span></span> | <span data-ttu-id="0f24a-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="0f24a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f24a-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f24a-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0f24a-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f24a-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f24a-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="0f24a-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0f24a-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f24a-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="0f24a-117">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="0f24a-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="0f24a-118">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f24a-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="0f24a-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0f24a-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="0f24a-120">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f24a-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="0f24a-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0f24a-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="0f24a-122">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="0f24a-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="0f24a-123">AzureRmSqlDatabaseSecondary yeni</span><span class="sxs-lookup"><span data-stu-id="0f24a-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="0f24a-124">Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır.</span><span class="sxs-lookup"><span data-stu-id="0f24a-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="0f24a-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0f24a-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="0f24a-126">Bir veya daha fazla veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="0f24a-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="0f24a-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="0f24a-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="0f24a-128">İkincil veritabanı toobe birincil sipariş tooinitiate yük devretme kümesinde geçer.</span><span class="sxs-lookup"><span data-stu-id="0f24a-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="0f24a-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="0f24a-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="0f24a-130">Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki Hello coğrafi Çoğaltma bağlantılarını alır.</span><span class="sxs-lookup"><span data-stu-id="0f24a-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="0f24a-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f24a-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0f24a-132">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="0f24a-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="0f24a-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f24a-133">Next steps</span></span>

<span data-ttu-id="0f24a-134">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0f24a-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0f24a-135">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0f24a-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
