---
title: "aaaAzure CLI komut dosyası örneği - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="520b4-103">Bir web uygulaması oluşturma ve yerel bir Git deposu koddan dağıtma</span><span class="sxs-lookup"><span data-stu-id="520b4-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="520b4-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve bir yerel Git deposu, web uygulama kodunuzda dağıtır.</span><span class="sxs-lookup"><span data-stu-id="520b4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="520b4-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="520b4-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="520b4-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="520b4-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="520b4-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="520b4-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="520b4-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="520b4-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="520b4-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="520b4-109">Script explanation</span></span>

<span data-ttu-id="520b4-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="520b4-110">This script uses hello following commands.</span></span> <span data-ttu-id="520b4-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="520b4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="520b4-112">Komut</span><span class="sxs-lookup"><span data-stu-id="520b4-112">Command</span></span> | <span data-ttu-id="520b4-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="520b4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="520b4-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="520b4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="520b4-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="520b4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="520b4-116">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="520b4-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="520b4-117">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="520b4-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="520b4-118">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="520b4-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="520b4-119">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="520b4-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="520b4-120">az webapp dağıtım kullanıcısı ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="520b4-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="520b4-121">Merhaba hesap düzeyinde dağıtım kimlik bilgileri App Service için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="520b4-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="520b4-122">az webapp dağıtım kaynağı config-yerel-git</span><span class="sxs-lookup"><span data-stu-id="520b4-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="520b4-123">Yerel bir Git deposu için bir kaynak denetimini yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="520b4-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="520b4-124">az webapp Gözat</span><span class="sxs-lookup"><span data-stu-id="520b4-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="520b4-125">Azure web uygulaması bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="520b4-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="520b4-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="520b4-126">Next steps</span></span>

<span data-ttu-id="520b4-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="520b4-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="520b4-128">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="520b4-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
