---
title: "aaaAzure CLI komut dosyası örneği - web uygulama tooCosmos DB bağlanma | Microsoft Docs"
description: "Azure CLI betik örnek - web uygulama tooCosmos DB Bağlan"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="e0903-103">Bir web uygulaması tooCosmos DB Bağlan</span><span class="sxs-lookup"><span data-stu-id="e0903-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="e0903-104">Bu senaryoda, nasıl toocreate Azure Cosmos DB hesabınız ve Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e0903-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="e0903-105">Uygulama ayarları kullanarak hello Cosmos DB toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="e0903-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e0903-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e0903-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e0903-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e0903-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e0903-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e0903-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e0903-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e0903-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e0903-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e0903-110">Script explanation</span></span>

<span data-ttu-id="e0903-111">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması, Cosmos DB ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0903-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="e0903-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="e0903-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e0903-113">Komut</span><span class="sxs-lookup"><span data-stu-id="e0903-113">Command</span></span> | <span data-ttu-id="e0903-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="e0903-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0903-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0903-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e0903-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0903-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0903-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0903-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e0903-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0903-118">Creates an App Service plan.</span></span> <span data-ttu-id="e0903-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="e0903-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e0903-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0903-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e0903-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0903-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e0903-122">az cosmosdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0903-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="e0903-123">Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0903-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="e0903-124">Merhaba veri depolanacağı budur.</span><span class="sxs-lookup"><span data-stu-id="e0903-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="e0903-125">az cosmosdb listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="e0903-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="e0903-126">Belirtilen Cosmos DB hesaba hello hello erişim anahtarlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="e0903-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="e0903-127">az webapp config appsettings ayarlama</span><span class="sxs-lookup"><span data-stu-id="e0903-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="e0903-128">Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e0903-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="e0903-129">Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="e0903-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0903-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0903-130">Next steps</span></span>

<span data-ttu-id="e0903-131">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0903-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e0903-132">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e0903-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
