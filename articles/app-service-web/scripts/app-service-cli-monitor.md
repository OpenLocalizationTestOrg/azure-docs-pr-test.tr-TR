---
title: "aaaAzure CLI komut dosyası örneği - web sunucu günlükleri ile bir web uygulaması izleme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - İzleyici web sunucu günlükleri ile bir web uygulaması"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="52c7c-103">Web sunucu günlükleri ile bir web uygulaması izleme</span><span class="sxs-lookup"><span data-stu-id="52c7c-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="52c7c-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı, web uygulaması oluşturun ve hello web uygulama tooenable web sunucu günlükleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="52c7c-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="52c7c-105">Daha sonra gözden geçirme için hello günlük dosyalarını indirir.</span><span class="sxs-lookup"><span data-stu-id="52c7c-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="52c7c-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52c7c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="52c7c-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="52c7c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="52c7c-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52c7c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="52c7c-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="52c7c-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="52c7c-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="52c7c-110">Script explanation</span></span>

<span data-ttu-id="52c7c-111">Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması ve tüm ilişkili kaynakları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="52c7c-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="52c7c-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="52c7c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="52c7c-113">Komut</span><span class="sxs-lookup"><span data-stu-id="52c7c-113">Command</span></span> | <span data-ttu-id="52c7c-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="52c7c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52c7c-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="52c7c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="52c7c-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="52c7c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="52c7c-117">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="52c7c-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="52c7c-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="52c7c-118">Creates an App Service plan.</span></span> <span data-ttu-id="52c7c-119">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="52c7c-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="52c7c-120">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="52c7c-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="52c7c-121">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="52c7c-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="52c7c-122">az webapp günlüğünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="52c7c-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="52c7c-123">Azure web uygulaması korunur hangi günlüklerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="52c7c-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="52c7c-124">az webapp oturum indirme</span><span class="sxs-lookup"><span data-stu-id="52c7c-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="52c7c-125">İndirmeler hello Merhaba bir Azure web uygulaması tooyour yerel makine günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="52c7c-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52c7c-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52c7c-126">Next steps</span></span>

<span data-ttu-id="52c7c-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52c7c-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="52c7c-128">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="52c7c-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
