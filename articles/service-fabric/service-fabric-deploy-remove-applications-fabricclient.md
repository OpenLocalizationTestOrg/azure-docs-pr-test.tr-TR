---
title: "Azure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "FabricClient API'ları dağıtmak ve Service Fabric uygulamaları kaldırmak için kullanın."
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
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="c494c-103">Dağıtma ve FabricClient kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="c494c-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c494c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c494c-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="c494c-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c494c-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="c494c-106">FabricClient API’leri</span><span class="sxs-lookup"><span data-stu-id="c494c-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="c494c-107">Bir kez bir [uygulama türü paketlenmiş][10], Azure Service Fabric kümesi içine dağıtımı için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="c494c-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="c494c-108">Dağıtım aşağıdaki üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="c494c-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="c494c-109">Uygulama paketi görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="c494c-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="c494c-110">Uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="c494c-110">Register the application type</span></span>
3. <span data-ttu-id="c494c-111">Uygulama örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c494c-111">Create the application instance</span></span>

<span data-ttu-id="c494c-112">Bir uygulamanın dağıtıldığını ve bir örnek kümede çalışan sonra uygulama örneği ve uygulama türünü silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c494c-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="c494c-113">Bir uygulamayı kümeden tamamen kaldırmak için aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="c494c-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="c494c-114">Çalışan Kaldır (veya Sil) uygulama örneği</span><span class="sxs-lookup"><span data-stu-id="c494c-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="c494c-115">Artık ihtiyacınız varsa uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="c494c-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="c494c-116">Uygulama paketi görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="c494c-116">Remove the application package from the image store</span></span>

