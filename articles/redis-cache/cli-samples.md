---
title: "Azure CLI Redis önbelleği örnekleri | Microsoft Docs"
description: "Azure Redis önbelleği için Azure CLI örneklerini içerir."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="4d898-103">Azure CLI örnekleri Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="4d898-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="4d898-104">Aşağıdaki tabloda Azure CLI kullanarak oluşturulan komut dosyalarını bash bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="4d898-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="4d898-105">**Önbelleği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4d898-105">**Create cache**</span></span>||
| [<span data-ttu-id="4d898-106">Bir önbellek oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d898-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="4d898-107">Bir kaynak grubu ve temel bir katman Azure Redis önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4d898-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="4d898-108">Kümeleme premium önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d898-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="4d898-109">Bir kaynak grubu ve premium katmanı önbelleği kümeleme özelliği etkinleştirilmiş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4d898-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="4d898-110">Önbellek ayrıntıları alma</span><span class="sxs-lookup"><span data-stu-id="4d898-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="4d898-111">Sağlama durumu da dahil olmak üzere bir Azure Redis önbelleği örneğinin ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="4d898-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="4d898-112">Ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma</span><span class="sxs-lookup"><span data-stu-id="4d898-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="4d898-113">Ana bilgisayar adı, bağlantı noktalarını ve anahtarları için bir Azure Redis önbelleği örneği alır.</span><span class="sxs-lookup"><span data-stu-id="4d898-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="4d898-114">**Web uygulaması artı önbelleği**</span><span class="sxs-lookup"><span data-stu-id="4d898-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="4d898-115">Bir web uygulamasını redis önbelleği için bağlama</span><span class="sxs-lookup"><span data-stu-id="4d898-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="4d898-116">Azure web uygulaması ve redis önbelleği oluşturur, ardından redis bağlantı ayrıntıları için uygulama ayarları ekler.</span><span class="sxs-lookup"><span data-stu-id="4d898-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="4d898-117">**Önbellek Sil**</span><span class="sxs-lookup"><span data-stu-id="4d898-117">**Delete cache**</span></span>||
| [<span data-ttu-id="4d898-118">Bir önbellek Sil</span><span class="sxs-lookup"><span data-stu-id="4d898-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="4d898-119">Bir Azure Redis önbelleği örneği siler</span><span class="sxs-lookup"><span data-stu-id="4d898-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="4d898-120">Azure CLI 2.0 hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4d898-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>