---
title: "Azure CLI 2.0 kullanarak aaaManage Azure Service Fabric uygulamaları"
description: "Azure CLI 2.0 kullanarak bir Azure Service Fabric toodeploy ekleme ve kaldırma uygulamalardan nasıl küme öğrenin."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="04a45-103">Azure Service Fabric uygulaması Azure CLI 2.0 kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="04a45-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="04a45-104">Bilgi nasıl bir Azure Service Fabric kümede çalışan toocreate ve delete uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="04a45-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04a45-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="04a45-105">Prerequisites</span></span>

* <span data-ttu-id="04a45-106">Azure CLI 2.0 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="04a45-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="04a45-107">Ardından, Service Fabric kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="04a45-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="04a45-108">Daha fazla bilgi için bkz: [Azure CLI 2.0 ile çalışmaya başlama](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="04a45-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="04a45-109">Dağıtılan bir Service Fabric uygulama paketi hazır toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="04a45-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="04a45-110">Hakkında daha fazla bilgi için tooauthor ve bir uygulama paketi okuma hakkında hello [Service Fabric uygulama modeli](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="04a45-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="04a45-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="04a45-111">Overview</span></span>

<span data-ttu-id="04a45-112">toodeploy yeni bir uygulama, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="04a45-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="04a45-113">Bir uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="04a45-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="04a45-114">Uygulama türü sağlayın.</span><span class="sxs-lookup"><span data-stu-id="04a45-114">Provision an application type.</span></span>
3. <span data-ttu-id="04a45-115">Bir uygulama oluşturmak ve belirtin.</span><span class="sxs-lookup"><span data-stu-id="04a45-115">Specify and create an application.</span></span>
4. <span data-ttu-id="04a45-116">Hizmetleri oluşturmak ve belirtin.</span><span class="sxs-lookup"><span data-stu-id="04a45-116">Specify and create services.</span></span>

<span data-ttu-id="04a45-117">tooremove varolan bir uygulamayı aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="04a45-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="04a45-118">Merhaba uygulaması silin.</span><span class="sxs-lookup"><span data-stu-id="04a45-118">Delete hello application.</span></span>
2. <span data-ttu-id="04a45-119">Sağlamayı kaldırma hello ilişkili uygulama türü.</span><span class="sxs-lookup"><span data-stu-id="04a45-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="04a45-120">Merhaba görüntü deposu içeriğini silin.</span><span class="sxs-lookup"><span data-stu-id="04a45-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="04a45-121">Yeni bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="04a45-121">Deploy a new application</span></span>

<span data-ttu-id="04a45-122">toodeploy yeni bir uygulama görevleri aşağıdaki tam hello.</span><span class="sxs-lookup"><span data-stu-id="04a45-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="04a45-123">Yeni bir uygulama paketi toohello görüntü deposu karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="04a45-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="04a45-124">Bir uygulamayı oluşturmadan önce hello uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="04a45-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="04a45-125">Örneğin, uygulama paketinizi hello ise `app_package_dir` dizin, aşağıdaki komutları tooupload hello dizin kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="04a45-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="04a45-126">Büyük uygulama paketlerini hello belirtebilirsiniz `--show-progress` seçeneği toodisplay hello hello karşıya yükleme ilerlemesini.</span><span class="sxs-lookup"><span data-stu-id="04a45-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="04a45-127">Sağlama hello uygulama türü</span><span class="sxs-lookup"><span data-stu-id="04a45-127">Provision hello application type</span></span>

<span data-ttu-id="04a45-128">Merhaba karşıya yükleme tamamlandığında, hello uygulaması sağlayın.</span><span class="sxs-lookup"><span data-stu-id="04a45-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="04a45-129">tooprovision hello uygulama, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="04a45-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="04a45-130">Merhaba değeri `application-type-build-path` uygulama paketinizi karşıya burada hello dizin hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="04a45-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="04a45-131">Bir uygulama türü ile uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="04a45-131">Create an application from an application type</span></span>

<span data-ttu-id="04a45-132">Merhaba uygulaması sağlama sonra komut tooname aşağıdaki hello kullanın ve uygulamanızı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="04a45-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="04a45-133">`app-name`Merhaba'a kadar olan hello uygulama örneğini toouse istediğiniz addır.</span><span class="sxs-lookup"><span data-stu-id="04a45-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="04a45-134">Ek parametreler hello daha önceden hazırlanan uygulama bildirimden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04a45-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="04a45-135">Merhaba uygulama adı, hello önek ile başlamalı `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="04a45-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="04a45-136">Merhaba yeni uygulama hizmetleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="04a45-136">Create services for hello new application</span></span>

<span data-ttu-id="04a45-137">Bir uygulama oluşturduktan sonra hizmetleri hello uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04a45-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="04a45-138">Aşağıdaki örneğine hello bizim uygulamadan yeni bir durum bilgisiz hizmet oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="04a45-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="04a45-139">bir uygulama oluşturun hello Hizmetleri hizmet bildirimi hello daha önceden hazırlanan uygulama paketinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="04a45-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="04a45-140">Uygulama dağıtımı ve durumunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="04a45-140">Verify application deployment and health</span></span>

<span data-ttu-id="04a45-141">bir uygulama ve hizmet başarılı bir şekilde dağıtılan olduğunu, tooverify denetleyin hello uygulama ve hizmet listelenir:</span><span class="sxs-lookup"><span data-stu-id="04a45-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="04a45-142">Merhaba hizmetin sistem durumunun iyi olduğundan tooverify benzer komutları tooretrieve hello durumunu hello hizmeti ile Merhaba uygulama kullanın:</span><span class="sxs-lookup"><span data-stu-id="04a45-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="04a45-143">Sağlıklı hizmetler ve uygulamalar sahip bir `HealthState` değerini `Ok`.</span><span class="sxs-lookup"><span data-stu-id="04a45-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="04a45-144">Varolan bir uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="04a45-144">Remove an existing application</span></span>

<span data-ttu-id="04a45-145">tooremove bir uygulama görevleri aşağıdaki tam hello.</span><span class="sxs-lookup"><span data-stu-id="04a45-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="04a45-146">Merhaba uygulamayı Sil</span><span class="sxs-lookup"><span data-stu-id="04a45-146">Delete hello application</span></span>

<span data-ttu-id="04a45-147">toodelete hello uygulama, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="04a45-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="04a45-148">Merhaba uygulama türü sağlama</span><span class="sxs-lookup"><span data-stu-id="04a45-148">Unprovision hello application type</span></span>

<span data-ttu-id="04a45-149">Merhaba uygulaması sildikten sonra artık ihtiyacınız varsa hello uygulama türü sağlamasını.</span><span class="sxs-lookup"><span data-stu-id="04a45-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="04a45-150">toounprovision hello uygulama türü, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="04a45-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="04a45-151">Merhaba türü adını ve türünü sürümü hello adı ve sürümü hello daha önceden hazırlanan uygulama bildiriminde eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="04a45-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="04a45-152">Merhaba uygulama paketini silmeniz</span><span class="sxs-lookup"><span data-stu-id="04a45-152">Delete hello application package</span></span>

<span data-ttu-id="04a45-153">Merhaba uygulama türü sağlamasını sonra artık ihtiyacınız varsa, hello uygulama paketi hello görüntü deposundan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04a45-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="04a45-154">Uygulama paketleri silme, disk alanını boşaltmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="04a45-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="04a45-155">Merhaba görüntü deposundan komutu aşağıdaki kullanım hello toodelete hello uygulama paketi:</span><span class="sxs-lookup"><span data-stu-id="04a45-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="04a45-156">`content-path`Merhaba uygulaması oluşturduğunuzda yüklediğiniz hello dizinin Hello adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04a45-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="04a45-157">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="04a45-157">Related articles</span></span>

* [<span data-ttu-id="04a45-158">Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="04a45-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="04a45-159">Service Fabric XPlat CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="04a45-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
