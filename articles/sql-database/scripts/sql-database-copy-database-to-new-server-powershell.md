---
title: "PowerShell örnek kopyası Azure SQL veritabanı yeni sunucu | Microsoft Docs"
description: "Yeni bir sunucuya SQL veritabanına kopyalamak için azure PowerShell örnek betiği"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="fe0cf-103">Yeni bir sunucuya SQL veritabanına kopyalamak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="fe0cf-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="fe0cf-104">Bu PowerShell komut dosyası örnek yeni bir sunucu varolan bir veritabanının bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="fe0cf-105">Bir veritabanını yeni bir sunucuya kopyalayın</span><span class="sxs-lookup"><span data-stu-id="fe0cf-105">Copy a database to a new server</span></span>

<span data-ttu-id="fe0cf-106">[!code-powershell[Ana](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "kopyalama veritabanını yeni sunucuya")]</span><span class="sxs-lookup"><span data-stu-id="fe0cf-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fe0cf-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="fe0cf-107">Clean up deployment</span></span>

<span data-ttu-id="fe0cf-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fe0cf-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fe0cf-109">Script explanation</span></span>

<span data-ttu-id="fe0cf-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-110">This script uses the following commands.</span></span> <span data-ttu-id="fe0cf-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fe0cf-112">Komut</span><span class="sxs-lookup"><span data-stu-id="fe0cf-112">Command</span></span> | <span data-ttu-id="fe0cf-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="fe0cf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe0cf-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fe0cf-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fe0cf-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fe0cf-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="fe0cf-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fe0cf-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="fe0cf-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fe0cf-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="fe0cf-119">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="fe0cf-120">AzureRmSqlDatabaseCopy yeni</span><span class="sxs-lookup"><span data-stu-id="fe0cf-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="fe0cf-121">Anlık görüntü şu anda kullandığı bir veritabanının bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="fe0cf-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fe0cf-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fe0cf-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="fe0cf-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fe0cf-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe0cf-124">Next steps</span></span>

<span data-ttu-id="fe0cf-125">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe0cf-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fe0cf-126">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fe0cf-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
