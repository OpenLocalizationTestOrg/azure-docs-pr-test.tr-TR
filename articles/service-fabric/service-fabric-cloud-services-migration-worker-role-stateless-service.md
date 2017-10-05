---
title: "Azure Cloud Services uygulamalar için mikro Dönüştür | Microsoft Docs"
description: "Bu kılavuz bulut hizmetlerinden Service Fabric geçirme yardımcı olmak için bulut Hizmetleri Web ve çalışan rolleri ve Service Fabric durum bilgisi olmayan hizmetler karşılaştırır."
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
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="be5d1-103">Web ve çalışan rolleri Service Fabric durum bilgisi olmayan hizmetler için dönüştürme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="be5d1-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="be5d1-104">Bu makalede, bulut Hizmetleri Web ve çalışan rolleri Service Fabric durum bilgisi olmayan hizmetler için nasıl geçirileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="be5d1-105">Bu en basit geçiş bulut hizmetlerinden Service Fabric, genel mimarisi kabaca aynı kalmasını gittiği uygulamalar için yoludur.</span><span class="sxs-lookup"><span data-stu-id="be5d1-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="be5d1-106">Service Fabric uygulaması projesi için bulut hizmeti projesi</span><span class="sxs-lookup"><span data-stu-id="be5d1-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="be5d1-107">Bir bulut hizmeti projesi ve bir Service Fabric uygulaması projesi benzer bir yapıya sahip ve her iki temsil dağıtım uygulamanız için - diğer bir deyişle, bunların her uygulamanızı çalıştırmak için dağıtılan eksiksiz paket tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="be5d1-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="be5d1-108">Bir bulut hizmeti projesi, bir veya daha fazla Web veya çalışan rolleri içerir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="be5d1-109">Benzer şekilde, bir Service Fabric uygulaması projesi bir veya daha fazla hizmet içeriyor.</span><span class="sxs-lookup"><span data-stu-id="be5d1-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="be5d1-110">Service Fabric uygulaması proje için bir dizi dağıtılan bir uygulamayı yalnızca tanımlar ancak bulut hizmeti projesi VM dağıtımı ile uygulama dağıtımı couples ve bu nedenle, VM yapılandırma ayarlarını içeren farktır var olan sanal makineleri bir Service Fabric kümesindeki.</span><span class="sxs-lookup"><span data-stu-id="be5d1-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="be5d1-111">Service Fabric kümesi yalnızca bir kez bir Resource Manager şablonu veya Azure portal aracılığıyla dağıtılır ve birden çok Service Fabric uygulamaları dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Service Fabric ve Cloud Services proje karşılaştırma][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="be5d1-113">Durum bilgisiz hizmetine çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="be5d1-113">Worker Role to stateless service</span></span>
<span data-ttu-id="be5d1-114">Kavramsal olarak, bir çalışan rolü iş yükü, her örneği aynıdır ve istekleri herhangi bir zamanda herhangi bir örneğine yönlendirilebilir anlamına durum bilgisiz iş yükünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="be5d1-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="be5d1-115">Her bir örnek, önceki isteği anımsaması beklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="be5d1-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="be5d1-116">İş yükü çalıştırır durumu, Azure Table Storage veya Azure belge DB gibi bir dış durum depolama alanını tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="be5d1-117">Service Fabric iş yükü bu tür bir durum bilgisiz hizmeti tarafından temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="be5d1-118">Çalışan rolü için Service Fabric geçiş için en kolay yaklaşım, durum bilgisi olmayan bir hizmete çalışan rolü kodunu dönüştürerek yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Durum bilgisiz hizmetine çalışan rolü][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="be5d1-120">Durum bilgisiz hizmetine Web rolü</span><span class="sxs-lookup"><span data-stu-id="be5d1-120">Web Role to stateless service</span></span>
<span data-ttu-id="be5d1-121">Benzer şekilde çalışan rolü, Web rolü ayrıca durum bilgisiz iş yükünü temsil eder ve böylece kavramsal, çok bir Service Fabric durum bilgisiz hizmetine eşlenebilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="be5d1-122">Ancak, Web rolünden farklı olarak, IIS Service Fabric desteklemez.</span><span class="sxs-lookup"><span data-stu-id="be5d1-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="be5d1-123">Bir web geçirmek için kendi kendini barındırır ve IIS veya ASP.NET Core 1 gibi System.Web bağlı olmayan bir web çerçevesidir ilk taşıma Web rolünden Hizmeti'ne uygulama için bir durum bilgisiz gerektirir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="be5d1-124">**Uygulama**</span><span class="sxs-lookup"><span data-stu-id="be5d1-124">**Application**</span></span> | <span data-ttu-id="be5d1-125">**Destekleniyor**</span><span class="sxs-lookup"><span data-stu-id="be5d1-125">**Supported**</span></span> | <span data-ttu-id="be5d1-126">**Geçiş yolu**</span><span class="sxs-lookup"><span data-stu-id="be5d1-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be5d1-127">ASP.NET Web formları</span><span class="sxs-lookup"><span data-stu-id="be5d1-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="be5d1-128">Hayır</span><span class="sxs-lookup"><span data-stu-id="be5d1-128">No</span></span> |<span data-ttu-id="be5d1-129">ASP.NET Core 1 MVC Dönüştür</span><span class="sxs-lookup"><span data-stu-id="be5d1-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="be5d1-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="be5d1-130">ASP.NET MVC</span></span> |<span data-ttu-id="be5d1-131">İle geçiş</span><span class="sxs-lookup"><span data-stu-id="be5d1-131">With Migration</span></span> |<span data-ttu-id="be5d1-132">ASP.NET yükseltmeye 1 MVC çekirdek</span><span class="sxs-lookup"><span data-stu-id="be5d1-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="be5d1-133">ASP.NET Web API'si</span><span class="sxs-lookup"><span data-stu-id="be5d1-133">ASP.NET Web API</span></span> |<span data-ttu-id="be5d1-134">İle geçiş</span><span class="sxs-lookup"><span data-stu-id="be5d1-134">With Migration</span></span> |<span data-ttu-id="be5d1-135">Kendini barındıran sunucu veya ASP.NET Core 1 kullanın</span><span class="sxs-lookup"><span data-stu-id="be5d1-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="be5d1-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="be5d1-136">ASP.NET Core 1</span></span> |<span data-ttu-id="be5d1-137">Evet</span><span class="sxs-lookup"><span data-stu-id="be5d1-137">Yes</span></span> |<span data-ttu-id="be5d1-138">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="be5d1-139">Giriş noktası API ve yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="be5d1-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="be5d1-140">Çalışan rolü ve Service Fabric API'leri teklif benzer giriş noktaları hizmeti:</span><span class="sxs-lookup"><span data-stu-id="be5d1-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="be5d1-141">**Giriş noktası**</span><span class="sxs-lookup"><span data-stu-id="be5d1-141">**Entry Point**</span></span> | <span data-ttu-id="be5d1-142">**Çalışan rolü**</span><span class="sxs-lookup"><span data-stu-id="be5d1-142">**Worker Role**</span></span> | <span data-ttu-id="be5d1-143">**Service Fabric hizmeti**</span><span class="sxs-lookup"><span data-stu-id="be5d1-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be5d1-144">İşleme</span><span class="sxs-lookup"><span data-stu-id="be5d1-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="be5d1-145">VM Başlat</span><span class="sxs-lookup"><span data-stu-id="be5d1-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="be5d1-146">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-146">N/A</span></span> |
| <span data-ttu-id="be5d1-147">VM'yi Durdur</span><span class="sxs-lookup"><span data-stu-id="be5d1-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="be5d1-148">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-148">N/A</span></span> |
| <span data-ttu-id="be5d1-149">İstemci istekleri için açık dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="be5d1-149">Open listener for client requests</span></span> |<span data-ttu-id="be5d1-150">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-150">N/A</span></span> |<ul><li> <span data-ttu-id="be5d1-151">`CreateServiceInstanceListener()`için durum bilgisiz</span><span class="sxs-lookup"><span data-stu-id="be5d1-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="be5d1-152">`CreateServiceReplicaListener()`durum bilgisi için</span><span class="sxs-lookup"><span data-stu-id="be5d1-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="be5d1-153">Çalışan rolü</span><span class="sxs-lookup"><span data-stu-id="be5d1-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="be5d1-154">Doku durum bilgisiz hizmeti</span><span class="sxs-lookup"><span data-stu-id="be5d1-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="be5d1-155">Hem birincil "Çalıştır" geçersiz kılma işlemeye başlamak üzere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="be5d1-156">Service Fabric Hizmetleri birleştirme `Run`, `Start`, ve `Stop` tek bir giriş noktasına `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="be5d1-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="be5d1-157">Hizmetinizi ne zaman çalışmaya başlaması gereken `RunAsync` başlar ve ne zaman çalışma durması gerektiğini `RunAsync` yöntemin CancellationToken durdurulma.</span><span class="sxs-lookup"><span data-stu-id="be5d1-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="be5d1-158">Yaşam döngüsü ve çalışan rolleri ve Service Fabric Hizmetleri ömrü arasında birkaç temel farklılıklar vardır:</span><span class="sxs-lookup"><span data-stu-id="be5d1-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="be5d1-159">**Yaşam döngüsü:** büyük bir VM çalışan rolü ise ve böylece kendi yaşam döngüsü bağlı zaman VM başlatır ve durdurur olaylarını içerir VM'ye farktır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="be5d1-160">Service Fabric hizmeti, birbiriyle ilgili olmayan olarak ne zaman konağı VM veya makine başlar ve durdurun, olayları içermez böylece VM döngüsü ayrı bir yaşam döngüsü sahiptir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="be5d1-161">**Yaşam süresi:** çalışan rolü örneği varsa geri `Run` yöntemi çıkar.</span><span class="sxs-lookup"><span data-stu-id="be5d1-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="be5d1-162">`RunAsync` Bir Service Fabric hizmeti yönteminde ancak çalıştırabilirsiniz tamamlanması ve hizmet örneği oluşturan kalır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="be5d1-163">Service Fabric, istemci isteklerini dinlemek Hizmetleri için isteğe bağlı iletişim Kurulum giriş noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="be5d1-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="be5d1-164">RunAsync ve iletişimi giriş noktası olan RunAsync yönteminde yeniden başlatmadan çıkmak için izin verilir - hizmetiniz yalnızca istemci isteklerini dinlemek veya yalnızca bir işleme döngüsü ya da her ikisini de çalıştırmak için seçebilirsiniz - Service Fabric hizmetlerini isteğe bağlı bir geçersiz kılma Hizmet örneği, çünkü istemci isteklerini dinlemek devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="be5d1-165">Uygulama API ve ortam</span><span class="sxs-lookup"><span data-stu-id="be5d1-165">Application API and environment</span></span>
<span data-ttu-id="be5d1-166">Bulut Hizmetleri ortam API bilgileri ve geçerli VM örneği yanı sıra diğer VM rolü örneklerini hakkında bilgi için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="be5d1-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="be5d1-167">Service Fabric, çalışma zamanı için ilgili bilgiler sağlar ve bir hizmet düğüm hakkında bazı bilgiler şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="be5d1-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="be5d1-168">**Ortam görev**</span><span class="sxs-lookup"><span data-stu-id="be5d1-168">**Environment Task**</span></span> | <span data-ttu-id="be5d1-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="be5d1-169">**Cloud Services**</span></span> | <span data-ttu-id="be5d1-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="be5d1-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be5d1-171">Yapılandırma ayarları ve değişiklik bildirimi</span><span class="sxs-lookup"><span data-stu-id="be5d1-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="be5d1-172">Yerel Depolama</span><span class="sxs-lookup"><span data-stu-id="be5d1-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="be5d1-173">Uç nokta bilgileri</span><span class="sxs-lookup"><span data-stu-id="be5d1-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="be5d1-174">Geçerli örnek:`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="be5d1-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="be5d1-175">Diğer roller ve örneği:`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="be5d1-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="be5d1-176">`NodeContext`Geçerli düğüm adresi</span><span class="sxs-lookup"><span data-stu-id="be5d1-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="be5d1-177">`FabricClient`ve `ServicePartitionResolver` hizmet uç noktası bulma</span><span class="sxs-lookup"><span data-stu-id="be5d1-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="be5d1-178">Ortam öykünmesi</span><span class="sxs-lookup"><span data-stu-id="be5d1-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="be5d1-179">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-179">N/A</span></span> |
| <span data-ttu-id="be5d1-180">Eşzamanlı değişiklik olayı</span><span class="sxs-lookup"><span data-stu-id="be5d1-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="be5d1-181">Yok</span><span class="sxs-lookup"><span data-stu-id="be5d1-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="be5d1-182">Yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="be5d1-182">Configuration settings</span></span>
<span data-ttu-id="be5d1-183">Bulut hizmetleri yapılandırma ayarlarında bir VM rolü için ayarlanır ve bu VM rolü tüm örnekleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="be5d1-184">Bu ayarlar, anahtar-değer çiftleri ServiceConfiguration.*.cscfg dosyalarında ayarlamak ve doğrudan RoleEnvironment erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="be5d1-185">Bir VM birden çok hizmet ve uygulamaları barındırmak için Service Fabric içinde ayarlarını ayrı ayrı her hizmet ve her uygulama yerine bir VM uygulayın.</span><span class="sxs-lookup"><span data-stu-id="be5d1-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="be5d1-186">Bir hizmet üç paketlerini oluşur:</span><span class="sxs-lookup"><span data-stu-id="be5d1-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="be5d1-187">**Kod:** hizmeti yürütülebilir dosyaları, ikili dosyaları, DLL'ler ve bir hizmetin ihtiyaç çalıştırmak için diğer dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="be5d1-188">**Config:** tüm yapılandırma dosyalarını ve ayarlarını bir hizmet için.</span><span class="sxs-lookup"><span data-stu-id="be5d1-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="be5d1-189">**Veri:** statik veri dosyalarını hizmetle ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="be5d1-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="be5d1-190">Bu paketleri her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="be5d1-191">Bulut Hizmetleri için benzer bir yapılandırma paketi program aracılığıyla bir API aracılığıyla erişilebilir ve olayları bir yapılandırma paketi değişikliği hizmetine bildirmek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="be5d1-192">Settings.xml dosyası anahtar-değer yapılandırması ve benzer bir App.config dosyası uygulama ayarları bölümüne program erişimi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="be5d1-193">Ancak, XML, JSON, YAML veya özel bir ikili biçimi olup bulut Hizmetleri, herhangi bir biçimdeki tüm yapılandırma dosyalarını bir Service Fabric yapılandırma paketi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="be5d1-194">Erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be5d1-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="be5d1-195">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="be5d1-195">Cloud Services</span></span>
<span data-ttu-id="be5d1-196">Yapılandırma ayarları ServiceConfiguration.*.cscfg üzerinden erişilebilir `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="be5d1-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="be5d1-197">Bu ayarlar, tüm rol örneklerinin aynı bulut hizmeti dağıtım genel olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="be5d1-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be5d1-198">Service Fabric</span></span>
<span data-ttu-id="be5d1-199">Her hizmetin kendi tek tek bir yapılandırma paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="be5d1-200">Hiçbir yerleşik mekanizması olduğunu genel yapılandırma ayarları için erişilebilir bir kümedeki tüm uygulamalar tarafından.</span><span class="sxs-lookup"><span data-stu-id="be5d1-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="be5d1-201">Service Fabric'ın özel Settings.xml yapılandırma dosyasının bir yapılandırma paketi içinde kullanırken, uygulama düzeyinde yapılandırma ayarlarını edinerek uygulama düzeyinde Settings.xml değerlerde üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="be5d1-202">Yapılandırma ayarları her hizmet örneği hizmetin aracılığıyla içinde erişimleri olan `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="be5d1-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="be5d1-203">Yapılandırma güncelleştirme olayları</span><span class="sxs-lookup"><span data-stu-id="be5d1-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="be5d1-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="be5d1-204">Cloud Services</span></span>
<span data-ttu-id="be5d1-205">`RoleEnvironment.Changed` Olay ortamında, bir yapılandırma değişikliği gibi bir değişiklik meydana geldiğinde tüm rol örneklerini bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="be5d1-206">Bu, yapılandırma güncelleştirmelerini rol örnekleri geri dönüştürme veya bir çalışan işleminin yeniden kullanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="be5d1-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be5d1-207">Service Fabric</span></span>
<span data-ttu-id="be5d1-208">Bir hizmette - kod, yapılandırma ve verileri - üç paket türlerinin her biri bir paket güncelleştirildi, eklenen veya kaldırılan bir hizmet örneği bildir olayları vardır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="be5d1-209">Bir hizmet birden çok paket her tür içerebilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="be5d1-210">Örneğin, bir hizmet birden çok yapılandırma paketleri, tek tek her sürümü tutulan ve yükseltilebilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="be5d1-211">Bu olaylar, hizmet örneği başlatmadan hizmet paketleri değişiklikleri kullanmak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="be5d1-212">Başlangıç görevi</span><span class="sxs-lookup"><span data-stu-id="be5d1-212">Startup tasks</span></span>
<span data-ttu-id="be5d1-213">Başlatma, bir uygulama başlatılmadan önce gerçekleştirilen eylemler görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="be5d1-214">Bir başlangıç görevi, genellikle yükseltilmiş ayrıcalıklar kullanarak kurulum komut dosyalarını çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="be5d1-215">Bulut Hizmetleri ve Service Fabric başlangıç görevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="be5d1-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="be5d1-216">Bir rol örneği bir parçası olduğundan Service Fabric herhangi belirli VM bağlanmayan bir hizmet için bir başlangıç görevi bağlıdır ancak bulut Hizmetleri'nde bir başlangıç görevi bir VM'ye bağlı olduğunu ana farktır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="be5d1-217">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="be5d1-217">Cloud Services</span></span> | <span data-ttu-id="be5d1-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be5d1-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be5d1-219">Yapılandırma konumu</span><span class="sxs-lookup"><span data-stu-id="be5d1-219">Configuration location</span></span> |<span data-ttu-id="be5d1-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="be5d1-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="be5d1-221">Ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="be5d1-221">Privileges</span></span> |<span data-ttu-id="be5d1-222">"sınırlı" veya "yükseltilmiş"</span><span class="sxs-lookup"><span data-stu-id="be5d1-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="be5d1-223">Sıralama</span><span class="sxs-lookup"><span data-stu-id="be5d1-223">Sequencing</span></span> |<span data-ttu-id="be5d1-224">"Basit", "arka plan", "ön"</span><span class="sxs-lookup"><span data-stu-id="be5d1-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="be5d1-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="be5d1-225">Cloud Services</span></span>
<span data-ttu-id="be5d1-226">Bulut Hizmetleri başlatma giriş noktası ServiceDefinition.csdef rol başına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="be5d1-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be5d1-227">Service Fabric</span></span>
<span data-ttu-id="be5d1-228">Service Fabric başlangıç giriş noktası ServiceManifest.xml hizmetinde başına yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="be5d1-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="be5d1-229">Geliştirme ortamı hakkında bir Not</span><span class="sxs-lookup"><span data-stu-id="be5d1-229">A note about development environment</span></span>
<span data-ttu-id="be5d1-230">Bulut Hizmetleri ve Service Fabric ile Visual Studio Proje şablonları ve hata ayıklama, yapılandırma ve hem yerel hem de dağıtımı Azure desteği ile tümleştirilir.</span><span class="sxs-lookup"><span data-stu-id="be5d1-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="be5d1-231">Service Fabric ve bulut hizmetlerini de bir yerel geliştirme çalışma zamanı ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="be5d1-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="be5d1-232">Farktır bulut hizmeti geliştirme çalışma zamanı, çalıştığı Azure ortamı öykünür olsa da, Service Fabric bir öykünücü kullanmaz - tam Service Fabric çalışma zamanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="be5d1-233">Yerel geliştirme makinenizde çalıştırma Service Fabric üretimde çalışan aynı ortamda ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="be5d1-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be5d1-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be5d1-234">Next steps</span></span>
<span data-ttu-id="be5d1-235">Service Fabric Reliable Services hakkında daha fazla bilgi ve bulut Hizmetleri ve Service Fabric uygulama mimarisi tamamını Service Fabric özelliklerden yararlanmak nasıl anlamak için arasındaki temel farklar.</span><span class="sxs-lookup"><span data-stu-id="be5d1-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="be5d1-236">Service Fabric Reliable Services ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="be5d1-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="be5d1-237">Bulut Hizmetleri ve Service Fabric arasındaki farklar kavramsal Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="be5d1-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
