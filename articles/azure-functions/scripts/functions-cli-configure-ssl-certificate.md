---
title: "aaaAzure CLI komut dosyası örneği - bağ özel SSL sertifika tooa işlevi uygulama | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - BIND özel SSL sertifika tooa işlevi uygulama azure'da"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="f39bb-103">Özel SSL sertifika tooa işlevi uygulama bağlama</span><span class="sxs-lookup"><span data-stu-id="f39bb-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="f39bb-104">Bu örnek betik bir işlev uygulaması App Service'te ile ilgili kaynaklarını oluşturur, ardından özel etki alanı adı tooit hello SSL sertifikasını bağlar.</span><span class="sxs-lookup"><span data-stu-id="f39bb-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="f39bb-105">Bu örnek için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="f39bb-105">For this sample, you need:</span></span>

* <span data-ttu-id="f39bb-106">Tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişin.</span><span class="sxs-lookup"><span data-stu-id="f39bb-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="f39bb-107">Geçerli. PFX dosyası ve kendi parolasını hello SSL sertifikası, tooupload istediğiniz ve bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f39bb-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="f39bb-108">bir SSL sertifikası toobind, işlevi uygulamanızı tüketim planı içinde değil, bir uygulama hizmeti planındaki oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f39bb-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f39bb-109">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f39bb-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f39bb-110">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="f39bb-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f39bb-111">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f39bb-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f39bb-112">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f39bb-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f39bb-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f39bb-113">Script explanation</span></span>

<span data-ttu-id="f39bb-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f39bb-114">This script uses hello following commands.</span></span> <span data-ttu-id="f39bb-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f39bb-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f39bb-116">Komut</span><span class="sxs-lookup"><span data-stu-id="f39bb-116">Command</span></span> | <span data-ttu-id="f39bb-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="f39bb-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f39bb-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39bb-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f39bb-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f39bb-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f39bb-120">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39bb-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f39bb-121">Bir uygulama hizmeti planı gerekli toobind SSL sertifikaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f39bb-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="f39bb-122">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39bb-122">az functionapp create</span></span>]() | <span data-ttu-id="f39bb-123">Bir işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f39bb-123">Creates a function app.</span></span> |
| [<span data-ttu-id="f39bb-124">az appservice web yapılandırma ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="f39bb-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="f39bb-125">Özel etki alanı toohello işlev uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="f39bb-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="f39bb-126">az appservice web yapılandırma ssl karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="f39bb-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="f39bb-127">Bir SSL sertifikası tooa işlevi uygulamayı yükler.</span><span class="sxs-lookup"><span data-stu-id="f39bb-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="f39bb-128">az appservice web yapılandırma ssl bağlama</span><span class="sxs-lookup"><span data-stu-id="f39bb-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="f39bb-129">Karşıya yüklenen bir SSL sertifikası tooa işlev uygulaması bağlar.</span><span class="sxs-lookup"><span data-stu-id="f39bb-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f39bb-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f39bb-130">Next steps</span></span>

<span data-ttu-id="f39bb-131">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f39bb-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f39bb-132">Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri]().</span><span class="sxs-lookup"><span data-stu-id="f39bb-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
