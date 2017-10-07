---
title: "aaaAzure CLI komut dosyası örneği - web uygulama tooa redis önbelleği bağlanma | Microsoft Docs"
description: "Azure CLI betik örnek - web uygulama tooa redis önbelleği Bağlan"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="e4c45-103">Bir web uygulaması tooa redis Önbelleği'ne bağlama</span><span class="sxs-lookup"><span data-stu-id="e4c45-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="e4c45-104">Bu senaryoda, nasıl toocreate bir Azure redis önbelleği ve Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e4c45-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="e4c45-105">Uygulama ayarları kullanarak hello redis önbelleği toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="e4c45-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e4c45-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e4c45-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e4c45-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e4c45-107">Script explanation</span></span>

<span data-ttu-id="e4c45-108">Bu komut dosyası toocreate bir kaynak grubu web uygulamasını redis önbelleği ve tüm ilişkili kaynakları komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4c45-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="e4c45-109">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="e4c45-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e4c45-110">Komut</span><span class="sxs-lookup"><span data-stu-id="e4c45-110">Command</span></span> | <span data-ttu-id="e4c45-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="e4c45-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4c45-112">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4c45-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e4c45-113">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4c45-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e4c45-114">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4c45-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e4c45-115">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4c45-115">Creates an App Service plan.</span></span> <span data-ttu-id="e4c45-116">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="e4c45-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e4c45-117">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4c45-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e4c45-118">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4c45-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e4c45-119">az redis oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4c45-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="e4c45-120">Yeni Redis önbelleği örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4c45-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="e4c45-121">Merhaba veri depolanacağı budur.</span><span class="sxs-lookup"><span data-stu-id="e4c45-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="e4c45-122">az redis listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="e4c45-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="e4c45-123">Merhaba redis önbelleği örneği Hello erişim anahtarlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="e4c45-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="e4c45-124">az webapp config appsettings ayarlama</span><span class="sxs-lookup"><span data-stu-id="e4c45-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="e4c45-125">Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4c45-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="e4c45-126">Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="e4c45-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4c45-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4c45-127">Next steps</span></span>

<span data-ttu-id="e4c45-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4c45-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e4c45-129">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e4c45-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
