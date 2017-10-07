---
title: "aaaAzure CLI betik Get hesabı anahtarları için Azure Cosmos DB | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Get hesabı Azure Cosmos DB tuşları"
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
ms.openlocfilehash: d6462b3eebc8bc6935a6fa07dcae37a33e5f382e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-hello-azure-cli"></a><span data-ttu-id="99879-103">Hello Azure CLI kullanarak Azure Cosmos DB için hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="99879-103">Get account keys for Azure Cosmos DB using hello Azure CLI</span></span>

<span data-ttu-id="99879-104">Bu örnek, her türlü Azure Cosmos DB hesabı için hesap anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="99879-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="99879-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="99879-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="99879-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="99879-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="99879-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="99879-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="99879-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="99879-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="99879-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="99879-109">Clean up deployment</span></span>

<span data-ttu-id="99879-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="99879-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="99879-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="99879-111">Script explanation</span></span>

<span data-ttu-id="99879-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="99879-112">This script uses hello following commands.</span></span> <span data-ttu-id="99879-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="99879-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="99879-114">Komut</span><span class="sxs-lookup"><span data-stu-id="99879-114">Command</span></span> | <span data-ttu-id="99879-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="99879-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="99879-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="99879-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="99879-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99879-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="99879-118">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="99879-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="99879-119">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="99879-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="99879-120">az cosmosdb listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="99879-120">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="99879-121">Konaklar SQL veritabanı hello mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99879-121">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="99879-122">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="99879-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="99879-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="99879-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99879-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99879-124">Next steps</span></span>

<span data-ttu-id="99879-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="99879-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="99879-126">Ek Azure Cosmos DB CLI kod örnekleri hello bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="99879-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
