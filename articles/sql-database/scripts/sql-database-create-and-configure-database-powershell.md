---
title: "Bir Azure SQL veritabanı PowerShell örnek-create | Microsoft Docs"
description: "Bir Azure SQL veritabanı oluşturmak için azure PowerShell örnek betiği"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="8d4c4-103">Tek bir Azure SQL veritabanı oluşturma ve bir güvenlik duvarı kuralı yapılandırmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="8d4c4-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="8d4c4-104">Bu PowerShell Betiği örnek bir Azure SQL veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="8d4c4-105">Betik başarılı şekilde gerçekleştirildikten sonra SQL veritabanı tüm Azure hizmetlerini ve yapılandırılan IP adresi erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8d4c4-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8d4c4-106">Sample script</span></span>

<span data-ttu-id="8d4c4-107">[!code-powershell[Ana](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "SQL veritabanı oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="8d4c4-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8d4c4-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8d4c4-108">Clean up deployment</span></span>

<span data-ttu-id="8d4c4-109">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8d4c4-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8d4c4-110">Script explanation</span></span>

<span data-ttu-id="8d4c4-111">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-111">This script uses the following commands.</span></span> <span data-ttu-id="8d4c4-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8d4c4-113">Komut</span><span class="sxs-lookup"><span data-stu-id="8d4c4-113">Command</span></span> | <span data-ttu-id="8d4c4-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d4c4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8d4c4-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d4c4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8d4c4-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8d4c4-117">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="8d4c4-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8d4c4-118">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8d4c4-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="8d4c4-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="8d4c4-120">Girilen IP adresi aralığından sunucusundaki tüm SQL veritabanlarına erişim sağlamak için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="8d4c4-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8d4c4-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="8d4c4-122">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="8d4c4-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d4c4-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8d4c4-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="8d4c4-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8d4c4-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d4c4-125">Next steps</span></span>

<span data-ttu-id="8d4c4-126">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8d4c4-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8d4c4-127">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8d4c4-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



