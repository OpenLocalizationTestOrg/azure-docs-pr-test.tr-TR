---
title: "Azure Service Fabric CLI kullanarak aaaManage Azure Service Fabric uygulamaları"
description: "Azure Service Fabric CLI kullanarak bir Azure Service Fabric toodeploy ekleme ve kaldırma uygulamalardan nasıl küme öğrenin"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="08c04-103">Azure Service Fabric uygulaması Azure Service Fabric CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="08c04-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="08c04-104">Bilgi nasıl bir Azure Service Fabric kümede çalışan toocreate ve delete uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="08c04-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08c04-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="08c04-105">Prerequisites</span></span>

* <span data-ttu-id="08c04-106">Service Fabric CLI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08c04-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="08c04-107">Ardından, Service Fabric kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="08c04-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="08c04-108">Daha fazla bilgi için bkz: [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="08c04-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="08c04-109">Dağıtılan bir Service Fabric uygulama paketi hazır toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="08c04-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="08c04-110">Hakkında daha fazla bilgi için tooauthor ve bir uygulama paketi okuma hakkında hello [Service Fabric uygulama modeli](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="08c04-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="08c04-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="08c04-111">Overview</span></span>

<span data-ttu-id="08c04-112">toodeploy yeni bir uygulama, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="08c04-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="08c04-113">Bir uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08c04-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="08c04-114">Uygulama türü sağlayın.</span><span class="sxs-lookup"><span data-stu-id="08c04-114">Provision an application type.</span></span>
3. <span data-ttu-id="08c04-115">Bir uygulama oluşturmak ve belirtin.</span><span class="sxs-lookup"><span data-stu-id="08c04-115">Specify and create an application.</span></span>
4. <span data-ttu-id="08c04-116">Hizmetleri oluşturmak ve belirtin.</span><span class="sxs-lookup"><span data-stu-id="08c04-116">Specify and create services.</span></span>

<span data-ttu-id="08c04-117">tooremove varolan bir uygulamayı aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="08c04-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="08c04-118">Merhaba uygulaması silin.</span><span class="sxs-lookup"><span data-stu-id="08c04-118">Delete hello application.</span></span>
2. <span data-ttu-id="08c04-119">Sağlamayı kaldırma hello ilişkili uygulama türü.</span><span class="sxs-lookup"><span data-stu-id="08c04-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="08c04-120">Merhaba görüntü deposu içeriğini silin.</span><span class="sxs-lookup"><span data-stu-id="08c04-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="08c04-121">Yeni bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="08c04-121">Deploy a new application</span></span>

<span data-ttu-id="08c04-122">toodeploy yeni bir uygulama görevleri aşağıdaki tam hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="08c04-123">Yeni bir uygulama paketi toohello görüntü deposu karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="08c04-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="08c04-124">Bir uygulamayı oluşturmadan önce hello uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08c04-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="08c04-125">Örneğin, uygulama paketinizi hello ise `app_package_dir` dizin, aşağıdaki komutları tooupload hello dizin kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="08c04-126">Büyük uygulama paketlerini hello belirtebilirsiniz `--show-progress` seçeneği toodisplay hello hello karşıya yükleme ilerlemesini.</span><span class="sxs-lookup"><span data-stu-id="08c04-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="08c04-127">Sağlama hello uygulama türü</span><span class="sxs-lookup"><span data-stu-id="08c04-127">Provision hello application type</span></span>

<span data-ttu-id="08c04-128">Merhaba karşıya yükleme tamamlandığında, hello uygulaması sağlayın.</span><span class="sxs-lookup"><span data-stu-id="08c04-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="08c04-129">tooprovision hello uygulama, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="08c04-130">Merhaba değeri `application-type-build-path` uygulama paketinizi karşıya burada hello dizin hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="08c04-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="08c04-131">Bir uygulama türü ile uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c04-131">Create an application from an application type</span></span>

