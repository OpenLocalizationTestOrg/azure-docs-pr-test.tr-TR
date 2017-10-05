---
title: "Azure Service Fabric Docker Compose Önizleme"
description: "Azure Service Fabric Service Fabric kullanarak var olan kapsayıcıları düzenlemek kolay hale getirmek için Docker Compose'u biçimi kabul eder. Bu destek, şu anda önizlemede değil."
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
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="40df2-104">Docker Compose Azure Service Fabric (Önizleme) uygulama desteği</span><span class="sxs-lookup"><span data-stu-id="40df2-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="40df2-105">Docker kullanan [docker-compose.yml](https://docs.docker.com/compose) çok kapsayıcı uygulamaları tanımlamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="40df2-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="40df2-106">Müşteriler için Azure Service Fabric varolan kapsayıcı uygulamaları düzenlemek için Docker aşina kolaylaştırmak için biz Docker Compose Önizleme desteği yerel olarak platform eklediniz.</span><span class="sxs-lookup"><span data-stu-id="40df2-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="40df2-107">Service Fabric sürüm 3 ve sonraki kabul edebileceği `docker-compose.yml` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="40df2-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="40df2-108">Bu destek önizlemede olmadığından, yalnızca bir alt kümesini oluşturma yönergeleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="40df2-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="40df2-109">Örneğin, uygulama yükseltmeler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="40df2-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="40df2-110">Ancak, istediğiniz zaman kaldırma ve bunları yükseltme yerine uygulamaları dağıtma.</span><span class="sxs-lookup"><span data-stu-id="40df2-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="40df2-111">Bu önizleme özelliğini kullanmak için 5.7 veya büyük karşılık gelen SDK ile birlikte Azure portalı üzerinden Service Fabric çalışma zamanı sürümü ile kümenizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40df2-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="40df2-112">Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="40df2-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="40df2-113">Service Fabric Docker Compose bir dosyada dağıtma</span><span class="sxs-lookup"><span data-stu-id="40df2-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="40df2-114">Aşağıdaki komutlar bir Service Fabric uygulaması oluşturma (adlı `fabric:/TestContainerApp` önceki örnekte), hangi izleyebilir ve başka bir Service Fabric uygulaması gibi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40df2-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="40df2-115">Sistem durumu sorgularının sayısı için belirtilen uygulama adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40df2-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="40df2-116">PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="40df2-116">Use PowerShell</span></span>

<span data-ttu-id="40df2-117">Service Fabric oluşturan bir uygulama, PowerShell içinde aşağıdaki komutu çalıştırarak bir docker-compose.yml dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="40df2-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="40df2-118">`RegistryUserName`ve `RegistryPassword` kapsayıcı kayıt defteri kullanıcı adı ve parola bakın.</span><span class="sxs-lookup"><span data-stu-id="40df2-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="40df2-119">Uygulama tamamladıktan sonra aşağıdaki komutu kullanarak durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40df2-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="40df2-120">PowerShell aracılığıyla oluşturma uygulamayı silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="40df2-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="40df2-121">Azure Service Fabric CLI (sfctl) kullanın</span><span class="sxs-lookup"><span data-stu-id="40df2-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="40df2-122">Alternatif olarak, aşağıdaki Service Fabric CLI komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40df2-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="40df2-123">Uygulamayı oluşturduktan sonra aşağıdaki komutu kullanarak durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40df2-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="40df2-124">Oluşturma uygulamayı silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="40df2-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="40df2-125">Desteklenen oluşturma yönergeleri</span><span class="sxs-lookup"><span data-stu-id="40df2-125">Supported Compose directives</span></span>

<span data-ttu-id="40df2-126">Bu önizleme bir alt kümesini aşağıdaki temelleri dahil olmak üzere Oluştur sürüm 3 biçiminden yapılandırma seçeneklerini destekler:</span><span class="sxs-lookup"><span data-stu-id="40df2-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="40df2-127">Hizmetleri > dağıtmak > çoğaltmaları</span><span class="sxs-lookup"><span data-stu-id="40df2-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="40df2-128">Hizmetleri > dağıtmak > yerleştirme > kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="40df2-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="40df2-129">Hizmetleri > dağıtmak > kaynak > sınırları</span><span class="sxs-lookup"><span data-stu-id="40df2-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="40df2-130">cpu-paylaşımları</span><span class="sxs-lookup"><span data-stu-id="40df2-130">-cpu-shares</span></span>
    * <span data-ttu-id="40df2-131">-bellek</span><span class="sxs-lookup"><span data-stu-id="40df2-131">-memory</span></span>
    * <span data-ttu-id="40df2-132">-bellek-değiştirme</span><span class="sxs-lookup"><span data-stu-id="40df2-132">-memory-swap</span></span>
