---
title: "aaaPowerShell örnek geri yükleme yedekleme Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği toorestore coğrafi olarak yedekli yedeklerden bir Azure SQL veritabanı"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="9ced9-103">PowerShell toorestore yedeklerden Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="9ced9-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="9ced9-104">Bu PowerShell Betiği örnek bir Azure SQL veritabanı coğrafi olarak yedekli bir yedekten geri yükler, bir silinen Azure SQL veritabanı tooits son yedekleme geri yükler ve bir Azure SQL veritabanı tooa belirli noktası sürede geri yükler.</span><span class="sxs-lookup"><span data-stu-id="9ced9-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9ced9-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9ced9-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9ced9-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="9ced9-106">Clean up deployment</span></span>

<span data-ttu-id="9ced9-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ced9-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9ced9-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="9ced9-108">Script explanation</span></span>

<span data-ttu-id="9ced9-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ced9-109">This script uses hello following commands.</span></span> <span data-ttu-id="9ced9-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="9ced9-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9ced9-111">Komut</span><span class="sxs-lookup"><span data-stu-id="9ced9-111">Command</span></span> | <span data-ttu-id="9ced9-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="9ced9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ced9-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ced9-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="9ced9-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ced9-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="9ced9-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="9ced9-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="9ced9-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ced9-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="9ced9-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9ced9-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="9ced9-118">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ced9-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="9ced9-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="9ced9-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="9ced9-120">Coğrafi olarak yedekli bir veritabanının yedeğini alır.</span><span class="sxs-lookup"><span data-stu-id="9ced9-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="9ced9-121">Geri yükleme-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9ced9-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="9ced9-122">Bir SQL veritabanını geri yükler.</span><span class="sxs-lookup"><span data-stu-id="9ced9-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="9ced9-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9ced9-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="9ced9-124">Bir Azure SQL veritabanı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9ced9-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="9ced9-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="9ced9-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="9ced9-126">Geri yüklediğiniz silinen bir veritabanını alır.</span><span class="sxs-lookup"><span data-stu-id="9ced9-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="9ced9-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ced9-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9ced9-128">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="9ced9-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ced9-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ced9-129">Next steps</span></span>

<span data-ttu-id="9ced9-130">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ced9-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9ced9-131">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9ced9-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
