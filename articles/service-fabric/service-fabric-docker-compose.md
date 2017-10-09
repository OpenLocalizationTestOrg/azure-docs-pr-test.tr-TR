---
title: "aaaAzure Service Fabric Docker oluşturan Önizleme"
description: "Azure Service Fabric Docker Compose biçimi toomake kabul eder, Service Fabric kullanarak, daha kolay tooorchestrate varolan kapsayıcıları. Bu destek, şu anda önizlemede değil."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="180d2-104">Docker Compose Azure Service Fabric (Önizleme) uygulama desteği</span><span class="sxs-lookup"><span data-stu-id="180d2-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="180d2-105">Docker kullanan hello [docker-compose.yml](https://docs.docker.com/compose) çok kapsayıcı uygulamaları tanımlamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="180d2-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="180d2-106">toomake, müşterilerin Azure Service Fabric Docker tooorchestrate varolan kapsayıcı uygulamaları aşina kolaylaştırır, biz Docker Compose Önizleme desteği yerel olarak hello platformunda eklediniz.</span><span class="sxs-lookup"><span data-stu-id="180d2-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="180d2-107">Service Fabric sürüm 3 ve sonraki kabul edebileceği `docker-compose.yml` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="180d2-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="180d2-108">Bu destek önizlemede olmadığından, yalnızca bir alt kümesini oluşturma yönergeleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="180d2-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="180d2-109">Örneğin, uygulama yükseltmeler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="180d2-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="180d2-110">Ancak, istediğiniz zaman kaldırma ve bunları yükseltme yerine uygulamaları dağıtma.</span><span class="sxs-lookup"><span data-stu-id="180d2-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="180d2-111">toouse Bu önizleme, 5.7 veya hello Service Fabric çalışma zamanı hello SDK karşılık gelen hello yanı sıra Azure portal aracılığıyla daha büyük sürümüyle kümenizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="180d2-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="180d2-112">Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="180d2-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="180d2-113">Service Fabric Docker Compose bir dosyada dağıtma</span><span class="sxs-lookup"><span data-stu-id="180d2-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="180d2-114">Merhaba aşağıdaki komutları bir Service Fabric uygulaması oluşturma (adlı `fabric:/TestContainerApp` örnek önceki hello içinde), hangi izleyebilir ve başka bir Service Fabric uygulaması gibi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180d2-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="180d2-115">Sistem durumu sorgularının sayısı için belirtilen uygulama adı hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180d2-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="180d2-116">PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="180d2-116">Use PowerShell</span></span>

<span data-ttu-id="180d2-117">Service Fabric oluşturan bir uygulama hello aşağıdaki PowerShell komutunu çalıştırarak bir docker-compose.yml dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="180d2-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="180d2-118">`RegistryUserName`ve `RegistryPassword` toohello kapsayıcı kayıt defteri kullanıcı adı ve parola bakın.</span><span class="sxs-lookup"><span data-stu-id="180d2-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="180d2-119">Merhaba uygulaması tamamladıktan sonra komutu aşağıdaki hello kullanarak durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180d2-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="180d2-120">toodelete PowerShell aracılığıyla oluşturma uygulama Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="180d2-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="180d2-121">Azure Service Fabric CLI (sfctl) kullanın</span><span class="sxs-lookup"><span data-stu-id="180d2-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="180d2-122">Alternatif olarak, Service Fabric CLI komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180d2-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="180d2-123">Merhaba uygulaması oluşturduktan sonra komutu aşağıdaki hello kullanarak durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180d2-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="180d2-124">toodelete hello oluşturma uygulama hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="180d2-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="180d2-125">Desteklenen oluşturma yönergeleri</span><span class="sxs-lookup"><span data-stu-id="180d2-125">Supported Compose directives</span></span>

<span data-ttu-id="180d2-126">Bu önizleme hello yapılandırma temelleri aşağıdaki hello dahil olmak üzere, hello Oluştur sürüm 3 biçimini seçeneklerinden kümesini destekler:</span><span class="sxs-lookup"><span data-stu-id="180d2-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="180d2-127">Hizmetleri > dağıtmak > çoğaltmaları</span><span class="sxs-lookup"><span data-stu-id="180d2-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="180d2-128">Hizmetleri > dağıtmak > yerleştirme > kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="180d2-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="180d2-129">Hizmetleri > dağıtmak > kaynak > sınırları</span><span class="sxs-lookup"><span data-stu-id="180d2-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="180d2-130">cpu-paylaşımları</span><span class="sxs-lookup"><span data-stu-id="180d2-130">-cpu-shares</span></span>
    * <span data-ttu-id="180d2-131">-bellek</span><span class="sxs-lookup"><span data-stu-id="180d2-131">-memory</span></span>
    * <span data-ttu-id="180d2-132">-bellek-değiştirme</span><span class="sxs-lookup"><span data-stu-id="180d2-132">-memory-swap</span></span>
