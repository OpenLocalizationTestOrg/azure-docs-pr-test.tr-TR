---
title: "aaaPowerShell örnek kopyası Azure SQL veritabanı yeni sunucu | Microsoft Docs"
description: "Azure PowerShell örnek betiği toocopy bir SQL veritabanı tooa yeni sunucusu"
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="d29e0-103">PowerShell toocopy bir SQL veritabanı tooa yeni sunucusuna kullanın</span><span class="sxs-lookup"><span data-stu-id="d29e0-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="d29e0-104">Bu PowerShell komut dosyası örnek yeni bir sunucu varolan bir veritabanının bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d29e0-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="d29e0-105">Veritabanı tooa yeni bir sunucu kopyalama</span><span class="sxs-lookup"><span data-stu-id="d29e0-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d29e0-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="d29e0-106">Clean up deployment</span></span>

<span data-ttu-id="d29e0-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="d29e0-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d29e0-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="d29e0-108">Script explanation</span></span>

<span data-ttu-id="d29e0-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="d29e0-109">This script uses hello following commands.</span></span> <span data-ttu-id="d29e0-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="d29e0-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d29e0-111">Komut</span><span class="sxs-lookup"><span data-stu-id="d29e0-111">Command</span></span> | <span data-ttu-id="d29e0-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="d29e0-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d29e0-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d29e0-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d29e0-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d29e0-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d29e0-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="d29e0-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d29e0-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d29e0-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d29e0-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d29e0-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="d29e0-118">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d29e0-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="d29e0-119">AzureRmSqlDatabaseCopy yeni</span><span class="sxs-lookup"><span data-stu-id="d29e0-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="d29e0-120">Merhaba geçerli saati hello anlık görüntü kullanan bir veritabanının bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d29e0-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="d29e0-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d29e0-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d29e0-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="d29e0-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d29e0-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d29e0-123">Next steps</span></span>

<span data-ttu-id="d29e0-124">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d29e0-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d29e0-125">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d29e0-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
