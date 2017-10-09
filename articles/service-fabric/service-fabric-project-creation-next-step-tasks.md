---
title: "aaaService doku proje oluşturma sonraki adımlar | Microsoft Docs"
description: "Bu makale bağlantılar tooa kümesi çekirdeği geliştirme görevleri için Service Fabric içerir"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="62ed9-103">Service Fabric uygulaması ve sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62ed9-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="62ed9-104">Azure Service Fabric uygulamanızı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="62ed9-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="62ed9-105">Bu makalede hello yapısıyla projenizi ve bazı olası sonraki adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="62ed9-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="62ed9-106">Uygulamanızı</span><span class="sxs-lookup"><span data-stu-id="62ed9-106">Your application</span></span>
<span data-ttu-id="62ed9-107">Her yeni uygulama, bir uygulama projesi içerir.</span><span class="sxs-lookup"><span data-stu-id="62ed9-107">Every new application includes an application project.</span></span> <span data-ttu-id="62ed9-108">Bir veya iki ek projeleri, seçilen hizmet hello türüne bağlı olarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="62ed9-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="62ed9-109">Merhaba uygulama projesi</span><span class="sxs-lookup"><span data-stu-id="62ed9-109">hello application project</span></span>
<span data-ttu-id="62ed9-110">Merhaba uygulama projesi oluşur:</span><span class="sxs-lookup"><span data-stu-id="62ed9-110">hello application project consists of:</span></span>

