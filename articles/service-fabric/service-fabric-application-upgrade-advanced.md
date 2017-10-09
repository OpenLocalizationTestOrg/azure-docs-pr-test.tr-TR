---
title: "Uygulama yükseltme konuları aaaAdvanced | Microsoft Docs"
description: "Bu makalede tooupgrading Service Fabric uygulaması ilgili bazı gelişmiş konular ele alınmaktadır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="8a609-103">Service Fabric uygulama yükseltme: Gelişmiş konular</span><span class="sxs-lookup"><span data-stu-id="8a609-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="8a609-104">Ekleme veya uygulama yükseltme sırasında hizmetleri kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="8a609-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="8a609-105">Yeni bir hizmet zaten dağıtılmış yayımlanan ve tooan uygulama yükseltme olarak eklediyseniz, hello yeni eklenen toohello dağıtılan uygulama hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="8a609-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="8a609-106">Bu tür yükseltme zaten hello uygulamanın parçası olan hello Hizmetleri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="8a609-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="8a609-107">Ancak, eklendi hello Hizmeti'nin bir örneğini hello yeni hizmet toobe için etkin başlatılmış olması gerekir (hello kullanarak `New-ServiceFabricService` cmdlet'i).</span><span class="sxs-lookup"><span data-stu-id="8a609-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="8a609-108">Hizmetleri, yükseltme işleminin bir parçası olarak uygulamadan de kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="8a609-109">Ancak, geçerli hizmetin tüm örneklerine ait hello to-edilecek silinmiş hello yükseltmeye devam etmeden önce durdurulması gerekir (hello kullanarak `Remove-ServiceFabricService` cmdlet'i).</span><span class="sxs-lookup"><span data-stu-id="8a609-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="8a609-110">El ile yükseltme moduna</span><span class="sxs-lookup"><span data-stu-id="8a609-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="8a609-111">Merhaba izlenmeyen el ile modu yalnızca başarısız veya askıya alınmış yükseltme için dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8a609-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="8a609-112">Merhaba izlenen hello yükseltme modu Service Fabric uygulamaları için önerilen moddur.</span><span class="sxs-lookup"><span data-stu-id="8a609-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="8a609-113">Azure Service Fabric toosupport geliştirme ve üretim kümeleri birden fazla yükseltme modu sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a609-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="8a609-114">Seçilen dağıtım seçenekleri farklı ortamlar için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="8a609-115">izlenen hello yükseltme uygulama hello en tipik yükseltme toouse hello üretim ortamında ' dir.</span><span class="sxs-lookup"><span data-stu-id="8a609-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="8a609-116">Merhaba yükselttiğinizde İlkesi belirtilmemişse, Service Fabric hello yükseltme devam etmeden önce hello uygulama sağlıklı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a609-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="8a609-117">Merhaba Uygulama Yöneticisi Uygulama yükseltme modu toohave toplam denetime hello hello aracılığıyla yükseltme işlemi ilerleme durumu çeşitli yükseltme etki alanlarının çalışırken hello el ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a609-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="8a609-118">Bu mod özelleştirilmiş veya karmaşık sistem durumu değerlendirme İlkesi gereklidir veya Geleneksel olmayan yükseltme gerçekleştiği yararlıdır (örneğin, Merhaba uygulaması veri kaybından zaten).</span><span class="sxs-lookup"><span data-stu-id="8a609-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="8a609-119">Son olarak, hello otomatik uygulama yükseltme geliştirme veya test ortamları tooprovide hızlı yineleme döngüsü sırasında hizmeti geliştirme için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8a609-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="8a609-120">Toomanual yükseltme modu Değiştir</span><span class="sxs-lookup"><span data-stu-id="8a609-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="8a609-121">**El ile**--hello geçerli UD ve değişiklik hello Dur hello uygulama yükseltmeyi modu tooUnmonitored el ile yükseltme.</span><span class="sxs-lookup"><span data-stu-id="8a609-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="8a609-122">Hello Yöneticisi gereken toomanually çağrısı **MoveNextApplicationUpgradeDomainAsync** tooproceed hello ile yükseltme veya yeni bir yükseltme başlatarak bir geri alma tetikler.</span><span class="sxs-lookup"><span data-stu-id="8a609-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="8a609-123">Merhaba yükseltme hello el ile moduna girdikten sonra yeni bir yükseltme başlatılana kadar hello el ile modunda kalır.</span><span class="sxs-lookup"><span data-stu-id="8a609-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="8a609-124">Hello **GetApplicationUpgradeProgressAsync** komut döndürür DOKU\_uygulama\_yükseltme\_durumu\_çalışırken\_İleri\_BEKLEMEDE.</span><span class="sxs-lookup"><span data-stu-id="8a609-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="8a609-125">Diff paketi ile yükseltme</span><span class="sxs-lookup"><span data-stu-id="8a609-125">Upgrade with a diff package</span></span>
<span data-ttu-id="8a609-126">Service Fabric uygulaması, tam ve müstakil uygulama paketiyle sağlama tarafından yükseltilebilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="8a609-127">Bir uygulama aynı zamanda yalnızca güncelleştirilmiş hello uygulama dosyalarını içeren bir fark paketini kullanarak yükseltilebilmesi için uygulama bildirimi ve hello hizmet bildirim dosyaları hello güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="8a609-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="8a609-128">Bir tam uygulama paketi tüm hello dosyaları gerekli toostart içerir ve Service Fabric uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8a609-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="8a609-129">Fark paketi hello son sağlamak ve hello geçerli yükseltme arasında değişen hello dosyaları içerir ve ayrıca dosyaları hello tam uygulama bildirimi ve hello hizmet bildirimi.</span><span class="sxs-lookup"><span data-stu-id="8a609-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="8a609-130">Merhaba uygulama bildirimini veya hello yapı düzende bulunamıyor hizmet bildirimi herhangi başvurusu için hello görüntü deposunda aranır.</span><span class="sxs-lookup"><span data-stu-id="8a609-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="8a609-131">Tam uygulama paketleri hello için bir uygulama toohello kümenin ilk yüklemesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8a609-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="8a609-132">Sonraki güncelleştirmeler tam uygulama paketi veya bir fark paket olabilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="8a609-133">Durumlar fark paket iyi bir seçimdir kullanırken:</span><span class="sxs-lookup"><span data-stu-id="8a609-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="8a609-134">Birkaç hizmet bildirim dosyaları ve/veya birkaç kod paketler, yapılandırma paketleri veya veri paketleri başvuruda bulunan bir geniş Uygulama paketiniz varsa, bir fark paket tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="8a609-135">Hello yapı düzeni doğrudan, uygulama derleme işlemini oluşturan bir dağıtım sistemi olduğunda bir fark paket tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="8a609-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="8a609-136">Bu durumda, Hello kod değişmediğinden olsa bile, yeni oluşturulan derlemeleri farklı bir sağlama toplamı alın.</span><span class="sxs-lookup"><span data-stu-id="8a609-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="8a609-137">Bir tam uygulama paketini kullanarak, tooupdate hello sürümünde tüm kod paketler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8a609-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="8a609-138">Diff paketini kullanarak, yalnızca değiştirilen hello dosyaları ve hello sürüm değiştiği hello bildirim dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a609-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="8a609-139">Bir uygulama, Visual Studio kullanarak yükseltildiğinde hello fark paketini otomatik olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="8a609-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="8a609-140">toocreate fark paketini el ile uygulama bildirimini hello ve hello hizmet bildirimlerini güncelleştirilmesi gerekir, ancak yalnızca değiştirilen hello paketler hello son uygulama paketinde eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="8a609-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="8a609-141">Örneğin, uygulama (sürüm numaraları anlama kolaylığı için sağlanan) aşağıdaki hello ile başlayalım:</span><span class="sxs-lookup"><span data-stu-id="8a609-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="8a609-142">Şimdi, PowerShell kullanarak bir fark paketini kullanarak tooupdate yalnızca hello kod paketi service1 istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8a609-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="8a609-143">Şimdi, güncelleştirilmiş uygulamanızı klasör yapısı aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8a609-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="8a609-144">Bu durumda, hello uygulama bildirim too2.0.0 ve hello hizmet bildirimi service1 tooreflect hello kod paketi güncelleştirme için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8a609-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="8a609-145">Uygulama paketinizi için Hello klasör yapısı aşağıdaki hello sahip olur:</span><span class="sxs-lookup"><span data-stu-id="8a609-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="8a609-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a609-146">Next steps</span></span>
<span data-ttu-id="8a609-147">[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a609-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="8a609-148">[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a609-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="8a609-149">Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8a609-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="8a609-150">Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="8a609-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="8a609-151">Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8a609-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