<span data-ttu-id="c494c-117">Kullanırsanız [uygulamalarında hata ayıklama ve dağıtma için Visual Studio](service-fabric-publish-app-remote-cluster.md) yerel geliştirme kümenizde yukarıdaki adımların tümünü otomatik olarak bir PowerShell komut dosyası işlenir.</span><span class="sxs-lookup"><span data-stu-id="c494c-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="c494c-118">Bu komut dosyası içinde bulunur *betikleri* uygulama projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="c494c-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="c494c-119">Bu makalede, Visual Studio dışında aynı işlemleri gerçekleştirebilmeleri için komut dosyası yaptıklarını üzerinde arka plan sağlar.</span><span class="sxs-lookup"><span data-stu-id="c494c-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="c494c-120">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="c494c-120">Connect to the cluster</span></span>
<span data-ttu-id="c494c-121">Oluşturarak kümeye bağlanın bir [FabricClient](/dotnet/api/system.fabric.fabricclient) bu makaledeki kod örnekleri birini çalıştırmadan önce örneği.</span><span class="sxs-lookup"><span data-stu-id="c494c-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="c494c-122">Yerel bir geliştirme kümesi veya bir uzak küme veya Azure Active Directory, X509 kullanılarak güvenlik altına kümeye bağlanma örnekleri için sertifikalar veya Windows Active Directory bkz [güvenli kümeye Bağlan](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="c494c-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="c494c-123">Yerel geliştirme kümeye bağlanmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c494c-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="c494c-124">Uygulama paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="c494c-124">Upload the application package</span></span>
<span data-ttu-id="c494c-125">Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c494c-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="c494c-126">Varsayılan olarak, ApplicationManifest.xml listelenen uygulama türü adı "MyApplicationType" bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c494c-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="c494c-127">Gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\&lt; kullanıcı adı&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="c494c-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="c494c-128">Uygulama paketini karşıya yükleme, iç Service Fabric bileşenleri tarafından erişilebilen bir konuma koyan.</span><span class="sxs-lookup"><span data-stu-id="c494c-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="c494c-129">Service Fabric uygulama paketi kaydı sırasında uygulama paketini doğrular.</span><span class="sxs-lookup"><span data-stu-id="c494c-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="c494c-130">Ancak, uygulama paketi yerel olarak (yani, yüklemeden önce) doğrulamak istiyorsanız, kullanmak [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c494c-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="c494c-131">[CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API küme görüntü deposu için uygulama paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="c494c-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="c494c-132">Uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package) ve PowerShell kullanarak görüntü deposuna kopyalama.</span><span class="sxs-lookup"><span data-stu-id="c494c-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="c494c-133">Sıkıştırma, boyutu ve dosya sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="c494c-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="c494c-134">Bkz: [görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) resim ve görüntü deposu hakkında ek bilgi için bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="c494c-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="c494c-135">Uygulama paketi Kaydet</span><span class="sxs-lookup"><span data-stu-id="c494c-135">Register the application package</span></span>
<span data-ttu-id="c494c-136">Uygulama türü ve sürümü, uygulama paketi kaydedildikten sonra kullanılabilir hale uygulama bildiriminde bildirildi.</span><span class="sxs-lookup"><span data-stu-id="c494c-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="c494c-137">Sistem önceki adımda karşıya yüklenen paket okur, paket doğrular, paket içeriğini işler ve işlenen paket bir iç sistem konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c494c-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="c494c-138">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) uygulama kümede yazın ve dağıtım kullanımına API kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c494c-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="c494c-139">[GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API tüm başarıyla kayıtlı uygulama türleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c494c-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="c494c-140">Bu API, kaydı yapıldığında belirlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c494c-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="c494c-141">Uygulama örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="c494c-141">Create an application instance</span></span>
<span data-ttu-id="c494c-142">Bir uygulama kullanarak başarıyla kaydettirildi herhangi bir uygulama türü örneği [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="c494c-143">Her bir uygulama adı ile başlamalıdır *"fabric:"* düzen ve her uygulama örneği (küme içinde) benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c494c-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="c494c-144">Hedef uygulama türü uygulama bildiriminde tanımlanan varsayılan hizmetlerin de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c494c-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="c494c-145">Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="c494c-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="c494c-146">Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlemleri kümesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="c494c-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="c494c-147">Hangi adlı görmek için uygulamalar ve hizmetler çalıştırmak kümede çalışan [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) ve [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API'leri.</span><span class="sxs-lookup"><span data-stu-id="c494c-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="c494c-148">Bir hizmet örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="c494c-148">Create a service instance</span></span>
<span data-ttu-id="c494c-149">Bir hizmet türünü kullanarak bir hizmet örneği [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="c494c-150">Hizmet, varsayılan hizmet uygulama bildiriminde olarak bildirilirse, uygulama örneği oluşturulduğunda hizmet örneği.</span><span class="sxs-lookup"><span data-stu-id="c494c-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="c494c-151">Çağırma [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API zaten örneği bir hizmet için bir hata kodu FabricErrorCode.ServiceAlreadyExists değerini içeren FabricException türünde bir özel durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="c494c-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="c494c-152">Bir hizmet örneği Kaldır</span><span class="sxs-lookup"><span data-stu-id="c494c-152">Remove a service instance</span></span>
<span data-ttu-id="c494c-153">Bir hizmet örneği artık gerekli olmadığında çalışmasını kaldırabilirsiniz çağırarak uygulama örneği [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="c494c-154">Bu işlem geri alınamaz ve hizmet durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="c494c-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="c494c-155">Bir uygulama örneğini kaldırma</span><span class="sxs-lookup"><span data-stu-id="c494c-155">Remove an application instance</span></span>
<span data-ttu-id="c494c-156">Uygulama örneğini artık gerekli olmadığında kalıcı olarak adını kullanarak kaldırabilirsiniz [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="c494c-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) tüm hizmet durumunu da, kalıcı olarak kaldırma uygulamaya ait tüm hizmetleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c494c-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="c494c-158">Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="c494c-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="c494c-159">Bir uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="c494c-159">Unregister an application type</span></span>
<span data-ttu-id="c494c-160">Belirli bir uygulama türü sürümü artık gerekli olduğunda, uygulama türünü kullanarak bu belirli sürümü kaydı [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="c494c-161">Kullanılmayan uygulama türleri sürümleri kaydını Image store tarafından kullanılan depolama alanını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="c494c-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="c494c-162">Uygulama türü sürümü, uygulama bu uygulama türü sürümü karşı örneği ve hiçbir bekleyen uygulama yükseltmesi bu uygulama türü sürümü başvurduğunuzdan sürece kaydı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c494c-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="c494c-163">Bir uygulama paketi görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="c494c-163">Remove an application package from the image store</span></span>
<span data-ttu-id="c494c-164">Bir uygulama paketi artık gerekli olmadığında kullanarak sistem kaynakları boşaltmak için görüntü deposundan silebilmek [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="c494c-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c494c-165">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c494c-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="c494c-166">Kopya ServiceFabricApplicationPackage bir ImageStoreConnectionString için sorar</span><span class="sxs-lookup"><span data-stu-id="c494c-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="c494c-167">Service Fabric SDK ortam zaten ayarlanmış doğru Varsayılanları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c494c-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="c494c-168">Ancak gerekirse, tüm komutlar için ImageStoreConnectionString Service Fabric kümesi kullanarak değer eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c494c-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="c494c-169">Küme bildiriminde ImageStoreConnectionString bulabilirsiniz kullanarak alınan [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) ve Get-ImageStoreConnectionStringFromClusterManifest komutlar:</span><span class="sxs-lookup"><span data-stu-id="c494c-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="c494c-170">**Get-ImageStoreConnectionStringFromClusterManifest** Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet, görüntü deposu bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c494c-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="c494c-171">SDK modülü içeri aktarmak için aşağıdakini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c494c-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="c494c-172">ImageStoreConnectionString küme bildiriminde bulunur:</span><span class="sxs-lookup"><span data-stu-id="c494c-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="c494c-173">Bkz: [görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) resim ve görüntü deposu hakkında ek bilgi için bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="c494c-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="c494c-174">Büyük uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="c494c-174">Deploy large application package</span></span>
<span data-ttu-id="c494c-175">Sorun: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API zaman aşımına uğruyor büyük uygulama paketi (GB sırasını).</span><span class="sxs-lookup"><span data-stu-id="c494c-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="c494c-176">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="c494c-176">Try:</span></span>
- <span data-ttu-id="c494c-177">Daha büyük zaman aşımını belirtmek [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) yöntemi ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c494c-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="c494c-178">Varsayılan olarak, zaman aşımı 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="c494c-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="c494c-179">Kaynak makine ve küme arasındaki ağ bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c494c-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="c494c-180">Bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c494c-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="c494c-181">İstemci makine küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede küme olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="c494c-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="c494c-182">Dış azaltma devreyi olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c494c-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="c494c-183">Örneğin, görüntü deposu azure depolama kullanacak şekilde yapılandırıldığında, karşıya yükleme kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="c494c-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="c494c-184">Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="c494c-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="c494c-185">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="c494c-185">Try:</span></span>
- <span data-ttu-id="c494c-186">[Paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) görüntü deposuna kopyalama önce.</span><span class="sxs-lookup"><span data-stu-id="c494c-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="c494c-187">Sıkıştırma küçültür ve hangi sırayla trafik miktarını azaltır ve bu Service Fabric çalışma dosyaları sayısı gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c494c-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="c494c-188">Karşıya yükleme işlemi (özellikle sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak kaydedin ve kaydı uygulama türü daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="c494c-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="c494c-189">Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API'si ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c494c-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="c494c-190">Birçok dosyalarıyla uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="c494c-190">Deploy application package with many files</span></span>
<span data-ttu-id="c494c-191">Sorun: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).</span><span class="sxs-lookup"><span data-stu-id="c494c-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="c494c-192">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="c494c-192">Try:</span></span>
- <span data-ttu-id="c494c-193">[Paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) görüntü deposuna kopyalama önce.</span><span class="sxs-lookup"><span data-stu-id="c494c-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="c494c-194">Sıkıştırma dosyalarının sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="c494c-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="c494c-195">Daha büyük zaman aşımını belirtmek [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) ile `timeout` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c494c-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="c494c-196">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="c494c-196">Code example</span></span>
<span data-ttu-id="c494c-197">Aşağıdaki örnek bir uygulama paketi görüntü deposuna kopyalar, uygulama türü sağlar, uygulama örneğini oluşturur, bir hizmet örneği oluşturur, uygulama türü kaydını hükümleri uygulama örneği kaldırır ve siler Uygulama paketi görüntü deposundan.</span><span class="sxs-lookup"><span data-stu-id="c494c-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

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

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
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

    //  Create the application instance.
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

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
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

    // Delete an application instance from the application type.
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

    // Un-provision the application type.
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

    // Delete the application package from a location in the image store.
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

## <a name="next-steps"></a><span data-ttu-id="c494c-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c494c-198">Next steps</span></span>
[<span data-ttu-id="c494c-199">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="c494c-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="c494c-200">Service Fabric sistem durumu giriş</span><span class="sxs-lookup"><span data-stu-id="c494c-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="c494c-201">Tanılama ve bir Service Fabric hizmeti sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c494c-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="c494c-202">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="c494c-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
