---
title: "bir Azure SQL veritabanı aaaPowerShell örnek-create | Microsoft Docs"
description: "Azure PowerShell örnek betiği toocreate bir Azure SQL veritabanı"
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
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="64a83-103">PowerShell toocreate tek bir Azure SQL veritabanı kullanın ve bir güvenlik duvarı kuralı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="64a83-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="64a83-104">Bu PowerShell Betiği örnek bir Azure SQL veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="64a83-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="64a83-105">Hello betik başarılı şekilde gerçekleştirildikten sonra SQL veritabanı tüm Azure hizmetlerinden erişilebilir hello ve başlangıç IP adresi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="64a83-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="64a83-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="64a83-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="64a83-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="64a83-107">Clean up deployment</span></span>

<span data-ttu-id="64a83-108">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="64a83-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="64a83-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="64a83-109">Script explanation</span></span>

<span data-ttu-id="64a83-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="64a83-110">This script uses hello following commands.</span></span> <span data-ttu-id="64a83-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="64a83-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="64a83-112">Komut</span><span class="sxs-lookup"><span data-stu-id="64a83-112">Command</span></span> | <span data-ttu-id="64a83-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="64a83-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="64a83-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="64a83-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="64a83-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64a83-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="64a83-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="64a83-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="64a83-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64a83-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="64a83-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="64a83-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="64a83-119">Merhaba girilen IP adresi aralığından hello sunucusunda bir güvenlik duvarı kuralı tooallow erişim tooall SQL veritabanları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64a83-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="64a83-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="64a83-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="64a83-121">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64a83-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="64a83-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="64a83-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="64a83-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="64a83-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="64a83-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64a83-124">Next steps</span></span>

<span data-ttu-id="64a83-125">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64a83-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="64a83-126">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="64a83-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



