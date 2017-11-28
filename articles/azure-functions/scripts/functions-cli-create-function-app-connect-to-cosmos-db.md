---
title: "aaaCreate tooan Azure Cosmos DB bağlanan bir Azure işlevi | Microsoft Docs"
description: "Azure CLI betik örnek - tooan Azure Cosmos DB bağlanan bir Azure işlevi oluşturma"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="f00c5-103">Tooan Azure Cosmos DB bağlanan bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="f00c5-104">Bu örnek betik, bir Azure işlevi uygulaması oluşturur ve tooan Azure Cosmos DB veritabanı bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f00c5-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f00c5-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="f00c5-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f00c5-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f00c5-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f00c5-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f00c5-108">Sample script</span></span>

<span data-ttu-id="f00c5-109">Bu örnek bir Azure işlevi uygulamasını oluşturur ve bir Cosmos DB endpoint ve erişim anahtarı tooapp ayarları ekler.</span><span class="sxs-lookup"><span data-stu-id="f00c5-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f00c5-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f00c5-110">Clean up deployment</span></span>

<span data-ttu-id="f00c5-111">Hello komut dosyası örneği çalıştırdıktan sonra hello izleyin komutu kullanılan tooremove hello kaynak grubu olabilir ve tüm kaynakları ilgili.</span><span class="sxs-lookup"><span data-stu-id="f00c5-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f00c5-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f00c5-112">Script explanation</span></span>

<span data-ttu-id="f00c5-113">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-113">This script uses hello following commands.</span></span> <span data-ttu-id="f00c5-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f00c5-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f00c5-115">Komut</span><span class="sxs-lookup"><span data-stu-id="f00c5-115">Command</span></span> | <span data-ttu-id="f00c5-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="f00c5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f00c5-117">az oturum açma</span><span class="sxs-lookup"><span data-stu-id="f00c5-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="f00c5-118">Oturum açma tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f00c5-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="f00c5-119">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f00c5-120">Konumu ile kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="f00c5-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="f00c5-121">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="f00c5-122">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-122">Create a storage account</span></span> |
| [<span data-ttu-id="f00c5-123">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="f00c5-124">Yeni bir işlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-124">Create a new function app</span></span> |
| [<span data-ttu-id="f00c5-125">az documentdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="f00c5-126">Documentdb veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f00c5-126">Create documentdb database</span></span> |
| [<span data-ttu-id="f00c5-127">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f00c5-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f00c5-128">Temizleme</span><span class="sxs-lookup"><span data-stu-id="f00c5-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f00c5-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f00c5-129">Next steps</span></span>

<span data-ttu-id="f00c5-130">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f00c5-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f00c5-131">Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f00c5-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




