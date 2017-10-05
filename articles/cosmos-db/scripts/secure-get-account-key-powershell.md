---
title: "Azure PowerShell Betiği Get hesabı anahtarları için cosmosdb | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Get hesap cosmosdb tuşları"
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
ms.openlocfilehash: 912e1af684c90cd84b6b00bacbc7dd8d4434c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="8aced-103">PowerShell kullanarak Azure Cosmos DB için hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="8aced-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="8aced-104">Bu örnek, her türlü Azure Cosmos DB hesabı için hesap anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="8aced-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8aced-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8aced-105">Sample script</span></span>

<span data-ttu-id="8aced-106">[!code-powershell[Ana](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "bir Azure Cosmos DB hesap anahtarı alma")]</span><span class="sxs-lookup"><span data-stu-id="8aced-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get the keys for an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8aced-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8aced-107">Clean up deployment</span></span>

<span data-ttu-id="8aced-108">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8aced-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8aced-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8aced-109">Script explanation</span></span>

<span data-ttu-id="8aced-110">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8aced-110">This script uses the following commands.</span></span> <span data-ttu-id="8aced-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="8aced-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8aced-112">Komut</span><span class="sxs-lookup"><span data-stu-id="8aced-112">Command</span></span> | <span data-ttu-id="8aced-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="8aced-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8aced-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8aced-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="8aced-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8aced-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8aced-116">AzureRmResource yeni</span><span class="sxs-lookup"><span data-stu-id="8aced-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="8aced-117">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8aced-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8aced-118">Çağırma AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="8aced-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="8aced-119">Azure CosmosDB hesabındaki bir eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="8aced-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="8aced-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8aced-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="8aced-121">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="8aced-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8aced-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8aced-122">Next steps</span></span>

<span data-ttu-id="8aced-123">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="8aced-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="8aced-124">Ek Azure Cosmos DB PowerShell komut dosyası örnekleri bulunabilir [Azure Cosmos DB PowerShell komut dosyalarını](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8aced-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>