* <span data-ttu-id="40df2-133">Hizmetleri > komutları</span><span class="sxs-lookup"><span data-stu-id="40df2-133">Services > Commands</span></span>
* <span data-ttu-id="40df2-134">Hizmetleri > ortamı</span><span class="sxs-lookup"><span data-stu-id="40df2-134">Services > Environment</span></span>
* <span data-ttu-id="40df2-135">Hizmetleri > bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="40df2-135">Services > Ports</span></span>
* <span data-ttu-id="40df2-136">Hizmetleri > görüntüsü</span><span class="sxs-lookup"><span data-stu-id="40df2-136">Services > Image</span></span>
* <span data-ttu-id="40df2-137">Hizmetleri > yalıtımını (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="40df2-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="40df2-138">Hizmetleri > günlüğü > sürücüsü</span><span class="sxs-lookup"><span data-stu-id="40df2-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="40df2-139">Hizmetleri > günlüğü > sürücü > Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="40df2-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="40df2-140">Birim & dağıtmak > birim</span><span class="sxs-lookup"><span data-stu-id="40df2-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="40df2-141">Bölümünde açıklandığı gibi kaynak sınırları, zorlama küme ayarlamak [Service Fabric kaynak İdaresi](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="40df2-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="40df2-142">Tüm diğer Docker Compose yönergeleri Bu önizleme için desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="40df2-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="40df2-143">ServiceDnsName hesaplama</span><span class="sxs-lookup"><span data-stu-id="40df2-143">ServiceDnsName computation</span></span>

<span data-ttu-id="40df2-144">Bir oluşturma dosyasında belirttiğiniz hizmet adını bir tam etki alanı adı ise (diğer bir deyişle, bir nokta [.] içerdiği), Service Fabric tarafından kayıtlı DNS adı `<ServiceName>` (nokta dahil).</span><span class="sxs-lookup"><span data-stu-id="40df2-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="40df2-145">Aksi durumda, her yol kesimi uygulama ad hizmeti DNS adı, üst düzey etki alanı etiketi olma ilk yol kesimi ile etki alanı etiketi olur.</span><span class="sxs-lookup"><span data-stu-id="40df2-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="40df2-146">Örneğin, belirtilen uygulama adı ise `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` kayıtlı DNS adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="40df2-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="40df2-147">Oluştur (örnek tanım) ve Service Fabric uygulama modeli (tür tanımı) arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="40df2-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="40df2-148">Docker-compose.yml dosyası kapsayıcılar kendi özellikler ve yapılandırmalar da dahil olmak üzere, dağıtılabilir bir dizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="40df2-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="40df2-149">Örneğin, dosyayı ortam değişkenleri ve bağlantı noktası içerebilir.</span><span class="sxs-lookup"><span data-stu-id="40df2-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="40df2-150">Docker-compose.yml dosyası kısıtlamalarından, kaynak sınırları ve DNS adları gibi dağıtım parametreleri de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40df2-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="40df2-151">[Service Fabric uygulama modeli](service-fabric-application-model.md) kullandığı hizmet türlerini ve aynı türde pek çok uygulama örnekleri bulunan uygulama türleri.</span><span class="sxs-lookup"><span data-stu-id="40df2-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="40df2-152">Örneğin, müşteri başına bir uygulama örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="40df2-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="40df2-153">Bu tür tabanlı modeli, çalışma zamanı ile kayıtlı aynı uygulama türünün birden fazla sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="40df2-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="40df2-154">Örneğin, bir müşterinin AppTypeA 1.0 türüyle örneği bir uygulama olabilir ve Müşteri B aynı türü ve sürümü örneği başka bir uygulama olabilir.</span><span class="sxs-lookup"><span data-stu-id="40df2-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="40df2-155">Uygulama bildirimleri uygulama türlerini tanımlayın ve uygulama oluşturduğunuzda uygulama adı ve dağıtım parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="40df2-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="40df2-156">Bu model esneklik sunar ancak biz de türleri bildirim dosyasından örtük nerede daha basit ve örnek tabanlı dağıtım modelini destekleyen planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="40df2-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="40df2-157">Bu modelde, her uygulamanın kendi bağımsız bildirimi alır.</span><span class="sxs-lookup"><span data-stu-id="40df2-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="40df2-158">Biz bu çalışmaların örneği tabanlı dağıtım biçimi olduğu docker-compose.yml için destek ekleyerek önizlemede.</span><span class="sxs-lookup"><span data-stu-id="40df2-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40df2-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40df2-159">Next steps</span></span>

* <span data-ttu-id="40df2-160">Üzerinde okuma [Service Fabric uygulama modeli](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="40df2-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="40df2-161">Service Fabric CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="40df2-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
