---
title: "Microsoft azure'da bulut Foundry başlangıç aaaGetting | Microsoft Docs"
description: "Microsoft Azure üzerinde OSS veya Bileşendirler bulut Foundry çalıştırın"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="145dc-103">Azure’da Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="145dc-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="145dc-104">Bulut Foundry bir açık kaynak platform olarak-hizmet (PaaS) oluşturmak, dağıtmak ve çeşitli dilleri ve çerçeveleri geliştirilen uygulamaları 12 faktör işletim ' dir.</span><span class="sxs-lookup"><span data-stu-id="145dc-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="145dc-105">Bu belgede Azure ve size nasıl başlayabiliriz bulut Foundry çalıştırmak için sahip hello seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="145dc-105">This document describes hello options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="145dc-106">Bulut Foundry teklifleri</span><span class="sxs-lookup"><span data-stu-id="145dc-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="145dc-107">Bulut Foundry kullanılabilir toorun Azure ile ilgili iki tür vardır: açık kaynak bulut Foundry (OSS CF) ve Bileşendirler bulut Foundry (PCF).</span><span class="sxs-lookup"><span data-stu-id="145dc-107">There are two forms of Cloud Foundry available toorun on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="145dc-108">OSS CF olan bir tamamen [açık kaynak](https://github.com/cloudfoundry) bulut Foundry sürümü hello bulut Foundry Foundation tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="145dc-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by hello Cloud Foundry Foundation.</span></span> <span data-ttu-id="145dc-109">Bir kurumsal dağıtım bulut Foundry Bileşendirler yazılım Inc., bileşendirler bulut Foundry Bazı hello iki teklifleri hello farklarını arayın.</span><span class="sxs-lookup"><span data-stu-id="145dc-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of hello differences between hello two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="145dc-110">Açık kaynak bulut Foundry</span><span class="sxs-lookup"><span data-stu-id="145dc-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="145dc-111">Azure üzerinde OSS bulut Foundry BOSH yönetmenin ilk dağıtma ve hello kullanarak bulut Foundry dağıtma dağıtabilirsiniz [Github'da sağlanan yönergeleri](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span><span class="sxs-lookup"><span data-stu-id="145dc-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using hello [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="145dc-112">OSS CF kullanma hakkında daha fazla toolearn bkz hello [belgelerine](https://docs.cloudfoundry.org/) hello bulut Foundry Foundation tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="145dc-112">toolearn more about using OSS CF, see hello [documentation](https://docs.cloudfoundry.org/) provided by hello Cloud Foundry Foundation.</span></span>

<span data-ttu-id="145dc-113">Microsoft, topluluk kanalları aşağıdaki hello aracılığıyla OSS CF için en yüksek çaba destek sağlar:</span><span class="sxs-lookup"><span data-stu-id="145dc-113">Microsoft provides best-effort support for OSS CF through hello following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="145dc-114">bosh azure CPI kanalda [bulut Foundry kayma](https://slack.cloudfoundry.org/)</span><span class="sxs-lookup"><span data-stu-id="145dc-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="145dc-115">cf bosh posta listesi</span><span class="sxs-lookup"><span data-stu-id="145dc-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="145dc-116">Hello için GitHub sorunları [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) ve [hizmet Aracısı](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="145dc-116">GitHub issues for hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="145dc-117">Bulut Foundry çalıştırdığı hello sanal makineler gibi Azure kaynaklarınızı desteği Hello düzeyini Azure destek sözleşmenizi temel alır.</span><span class="sxs-lookup"><span data-stu-id="145dc-117">hello level of support for your Azure resources, such as hello virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="145dc-118">En yüksek çaba topluluk desteği yalnızca toohello bulut Foundry özgü bileşenleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="145dc-118">Best-effort community support only applies toohello Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="145dc-119">Bileşendirler bulut Foundry</span><span class="sxs-lookup"><span data-stu-id="145dc-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="145dc-120">Bileşendirler bulut Foundry hello içeren bir dizi özel yönetim araçları ve kurumsal destek birlikte hello OSS dağıtım olarak aynı çekirdek platformu.</span><span class="sxs-lookup"><span data-stu-id="145dc-120">Pivotal Cloud Foundry includes hello same core platform as hello OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="145dc-121">Azure üzerinde PCF toorun Pivotal lisanstan edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="145dc-121">toorun PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="145dc-122">Merhaba PCF hello Azure Market tekliften 90 günlük deneme lisansı içerir.</span><span class="sxs-lookup"><span data-stu-id="145dc-122">hello PCF offer from hello Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="145dc-123">Merhaba araçlarda [Bileşendirler Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), dağıtımını ve bir bulut Foundry temel yönetimini kolaylaştıran bir web uygulaması ve [Bileşendirler uygulamaları Yöneticisi](https://docs.pivotal.io/pivotalcf/console/), yönetmek için bir web uygulaması Kullanıcılar ve uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="145dc-123">hello tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="145dc-124">Ayrıca toohello destek kanallarını, yukarıdaki OSS CF için listelenen PCF lisans, toocontact Pivotal desteği hakkı verir.</span><span class="sxs-lookup"><span data-stu-id="145dc-124">In addition toohello support channels listed for OSS CF above, a PCF license entitles you toocontact Pivotal for support.</span></span> <span data-ttu-id="145dc-125">Microsoft ve Pivotal toocontact izin destek iş akışları konusunda yardım almak için her iki taraf da etkinleştirdiyseniz ve burada hello sorunu arasındadır bağlı olarak uygun şekilde yönlendirilmesini, soru sahiptir.</span><span class="sxs-lookup"><span data-stu-id="145dc-125">Microsoft and Pivotal have also enabled support workflows that allow you toocontact either party for assistance and have your inquiry routed appropriately depending on where hello issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="145dc-126">Azure hizmet Aracısı</span><span class="sxs-lookup"><span data-stu-id="145dc-126">Azure Service Broker</span></span>

<span data-ttu-id="145dc-127">Bulut Foundry teşvik eden hello ["on iki öğeli uygulama"](https://12factor.net/) temiz ayrılması durum bilgisiz uygulama işlemleri ve durum bilgisi olan hizmetler yedekleme yükseltir Metodoloji.</span><span class="sxs-lookup"><span data-stu-id="145dc-127">Cloud Foundry encourages hello ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="145dc-128">[Hizmet aracıların](https://docs.cloudfoundry.org/services/api.html) tutarlı bir yol tooprovision sunar ve yedekleme hizmetleri tooapplications bağlayın.</span><span class="sxs-lookup"><span data-stu-id="145dc-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way tooprovision and bind backing services tooapplications.</span></span> <span data-ttu-id="145dc-129">Merhaba [Azure hizmet Aracısı](https://github.com/Azure/meta-azure-service-broker) hello bazıları Azure depolama ve Azure SQL dahil olmak üzere bu kanal üzerinden anahtar Azure hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="145dc-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of hello key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="145dc-130">Bileşendirler bulut Foundry kullanıyorsanız, hello hizmet aracısı ayrıca olduğu [kullanılabilir bir kutucuk olarak](https://docs.pivotal.io/azure-sb/installing.html) hello Bileşendirler ağ alanından.</span><span class="sxs-lookup"><span data-stu-id="145dc-130">If you are using Pivotal Cloud Foundry, hello service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from hello Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="145dc-131">İlgili kaynaklar</span><span class="sxs-lookup"><span data-stu-id="145dc-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="145dc-132">Visual Studio Team Services eklentisi</span><span class="sxs-lookup"><span data-stu-id="145dc-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="145dc-133">Bulut Foundry hello kullanımını sürekli tümleştirme (CI) ve kesintisiz teslim (CD) dahil olmak üzere uygun tooagile yazılım geliştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="145dc-133">Cloud Foundry is well suited tooagile software development, including hello use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="145dc-134">Projelerinizi Visual Studio Team Services (VSTS) toomanage kullanıyorsanız ve tooset bulut Foundry hedefleme CI/CD işlem hattı kurmak istediğiniz, hello kullanabilirsiniz [VSTS bulut Foundry yapı uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span><span class="sxs-lookup"><span data-stu-id="145dc-134">If you use Visual Studio Team Services (VSTS) toomanage your projects and would like tooset up a CI/CD pipeline targeting Cloud Foundry, you can use hello [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="145dc-135">Merhaba eklentisi basit tooconfigure kolaylaştırır ve dağıtımları tooCloud Foundry, Azure veya başka bir çalışan olup olmadığını otomatikleştirmek ortamı.</span><span class="sxs-lookup"><span data-stu-id="145dc-135">hello plugin makes it simple tooconfigure and automate deployments tooCloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="145dc-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="145dc-136">Next steps</span></span>

- [<span data-ttu-id="145dc-137">Azure Market hello Bileşendirler bulut Foundry dağıtma</span><span class="sxs-lookup"><span data-stu-id="145dc-137">Deploy Pivotal Cloud Foundry from hello Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="145dc-138">Bir uygulama tooCloud azure'da Foundry dağıtma</span><span class="sxs-lookup"><span data-stu-id="145dc-138">Deploy an app tooCloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)
