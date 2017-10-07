---
title: "Azure Cloud Services uygulamalarını toomicroservices aaaConvert | Microsoft Docs"
description: "Bu kılavuz bulut Hizmetleri Web karşılaştırır ve çalışan rolleri ve Service Fabric durum bilgisi olmayan hizmetler toohelp bulut Hizmetleri tooService doku ' geçirme."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="a55d9-103">Tooconverting Web ve çalışan rolleri tooService doku durum bilgisi olmayan hizmetler Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a55d9-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="a55d9-104">Bu makalede nasıl toomigrate, bulut Hizmetleri Web ve çalışan rolleri tooService doku durum bilgisi olmayan hizmetler.</span><span class="sxs-lookup"><span data-stu-id="a55d9-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="a55d9-105">Uygulamalar, genel mimarisi toostay kabaca gittiği aynı hello için bulut Hizmetleri tooService doku hello en basit geçiş yolu budur.</span><span class="sxs-lookup"><span data-stu-id="a55d9-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="a55d9-106">Bulut hizmeti projesi tooService doku uygulama projesi</span><span class="sxs-lookup"><span data-stu-id="a55d9-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="a55d9-107">Uygulamanızı dağıtılan toorun hello tam paket uygulamanız - diğer bir deyişle, bunların her tanımlamak için bir bulut hizmeti projesi ve bir Service Fabric uygulaması projesi benzer bir yapıya ve her iki temsil hello dağıtım birimi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="a55d9-108">Bir bulut hizmeti projesi, bir veya daha fazla Web veya çalışan rolleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="a55d9-109">Benzer şekilde, bir Service Fabric uygulaması projesi bir veya daha fazla hizmet içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a55d9-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="a55d9-110">Merhaba Service Fabric uygulaması projesi yalnızca dağıtılacak bir uygulama tanımlar ancak hello hello bulut hizmeti projesi tüm çiftler VM dağıtımı ile uygulama dağıtımı hello ve bu nedenle, VM yapılandırma ayarlarını içeren farktır Service Fabric kümesindeki var olan VM'ler tooa kümesi.</span><span class="sxs-lookup"><span data-stu-id="a55d9-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="a55d9-111">hello Azure portal veya bir Resource Manager şablonu aracılığıyla ve birden çok Service Fabric uygulamaları kullanılabilecek tooit dağıtıldığında hello Service Fabric kümesi kendisi yalnızca dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Service Fabric ve Cloud Services proje karşılaştırma][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="a55d9-113">Çalışan rolü toostateless hizmeti</span><span class="sxs-lookup"><span data-stu-id="a55d9-113">Worker Role toostateless service</span></span>
<span data-ttu-id="a55d9-114">Kavramsal olarak, bir çalışan rolü hello iş yükü, her örneği aynıdır ve istekleri yönlendirilmiş tooany örnek herhangi bir zamanda olabilir anlamına durum bilgisiz iş yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a55d9-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="a55d9-115">Her bir örnek beklenen tooremember hello önceki isteği değil.</span><span class="sxs-lookup"><span data-stu-id="a55d9-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="a55d9-116">Merhaba iş yükü çalışır durum üzerinde Azure Table Storage veya Azure belge DB gibi bir dış durum depolama alanını tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="a55d9-117">Service Fabric iş yükü bu tür bir durum bilgisiz hizmeti tarafından temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="a55d9-118">Merhaba basit bir yaklaşım toomigrating çalışan rolü tooService doku çalışan rolü kodunu tooa durum bilgisiz hizmet dönüştürme yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Çalışan rolü tooStateless hizmeti][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="a55d9-120">Web rolü toostateless hizmeti</span><span class="sxs-lookup"><span data-stu-id="a55d9-120">Web Role toostateless service</span></span>
<span data-ttu-id="a55d9-121">Benzer tooWorker rolü, Web rolü ayrıca durum bilgisiz iş yükünü temsil eder ve bu nedenle kavramsal çok eşlenen tooa Service Fabric durum bilgisiz hizmet olabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="a55d9-122">Ancak, Web rolünden farklı olarak, IIS Service Fabric desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a55d9-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="a55d9-123">toomigrate bir web uygulaması Web rolü tooa durum bilgisiz hizmetinden kendi kendini barındırır ve IIS veya ASP.NET Core 1 gibi System.Web bağlı olmayan ilk taşıma tooa web framework gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="a55d9-124">**Uygulama**</span><span class="sxs-lookup"><span data-stu-id="a55d9-124">**Application**</span></span> | <span data-ttu-id="a55d9-125">**Destekleniyor**</span><span class="sxs-lookup"><span data-stu-id="a55d9-125">**Supported**</span></span> | <span data-ttu-id="a55d9-126">**Geçiş yolu**</span><span class="sxs-lookup"><span data-stu-id="a55d9-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a55d9-127">ASP.NET Web formları</span><span class="sxs-lookup"><span data-stu-id="a55d9-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="a55d9-128">Hayır</span><span class="sxs-lookup"><span data-stu-id="a55d9-128">No</span></span> |<span data-ttu-id="a55d9-129">Dönüştürme tooASP.NET 1 MVC çekirdek</span><span class="sxs-lookup"><span data-stu-id="a55d9-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="a55d9-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="a55d9-130">ASP.NET MVC</span></span> |<span data-ttu-id="a55d9-131">İle geçiş</span><span class="sxs-lookup"><span data-stu-id="a55d9-131">With Migration</span></span> |<span data-ttu-id="a55d9-132">Yükseltme tooASP.NET 1 MVC çekirdek</span><span class="sxs-lookup"><span data-stu-id="a55d9-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="a55d9-133">ASP.NET Web API'si</span><span class="sxs-lookup"><span data-stu-id="a55d9-133">ASP.NET Web API</span></span> |<span data-ttu-id="a55d9-134">İle geçiş</span><span class="sxs-lookup"><span data-stu-id="a55d9-134">With Migration</span></span> |<span data-ttu-id="a55d9-135">Kendini barındıran sunucu veya ASP.NET Core 1 kullanın</span><span class="sxs-lookup"><span data-stu-id="a55d9-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="a55d9-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="a55d9-136">ASP.NET Core 1</span></span> |<span data-ttu-id="a55d9-137">Evet</span><span class="sxs-lookup"><span data-stu-id="a55d9-137">Yes</span></span> |<span data-ttu-id="a55d9-138">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="a55d9-139">Giriş noktası API ve yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="a55d9-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="a55d9-140">Çalışan rolü ve Service Fabric API'leri teklif benzer giriş noktaları hizmeti:</span><span class="sxs-lookup"><span data-stu-id="a55d9-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="a55d9-141">**Giriş noktası**</span><span class="sxs-lookup"><span data-stu-id="a55d9-141">**Entry Point**</span></span> | <span data-ttu-id="a55d9-142">**Çalışan rolü**</span><span class="sxs-lookup"><span data-stu-id="a55d9-142">**Worker Role**</span></span> | <span data-ttu-id="a55d9-143">**Service Fabric hizmeti**</span><span class="sxs-lookup"><span data-stu-id="a55d9-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a55d9-144">İşleme</span><span class="sxs-lookup"><span data-stu-id="a55d9-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="a55d9-145">VM Başlat</span><span class="sxs-lookup"><span data-stu-id="a55d9-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="a55d9-146">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-146">N/A</span></span> |
| <span data-ttu-id="a55d9-147">VM'yi Durdur</span><span class="sxs-lookup"><span data-stu-id="a55d9-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="a55d9-148">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-148">N/A</span></span> |
| <span data-ttu-id="a55d9-149">İstemci istekleri için açık dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="a55d9-149">Open listener for client requests</span></span> |<span data-ttu-id="a55d9-150">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-150">N/A</span></span> |<ul><li> <span data-ttu-id="a55d9-151">`CreateServiceInstanceListener()`için durum bilgisiz</span><span class="sxs-lookup"><span data-stu-id="a55d9-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="a55d9-152">`CreateServiceReplicaListener()`durum bilgisi için</span><span class="sxs-lookup"><span data-stu-id="a55d9-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="a55d9-153">Çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="a55d9-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="a55d9-154">Doku durum bilgisiz hizmeti</span><span class="sxs-lookup"><span data-stu-id="a55d9-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="a55d9-155">Hem birincil "Çalıştır" geçersiz kılma hangi toobegin işlemede sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="a55d9-156">Service Fabric Hizmetleri birleştirme `Run`, `Start`, ve `Stop` tek bir giriş noktasına `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="a55d9-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="a55d9-157">Hizmetinizi ne zaman çalışmaya başlaması gereken `RunAsync` başlar ve hello çalışma durması gerektiğini `RunAsync` yöntemin CancellationToken durdurulma.</span><span class="sxs-lookup"><span data-stu-id="a55d9-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="a55d9-158">Merhaba yaşam döngüsü ve çalışan rolleri ve Service Fabric Hizmetleri ömrü arasında birkaç temel farklılıklar vardır:</span><span class="sxs-lookup"><span data-stu-id="a55d9-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="a55d9-159">**Yaşam döngüsü:** çalışan rolü VM ve bu nedenle, yaşam döngüsü olduğunu bağlı toohello zaman hello VM başlatır ve durdurur olaylarını içerir VM hello büyük fark vardır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="a55d9-160">Service Fabric hizmeti, birbiriyle ilgili olmayan gibi hello zaman konak VM veya makine başlar ve durdurun, olayları içermez böylece hello VM döngüsü, ayrı bir yaşam döngüsü sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="a55d9-161">**Yaşam süresi:** çalışan rolü örneği hello varsa geri `Run` yöntemi çıkar.</span><span class="sxs-lookup"><span data-stu-id="a55d9-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="a55d9-162">Merhaba `RunAsync` bir Service Fabric hizmeti yönteminde ancak çalıştırabilirsiniz toocompletion ve hello hizmet örneği oluşturan kalacak.</span><span class="sxs-lookup"><span data-stu-id="a55d9-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="a55d9-163">Service Fabric, istemci isteklerini dinlemek Hizmetleri için isteğe bağlı iletişim Kurulum giriş noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="a55d9-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="a55d9-164">Merhaba RunAsync ve iletişim giriş noktası hello RunAsync yöntemi olmadan tooexit izin - hizmetiniz tooonly dinleme tooclient istekleri seçin veya yalnızca bir işleme döngüsü ya da her ikisini de Çalıştır - Service Fabric hizmetlerini isteğe bağlı bir geçersiz kılma olan istemci istekleri için toolisten devam çünkü hello hizmet örneği, yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="a55d9-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="a55d9-165">Uygulama API ve ortam</span><span class="sxs-lookup"><span data-stu-id="a55d9-165">Application API and environment</span></span>
<span data-ttu-id="a55d9-166">Merhaba bulut Hizmetleri ortam API bilgi ve işlevsellik hello geçerli VM örneği yanı sıra diğer VM rolü örneklerini hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a55d9-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="a55d9-167">Service Fabric tooits çalışma zamanı ile ilgili bilgiler ve hello düğüm hizmet hakkındaki bazı bilgileri şu anda çalışan sağlar.</span><span class="sxs-lookup"><span data-stu-id="a55d9-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="a55d9-168">**Ortam görev**</span><span class="sxs-lookup"><span data-stu-id="a55d9-168">**Environment Task**</span></span> | <span data-ttu-id="a55d9-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="a55d9-169">**Cloud Services**</span></span> | <span data-ttu-id="a55d9-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="a55d9-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a55d9-171">Yapılandırma ayarları ve değişiklik bildirimi</span><span class="sxs-lookup"><span data-stu-id="a55d9-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="a55d9-172">Yerel Depolama</span><span class="sxs-lookup"><span data-stu-id="a55d9-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="a55d9-173">Uç nokta bilgileri</span><span class="sxs-lookup"><span data-stu-id="a55d9-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="a55d9-174">Geçerli örnek:`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="a55d9-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="a55d9-175">Diğer roller ve örneği:`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="a55d9-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="a55d9-176">`NodeContext`Geçerli düğüm adresi</span><span class="sxs-lookup"><span data-stu-id="a55d9-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="a55d9-177">`FabricClient`ve `ServicePartitionResolver` hizmet uç noktası bulma</span><span class="sxs-lookup"><span data-stu-id="a55d9-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="a55d9-178">Ortam öykünmesi</span><span class="sxs-lookup"><span data-stu-id="a55d9-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="a55d9-179">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-179">N/A</span></span> |
| <span data-ttu-id="a55d9-180">Eşzamanlı değişiklik olayı</span><span class="sxs-lookup"><span data-stu-id="a55d9-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="a55d9-181">Yok</span><span class="sxs-lookup"><span data-stu-id="a55d9-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="a55d9-182">Yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="a55d9-182">Configuration settings</span></span>
<span data-ttu-id="a55d9-183">Bulut hizmetleri yapılandırma ayarlarında bir VM rolü için ayarlanır ve bu VM rolü örneklerini tooall uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a55d9-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="a55d9-184">Bu ayarlar, anahtar-değer çiftleri ServiceConfiguration.*.cscfg dosyalarında ayarlamak ve doğrudan RoleEnvironment erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="a55d9-185">Bir VM birden çok hizmet ve uygulamaları barındırmak için Service Fabric içinde ayarlarını ayrı ayrı tooa VM yazmak yerine tooeach hizmetini ve tooeach uygulama uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a55d9-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="a55d9-186">Bir hizmet üç paketlerini oluşur:</span><span class="sxs-lookup"><span data-stu-id="a55d9-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="a55d9-187">**Kod:** hello hizmeti yürütülebilir dosyaları, ikili dosyaları, DLL'ler ve diğer dosyaları içeren bir hizmet toorun gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a55d9-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="a55d9-188">**Config:** tüm yapılandırma dosyalarını ve ayarlarını bir hizmet için.</span><span class="sxs-lookup"><span data-stu-id="a55d9-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="a55d9-189">**Veri:** hello hizmetiyle ilişkili statik veri dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a55d9-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="a55d9-190">Bu paketleri her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="a55d9-191">Benzer tooCloud Hizmetleri, bir yapılandırma paketi bir API aracılığıyla programlı olarak erişilebilir ve bir yapılandırma paketi değişikliği kullanılabilir toonotify hello hizmetine olaylardır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="a55d9-192">Settings.xml dosyası anahtar-değer yapılandırma ve programlı erişim benzer toohello uygulama ayarları bölümünde bir App.config dosyası için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="a55d9-193">Ancak, XML, JSON, YAML veya özel bir ikili biçimi olup bulut Hizmetleri, herhangi bir biçimdeki tüm yapılandırma dosyalarını bir Service Fabric yapılandırma paketi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="a55d9-194">Erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a55d9-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="a55d9-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a55d9-195">Cloud Services</span></span>
<span data-ttu-id="a55d9-196">Yapılandırma ayarları ServiceConfiguration.*.cscfg üzerinden erişilebilir `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="a55d9-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="a55d9-197">Bu ayarları hello genel olarak kullanılabilir tooall rol örnekleri olan aynı bulut hizmeti dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="a55d9-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="a55d9-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a55d9-198">Service Fabric</span></span>
<span data-ttu-id="a55d9-199">Her hizmetin kendi tek tek bir yapılandırma paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="a55d9-200">Hiçbir yerleşik mekanizması olduğunu genel yapılandırma ayarları için erişilebilir bir kümedeki tüm uygulamalar tarafından.</span><span class="sxs-lookup"><span data-stu-id="a55d9-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="a55d9-201">Service Fabric'ın özel Settings.xml yapılandırma dosyasının bir yapılandırma paketi içinde kullanırken, uygulama düzeyinde yapılandırma ayarlarını edinerek hello uygulama düzeyinde Settings.xml değerlerde üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="a55d9-202">Yapılandırma ayarları hello hizmetin aracılığıyla her hizmet örneği içinde erişimleri olan `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="a55d9-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="a55d9-203">Yapılandırma güncelleştirme olayları</span><span class="sxs-lookup"><span data-stu-id="a55d9-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="a55d9-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a55d9-204">Cloud Services</span></span>
<span data-ttu-id="a55d9-205">Merhaba `RoleEnvironment.Changed` tüm rol örneklerinin bir değişiklik olduğunda oluşur bir yapılandırma değişikliği gibi hello ortamda kullanılan toonotify bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="a55d9-206">Rol örnekleri geri dönüştürme ya da bir çalışan işleminin yeniden başlatmadan olmadan kullanılan tooconsume yapılandırma güncelleştirmeleri budur.</span><span class="sxs-lookup"><span data-stu-id="a55d9-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="a55d9-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a55d9-207">Service Fabric</span></span>
<span data-ttu-id="a55d9-208">Bir hizmette - kod, yapılandırma ve verileri - hello üç paket türlerinin her biri bir paket güncelleştirildi, eklenen veya kaldırılan bir hizmet örneği bildir olayları vardır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="a55d9-209">Bir hizmet birden çok paket her tür içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="a55d9-210">Örneğin, bir hizmet birden çok yapılandırma paketleri, tek tek her sürümü tutulan ve yükseltilebilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="a55d9-211">Bu olaylar, hello hizmet örneği başlatmadan hizmet paketleri, kullanılabilir tooconsume değişir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="a55d9-212">Başlangıç görevi</span><span class="sxs-lookup"><span data-stu-id="a55d9-212">Startup tasks</span></span>
<span data-ttu-id="a55d9-213">Başlatma, bir uygulama başlatılmadan önce gerçekleştirilen eylemler görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="a55d9-214">Yükseltilmiş ayrıcalıklar kullanarak genellikle kullanılan toorun Kurulum betikleri bir başlangıç görevdir.</span><span class="sxs-lookup"><span data-stu-id="a55d9-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="a55d9-215">Bulut Hizmetleri ve Service Fabric başlangıç görevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a55d9-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="a55d9-216">Merhaba temel fark söz konusu bulut Hizmetleri, bir rol örneği bir parçası olduğundan Service Fabric bağlı tooany değil bağlı tooa hizmet başlangıç görevi iken bir başlangıç görevi bağlı tooa VM belirli VM.</span><span class="sxs-lookup"><span data-stu-id="a55d9-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="a55d9-217">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a55d9-217">Cloud Services</span></span> | <span data-ttu-id="a55d9-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a55d9-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a55d9-219">Yapılandırma konumu</span><span class="sxs-lookup"><span data-stu-id="a55d9-219">Configuration location</span></span> |<span data-ttu-id="a55d9-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="a55d9-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="a55d9-221">Ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="a55d9-221">Privileges</span></span> |<span data-ttu-id="a55d9-222">"sınırlı" veya "yükseltilmiş"</span><span class="sxs-lookup"><span data-stu-id="a55d9-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="a55d9-223">Sıralama</span><span class="sxs-lookup"><span data-stu-id="a55d9-223">Sequencing</span></span> |<span data-ttu-id="a55d9-224">"Basit", "arka plan", "ön"</span><span class="sxs-lookup"><span data-stu-id="a55d9-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="a55d9-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a55d9-225">Cloud Services</span></span>
<span data-ttu-id="a55d9-226">Bulut Hizmetleri başlatma giriş noktası ServiceDefinition.csdef rol başına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="a55d9-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a55d9-227">Service Fabric</span></span>
<span data-ttu-id="a55d9-228">Service Fabric başlangıç giriş noktası ServiceManifest.xml hizmetinde başına yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="a55d9-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="a55d9-229">Geliştirme ortamı hakkında bir Not</span><span class="sxs-lookup"><span data-stu-id="a55d9-229">A note about development environment</span></span>
<span data-ttu-id="a55d9-230">Bulut Hizmetleri ve Service Fabric tümleşik ile Visual Studio Proje şablonları ve hata ayıklama, yapılandırma ve her ikisi de yerel olarak dağıtma desteği ve tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a55d9-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="a55d9-231">Service Fabric ve bulut hizmetlerini de bir yerel geliştirme çalışma zamanı ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a55d9-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="a55d9-232">Merhaba, farktır sırada hello bulut hizmeti geliştirme çalışma zamanı öykünür Merhaba, çalıştığı Azure ortamı, Service Fabric bir öykünücü kullanmaz - hello tam Service Fabric çalışma zamanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a55d9-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="a55d9-233">Merhaba Service Fabric, yerel geliştirme makinenizde çalıştırma ortamıdır hello üretimde çalışan aynı ortamı.</span><span class="sxs-lookup"><span data-stu-id="a55d9-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a55d9-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a55d9-234">Next steps</span></span>
<span data-ttu-id="a55d9-235">Service Fabric Reliable Services ve hello bulut Hizmetleri ve Service Fabric uygulama mimarisi toounderstand hello tam tootake avantajlarından Service Fabric özelliklerinin nasıl ayarlanacağını arasındaki temel farklar hakkında daha fazlasını okuyun.</span><span class="sxs-lookup"><span data-stu-id="a55d9-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="a55d9-236">Service Fabric Reliable Services ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a55d9-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="a55d9-237">Bulut Hizmetleri ve Service Fabric arasındaki kavramsal Kılavuzu toohello farklar</span><span class="sxs-lookup"><span data-stu-id="a55d9-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
