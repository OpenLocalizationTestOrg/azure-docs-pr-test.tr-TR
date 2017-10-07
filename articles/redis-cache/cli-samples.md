---
title: "aaaAzure CLI Redis önbelleği örnekleri | Microsoft Docs"
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
ms.openlocfilehash: a2eb6f7267951faca599a43ff29b46beb05fea6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="c212b-103">Azure CLI örnekleri Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="c212b-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="c212b-104">Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure CLI kullanarak oluşturulan komut dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c212b-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="c212b-105">**Önbelleği oluşturma**</span><span class="sxs-lookup"><span data-stu-id="c212b-105">**Create cache**</span></span>||
| [<span data-ttu-id="c212b-106">Bir önbellek oluşturma</span><span class="sxs-lookup"><span data-stu-id="c212b-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="c212b-107">Bir kaynak grubu ve temel bir katman Azure Redis önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c212b-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="c212b-108">Kümeleme premium önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c212b-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="c212b-109">Bir kaynak grubu ve premium katmanı önbelleği kümeleme özelliği etkinleştirilmiş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c212b-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="c212b-110">Önbellek ayrıntıları alma</span><span class="sxs-lookup"><span data-stu-id="c212b-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="c212b-111">Sağlama durumu da dahil olmak üzere bir Azure Redis önbelleği örneğinin ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="c212b-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="c212b-112">Merhaba ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma</span><span class="sxs-lookup"><span data-stu-id="c212b-112">Get hello hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="c212b-113">Merhaba ana bilgisayar adı, bağlantı noktalarını ve anahtarları için bir Azure Redis önbelleği örneği alır.</span><span class="sxs-lookup"><span data-stu-id="c212b-113">Gets hello hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="c212b-114">**Web uygulaması artı önbelleği**</span><span class="sxs-lookup"><span data-stu-id="c212b-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="c212b-115">Bir web uygulaması tooa redis Önbelleği'ne bağlama</span><span class="sxs-lookup"><span data-stu-id="c212b-115">Connect a web app tooa redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="c212b-116">Azure web uygulaması ve redis önbelleği oluşturur, ardından hello redis bağlantı ayrıntıları toohello uygulama ayarlarını ekler.</span><span class="sxs-lookup"><span data-stu-id="c212b-116">Creates an Azure web app and a redis cache, then adds hello redis connection details toohello app settings.</span></span> |
|<span data-ttu-id="c212b-117">**Önbellek Sil**</span><span class="sxs-lookup"><span data-stu-id="c212b-117">**Delete cache**</span></span>||
| [<span data-ttu-id="c212b-118">Bir önbellek Sil</span><span class="sxs-lookup"><span data-stu-id="c212b-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="c212b-119">Bir Azure Redis önbelleği örneği siler</span><span class="sxs-lookup"><span data-stu-id="c212b-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="c212b-120">Azure CLI 2.0 hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c212b-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>