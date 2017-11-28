---
title: "Azure CLI komut dosyası örneği - özel bir SSL sertifikası bir işlev uygulaması bağlama | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bağ azure'da bir işlev uygulaması için özel bir SSL sertifikası"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="a9fb1-103">Bir işlev uygulaması için özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="a9fb1-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="a9fb1-104">Bu örnek betik bir işlev uygulaması App Service'te ile ilgili kaynaklarını oluşturur, ardından özel etki alanı adı SSL sertifikası kendisine bağlar.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="a9fb1-105">Bu örnek için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="a9fb1-105">For this sample, you need:</span></span>

* <span data-ttu-id="a9fb1-106">Etki alanı kayıt şirketinizin DNS yapılandırma sayfasına erişim.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="a9fb1-107">Geçerli. PFX dosyası ve SSL sertifikasının parolası karşıya yüklemek ve bağlamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="a9fb1-108">Bir SSL sertifikası bağlamak için işlevi uygulamanıza bir uygulama hizmeti planı yer alan ve tüketim planı oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9fb1-109">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9fb1-110">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="a9fb1-111">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9fb1-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a9fb1-112">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a9fb1-112">Sample script</span></span>

<span data-ttu-id="a9fb1-113">[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "bir web uygulaması için özel bir SSL sertifikası bağlama")]</span><span class="sxs-lookup"><span data-stu-id="a9fb1-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a9fb1-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a9fb1-114">Script explanation</span></span>

<span data-ttu-id="a9fb1-115">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-115">This script uses the following commands.</span></span> <span data-ttu-id="a9fb1-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a9fb1-117">Komut</span><span class="sxs-lookup"><span data-stu-id="a9fb1-117">Command</span></span> | <span data-ttu-id="a9fb1-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="a9fb1-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9fb1-119">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fb1-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a9fb1-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9fb1-121">az uygulama hizmeti planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fb1-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a9fb1-122">SSL sertifikaları bağlamak için gerekli bir uygulama hizmeti planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="a9fb1-123">az functionapp oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9fb1-123">az functionapp create</span></span>]() | <span data-ttu-id="a9fb1-124">Bir işlev uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-124">Creates a function app.</span></span> |
| [<span data-ttu-id="a9fb1-125">az appservice web yapılandırma ana bilgisayar adı ekleyin</span><span class="sxs-lookup"><span data-stu-id="a9fb1-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="a9fb1-126">Özel bir etki alanı işlev uygulaması eşler.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="a9fb1-127">az appservice web yapılandırma ssl karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="a9fb1-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="a9fb1-128">Bir SSL sertifikası bir işlev uygulaması yükler.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="a9fb1-129">az appservice web yapılandırma ssl bağlama</span><span class="sxs-lookup"><span data-stu-id="a9fb1-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="a9fb1-130">Karşıya yüklenen bir SSL sertifikası bir işlev uygulaması bağlar.</span><span class="sxs-lookup"><span data-stu-id="a9fb1-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9fb1-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9fb1-131">Next steps</span></span>

<span data-ttu-id="a9fb1-132">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9fb1-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9fb1-133">Ek uygulama hizmeti CLI kod örnekleri bulunabilir [Azure App Service belgeleri]().</span><span class="sxs-lookup"><span data-stu-id="a9fb1-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
