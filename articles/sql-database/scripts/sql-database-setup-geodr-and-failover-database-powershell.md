---
title: "PowerShell örnek etkin coğrafi çoğaltma tek Azure SQL veritabanı | Microsoft Docs"
description: "Tek bir Azure SQL veritabanı için etkin coğrafi çoğaltma ayarlamak için azure PowerShell örnek betiği"
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="67340-103">Tek bir Azure SQL veritabanı için etkin coğrafi çoğaltma yapılandırmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="67340-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="67340-104">Bu PowerShell Betiği örneği tek bir Azure SQL veritabanı için etkin coğrafi çoğaltma yapılandırır ve Azure SQL veritabanı için bir ikincil çoğaltma üzerinden başarısız.</span><span class="sxs-lookup"><span data-stu-id="67340-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="67340-105">Örnek komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="67340-105">Sample scripts</span></span>

<span data-ttu-id="67340-106">[!code-powershell[Ana](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "tek veritabanı için etkin coğrafi çoğaltma ayarlama")]</span><span class="sxs-lookup"><span data-stu-id="67340-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="67340-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="67340-107">Clean up deployment</span></span>

<span data-ttu-id="67340-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="67340-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="67340-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="67340-109">Script explanation</span></span>

<span data-ttu-id="67340-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="67340-110">This script uses the following commands.</span></span> <span data-ttu-id="67340-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="67340-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="67340-112">Komut</span><span class="sxs-lookup"><span data-stu-id="67340-112">Command</span></span> | <span data-ttu-id="67340-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="67340-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67340-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="67340-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="67340-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67340-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67340-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="67340-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="67340-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67340-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="67340-118">Yeni-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="67340-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="67340-119">Bir esnek havuz bir mantıksal sunucu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67340-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="67340-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="67340-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="67340-121">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="67340-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="67340-122">AzureRmSqlDatabaseSecondary yeni</span><span class="sxs-lookup"><span data-stu-id="67340-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="67340-123">Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır.</span><span class="sxs-lookup"><span data-stu-id="67340-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="67340-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="67340-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="67340-125">Bir veya daha fazla veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="67340-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="67340-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="67340-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="67340-127">Yük devretme başlatmak için birincil olarak ikincil bir veritabanı geçer.</span><span class="sxs-lookup"><span data-stu-id="67340-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="67340-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="67340-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="67340-129">Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki coğrafi Çoğaltma bağlantılarını alır.</span><span class="sxs-lookup"><span data-stu-id="67340-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="67340-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="67340-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="67340-131">Bir SQL veritabanı ve belirtilen ikincil veritabanı arasında veri kopyalama sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="67340-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="67340-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="67340-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="67340-133">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="67340-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="67340-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67340-134">Next steps</span></span>

<span data-ttu-id="67340-135">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67340-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="67340-136">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="67340-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
