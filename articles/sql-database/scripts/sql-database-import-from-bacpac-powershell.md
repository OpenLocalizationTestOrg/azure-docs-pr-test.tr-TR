---
title: "aaaPowerShell örnek alma bacpac dosya Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği tooimport bir bacpac bir SQL veritabanına döşeme"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="f38ae-103">Bir Azure SQL veritabanına PowerShell tooimport bir bacpac dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="f38ae-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="f38ae-104">Bu PowerShell Betiği örneği bir veritabanından içe aktaran bir **bacpac** bir Azure SQL veritabanı dosyasına.</span><span class="sxs-lookup"><span data-stu-id="f38ae-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f38ae-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f38ae-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f38ae-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f38ae-106">Clean up deployment</span></span>

<span data-ttu-id="f38ae-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f38ae-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f38ae-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f38ae-108">Script explanation</span></span>

<span data-ttu-id="f38ae-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f38ae-109">This script uses hello following commands.</span></span> <span data-ttu-id="f38ae-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f38ae-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f38ae-111">Komut</span><span class="sxs-lookup"><span data-stu-id="f38ae-111">Command</span></span> | <span data-ttu-id="f38ae-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="f38ae-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f38ae-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f38ae-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f38ae-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f38ae-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f38ae-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="f38ae-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f38ae-116">Konaklar SQL veritabanı hello mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f38ae-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="f38ae-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="f38ae-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="f38ae-118">Merhaba girilen IP adresi aralığından hello sunucusunda bir güvenlik duvarı kuralı tooallow erişim tooall SQL veritabanları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f38ae-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="f38ae-119">AzureRmSqlDatabaseImport yeni</span><span class="sxs-lookup"><span data-stu-id="f38ae-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="f38ae-120">İçeri aktarmalar .bacpac bir dosya ve hello sunucuda yeni bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f38ae-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="f38ae-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f38ae-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f38ae-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="f38ae-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f38ae-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f38ae-123">Next steps</span></span>

<span data-ttu-id="f38ae-124">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f38ae-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f38ae-125">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f38ae-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