* <span data-ttu-id="62ed9-111">Uygulamayı oluşturan başvurular toohello Hizmetleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="62ed9-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="62ed9-112">Üç toomaintain Tercihler--Tercihler ilgili tooa küme uç noktası ve olup tooperform yükseltme dağıtımları varsayılan olarak gibi farklı ortamlarda çalışmak için kullanabileceğiniz profilleri (1-düğümü yerel, 5-Node yerel ve bulut) yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="62ed9-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="62ed9-113">Üç uygulama parametreleri dosyalarını (aynı yukarıdaki) bir hizmet için bölümleri toocreate hello sayısı gibi toomaintain ortama özgü uygulama yapılandırmaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="62ed9-114">Bir dağıtım komut dosyası toodeploy uygulamanızı hello komut satırından veya bir otomatik sürekli tümleştirme ve dağıtım ardışık parçası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="62ed9-115">Merhaba uygulaması açıklar hello uygulama bildirimi.</span><span class="sxs-lookup"><span data-stu-id="62ed9-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="62ed9-116">Merhaba bildirimi hello ApplicationPackageRoot klasörü altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="62ed9-117">Durum bilgisiz hizmeti</span><span class="sxs-lookup"><span data-stu-id="62ed9-117">Stateless service</span></span>
<span data-ttu-id="62ed9-118">Yeni bir durum bilgisiz hizmet eklediğinizde, Visual Studio gelen descended türünü içeren bir hizmet projesi tooyour çözümünü ekler `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="62ed9-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="62ed9-119">Merhaba hizmeti bir sayaç yerel bir değişkende artırır.</span><span class="sxs-lookup"><span data-stu-id="62ed9-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="62ed9-120">Durum bilgisi olan hizmet</span><span class="sxs-lookup"><span data-stu-id="62ed9-120">Stateful service</span></span>
<span data-ttu-id="62ed9-121">Yeni bir durum bilgisi olan hizmet eklediğinizde, Visual Studio gelen descended türünü içeren bir hizmet projesi tooyour çözümünü ekler `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="62ed9-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="62ed9-122">Merhaba hizmet artırır bir sayaç kendi `RunAsync` yöntemi ve depoları hello sonucunda bir `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="62ed9-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="62ed9-123">Aktör hizmeti</span><span class="sxs-lookup"><span data-stu-id="62ed9-123">Actor service</span></span>
<span data-ttu-id="62ed9-124">Yeni bir güvenilir aktör eklediğinizde, Visual Studio iki projeler tooyour çözümü ekler: aktör projesinde hem de bir arabirim projesi.</span><span class="sxs-lookup"><span data-stu-id="62ed9-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="62ed9-125">Merhaba aktör proje ayarı için yöntemler sağlar ve bir sayacın başlangıç değerini alma güvenilir bir şekilde hello aktör'ın durum kalıcı.</span><span class="sxs-lookup"><span data-stu-id="62ed9-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="62ed9-126">Merhaba arabirimi proje bir arabirim diğer hizmetler sağlar tooinvoke hello aktör kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="62ed9-127">Durum bilgisiz Web API'si</span><span class="sxs-lookup"><span data-stu-id="62ed9-127">Stateless Web API</span></span>
<span data-ttu-id="62ed9-128">Merhaba durum bilgisiz Web API projesi sağlar temel bir web hizmeti uygulama tooexternal istemcileriniz tooopen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="62ed9-129">Nasıl hello proje yapılandırılmış hakkında daha fazla bilgi için bkz: [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="62ed9-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="62ed9-130">ASP.NET Çekirdeği</span><span class="sxs-lookup"><span data-stu-id="62ed9-130">ASP.NET core</span></span>
<span data-ttu-id="62ed9-131">Merhaba Service Fabric SDK aynı kümesini tek başına ASP.NET Core projeleri için kullanılabilir olan ASP.NET Core şablonları, hello sağlar: boş [Web API][aspnet-webapi], ve [Web uygulaması][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="62ed9-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="62ed9-132">Konuk yürütülebilir dosyalar ve Konuk kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="62ed9-132">Guest executables and guest containers</span></span>

<span data-ttu-id="62ed9-133">Service Fabric 'Konuk' hello platformun programlama modeli ile yerleşik olmayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="62ed9-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="62ed9-134">Bir konuk hello ikili dosyalar ya da paketleyebilirsiniz [hello uygulama paketindeki doğrudan](service-fabric-deploy-existing-app.md) veya [bir kapsayıcı görüntüsü aracılığıyla](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="62ed9-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="62ed9-135">Her iki durumda da, Visual Studio hello hello gerekli yapıları oluşturur **ApplicationPackageRoot** hello uygulama projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="62ed9-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="62ed9-136">Visual Studio Hello kodu başka bir yerde zaten mevcut olduğundan yeni bir hizmet projesi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="62ed9-137">Konuk projeleri hello Service Fabric uygulaması projesi toomanage isterseniz, bunları toohello ekleyebilirsiniz aynı Visual Studio çözümü.</span><span class="sxs-lookup"><span data-stu-id="62ed9-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62ed9-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62ed9-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="62ed9-139">Bir Azure kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62ed9-139">Create an Azure cluster</span></span>
<span data-ttu-id="62ed9-140">Merhaba Service Fabric SDK, geliştirme ve test için yerel bir küme sağlar.</span><span class="sxs-lookup"><span data-stu-id="62ed9-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="62ed9-141">Azure, kümede toocreate bkz [hello Azure portal ' bir Service Fabric kümesi ayarlama][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="62ed9-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="62ed9-142">Uygulama tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="62ed9-142">Publish your application tooAzure</span></span>
<span data-ttu-id="62ed9-143">Visual Studio tooan Azure küme uygulamadan doğrudan yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62ed9-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="62ed9-144">toolearn nasıl bkz [uygulama tooAzure yayımlama][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="62ed9-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="62ed9-145">Service Fabric Explorer toovisualize kümenizi kullanın</span><span class="sxs-lookup"><span data-stu-id="62ed9-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="62ed9-146">Service Fabric Explorer kolay bir yolu toovisualize dağıtılan uygulamalar ve fiziksel düzenini de dahil olmak üzere kümenizi sunar.</span><span class="sxs-lookup"><span data-stu-id="62ed9-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="62ed9-147">toolearn daha, fazla [Service Fabric Explorer kullanarak kümenizi görselleştirme][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="62ed9-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="62ed9-148">Sürümü ve hizmetlerinizi yükseltme</span><span class="sxs-lookup"><span data-stu-id="62ed9-148">Version and upgrade your services</span></span>
<span data-ttu-id="62ed9-149">Service Fabric bağımsız sürüm oluşturma ve uygulamada bağımsız Hizmetleri yükseltme sağlar.</span><span class="sxs-lookup"><span data-stu-id="62ed9-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="62ed9-150">toolearn daha, fazla [sürüm oluşturma ve hizmetlerinizi yükseltme][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="62ed9-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="62ed9-151">Visual Studio Team Services ile sürekli tümleştirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="62ed9-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="62ed9-152">Service Fabric uygulamanız için bir sürekli tümleştirme işlemini ayarlayabilirsiniz nasıl toolearn bkz [sürekli tümleştirme ile Visual Studio Team Services yapılandırma][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="62ed9-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
