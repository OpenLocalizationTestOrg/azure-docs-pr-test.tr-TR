---
title: Azure Service Fabric Linux'ta | Microsoft Docs
description: "Service Fabric kümeleri, Linux ve Java, anlamına gelir, dağıtabilmesi ve Java ve C# Linux'ta yazılmış konak Service Fabric uygulamaları destekler."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="59c2e-103">Service Fabric Linux</span><span class="sxs-lookup"><span data-stu-id="59c2e-103">Service Fabric on Linux</span></span>
<span data-ttu-id="59c2e-104">Service Fabric Linux'ta önizlemesini oluşturmak, dağıtmak ve Linux üzerinde yüksek oranda kullanılabilir, ölçeklendirilebilir uygulamalar Windows üzerinde gibi yönetme sağlar.</span><span class="sxs-lookup"><span data-stu-id="59c2e-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="59c2e-105">Service Fabric çerçeveleri (Reliable Services ve Reliable Actors) yanı sıra C# (.NET Core) Linux'ta Java mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="59c2e-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="59c2e-106">Ayrıca, oluşturabilirsiniz [Konuk yürütülebilir Hizmetleri](service-fabric-deploy-existing-app.md) herhangi bir dil veya framework ile.</span><span class="sxs-lookup"><span data-stu-id="59c2e-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="59c2e-107">Ayrıca, preview yönetme Docker kapsayıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="59c2e-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="59c2e-108">Docker kapsayıcıları Konuk yürütülebilir dosyalar veya Service Fabric çerçeveleri kullanan yerel Service Fabric hizmetler çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59c2e-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="59c2e-109">Service Fabric Linux (işletim sistemi özellikleri ve programlama dili desteği hariç) kavramsal olarak Windows Service Fabric eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="59c2e-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="59c2e-110">Bu nedenle, çoğu bizim [var olan belgeler](http://aka.ms/servicefabricdocs) teknolojisiyle tanıdık alma yardımcı uygular.</span><span class="sxs-lookup"><span data-stu-id="59c2e-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="59c2e-111">Desteklenen işletim sistemleri ve programlama dilleri</span><span class="sxs-lookup"><span data-stu-id="59c2e-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="59c2e-112">Sınırlı Önizleme Ubuntu Server 16.04 çalıştıran Azure'da çoklu makine kümeleri yanı sıra bir kutusunu geliştirme kümelerin oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="59c2e-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="59c2e-113">Önizleme Reliable Actors ve güvenilir durum bilgisi olmayan hizmetler çerçeveleri Java ve C# içinde Konuk yürütülebilir dosyaları ve Docker kapsayıcıları yönetme ek olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="59c2e-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="59c2e-114">Güvenilir koleksiyonları Linux içinde henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="59c2e-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="59c2e-115">Tek başına kümeleri desteklenmeyen ya - yalnızca bir kutusunu ve de Azure Linux çoklu makine kümeleri Önizleme'de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="59c2e-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="59c2e-116">Desteklenen araçları</span><span class="sxs-lookup"><span data-stu-id="59c2e-116">Supported tooling</span></span>
<span data-ttu-id="59c2e-117">Önizleme Service Fabric CLI aracılığıyla etkileşim destekler.</span><span class="sxs-lookup"><span data-stu-id="59c2e-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="59c2e-118">Java geliştiricileri için Eclipse ve Yeoman ile tümleştirme, OSX ve Linux üzerinde desteklenen Eclipse ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="59c2e-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="59c2e-119">OSX tümleştirme vagrant aracılığıyla başlık altında bir Linux VM kullanır.</span><span class="sxs-lookup"><span data-stu-id="59c2e-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="59c2e-120">C# geliştiricileri için Yeoman ile tümleştirme, uygulama şablonları oluşturmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="59c2e-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c2e-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59c2e-121">Next steps</span></span>

* <span data-ttu-id="59c2e-122">İle tanışın [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çerçeveleri programlama</span><span class="sxs-lookup"><span data-stu-id="59c2e-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="59c2e-123">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="59c2e-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="59c2e-124">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="59c2e-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="59c2e-125">Linux üzerinde ilk Service Fabric Java uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="59c2e-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="59c2e-126">Service Fabric sürekli tümleştirme ve dağıtım Jenkins ve GitHub ile Kurulum</span><span class="sxs-lookup"><span data-stu-id="59c2e-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="59c2e-127">Service Fabric Windows/Linux farkları</span><span class="sxs-lookup"><span data-stu-id="59c2e-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
