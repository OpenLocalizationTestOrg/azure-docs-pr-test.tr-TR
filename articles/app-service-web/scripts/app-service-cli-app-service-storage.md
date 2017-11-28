---
title: "aaaAzure CLI komut dosyası örneği - bağlantı bir web uygulaması tooa depolama hesabı | Microsoft Docs"
description: "Azure CLI betik örnek - bir web uygulaması tooa depolama hesabı Bağlan"
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
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="6c291-103">Bir web uygulaması tooa depolama hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="6c291-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="6c291-104">Bu senaryoda, nasıl toocreate bir Azure depolama hesabı ve bir Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6c291-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="6c291-105">Uygulama ayarları kullanarak hello depolama hesabı toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="6c291-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c291-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6c291-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6c291-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="6c291-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6c291-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c291-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="6c291-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6c291-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6c291-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6c291-110">Script explanation</span></span>

<span data-ttu-id="6c291-111">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması, depolama hesabı ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="6c291-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="6c291-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="6c291-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c291-113">Komut</span><span class="sxs-lookup"><span data-stu-id="6c291-113">Command</span></span> | <span data-ttu-id="6c291-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="6c291-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c291-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c291-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c291-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c291-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c291-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c291-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6c291-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c291-118">Creates an App Service plan.</span></span> <span data-ttu-id="6c291-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="6c291-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6c291-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c291-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6c291-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c291-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6c291-122">az depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c291-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="6c291-123">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c291-123">Creates a storage account.</span></span> <span data-ttu-id="6c291-124">Merhaba statik varlıklar depolanacağı budur.</span><span class="sxs-lookup"><span data-stu-id="6c291-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="6c291-125">az depolama hesabı Göster-bağlantı-dizesi</span><span class="sxs-lookup"><span data-stu-id="6c291-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="6c291-126">az webapp config appsettings ayarlama</span><span class="sxs-lookup"><span data-stu-id="6c291-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="6c291-127">Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="6c291-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="6c291-128">Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="6c291-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c291-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c291-129">Next steps</span></span>

<span data-ttu-id="6c291-130">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c291-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c291-131">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c291-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
