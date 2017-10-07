---
title: "aaaAzure CLI komut dosyası örneği - bağ özel bir SSL sertifikası tooa web uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - BIND özel bir SSL sertifikası tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="91896-103">Özel SSL sertifika tooa web uygulama bağlama</span><span class="sxs-lookup"><span data-stu-id="91896-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="91896-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur, ardından özel etki alanı adı tooit hello SSL sertifikasını bağlar.</span><span class="sxs-lookup"><span data-stu-id="91896-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="91896-105">Bu örnek için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="91896-105">For this sample, you will need:</span></span>

* <span data-ttu-id="91896-106">Tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişin.</span><span class="sxs-lookup"><span data-stu-id="91896-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="91896-107">Geçerli. PFX dosyası ve kendi parolasını hello SSL sertifikası, tooupload istediğiniz ve bağlayın.</span><span class="sxs-lookup"><span data-stu-id="91896-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91896-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="91896-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91896-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="91896-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="91896-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91896-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="91896-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="91896-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="91896-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="91896-112">Script explanation</span></span>

<span data-ttu-id="91896-113">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="91896-113">This script uses hello following commands.</span></span> <span data-ttu-id="91896-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="91896-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="91896-115">Komut</span><span class="sxs-lookup"><span data-stu-id="91896-115">Command</span></span> | <span data-ttu-id="91896-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="91896-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91896-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="91896-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91896-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91896-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91896-119">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91896-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="91896-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91896-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="91896-121">az webapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="91896-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="91896-122">Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91896-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="91896-123">az webapp config ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="91896-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="91896-124">Bir özel etki alanı tooa web uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="91896-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="91896-125">az webapp config ssl karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="91896-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="91896-126">Bir SSL sertifikası tooa web uygulamasını yükler.</span><span class="sxs-lookup"><span data-stu-id="91896-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="91896-127">az webapp config ssl bağlama</span><span class="sxs-lookup"><span data-stu-id="91896-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="91896-128">Karşıya yüklenen bir SSL sertifikası tooa web uygulaması bağlar.</span><span class="sxs-lookup"><span data-stu-id="91896-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91896-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91896-129">Next steps</span></span>

<span data-ttu-id="91896-130">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91896-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91896-131">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91896-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
