---
title: "PowerShell komut dosyası Get Azure Cosmos DB bağlantı dizesi MongoDB uygulamalar için aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Get Azure Cosmos DB bağlantı dizesi MongoDB uygulamalar için"
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
ms.openlocfilehash: d04502b8f59bb6f3cb8bec696595f962b479fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="b3c29-103">PowerShell kullanarak MongoDB uygulamaları için Azure Cosmos DB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="b3c29-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="b3c29-104">Bu örnek bir PowerShell kullanarak MongoDB uygulamaları için Azure Cosmos DB bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="b3c29-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b3c29-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b3c29-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get hello MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b3c29-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="b3c29-106">Clean up deployment</span></span>

<span data-ttu-id="b3c29-107">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b3c29-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b3c29-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b3c29-108">Script explanation</span></span>

<span data-ttu-id="b3c29-109">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3c29-109">This script uses hello following commands.</span></span> <span data-ttu-id="b3c29-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="b3c29-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b3c29-111">Komut</span><span class="sxs-lookup"><span data-stu-id="b3c29-111">Command</span></span> | <span data-ttu-id="b3c29-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="b3c29-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3c29-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3c29-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="b3c29-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3c29-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3c29-115">AzureRmResource yeni</span><span class="sxs-lookup"><span data-stu-id="b3c29-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="b3c29-116">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3c29-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b3c29-117">Çağırma AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="b3c29-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="b3c29-118">Hello Azure CosmosDB hesabı eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="b3c29-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="b3c29-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3c29-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="b3c29-120">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="b3c29-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b3c29-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3c29-121">Next steps</span></span>

<span data-ttu-id="b3c29-122">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="b3c29-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="b3c29-123">Ek Azure Cosmos DB PowerShell komut dosyası örnekleri hello bulunabilir [Azure Cosmos DB PowerShell komut dosyalarını](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3c29-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
