---
title: "PowerShell örnek alma bacpac dosya Azure SQL veritabanı | Microsoft Docs"
description: "Bir bacpac döşeme bir SQL veritabanına aktarmak için azure PowerShell örnek betiği"
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="638f3-103">Bir Azure SQL veritabanına bir bacpac dosya aktarmak için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="638f3-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="638f3-104">Bu PowerShell Betiği örneği bir veritabanından içe aktaran bir **bacpac** bir Azure SQL veritabanı dosyasına.</span><span class="sxs-lookup"><span data-stu-id="638f3-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="638f3-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="638f3-105">Sample script</span></span>

<span data-ttu-id="638f3-106">[!code-powershell[Ana](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "SQL veritabanı oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="638f3-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="638f3-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="638f3-107">Clean up deployment</span></span>

<span data-ttu-id="638f3-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="638f3-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="638f3-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="638f3-109">Script explanation</span></span>

<span data-ttu-id="638f3-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="638f3-110">This script uses the following commands.</span></span> <span data-ttu-id="638f3-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="638f3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="638f3-112">Komut</span><span class="sxs-lookup"><span data-stu-id="638f3-112">Command</span></span> | <span data-ttu-id="638f3-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="638f3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="638f3-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="638f3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="638f3-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="638f3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="638f3-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="638f3-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="638f3-117">SQL veritabanı barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="638f3-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="638f3-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="638f3-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="638f3-119">Girilen IP adresi aralığından sunucusundaki tüm SQL veritabanlarına erişim sağlamak için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="638f3-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="638f3-120">AzureRmSqlDatabaseImport yeni</span><span class="sxs-lookup"><span data-stu-id="638f3-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="638f3-121">İçeri aktarmalar .bacpac bir dosya ve sunucuda yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="638f3-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="638f3-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="638f3-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="638f3-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="638f3-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="638f3-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="638f3-124">Next steps</span></span>

<span data-ttu-id="638f3-125">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="638f3-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="638f3-126">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="638f3-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
