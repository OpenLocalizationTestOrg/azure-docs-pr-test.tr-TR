---
title: "aaaAzure MongoDB uygulamalar için CLI betik Get Azure Cosmos DB bağlantı dizesi | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Get Azure Cosmos DB bağlantı dizesi MongoDB uygulamalar için"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 9b0a4bf020039c9bf9554b4199a279622c15a15d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-hello-azure-cli"></a><span data-ttu-id="fea79-103">Hello Azure CLI kullanarak MongoDB uygulamaları için Azure Cosmos DB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="fea79-103">Get an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI</span></span>

<span data-ttu-id="fea79-104">Bu örnek hello Azure CLI kullanarak MongoDB uygulamaları için bir Azure Cosmos DB bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="fea79-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fea79-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fea79-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fea79-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="fea79-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fea79-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fea79-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fea79-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fea79-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fea79-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="fea79-109">Clean up deployment</span></span>

<span data-ttu-id="fea79-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="fea79-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fea79-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fea79-111">Script explanation</span></span>

<span data-ttu-id="fea79-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="fea79-112">This script uses hello following commands.</span></span> <span data-ttu-id="fea79-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="fea79-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fea79-114">Komut</span><span class="sxs-lookup"><span data-stu-id="fea79-114">Command</span></span> | <span data-ttu-id="fea79-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="fea79-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fea79-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fea79-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fea79-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fea79-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fea79-118">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fea79-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="fea79-119">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fea79-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="fea79-120">az cosmosdb listesi-bağlantı-dizeleri</span><span class="sxs-lookup"><span data-stu-id="fea79-120">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="fea79-121">Merhaba bağlantı dizesi hello hesabının alır.</span><span class="sxs-lookup"><span data-stu-id="fea79-121">Gets hello connection string for hello account.</span></span>|
| [<span data-ttu-id="fea79-122">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="fea79-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="fea79-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="fea79-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fea79-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fea79-124">Next steps</span></span>

<span data-ttu-id="fea79-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fea79-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fea79-126">Ek Azure Cosmos DB CLI kod örnekleri hello bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fea79-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
