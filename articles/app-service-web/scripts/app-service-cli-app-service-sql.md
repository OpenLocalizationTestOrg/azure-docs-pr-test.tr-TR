---
title: "aaaAzure CLI komut dosyası örneği - web uygulama tooa SQL veritabanına bağlanma | Microsoft Docs"
description: "Azure CLI betik örnek - web uygulama tooa SQL veritabanına bağlan"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="46eb1-103">Web uygulaması tooa SQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="46eb1-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="46eb1-104">Bu senaryoda, nasıl toocreate bir Azure SQL veritabanı ve bir Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="46eb1-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="46eb1-105">Uygulama ayarları kullanarak hello SQL veritabanı toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="46eb1-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="46eb1-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="46eb1-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="46eb1-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="46eb1-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="46eb1-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46eb1-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="46eb1-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="46eb1-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="46eb1-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="46eb1-110">Script explanation</span></span>

<span data-ttu-id="46eb1-111">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması, SQL veritabanı ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="46eb1-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="46eb1-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="46eb1-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="46eb1-113">Komut</span><span class="sxs-lookup"><span data-stu-id="46eb1-113">Command</span></span> | <span data-ttu-id="46eb1-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="46eb1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="46eb1-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="46eb1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="46eb1-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="46eb1-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="46eb1-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="46eb1-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-118">Creates an App Service plan.</span></span> <span data-ttu-id="46eb1-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="46eb1-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="46eb1-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="46eb1-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="46eb1-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="46eb1-122">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="46eb1-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="46eb1-123">Bir SQL veritabanı sunucusuna oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="46eb1-124">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="46eb1-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="46eb1-125">SQL veritabanı sunucusuna hello ile yeni bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="46eb1-126">az webapp config appsettings ayarlama</span><span class="sxs-lookup"><span data-stu-id="46eb1-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="46eb1-127">Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="46eb1-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="46eb1-128">Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="46eb1-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="46eb1-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46eb1-129">Next steps</span></span>

<span data-ttu-id="46eb1-130">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="46eb1-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="46eb1-131">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="46eb1-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
