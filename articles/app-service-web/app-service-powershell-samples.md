---
title: "Azure PowerShell örnekleri - App Service | Microsoft Docs"
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
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="f986f-103">Azure PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="f986f-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="f986f-104">Aşağıdaki tabloda Azure PowerShell kullanılarak oluşturulan komut dosyalarını bash bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="f986f-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="f986f-105">**Uygulama oluşturma**</span><span class="sxs-lookup"><span data-stu-id="f986f-105">**Create app**</span></span>||
| [<span data-ttu-id="f986f-106">Github'dan dağıtımı ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f986f-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-107">Kod Github'dan çeken bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f986f-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="f986f-108">GitHub’dan sürekli dağıtım ile bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f986f-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-109">Sürekli olarak kod github'dan dağıtan bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f986f-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="f986f-110">Bir web uygulaması oluşturma ve FTP koduyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="f986f-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-111">Bir Azure web app ve karşıya yükleme dosyaları FTP kullanarak yerel bir dizinden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f986f-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="f986f-112">Yerel Git deposundan web uygulaması oluşturma ve kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="f986f-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-113">Azure web uygulaması oluşturur ve kodun bir yerel Git deposundan yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f986f-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="f986f-114">Hazırlık ortamında web uygulaması oluşturma ve kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="f986f-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-115">Kod değişiklikleri hazırlama için bir dağıtım yuvası ile bir Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f986f-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="f986f-116">**Uygulamayı yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="f986f-116">**Configure app**</span></span>||
| [<span data-ttu-id="f986f-117">Özel bir etki alanını bir web uygulaması ile eşleştirme</span><span class="sxs-lookup"><span data-stu-id="f986f-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-118">Azure web uygulaması oluşturur ve bir özel etki alanı adı için eşleştirir.</span><span class="sxs-lookup"><span data-stu-id="f986f-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="f986f-119">Bir web uygulaması için özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="f986f-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-120">Azure web uygulaması oluşturur ve SSL sertifikası özel etki alanı adı kendisine bağlar.</span><span class="sxs-lookup"><span data-stu-id="f986f-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="f986f-121">**Ölçek uygulama**</span><span class="sxs-lookup"><span data-stu-id="f986f-121">**Scale app**</span></span>||
| [<span data-ttu-id="f986f-122">Web uygulamasını el ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f986f-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-123">Azure web uygulaması oluşturur ve bunu 2 örneklerinde ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="f986f-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="f986f-124">Web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f986f-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-125">İki farklı coğrafi bölgelerde iki Azure web uygulamaları oluşturur ve bunları Azure trafik Yöneticisi'ni kullanarak tek bir uç noktası aracılığıyla kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f986f-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="f986f-126">**Uygulama kaynaklarına bağlanma**</span><span class="sxs-lookup"><span data-stu-id="f986f-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="f986f-127">Bir web uygulaması bir SQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="f986f-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-128">Azure web uygulaması ve SQL veritabanı oluşturur, ardından veritabanı bağlantı dizesi için uygulama ayarları ekler.</span><span class="sxs-lookup"><span data-stu-id="f986f-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="f986f-129">Bir web uygulamasını bir depolama hesabına bağlama</span><span class="sxs-lookup"><span data-stu-id="f986f-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="f986f-130">Azure web uygulaması ve bir depolama hesabı oluşturur, ardından depolama bağlantı dizesi için uygulama ayarları ekler.</span><span class="sxs-lookup"><span data-stu-id="f986f-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="f986f-131">**İzleyici uygulama**</span><span class="sxs-lookup"><span data-stu-id="f986f-131">**Monitor app**</span></span>||
| [<span data-ttu-id="f986f-132">Web sunucusu günlükleri ile bir web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="f986f-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="f986f-133">Azure web uygulaması oluşturur, bunun için günlük kaydını etkinleştirir ve yerel makinenize günlükleri indirir.</span><span class="sxs-lookup"><span data-stu-id="f986f-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