* <span data-ttu-id="180d2-133">Hizmetleri > komutları</span><span class="sxs-lookup"><span data-stu-id="180d2-133">Services > Commands</span></span>
* <span data-ttu-id="180d2-134">Hizmetleri > ortamı</span><span class="sxs-lookup"><span data-stu-id="180d2-134">Services > Environment</span></span>
* <span data-ttu-id="180d2-135">Hizmetleri > bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="180d2-135">Services > Ports</span></span>
* <span data-ttu-id="180d2-136">Hizmetleri > görüntüsü</span><span class="sxs-lookup"><span data-stu-id="180d2-136">Services > Image</span></span>
* <span data-ttu-id="180d2-137">Hizmetleri > yalıtımını (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="180d2-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="180d2-138">Hizmetleri > günlüğü > sürücüsü</span><span class="sxs-lookup"><span data-stu-id="180d2-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="180d2-139">Hizmetleri > günlüğü > sürücü > Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="180d2-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="180d2-140">Birim & dağıtmak > birim</span><span class="sxs-lookup"><span data-stu-id="180d2-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="180d2-141">Bölümünde açıklandığı gibi hello küme kaynak sınırları, zorlama ayarlamak [Service Fabric kaynak İdaresi](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="180d2-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="180d2-142">Tüm diğer Docker Compose yönergeleri Bu önizleme için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="180d2-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="180d2-143">ServiceDnsName hesaplama</span><span class="sxs-lookup"><span data-stu-id="180d2-143">ServiceDnsName computation</span></span>

<span data-ttu-id="180d2-144">Oluşturma dosyasında belirttiğiniz hello hizmet adı tam etki alanı adı ise (diğer bir deyişle, bir nokta [.] içerdiği), Service Fabric tarafından kayıtlı hello DNS adı `<ServiceName>` (Merhaba nokta dahil).</span><span class="sxs-lookup"><span data-stu-id="180d2-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="180d2-145">Aksi durumda, her yol kesimi hello uygulama adı, etki alanı etiketi hello en üst düzey etki alanı etiketi olma hello ilk yol kesimi ile Merhaba hizmeti DNS adı olur.</span><span class="sxs-lookup"><span data-stu-id="180d2-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="180d2-146">Örneğin, uygulama adı hello belirtilen ise `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` kayıtlı DNS adı hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="180d2-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="180d2-147">Oluştur (örnek tanım) ve Service Fabric uygulama modeli (tür tanımı) arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="180d2-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="180d2-148">Docker-compose.yml dosyası kapsayıcılar kendi özellikler ve yapılandırmalar da dahil olmak üzere, dağıtılabilir bir dizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="180d2-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="180d2-149">Örneğin, ortam değişkenleri ve bağlantı noktaları hello dosyası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="180d2-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="180d2-150">Merhaba docker-compose.yml dosyası kısıtlamalarından, kaynak sınırları ve DNS adları gibi dağıtım parametreleri de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180d2-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="180d2-151">Merhaba [Service Fabric uygulama modeli](service-fabric-application-model.md) kullandığı hizmet türlerini ve uygulama türleri, pek çok uygulama örneğini bulunan hello aynı türde.</span><span class="sxs-lookup"><span data-stu-id="180d2-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="180d2-152">Örneğin, müşteri başına bir uygulama örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="180d2-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="180d2-153">Bu tür tabanlı model hello birden fazla sürümünü destekleyen hello çalışma zamanı ile kayıtlı aynı uygulama türü.</span><span class="sxs-lookup"><span data-stu-id="180d2-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="180d2-154">Örneğin, bir müşteri AppTypeA 1.0 türüyle örneği bir uygulama olabilir ve Müşteri B ile Merhaba örneği başka bir uygulama olabilir aynı türü ve sürümü.</span><span class="sxs-lookup"><span data-stu-id="180d2-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="180d2-155">Merhaba uygulama bildirimleri hello uygulama türlerini tanımlayın ve Merhaba uygulaması oluşturduğunuzda hello uygulama adını ve dağıtım parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="180d2-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="180d2-156">Bu model esneklik sunar ancak biz de toosupport türleri hello bildirim dosyasındaki örtük nerede daha basit ve örnek tabanlı dağıtım modeli planladığınıza.</span><span class="sxs-lookup"><span data-stu-id="180d2-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="180d2-157">Bu modelde, her uygulamanın kendi bağımsız bildirimi alır.</span><span class="sxs-lookup"><span data-stu-id="180d2-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="180d2-158">Biz bu çalışmaların örneği tabanlı dağıtım biçimi olduğu docker-compose.yml için destek ekleyerek önizlemede.</span><span class="sxs-lookup"><span data-stu-id="180d2-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="180d2-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="180d2-159">Next steps</span></span>

* <span data-ttu-id="180d2-160">Merhaba üzerinde okuma [Service Fabric uygulama modeli](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="180d2-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="180d2-161">Service Fabric CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="180d2-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
