---
title: "Azure CLI betik örnek - bir web uygulaması Cosmos Veritabanına bağlanın | Microsoft Docs"
description: "Azure CLI betik örnek - bir web uygulaması Cosmos Veritabanına bağlanın"
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="0a914-103">Bir web uygulaması Cosmos Veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="0a914-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="0a914-104">Bu senaryoda, bir Azure Cosmos DB hesap ve bir Azure web uygulamasına nasıl oluşturulacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0a914-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="0a914-105">Daha sonra uygulama ayarları kullanarak web uygulaması Cosmos DB bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="0a914-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a914-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a914-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0a914-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0a914-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="0a914-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0a914-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0a914-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0a914-109">Sample script</span></span>

<span data-ttu-id="0a914-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="0a914-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0a914-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0a914-111">Script explanation</span></span>

<span data-ttu-id="0a914-112">Bu komut dosyasını bir kaynak grubu, web uygulaması Cosmos DB oluşturmak için aşağıdaki komutları kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="0a914-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="0a914-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="0a914-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0a914-114">Komut</span><span class="sxs-lookup"><span data-stu-id="0a914-114">Command</span></span> | <span data-ttu-id="0a914-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="0a914-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a914-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a914-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0a914-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a914-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0a914-118">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a914-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0a914-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a914-119">Creates an App Service plan.</span></span> <span data-ttu-id="0a914-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="0a914-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="0a914-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a914-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0a914-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a914-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0a914-123">az cosmosdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a914-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="0a914-124">Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a914-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="0a914-125">Veri depolanacağı budur.</span><span class="sxs-lookup"><span data-stu-id="0a914-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="0a914-126">az cosmosdb listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="0a914-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="0a914-127">Belirtilen Cosmos DB hesabı için erişim anahtarlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="0a914-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="0a914-128">az webapp config appsettings ayarlama</span><span class="sxs-lookup"><span data-stu-id="0a914-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="0a914-129">Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0a914-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="0a914-130">Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="0a914-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a914-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0a914-131">Next steps</span></span>

<span data-ttu-id="0a914-132">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a914-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0a914-133">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0a914-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
