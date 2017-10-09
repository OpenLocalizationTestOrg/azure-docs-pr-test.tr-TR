---
title: "aaaAzure kapsayıcı örnekleri genel bakış | Azure belgeleri"
description: "Azure Container Instances’ı Anlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="c374a-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="c374a-103">Azure Container Instances</span></span>

<span data-ttu-id="c374a-104">Kapsayıcıları hızlı bir şekilde hello tercih edilen yol toopackage gelmektedir, dağıtın ve bulut uygulamalarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="c374a-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="c374a-105">Azure kapsayıcı örnekleri hello en hızlı ve kolay şekilde toorun bir kapsayıcıda Azure, herhangi bir sanal makine tooprovision kalmadan ve üst düzey hizmet tooadopt kalmadan sunar.</span><span class="sxs-lookup"><span data-stu-id="c374a-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="c374a-106">Yalıtılmış kapsayıcılarda çalışabileceğiniz senaryolar (basit uygulamalar, görev otomasyonu ve sürüm işleri gibi) için Azure Container Instances harika bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="c374a-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="c374a-107">Merhaba öneririz burada dosyalarda tam birden çok kapsayıcı, otomatik ölçeklendirme ve Eşgüdümlü uygulama yükseltmelerini arasında hizmet bulma de dahil olmak üzere, kapsayıcı orchestration senaryoları için [Azure kapsayıcı hizmeti](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="c374a-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="c374a-108">Hızlı başlangıç süreleri</span><span class="sxs-lookup"><span data-stu-id="c374a-108">Fast startup times</span></span>

<span data-ttu-id="c374a-109">Kapsayıcılar, sanal makinelerde önemli başlangıç süresi avantajları sunar.</span><span class="sxs-lookup"><span data-stu-id="c374a-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="c374a-110">Azure kapsayıcı örnekleriyle bir kapsayıcı Azure'da hello gerek tooprovision olmadan saniye başlatmak ve VM'ler yönetin.</span><span class="sxs-lookup"><span data-stu-id="c374a-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="c374a-111">Hiper yönetici düzeyinde güvenlik</span><span class="sxs-lookup"><span data-stu-id="c374a-111">Hypervisor-level security</span></span>

<span data-ttu-id="c374a-112">Geçmişte kapsayıcılar, uygulama bağımlılığı yalıtımı ve kaynak idaresi olanakları sağlıyor ancak birden çok kiracılı zorlu kullanımlar için yeterli kabul edilmiyordu.</span><span class="sxs-lookup"><span data-stu-id="c374a-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="c374a-113">Azure Container Instances ile uygulamanız,sanal makine yerine kapsayıcıda yalıtılır.</span><span class="sxs-lookup"><span data-stu-id="c374a-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="c374a-114">Özel boyutlar</span><span class="sxs-lookup"><span data-stu-id="c374a-114">Custom sizes</span></span>

<span data-ttu-id="c374a-115">Yalnızca tek bir uygulama, ancak bu uygulamaların tam gereksinimlerini hello büyük ölçüde değişebilir genellikle en iyi duruma getirilmiş toorun kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="c374a-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="c374a-116">Azure Container Instances kullandığınızda, CPU çekirdekleri ve bellek açısından tam olarak gerek duyduğunuz kadar kaynak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c374a-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="c374a-117">Ne istemcinin göre tarafından hello fatura ödeme, gereksinimlerinize göre harcama ince iyileştirebilirsiniz şekilde ikinci.</span><span class="sxs-lookup"><span data-stu-id="c374a-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="c374a-118">Genel IP bağlantısı</span><span class="sxs-lookup"><span data-stu-id="c374a-118">Public IP connectivity</span></span>

<span data-ttu-id="c374a-119">Azure kapsayıcı örnekleriyle kapsayıcılarınızı getirebilir doğrudan toohello Internet ortak IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="c374a-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="c374a-120">Hello gelecekteki, biz bizim ağ yeteneklerini tooinclude tümleştirme sanal ağlarla genişletin, yük dengeleyicileri ve diğer çekirdek bölümleri hello Azure ağ altyapısı.</span><span class="sxs-lookup"><span data-stu-id="c374a-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="c374a-121">Kalıcı depolama</span><span class="sxs-lookup"><span data-stu-id="c374a-121">Persistent storage</span></span>

<span data-ttu-id="c374a-122">tooretrieve ve Azure kapsayıcı örnekleri durumuyla kalıcı, doğrudan bağlama Azure dosya paylaşımları sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="c374a-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="c374a-123">Linux ve Windows kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="c374a-123">Linux and Windows containers</span></span>

<span data-ttu-id="c374a-124">Azure kapsayıcı örnekleri, hem Windows zamanlayabilir ve aynı API ile Linux kapsayıcıları hello.</span><span class="sxs-lookup"><span data-stu-id="c374a-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="c374a-125">Yalnızca hello temel işletim sistemi türü ve şey aynı göstermek.</span><span class="sxs-lookup"><span data-stu-id="c374a-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="c374a-126">Birlikte zamanlanmış gruplar</span><span class="sxs-lookup"><span data-stu-id="c374a-126">Co-scheduled groups</span></span>

<span data-ttu-id="c374a-127">Azure Container Instances, aynı ana makineyi, yerel ağı, depolama alanını ve yaşam döngüsünü paylaşan birden çok kapsayıcı grubunun zamanlanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c374a-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="c374a-128">Bu, toocombine ana uygulamanızı başkalarıyla sağlar destekleyen bir rol, günlüğe kaydetme gibi davranan.</span><span class="sxs-lookup"><span data-stu-id="c374a-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c374a-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c374a-129">Next steps</span></span>

<span data-ttu-id="c374a-130">Tek bir komut kullanarak bir kapsayıcı tooAzure dağıtmayı deneyin bizim [Hızlı Başlangıç Kılavuzu](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c374a-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
