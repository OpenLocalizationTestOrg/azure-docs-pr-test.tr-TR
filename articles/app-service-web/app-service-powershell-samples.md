---
title: "aaaAzure PowerShell örnekleri - App Service | Microsoft Docs"
description: "Azure PowerShell örnekleri - uygulama hizmeti"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b7b4a030364f797195522c56fbae5b7f530d4d1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="1ca12-103">Azure PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="1ca12-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="1ca12-104">Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure PowerShell kullanılarak oluşturulan komut dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1ca12-104">hello following table includes links toobash scripts built using hello Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="1ca12-105">**Uygulama oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1ca12-105">**Create app**</span></span>||
| [<span data-ttu-id="1ca12-106">Github'dan dağıtımı ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca12-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-107">Kod Github'dan çeken bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca12-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="1ca12-108">GitHub’dan sürekli dağıtım ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca12-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-109">Sürekli olarak kod github'dan dağıtan bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca12-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="1ca12-110">Bir web uygulaması oluşturma ve FTP koduyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="1ca12-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-111">Bir Azure web app ve karşıya yükleme dosyaları FTP kullanarak yerel bir dizinden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca12-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="1ca12-112">Yerel Git deposundan web uygulaması oluşturma ve kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="1ca12-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-113">Azure web uygulaması oluşturur ve kodun bir yerel Git deposundan yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="1ca12-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="1ca12-114">Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma</span><span class="sxs-lookup"><span data-stu-id="1ca12-114">Create a web app and deploy code tooa staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-115">Kod değişiklikleri hazırlama için bir dağıtım yuvası ile bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca12-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="1ca12-116">**Uygulamayı yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="1ca12-116">**Configure app**</span></span>||
| [<span data-ttu-id="1ca12-117">Bir özel etki alanı tooa web uygulaması eşleme</span><span class="sxs-lookup"><span data-stu-id="1ca12-117">Map a custom domain tooa web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-118">Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit eşler.</span><span class="sxs-lookup"><span data-stu-id="1ca12-118">Creates an Azure web app and maps a custom domain name tooit.</span></span> |
| [<span data-ttu-id="1ca12-119">Özel SSL sertifika tooa web uygulama bağlama</span><span class="sxs-lookup"><span data-stu-id="1ca12-119">Bind a custom SSL certificate tooa web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-120">Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit hello SSL sertifikasını bağlar.</span><span class="sxs-lookup"><span data-stu-id="1ca12-120">Creates an Azure web app and binds hello SSL certificate of a custom domain name tooit.</span></span> |
|<span data-ttu-id="1ca12-121">**Ölçek uygulama**</span><span class="sxs-lookup"><span data-stu-id="1ca12-121">**Scale app**</span></span>||
| [<span data-ttu-id="1ca12-122">Web uygulamasını el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ca12-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-123">Azure web uygulaması oluşturur ve bunu 2 örneklerinde ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="1ca12-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="1ca12-124">Web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1ca12-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-125">İki farklı coğrafi bölgelerde iki Azure web uygulamaları oluşturur ve bunları Azure trafik Yöneticisi'ni kullanarak tek bir uç noktası aracılığıyla kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="1ca12-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="1ca12-126">**Uygulama tooresources Bağlan**</span><span class="sxs-lookup"><span data-stu-id="1ca12-126">**Connect app tooresources**</span></span>||
| [<span data-ttu-id="1ca12-127">Bir web uygulaması tooa SQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="1ca12-127">Connect a web app tooa SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-128">Azure web uygulaması ve SQL veritabanı oluşturur ve ardından hello veritabanı bağlantı dizesi toohello uygulama ayarlarını ekler.</span><span class="sxs-lookup"><span data-stu-id="1ca12-128">Creates an Azure web app and a SQL database, then adds hello database connection string toohello app settings.</span></span> |
| [<span data-ttu-id="1ca12-129">Bir web uygulaması tooa depolama hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="1ca12-129">Connect a web app tooa storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="1ca12-130">Azure web uygulaması ve bir depolama hesabı oluşturur, ardından hello depolama bağlantı dizesi toohello uygulama ayarları ekler.</span><span class="sxs-lookup"><span data-stu-id="1ca12-130">Creates an Azure web app and a storage account, then adds hello storage connection string toohello app settings.</span></span> |
|<span data-ttu-id="1ca12-131">**İzleyici uygulama**</span><span class="sxs-lookup"><span data-stu-id="1ca12-131">**Monitor app**</span></span>||
| [<span data-ttu-id="1ca12-132">Web sunucusu günlükleri ile bir web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="1ca12-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="1ca12-133">Azure web uygulaması oluşturur, bunun için günlük kaydını etkinleştirir ve hello günlükleri tooyour yerel makine indirir.</span><span class="sxs-lookup"><span data-stu-id="1ca12-133">Creates an Azure web app, enables logging for it, and downloads hello logs tooyour local machine.</span></span> |
| | |
