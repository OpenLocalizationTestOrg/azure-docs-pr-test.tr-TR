---
title: "Azure CLI komut dosyası örneği - İzleyici web sunucu günlükleri ile bir web uygulaması | Microsoft Docs"
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
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="fc6d1-103">Web sunucu günlükleri ile bir web uygulaması izleme</span><span class="sxs-lookup"><span data-stu-id="fc6d1-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="fc6d1-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı, web uygulaması oluşturmak ve web sunucusu günlüklerini etkinleştirmek için web uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="fc6d1-105">Ardından, gözden geçirme için günlük dosyalarını indirir.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc6d1-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fc6d1-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="fc6d1-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fc6d1-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fc6d1-109">Sample script</span></span>

<span data-ttu-id="fc6d1-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "izleme günlükleri")]</span><span class="sxs-lookup"><span data-stu-id="fc6d1-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fc6d1-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fc6d1-111">Script explanation</span></span>

<span data-ttu-id="fc6d1-112">Bu komut, bir kaynak grubu, web uygulaması ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="fc6d1-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fc6d1-114">Komut</span><span class="sxs-lookup"><span data-stu-id="fc6d1-114">Command</span></span> | <span data-ttu-id="fc6d1-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="fc6d1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc6d1-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc6d1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc6d1-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc6d1-118">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc6d1-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fc6d1-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-119">Creates an App Service plan.</span></span> <span data-ttu-id="fc6d1-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="fc6d1-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc6d1-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fc6d1-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fc6d1-123">az webapp günlüğünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fc6d1-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="fc6d1-124">Azure web uygulaması korunur hangi günlüklerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="fc6d1-125">az webapp oturum indirme</span><span class="sxs-lookup"><span data-stu-id="fc6d1-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="fc6d1-126">Günlüklerini indirmeleri yerel makinenize Azure web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc6d1-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc6d1-127">Next steps</span></span>

<span data-ttu-id="fc6d1-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc6d1-129">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
