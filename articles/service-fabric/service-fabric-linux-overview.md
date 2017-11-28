---
title: Service Fabric Linux'ta aaaAzure | Microsoft Docs
description: "Service Fabric kümeleri, Linux ve mümkün toodeploy ve ana bilgisayar Service Fabric uygulamaları Linux üzerinde Java ve C# içinde yazılmış olacak anlamına gelir Java destekler."
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
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="27564-103">Service Fabric Linux</span><span class="sxs-lookup"><span data-stu-id="27564-103">Service Fabric on Linux</span></span>
<span data-ttu-id="27564-104">Service Fabric Linux'ta Hello önizlemesini toobuild sağlar, dağıtın ve Linux üzerinde yüksek oranda kullanılabilir, ölçeklendirilebilir uygulamalar Windows üzerinde gibi yönetin.</span><span class="sxs-lookup"><span data-stu-id="27564-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="27564-105">Merhaba Service Fabric çerçeveler (Reliable Services ve Reliable Actors) toplama tooC # (.NET Core) Linux üzerinde Java mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="27564-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="27564-106">Ayrıca, oluşturabilirsiniz [Konuk yürütülebilir Hizmetleri](service-fabric-deploy-existing-app.md) herhangi bir dil veya framework ile.</span><span class="sxs-lookup"><span data-stu-id="27564-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="27564-107">Ayrıca, hello Önizleme yönetme Docker kapsayıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="27564-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="27564-108">Docker kapsayıcıları Konuk yürütülebilir dosyalar veya hello Service Fabric çerçeveler kullanan yerel Service Fabric hizmetler çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27564-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="27564-109">Service Fabric Linux'ta (dışında işletim sistemi özellikleri ve programlama dili desteği) kavramsal olarak eşdeğer tooService Windows Fabric ' dir.</span><span class="sxs-lookup"><span data-stu-id="27564-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="27564-110">Bu nedenle, çoğu bizim [var olan belgeler](http://aka.ms/servicefabricdocs) hello teknolojisiyle tanıdık alma yardımcı uygular.</span><span class="sxs-lookup"><span data-stu-id="27564-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="27564-111">Desteklenen işletim sistemleri ve programlama dilleri</span><span class="sxs-lookup"><span data-stu-id="27564-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="27564-112">sınırlı hello Önizleme destekler hello bir kutusunu geliştirme oluşturulmasını ayrıca toomulti makine Azure Ubuntu Server 16.04 çalıştıran kümeler.</span><span class="sxs-lookup"><span data-stu-id="27564-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="27564-113">Reliable Actors hello ve ayrıca tooguest yürütülebilir dosyaları ve Docker kapsayıcıları yönetme Java ve C# içinde güvenilir durum bilgisi olmayan hizmetler çerçeve hello Hello Önizleme destekler.</span><span class="sxs-lookup"><span data-stu-id="27564-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="27564-114">Güvenilir koleksiyonları Linux içinde henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="27564-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="27564-115">Tek başına kümeleri desteklenmeyen ya - yalnızca bir kutusunu ve de Azure Linux çoklu makine kümeleri hello Önizleme'de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="27564-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="27564-116">Desteklenen araçları</span><span class="sxs-lookup"><span data-stu-id="27564-116">Supported tooling</span></span>
<span data-ttu-id="27564-117">Merhaba Önizleme Service Fabric CLI aracılığıyla hello kümesi ile etkileşimi destekler.</span><span class="sxs-lookup"><span data-stu-id="27564-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="27564-118">Java geliştiricileri için Eclipse ve Yeoman ile tümleştirme, OSX ve Linux üzerinde desteklenen Eclipse ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="27564-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="27564-119">Merhaba OSX tümleştirme vagrant aracılığıyla hello başlık altında bir Linux VM kullanır.</span><span class="sxs-lookup"><span data-stu-id="27564-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="27564-120">C# geliştiricileri için Yeoman ile tümleştirme toogenerate uygulama şablonları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="27564-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27564-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27564-121">Next steps</span></span>

* <span data-ttu-id="27564-122">Merhaba ile tanışın [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çerçeveleri programlama</span><span class="sxs-lookup"><span data-stu-id="27564-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="27564-123">Linux üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="27564-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="27564-124">OSX üzerinde geliştirme ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="27564-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="27564-125">Linux üzerinde ilk Service Fabric Java uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="27564-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="27564-126">Service Fabric sürekli tümleştirme ve dağıtım Jenkins ve GitHub ile Kurulum</span><span class="sxs-lookup"><span data-stu-id="27564-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="27564-127">Service Fabric Windows/Linux farkları</span><span class="sxs-lookup"><span data-stu-id="27564-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
