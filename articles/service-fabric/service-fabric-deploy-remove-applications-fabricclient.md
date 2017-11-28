---
title: "aaaAzure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "Merhaba FabricClient API'leri toodeploy kullanın ve Service Fabric uygulamaları kaldırın."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="38382-103">Dağıtma ve FabricClient kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="38382-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38382-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38382-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="38382-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38382-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="38382-106">FabricClient API’leri</span><span class="sxs-lookup"><span data-stu-id="38382-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="38382-107">Bir kez bir [uygulama türü paketlenmiş][10], Azure Service Fabric kümesi içine dağıtımı için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="38382-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="38382-108">Dağıtım hello aşağıdaki üç adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="38382-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="38382-109">Merhaba uygulama paketi toohello görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="38382-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="38382-110">Merhaba uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="38382-110">Register hello application type</span></span>
3. <span data-ttu-id="38382-111">Merhaba uygulama örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="38382-111">Create hello application instance</span></span>

<span data-ttu-id="38382-112">Bir uygulamanın dağıtıldığını ve bir örnek hello kümede çalışan sonra hello uygulama örneği ve uygulama türünü silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38382-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="38382-113">bir uygulama hello kümeden toocompletely Kaldır hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="38382-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="38382-114">Uygulama örneğini çalıştıran hello Kaldır (veya Sil)</span><span class="sxs-lookup"><span data-stu-id="38382-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="38382-115">Artık ihtiyacınız varsa hello uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="38382-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="38382-116">Merhaba görüntü deposundan Hello uygulama paketini kaldırma</span><span class="sxs-lookup"><span data-stu-id="38382-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="38382-117">Kullanırsanız [uygulamalarında hata ayıklama ve dağıtma için Visual Studio](service-fabric-publish-app-remote-cluster.md) yerel geliştirme kümenizde yukarıdaki adımların tümünü hello bir PowerShell komut dosyası otomatik olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="38382-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="38382-118">Bu komut dosyası hello bulunan *komut dosyaları* hello uygulama projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="38382-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="38382-119">Bu makalede, gerçekleştirebilmeleri için komut dosyası yaptıklarını üzerinde arka plan sağlar hello Visual Studio dışında aynı işlemleri.</span><span class="sxs-lookup"><span data-stu-id="38382-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="38382-120">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="38382-120">Connect toohello cluster</span></span>
<span data-ttu-id="38382-121">Toohello küme oluşturarak bağlanabilecek bir [FabricClient](/dotnet/api/system.fabric.fabricclient) , herhangi bir hello bu makaledeki kod örnekleri çalıştırmadan önce örneği.</span><span class="sxs-lookup"><span data-stu-id="38382-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="38382-122">Bağlantı tooa yerel geliştirme küme veya uzaktan küme veya küme Azure Active Directory, X509 kullanılarak güvenli örnekleri için sertifikalar veya Windows Active Directory bkz [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="38382-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="38382-123">Merhaba aşağıdaki komutu çalıştırarak tooconnect toohello yerel geliştirme kümesi:</span><span class="sxs-lookup"><span data-stu-id="38382-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="38382-124">Merhaba uygulama paketini karşıya yükleyin</span><span class="sxs-lookup"><span data-stu-id="38382-124">Upload hello application package</span></span>
<span data-ttu-id="38382-125">Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38382-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="38382-126">Varsayılan olarak, "MyApplicationType" Merhaba ApplicationManifest.xml listelenen hello uygulama türü adı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="38382-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="38382-127">Merhaba hello gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\&lt; kullanıcı adı&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="38382-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="38382-128">Karşıya yükleme hello uygulama paketi hello iç Service Fabric bileşenleri tarafından erişilebilen bir konumda koyar.</span><span class="sxs-lookup"><span data-stu-id="38382-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="38382-129">Service Fabric hello uygulama paketi hello uygulama paketi hello kayıt sırasında doğrular.</span><span class="sxs-lookup"><span data-stu-id="38382-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="38382-130">(Yani, yüklemeden önce) tooverify hello uygulama paketi yerel olarak istiyorsanız, ancak hello kullanın [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="38382-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="38382-131">Merhaba [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API hello uygulama paketi toohello küme görüntü deposuna karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="38382-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="38382-132">Merhaba uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package) ve PowerShell kullanarak toohello Image store kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="38382-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="38382-133">Merhaba sıkıştırma hello boyutunu ve dosya hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="38382-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="38382-134">Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="38382-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="38382-135">YAZMAÇ hello uygulama paketi</span><span class="sxs-lookup"><span data-stu-id="38382-135">Register hello application package</span></span>
<span data-ttu-id="38382-136">Merhaba uygulama türü ve sürümü hello uygulama paketi kaydedildikten sonra kullanılabilir hale hello uygulama bildiriminde bildirildi.</span><span class="sxs-lookup"><span data-stu-id="38382-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="38382-137">Merhaba sistem hello önceki adımda karşıya yüklenen hello paket okur hello paket doğrular, hello paket içeriğini işler ve işlenen hello paket tooan iç sistem konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="38382-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="38382-138">Merhaba [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API yazmaçlar hello hello kümedeki uygulama türü ve dağıtım için kullanılabilir hale getirmek.</span><span class="sxs-lookup"><span data-stu-id="38382-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="38382-139">Merhaba [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API tüm başarıyla kayıtlı uygulama türleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="38382-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="38382-140">Merhaba kaydı yapıldığında bu API toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38382-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="38382-141">Uygulama örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="38382-141">Create an application instance</span></span>
<span data-ttu-id="38382-142">Hello kullanarak başarıyla kaydettirildi herhangi bir uygulama türü'ten bir uygulamanın örneği [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="38382-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="38382-143">her uygulamanın Hello adı hello ile başlamalı *"fabric:"* düzen ve her uygulama örneği (küme içinde) benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="38382-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="38382-144">Hello uygulama bildiriminde hello hedef uygulama türünün tanımlı hiçbir varsayılan hizmetleri de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="38382-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="38382-145">Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="38382-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="38382-146">Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlemleri kümesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="38382-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="38382-147">uygulamalar ve hizmetler olarak adlandırılan toosee hello çalıştırmak hello kümede çalışan [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) ve [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API'leri.</span><span class="sxs-lookup"><span data-stu-id="38382-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="38382-148">Bir hizmet örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="38382-148">Create a service instance</span></span>
<span data-ttu-id="38382-149">Hello kullanarak bir hizmet türünün alanından bir hizmet örneği [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="38382-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="38382-150">Merhaba hizmeti varsayılan hizmet hello uygulama bildiriminde olarak bildirilirse hello uygulama örneği oluşturulduğunda hello hizmet örneği.</span><span class="sxs-lookup"><span data-stu-id="38382-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="38382-151">Arama hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API zaten örneği bir hizmet için bir hata kodu FabricErrorCode.ServiceAlreadyExists değerini içeren FabricException türünde bir özel durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="38382-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="38382-152">Bir hizmet örneği Kaldır</span><span class="sxs-lookup"><span data-stu-id="38382-152">Remove a service instance</span></span>
<span data-ttu-id="38382-153">Bir hizmet örneği artık gerekli olmadığında, bu uygulama örneği tarafından arama hello çalıştıran hello kaldırabilirsiniz [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="38382-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="38382-154">Bu işlem geri alınamaz ve hizmet durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="38382-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="38382-155">Bir uygulama örneğini kaldırma</span><span class="sxs-lookup"><span data-stu-id="38382-155">Remove an application instance</span></span>
<span data-ttu-id="38382-156">Uygulama örneğini artık gerekli olmadığında kalıcı olarak hello kullanarak adıyla kaldırabilirsiniz [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="38382-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="38382-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) tüm hizmet durumunu da, kalıcı olarak kaldırma toohello uygulama ait tüm hizmetleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="38382-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="38382-158">Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="38382-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="38382-159">Bir uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="38382-159">Unregister an application type</span></span>
<span data-ttu-id="38382-160">Belirli bir uygulama türü sürümü artık gerekli olmadığında bu belirli sürümü hello kullanarak hello uygulama türü kaydını [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="38382-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="38382-161">Uygulama türü sürümleri depolama alanı hello Image store tarafından kullanılan kaydı siliniyor kullanılmayan sürümleri.</span><span class="sxs-lookup"><span data-stu-id="38382-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="38382-162">Uygulama türü sürümü, uygulama bu hello uygulama türü sürümü karşı örneği ve hiçbir bekleyen uygulama yükseltmesi hello uygulama türü sürümünün başvurduğunuzdan sürece kaydı olabilir.</span><span class="sxs-lookup"><span data-stu-id="38382-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="38382-163">Bir uygulama paketi hello görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="38382-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="38382-164">Bir uygulama paketi artık gerekli olmadığında hello görüntü deposu toofree hello kullanarak sistem kaynaklarının gelen silebilmek [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="38382-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="38382-165">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="38382-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="38382-166">Kopya ServiceFabricApplicationPackage bir ImageStoreConnectionString için sorar</span><span class="sxs-lookup"><span data-stu-id="38382-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="38382-167">Merhaba Service Fabric SDK ortam zaten hello Varsayılanlarını Ayarla doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="38382-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="38382-168">Ancak gerekirse, hello ImageStoreConnectionString tüm komutlar için Service Fabric kümesi kullanarak bu hello hello değeri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="38382-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="38382-169">Merhaba küme bildiriminde hello ImageStoreConnectionString bulabilirsiniz hello kullanarak alınan [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) ve Get-ImageStoreConnectionStringFromClusterManifest komutlar:</span><span class="sxs-lookup"><span data-stu-id="38382-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="38382-170">Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="38382-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="38382-171">çalıştırma tooimport hello SDK Modülü:</span><span class="sxs-lookup"><span data-stu-id="38382-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="38382-172">Merhaba ImageStoreConnectionString hello küme bildiriminde bulunur:</span><span class="sxs-lookup"><span data-stu-id="38382-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="38382-173">Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="38382-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="38382-174">Büyük uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="38382-174">Deploy large application package</span></span>
<span data-ttu-id="38382-175">Sorun: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API zaman aşımına uğruyor büyük uygulama paketi (GB sırasını).</span><span class="sxs-lookup"><span data-stu-id="38382-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="38382-176">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="38382-176">Try:</span></span>
- <span data-ttu-id="38382-177">Daha büyük zaman aşımını belirtmek [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) yöntemi ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="38382-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="38382-178">Varsayılan olarak, hello zaman aşımı 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="38382-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="38382-179">Kaynak makine ve küme arasındaki Hello ağ bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="38382-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="38382-180">Merhaba bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="38382-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="38382-181">Merhaba istemci makine hello küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede hello küme olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="38382-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="38382-182">Dış azaltma devreyi olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="38382-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="38382-183">Örneğin, Hello Image store yapılandırılmış toouse azure depolama olduğunda, karşıya yükleme kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="38382-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="38382-184">Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API zaman aşımına uğradı. Deneyin:</span><span class="sxs-lookup"><span data-stu-id="38382-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="38382-185">[Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.</span><span class="sxs-lookup"><span data-stu-id="38382-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="38382-186">Hello sıkıştırma hello boyutunu azaltır ve hangi sırayla hello trafik miktarını azaltır ve bu Service Fabric çalışma hello dosya sayısı, gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38382-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="38382-187">Merhaba karşıya yükleme işlemi (özellikle hello sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak daha hızlı kaydedin ve kaydı hello uygulama türü.</span><span class="sxs-lookup"><span data-stu-id="38382-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="38382-188">Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API'si ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="38382-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="38382-189">Birçok dosyalarıyla uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="38382-189">Deploy application package with many files</span></span>
<span data-ttu-id="38382-190">Sorun: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).</span><span class="sxs-lookup"><span data-stu-id="38382-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="38382-191">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="38382-191">Try:</span></span>
- <span data-ttu-id="38382-192">[Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.</span><span class="sxs-lookup"><span data-stu-id="38382-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="38382-193">Merhaba sıkıştırma dosyaları hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="38382-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="38382-194">Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="38382-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="38382-195">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="38382-195">Code example</span></span>
<span data-ttu-id="38382-196">Merhaba aşağıdaki örnek bir uygulama paketi toohello görüntü deposu kopyalar, hazırlar hello uygulama türü, uygulama örneğini oluşturur, hello uygulama türü, bir hizmet örneği, kaldırır hello Uygulama örneğinin kaydını hükümleri oluşturur ve Merhaba uygulama paketi hello görüntü deposundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="38382-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="38382-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38382-197">Next steps</span></span>
[<span data-ttu-id="38382-198">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="38382-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="38382-199">Service Fabric sistem durumu giriş</span><span class="sxs-lookup"><span data-stu-id="38382-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="38382-200">Tanılama ve bir Service Fabric hizmeti sorun giderme</span><span class="sxs-lookup"><span data-stu-id="38382-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="38382-201">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="38382-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
