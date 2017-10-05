---
title: "Bir Azure Cosmos DB'ye bağlanacak bir Azure işlevi oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir Azure Cosmos DB'ye bağlanacak bir Azure işlevi oluşturma"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="62b04-103">Bir Azure Cosmos DB'ye bağlanacak bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="62b04-104">Bu örnek betik Azure işlev uygulaması oluşturur ve bir Azure Cosmos DB veritabanına bağlar.</span><span class="sxs-lookup"><span data-stu-id="62b04-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="62b04-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="62b04-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="62b04-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62b04-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="62b04-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62b04-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="62b04-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="62b04-108">Sample script</span></span>

<span data-ttu-id="62b04-109">Bu örnek bir Azure işlev uygulaması oluşturur ve uygulama ayarlarını Cosmos DB uç noktası ve erişim anahtarı ekler.</span><span class="sxs-lookup"><span data-stu-id="62b04-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="62b04-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "bir Azure Cosmos DB'ye bağlanacak bir Azure işlevi oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="62b04-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="62b04-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="62b04-111">Clean up deployment</span></span>

<span data-ttu-id="62b04-112">Komut dosyası örneği çalıştırdıktan sonra kaynak grubunu kaldırmak için izleme komut kullanılabilir ve tüm kaynakları ilgili.</span><span class="sxs-lookup"><span data-stu-id="62b04-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="62b04-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="62b04-113">Script explanation</span></span>

<span data-ttu-id="62b04-114">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="62b04-114">This script uses the following commands.</span></span> <span data-ttu-id="62b04-115">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="62b04-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="62b04-116">Komut</span><span class="sxs-lookup"><span data-stu-id="62b04-116">Command</span></span> | <span data-ttu-id="62b04-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="62b04-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62b04-118">az oturum açma</span><span class="sxs-lookup"><span data-stu-id="62b04-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="62b04-119">Azure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="62b04-119">Login to Azure.</span></span> |
| [<span data-ttu-id="62b04-120">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62b04-121">Konumu ile kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="62b04-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="62b04-122">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="62b04-123">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-123">Create a storage account</span></span> |
| [<span data-ttu-id="62b04-124">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="62b04-125">Yeni bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-125">Create a new function app</span></span> |
| [<span data-ttu-id="62b04-126">az documentdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="62b04-127">Documentdb veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62b04-127">Create documentdb database</span></span> |
| [<span data-ttu-id="62b04-128">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="62b04-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="62b04-129">Temizleme</span><span class="sxs-lookup"><span data-stu-id="62b04-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62b04-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62b04-130">Next steps</span></span>

<span data-ttu-id="62b04-131">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62b04-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62b04-132">Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="62b04-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