<span data-ttu-id="08c04-132">Merhaba uygulaması sağlama sonra komut tooname aşağıdaki hello kullanın ve uygulamanızı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="08c04-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="08c04-133">`app-name`Merhaba'a kadar olan hello uygulama örneğini toouse istediğiniz addır.</span><span class="sxs-lookup"><span data-stu-id="08c04-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="08c04-134">Daha önceden hazırlanan uygulama bildirimden ek parametreler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c04-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="08c04-135">Merhaba uygulama adı, hello önek ile başlamalı `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="08c04-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="08c04-136">Merhaba yeni uygulama hizmetleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c04-136">Create services for hello new application</span></span>

<span data-ttu-id="08c04-137">Bir uygulama oluşturduktan sonra hizmetleri hello uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c04-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="08c04-138">Aşağıdaki örneğine hello bizim uygulamadan yeni bir durum bilgisiz hizmet oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="08c04-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="08c04-139">bir uygulama oluşturun hello Hizmetleri hizmet bildirimi hello daha önceden hazırlanan uygulama paketinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="08c04-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="08c04-140">Uygulama dağıtımı ve durumunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="08c04-140">Verify application deployment and health</span></span>

<span data-ttu-id="08c04-141">tooverify her şeyi sağlıklı olduğundan, sistem durumu komutları aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="08c04-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="08c04-142">Merhaba hizmetin sistem durumunun iyi olduğundan tooverify benzer komutları tooretrieve hello sistem hello hizmet ve uygulama durumunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="08c04-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="08c04-143">Sağlıklı hizmetler ve uygulamalar sahip bir `HealthState` değerini `Ok`.</span><span class="sxs-lookup"><span data-stu-id="08c04-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="08c04-144">Varolan bir uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="08c04-144">Remove an existing application</span></span>

<span data-ttu-id="08c04-145">tooremove bir uygulama görevleri aşağıdaki tam hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="08c04-146">Merhaba uygulamayı Sil</span><span class="sxs-lookup"><span data-stu-id="08c04-146">Delete hello application</span></span>

<span data-ttu-id="08c04-147">toodelete hello uygulama, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="08c04-148">Merhaba uygulama türü sağlama</span><span class="sxs-lookup"><span data-stu-id="08c04-148">Unprovision hello application type</span></span>

<span data-ttu-id="08c04-149">Merhaba uygulaması sildikten sonra artık ihtiyacınız varsa hello uygulama türü sağlamasını.</span><span class="sxs-lookup"><span data-stu-id="08c04-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="08c04-150">toounprovision hello uygulama türü, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="08c04-151">Merhaba türü adını ve türünü sürümü hello adı ve sürümü hello daha önceden hazırlanan uygulama bildiriminde eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c04-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="08c04-152">Merhaba uygulama paketini silmeniz</span><span class="sxs-lookup"><span data-stu-id="08c04-152">Delete hello application package</span></span>

<span data-ttu-id="08c04-153">Merhaba uygulama türü sağlamasını sonra artık ihtiyacınız varsa, hello uygulama paketi hello görüntü deposundan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c04-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="08c04-154">Uygulama paketleri silme, disk alanını boşaltmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="08c04-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="08c04-155">Merhaba görüntü deposundan komutu aşağıdaki kullanım hello toodelete hello uygulama paketi:</span><span class="sxs-lookup"><span data-stu-id="08c04-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="08c04-156">`content-path`Merhaba uygulaması oluşturduğunuzda yüklediğiniz hello dizinin Hello adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="08c04-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="08c04-157">Uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="08c04-157">Upgrade application</span></span>

<span data-ttu-id="08c04-158">Uygulamanızı oluşturduktan sonra bunu yineleyebilir hello aynı adımları tooprovision ikinci sürümü, uygulamanızın kümesi.</span><span class="sxs-lookup"><span data-stu-id="08c04-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="08c04-159">Ardından, Service Fabric uygulama yükseltme işlemine toorunning hello ikinci sürümü Merhaba uygulaması geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="08c04-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="08c04-160">Daha fazla bilgi için üzerinde hello belgelerine bakın. [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="08c04-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="08c04-161">tooperform, yükseltme uygulama hello kullanarak ilk sağlama hello ileri sürümünü aynı komutları önceki gibi hello:</span><span class="sxs-lookup"><span data-stu-id="08c04-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="08c04-162">Tooperform izlenen otomatik yükseltmeyi başlatın ardından hello yükseltme hello aşağıdaki komutu çalıştırarak önerilir:</span><span class="sxs-lookup"><span data-stu-id="08c04-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="08c04-163">Yükseltmeler ne olursa olsun kümesi belirtilen ile varolan parametreler geçersiz.</span><span class="sxs-lookup"><span data-stu-id="08c04-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="08c04-164">Uygulama parametreleri bağımsız değişkenleri toohello yükseltme komutu, gerekirse geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c04-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="08c04-165">Uygulama parametreleri bir JSON nesnesi olarak kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="08c04-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="08c04-166">tooretrieve herhangi bir parametre daha önce belirtilen, hello kullanabilirsiniz `sfctl application info` komutu.</span><span class="sxs-lookup"><span data-stu-id="08c04-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="08c04-167">Uygulama yükseltme devam ederken, hello durum kullanılarak alınabilir `sfctl application upgrade-status` komutu.</span><span class="sxs-lookup"><span data-stu-id="08c04-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="08c04-168">Son olarak, bir yükseltme devam ediyor ve iptal toobe gerekirse hello kullanabilirsiniz `sfctl application upgrade-rollback` geri tooroll hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="08c04-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08c04-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08c04-169">Next steps</span></span>

* [<span data-ttu-id="08c04-170">Service Fabric CLI temelleri</span><span class="sxs-lookup"><span data-stu-id="08c04-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="08c04-171">Service Fabric Linux'ta ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="08c04-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="08c04-172">Service Fabric uygulama yükseltme başlatma</span><span class="sxs-lookup"><span data-stu-id="08c04-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
