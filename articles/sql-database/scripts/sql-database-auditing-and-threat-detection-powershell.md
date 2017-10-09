---
title: "aaaPowerShell örnek denetim tehdit algılama-Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek komut dosyası tooconfigure denetim ve tehdit algılama bir Azure SQL veritabanı"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="8d378-103">PowerShell, tooconfigure SQL veritabanı denetim ve tehdit algılama kullanın</span><span class="sxs-lookup"><span data-stu-id="8d378-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="8d378-104">Bu PowerShell Betiği örneği SQL veritabanı denetim ve tehdit algılama yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8d378-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8d378-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8d378-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8d378-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8d378-106">Clean up deployment</span></span>

<span data-ttu-id="8d378-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d378-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8d378-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8d378-108">Script explanation</span></span>

<span data-ttu-id="8d378-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="8d378-109">This script uses hello following commands.</span></span> <span data-ttu-id="8d378-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="8d378-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8d378-111">Komut</span><span class="sxs-lookup"><span data-stu-id="8d378-111">Command</span></span> | <span data-ttu-id="8d378-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="8d378-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8d378-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d378-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8d378-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d378-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8d378-115">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="8d378-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8d378-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d378-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8d378-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8d378-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="8d378-118">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d378-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="8d378-119">Yeni-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="8d378-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="8d378-120">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d378-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="8d378-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="8d378-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="8d378-122">Bir veritabanı için Denetim İlkesi Hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8d378-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="8d378-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="8d378-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="8d378-124">Tehdit algılama İlkesi, bir veritabanı üzerinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8d378-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="8d378-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8d378-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8d378-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="8d378-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8d378-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d378-127">Next steps</span></span>

<span data-ttu-id="8d378-128">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8d378-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8d378-129">Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8d378-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
