---
title: "Azure Cosmos DB aaaAzure PowerShell komut dosyası-Multiregion çoğaltma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Azure Cosmos DB için Multiregion çoğaltma"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="edc52-103">Birden çok bölgeye Azure Cosmos DB veritabanı hesabı çoğaltabilir ve yük devretme öncelikleri PowerShell kullanarak yapılandırmanız</span><span class="sxs-lookup"><span data-stu-id="edc52-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="edc52-104">Bu örnek, birden çok bölgelerdeki Azure Cosmos DB veritabanı hesabı herhangi bir tür yinelenir ve PowerShell kullanarak yük devretme öncelikleri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="edc52-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="edc52-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="edc52-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="edc52-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="edc52-106">Clean up deployment</span></span>

<span data-ttu-id="edc52-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="edc52-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="edc52-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="edc52-108">Script explanation</span></span>

<span data-ttu-id="edc52-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="edc52-109">This script uses hello following commands.</span></span> <span data-ttu-id="edc52-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="edc52-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="edc52-111">Komut</span><span class="sxs-lookup"><span data-stu-id="edc52-111">Command</span></span> | <span data-ttu-id="edc52-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="edc52-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="edc52-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="edc52-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="edc52-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc52-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="edc52-115">AzureRmResource yeni</span><span class="sxs-lookup"><span data-stu-id="edc52-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="edc52-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="edc52-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="edc52-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="edc52-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="edc52-118">Merhaba veritabanı hesabı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="edc52-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="edc52-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="edc52-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="edc52-120">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="edc52-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="edc52-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edc52-121">Next steps</span></span>

<span data-ttu-id="edc52-122">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="edc52-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="edc52-123">Ek Azure Cosmos DB PowerShell komut dosyası örnekleri hello bulunabilir [Azure Cosmos DB PowerShell komut dosyalarını](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="edc52-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
