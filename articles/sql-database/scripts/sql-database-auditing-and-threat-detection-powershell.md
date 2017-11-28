---
title: "PowerShell örnek denetim tehdit algılaması Azure SQL veritabanı | Microsoft Docs"
description: "Bir Azure SQL veritabanı'nda denetim ve tehdit algılama yapılandırmak için azure PowerShell örnek betiği"
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="90dca-103">SQL veritabanı denetim ve tehdit algılama yapılandırmak için PowerShell kullanın</span><span class="sxs-lookup"><span data-stu-id="90dca-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="90dca-104">Bu PowerShell Betiği örneği SQL veritabanı denetim ve tehdit algılama yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="90dca-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="90dca-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="90dca-105">Sample script</span></span>

<span data-ttu-id="90dca-106">[!code-powershell[Ana](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "denetim ve tehdit algılama yapılandırın")]</span><span class="sxs-lookup"><span data-stu-id="90dca-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="90dca-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="90dca-107">Clean up deployment</span></span>

<span data-ttu-id="90dca-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="90dca-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="90dca-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="90dca-109">Script explanation</span></span>

<span data-ttu-id="90dca-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="90dca-110">This script uses the following commands.</span></span> <span data-ttu-id="90dca-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="90dca-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="90dca-112">Komut</span><span class="sxs-lookup"><span data-stu-id="90dca-112">Command</span></span> | <span data-ttu-id="90dca-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="90dca-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="90dca-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="90dca-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="90dca-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90dca-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="90dca-116">AzureRmSqlServer yeni</span><span class="sxs-lookup"><span data-stu-id="90dca-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="90dca-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90dca-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="90dca-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="90dca-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="90dca-119">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90dca-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="90dca-120">Yeni-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="90dca-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="90dca-121">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90dca-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="90dca-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="90dca-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="90dca-123">Bir veritabanı için Denetim İlkesi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="90dca-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="90dca-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="90dca-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="90dca-125">Tehdit algılama İlkesi, bir veritabanı üzerinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="90dca-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="90dca-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="90dca-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="90dca-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="90dca-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="90dca-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90dca-128">Next steps</span></span>

<span data-ttu-id="90dca-129">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="90dca-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="90dca-130">Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="90dca-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
