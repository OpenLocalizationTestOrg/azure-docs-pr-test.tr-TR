---
title: "Azure Container Instances’a Genel Bakış | Azure Docs"
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
ms.openlocfilehash: 3fb230c6b16a57e3650abf2000acdfe944cd633c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="1a183-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="1a183-103">Azure Container Instances</span></span>

<span data-ttu-id="1a183-104">Kapsayıcılar, bulut uygulamalarını hızlı bir şekilde paketlemek, dağıtmak ve yönetmek için giderek daha fazla tercih edilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1a183-104">Containers are quickly becoming the preferred way to package, deploy, and manage cloud applications.</span></span> <span data-ttu-id="1a183-105">Azure Container Instances, herhangi bir sanal makine sağlamak ve daha yüksek düzeyde bir hizmeti benimsemek zorunda kalmadan Azure içinde kapsayıcı çalıştırmanın en hızlı ve en kolay yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="1a183-105">Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to provision any virtual machines and without having to adopt a higher-level service.</span></span> 

<span data-ttu-id="1a183-106">Yalıtılmış kapsayıcılarda çalışabileceğiniz senaryolar (basit uygulamalar, görev otomasyonu ve sürüm işleri gibi) için Azure Container Instances harika bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="1a183-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="1a183-107">Eksiksiz bir kapsayıcı düzenlemesi gerektiren senaryolar (birden çok kapsayıcıda hizmet bulma, otomatik ölçeklendirme ve eşgüdümlü uygulama yükseltmeleri gibi) için [Azure Container Service](https://docs.microsoft.com/azure/container-service/)’i öneririz.</span><span class="sxs-lookup"><span data-stu-id="1a183-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="1a183-108">Hızlı başlangıç süreleri</span><span class="sxs-lookup"><span data-stu-id="1a183-108">Fast startup times</span></span>

<span data-ttu-id="1a183-109">Kapsayıcılar, sanal makinelerde önemli başlangıç süresi avantajları sunar.</span><span class="sxs-lookup"><span data-stu-id="1a183-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="1a183-110">Azure Container Instances sayesinde Azure’da, sanal makineleri sağlamaya ve yönetmeye gerek kalmadan saniyeler içinde kapsayıcı başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-110">With Azure Container Instances, you can start a container in Azure in seconds without the need to provision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="1a183-111">Hiper yönetici düzeyinde güvenlik</span><span class="sxs-lookup"><span data-stu-id="1a183-111">Hypervisor-level security</span></span>

<span data-ttu-id="1a183-112">Geçmişte kapsayıcılar, uygulama bağımlılığı yalıtımı ve kaynak idaresi olanakları sağlıyor ancak birden çok kiracılı zorlu kullanımlar için yeterli kabul edilmiyordu.</span><span class="sxs-lookup"><span data-stu-id="1a183-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="1a183-113">Azure Container Instances ile uygulamanız,sanal makine yerine kapsayıcıda yalıtılır.</span><span class="sxs-lookup"><span data-stu-id="1a183-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="1a183-114">Özel boyutlar</span><span class="sxs-lookup"><span data-stu-id="1a183-114">Custom sizes</span></span>

<span data-ttu-id="1a183-115">Kapsayıcılar genellikle tek bir uygulamayı çalıştırmak üzere iyileştirilmiştir, ancak söz konusu uygulamaların tam gereksinimleri önemli ölçüde farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a183-115">Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="1a183-116">Azure Container Instances kullandığınızda, CPU çekirdekleri ve bellek açısından tam olarak gerek duyduğunuz kadar kaynak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="1a183-117">Yalnızca istedikleriniz için, saniye başına faturalandırılır ve harcamalarınızı ihtiyaçlarınıza uyacak şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-117">You pay based on what you request, billed by the second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="1a183-118">Genel IP bağlantısı</span><span class="sxs-lookup"><span data-stu-id="1a183-118">Public IP connectivity</span></span>

<span data-ttu-id="1a183-119">Azure Container Instances ile kapsayıcılarınızı İnternet üzerinde genel IP adresi ile doğrudan kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-119">With Azure Container Instances, you can expose your containers directly to the internet with a public IP address.</span></span> <span data-ttu-id="1a183-120">Gelecekte ağ olanaklarımızı, sanal ağlar ile tümleştirmeyi, yük dengeleyicileri ve Azure ağ altyapısının diğer çekirdek bölümlerini içerecek şekilde genişleteceğiz.</span><span class="sxs-lookup"><span data-stu-id="1a183-120">In the future, we will expand our networking capabilities to include integration with virtual networks, load balancers, and other core parts of the Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="1a183-121">Kalıcı depolama</span><span class="sxs-lookup"><span data-stu-id="1a183-121">Persistent storage</span></span>

<span data-ttu-id="1a183-122">Azure Container Instances ile durum alma ve durumu kalıcı hale getirme işlemleri için, Azure dosya paylaşımlarını doğrudan bağlama olanağı sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="1a183-122">To retrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="1a183-123">Linux ve Windows kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="1a183-123">Linux and Windows containers</span></span>

<span data-ttu-id="1a183-124">Azure Container Instances sayesinde, aynı API ile hem Windows hem de Linux kapsayıcıları zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-124">With Azure Container Instances, you can schedule both Windows and Linux containers with the same API.</span></span> <span data-ttu-id="1a183-125">Bunun için temel işletim sistemi türünü belirtmeniz yeterlidir, diğer her şey aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1a183-125">Simply indicate the base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="1a183-126">Birlikte zamanlanmış gruplar</span><span class="sxs-lookup"><span data-stu-id="1a183-126">Co-scheduled groups</span></span>

<span data-ttu-id="1a183-127">Azure Container Instances, aynı ana makineyi, yerel ağı, depolama alanını ve yaşam döngüsünü paylaşan birden çok kapsayıcı grubunun zamanlanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1a183-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="1a183-128">Böylece ana uygulamanızı, günlüğe kaydetme gibi diğer destekleyici uygulamalarla birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a183-128">This enables you to combine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a183-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a183-129">Next steps</span></span>

<span data-ttu-id="1a183-130">[Hızlı başlangıç kılavuzumuzu](container-instances-quickstart.md) kullanarak bir kapsayıcıyı tek bir komutla Azure’a dağıtmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1a183-130">Try deploying a container to Azure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>