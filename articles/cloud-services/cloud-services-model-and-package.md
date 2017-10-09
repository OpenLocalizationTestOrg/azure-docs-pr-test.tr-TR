---
title: aaaWhat olan bir bulut hizmeti modeli ve paket | Microsoft Docs
description: "Merhaba bulut hizmeti modeli (.csdef, .cscfg) ve Azure paketine (.cspkg) açıklanır"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="7c8da-103">Merhaba bulut hizmeti modeli nedir ve nasıl paket?</span><span class="sxs-lookup"><span data-stu-id="7c8da-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="7c8da-104">Bir bulut hizmeti üç bileşenlerini hello hizmet tanımı oluşturulur *(.csdef)*, hizmet yapılandırması hello *(.cscfg)*ve bir hizmet paketi *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="7c8da-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="7c8da-105">Her iki hello **ServiceDefinition.csdef** ve **ServiceConfig.cscfg** dosyaları XML tabanlı ve topluca hello modeli olarak adlandırılan hello bulut hizmeti ve nasıl yapılandırılır; hello yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="7c8da-106">Merhaba **ServicePackage.cspkg** hello oluşturulan bir zip dosyası **ServiceDefinition.csdef** ve bunun yanı sıra, tüm gerekli hello ikili tabanlı bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="7c8da-107">Azure, her iki hello bir bulut hizmeti oluşturur **ServicePackage.cspkg** ve hello **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="7c8da-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="7c8da-108">Azure'da Hello bulut hizmeti çalışır duruma geldiğinde hello yeniden yapılandırabilirsiniz **ServiceConfig.cscfg** dosyası, ancak hello tanımı alter olamaz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="7c8da-109">Ne hakkında daha fazla tooknow istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="7c8da-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="7c8da-110">Merhaba hakkında daha fazla tooknow istediğiniz [ServiceDefinition.csdef](#csdef) ve [ServiceConfig.cscfg](#cscfg) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7c8da-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="7c8da-111">Zaten bu hakkında bilebilirim ver [bazı örnekler](#next-steps) üzerinde ne ı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="7c8da-112">Toocreate hello istediğiniz [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="7c8da-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="7c8da-113">Visual Studio kullanarak ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="7c8da-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="7c8da-114">[Bir bulut hizmeti oluştur][vs_create]</span><span class="sxs-lookup"><span data-stu-id="7c8da-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="7c8da-115">[Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="7c8da-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="7c8da-116">[Bir bulut hizmeti projesini dağıtma][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="7c8da-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="7c8da-117">[Bir bulut hizmeti örneği içine Uzak Masaüstü][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="7c8da-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="7c8da-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="7c8da-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="7c8da-119">Merhaba **ServiceDefinition.csdef** dosyayı belirtir Azure tooconfigure tarafından kullanılan hello ayarları bir bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="7c8da-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="7c8da-120">Merhaba [Azure Hizmet tanım Şeması (.csdef dosyası)](https://msdn.microsoft.com/library/azure/ee758711.aspx) hello izin verilen biçim için bir hizmet tanımı dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="7c8da-121">Merhaba aşağıdaki örnek hello Web ve çalışan rolleri için tanımlanan hello ayarlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7c8da-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="7c8da-122">Toohello başvurabilir [Hizmet tanım Şeması](https://msdn.microsoft.com/library/azure/ee758711.aspx) daha iyi burada kullanılan hello XML Şeması anlamak için Bununla birlikte, İşte bazı hello öğeleri hızlı bir açıklaması:</span><span class="sxs-lookup"><span data-stu-id="7c8da-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="7c8da-123">**Siteleri**</span><span class="sxs-lookup"><span data-stu-id="7c8da-123">**Sites**</span></span>  
<span data-ttu-id="7c8da-124">IIS7'de barındırılan Web siteleri veya web uygulamaları için Hello tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="7c8da-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="7c8da-125">**InputEndpoints**</span></span>  
<span data-ttu-id="7c8da-126">Uç noktalar için Hello tanımları içeren toocontact hello bulut hizmeti kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="7c8da-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="7c8da-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="7c8da-128">Rol örnekleri toocommunicate birbirleriyle tarafından kullanılan uç noktaları için Hello tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="7c8da-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="7c8da-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="7c8da-130">Belirli bir rol özellikleri için Hello ayarı tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="7c8da-131">**Sertifikalar**</span><span class="sxs-lookup"><span data-stu-id="7c8da-131">**Certificates**</span></span>  
<span data-ttu-id="7c8da-132">Bir rol için gerekli sertifikaları için Hello tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="7c8da-133">Merhaba önceki kod örneğinde hello yapılandırmasını Azure bağlanmak için kullanılan bir sertifika gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="7c8da-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="7c8da-134">**LocalResources**</span></span>  
<span data-ttu-id="7c8da-135">Yerel depolama kaynaklarını Hello tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="7c8da-136">Yerel depolama kaynağı hello sanal makinenin bir rol örneği çalıştığı hello dosya sisteminde ayrılmış bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="7c8da-137">**İçeri aktarmalar**</span><span class="sxs-lookup"><span data-stu-id="7c8da-137">**Imports**</span></span>  
<span data-ttu-id="7c8da-138">İçeri aktarılan modüller Hello tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="7c8da-139">Hello önceki kod örneğinde, Uzak Masaüstü Bağlantısı ve Azure bağlanmak için hello modülleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="7c8da-140">**Başlangıç**</span><span class="sxs-lookup"><span data-stu-id="7c8da-140">**Startup**</span></span>  
<span data-ttu-id="7c8da-141">Merhaba rol başladığında çalıştırılan görevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="7c8da-142">Merhaba görevler bir .cmd veya yürütülebilir dosya içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="7c8da-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="7c8da-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="7c8da-144">Bulut hizmetiniz için hello ayarlarının Hello yapılandırmasını hello başlangıç değerleri belirlenir **ServiceConfiguration.cscfg** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c8da-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="7c8da-145">Bu dosyadaki her rol için toodeploy istediğiniz örneklerinin hello sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="7c8da-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="7c8da-146">Merhaba değerleri hello hizmet tanımı dosyasında tanımlanan hello yapılandırma ayarları için toohello hizmet yapılandırma dosyası eklenir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="7c8da-147">Merhaba bulut hizmetiyle ilişkili tüm yönetim sertifikaları için Hello parmak izleri toohello dosya de eklenir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="7c8da-148">Merhaba [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx) hello izin verilen biçim için bir hizmet yapılandırma dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="7c8da-149">Merhaba hizmet yapılandırma dosyası Merhaba uygulaması ile paketlenmiştir değil ancak ayrı bir dosya olarak karşıya yüklenen tooAzure olduğu ve kullanılan tooconfigure hello bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="7c8da-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="7c8da-150">Bulut hizmetinizi gerek olmadan yeni bir hizmet yapılandırma dosyası karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="7c8da-151">Merhaba bulut hizmeti çalışırken hello yapılandırma değerlerini hello bulut hizmeti için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="7c8da-152">Merhaba aşağıdaki örnek hello Web ve çalışan rolleri için tanımlanan hello yapılandırma ayarlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7c8da-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="7c8da-153">Toohello başvurabilir [hizmet yapılandırma şeması](https://msdn.microsoft.com/library/azure/ee758710.aspx) burada kullanılan daha iyi anlamak hello XML Şeması, ancak hello öğeleri hızlı bir açıklaması aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7c8da-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="7c8da-154">**Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="7c8da-154">**Instances**</span></span>  
<span data-ttu-id="7c8da-155">Örnekleri hello rol için çalışan sayısı hello yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="7c8da-156">tooprevent, bulut hizmet olası yükseltmeleri sırasında kullanılamaz hale gelmesini web dönük rollerinizi birden fazla örneğini dağıtmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="7c8da-157">Birden fazla örneği dağıtarak hello toohello yönergeleri uymak [Azure işlem hizmet düzeyi sözleşmesi (SLA)](http://azure.microsoft.com/support/legal/sla/), Internet'e yönelik rolleri, iki %99,95 harici bağlantı garanti eder ya da daha fazla rol örnekleri için bir hizmet dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="7c8da-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="7c8da-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="7c8da-159">Çalışan rolü için örnekler hello Hello ayarlarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="7c8da-160">Merhaba Hello adını `<Setting>` öğeleri hello Ayar tanımlarına hello hizmet tanımı dosyasında eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="7c8da-161">**Sertifikalar**</span><span class="sxs-lookup"><span data-stu-id="7c8da-161">**Certificates**</span></span>  
<span data-ttu-id="7c8da-162">Merhaba hizmeti tarafından kullanılan hello sertifikaları yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="7c8da-163">Merhaba önceki kod örneğinde nasıl toodefine hello hello RemoteAccess modülü için sertifika gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="7c8da-164">Merhaba hello değerini *parmak izi* toohello parmak izi hello sertifika toouse özniteliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="7c8da-165">Merhaba sertifika parmak izi Hello toohello yapılandırma dosyasını bir metin düzenleyicisi kullanarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="7c8da-166">Ya da hello değer üzerinde hello eklenebilir **sertifikaları** hello sekmesinde **özellikleri** Visual Studio'da hello rolünün sayfası.</span><span class="sxs-lookup"><span data-stu-id="7c8da-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="7c8da-167">Rol örnekleri için bağlantı noktalarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="7c8da-167">Defining ports for role instances</span></span>
<span data-ttu-id="7c8da-168">Azure yalnızca bir giriş noktası tooa web rolü sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="7c8da-169">Tüm trafiği aracılığıyla bir IP adresi oluştuğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="7c8da-170">Merhaba ana bilgisayar üstbilgisi toodirect hello isteği toohello doğru konuma yapılandırarak, Web siteleri tooshare bir bağlantı noktası yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="7c8da-171">Başlangıç IP adresi uygulamaları toolisten toowell bilinen bağlantı noktalarını da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="7c8da-172">Merhaba aşağıdaki örnek bir Web sitesi ve web uygulaması içeren bir web rolü için başlangıç yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="7c8da-173">Hello Web sitesi bağlantı noktası 80 üzerinde hello varsayılan giriş konumu olarak yapılandırılır ve hello web uygulamalardır yapılandırılmış tooreceive isteklerinden "mail.mysite.cloudapp.net" adlı bir alternatif ana bilgisayar üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="7c8da-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="7c8da-174">Bir rolün Hello yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="7c8da-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="7c8da-175">Azure'da hello hizmet çevrimdışı bırakmadan çalışırken, bulut hizmetinizin hello yapılandırma güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="7c8da-176">toochange yapılandırma bilgilerini, yeni bir yapılandırma dosyası ya da yükleyebilir veya düzenleme hello yapılandırma dosyasında yerleştirin ve hizmetini çalıştıran tooyour uygulayın.</span><span class="sxs-lookup"><span data-stu-id="7c8da-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="7c8da-177">Merhaba aşağıdaki değişiklikleri hizmet toohello yapılandırmasını yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="7c8da-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="7c8da-178">**Merhaba değerleri yapılandırma ayarlarını değiştirme**</span><span class="sxs-lookup"><span data-stu-id="7c8da-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="7c8da-179">Bir yapılandırma ayarı değişiklikleri, bir rol örneği hello örneği çevrimiçi durumdayken tooapply hello değişiklik veya toorecycle hello örnek düzgün biçimde seçin ve hello örneği çevrimdışı durumdayken hello değişikliği uygulamak.</span><span class="sxs-lookup"><span data-stu-id="7c8da-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="7c8da-180">**Merhaba Hizmeti topolojisi rol örneklerinin değiştirme**</span><span class="sxs-lookup"><span data-stu-id="7c8da-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="7c8da-181">Topolojisi değişiklikleri bir örneği burada kaldırılmakta dışında çalışan örneklerini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="7c8da-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="7c8da-182">Tüm kalan örnekleri geri dönüşüm toobe genellikle gerekmez; Ancak, rol örnekleri toorecycle yanıt tooa topoloji değişikliği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="7c8da-183">**Merhaba sertifika parmak izi değiştirme**</span><span class="sxs-lookup"><span data-stu-id="7c8da-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="7c8da-184">Rol örneği çevrimdışı olduğunda, yalnızca bir sertifika güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c8da-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="7c8da-185">Bir sertifika eklenmiş, silinmiş veya rol örneği çevrimiçi durumdayken değişti, Azure düzgün biçimde hello örneği çevrimdışı tooupdate hello sertifika alır ve hello değişiklik tamamlandıktan sonra yeniden çevrimiçi duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="7c8da-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="7c8da-186">Yapılandırma değişiklikleriyle hizmeti çalışma zamanı olayları işleme</span><span class="sxs-lookup"><span data-stu-id="7c8da-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="7c8da-187">Merhaba [Azure çalışma zamanı kitaplığı](https://msdn.microsoft.com/library/azure/mt419365.aspx) hello içeren [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) ad alanı bir rolden Azure ortamı hello ile etkileşim kurmaya yönelik sınıflar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="7c8da-188">Merhaba [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) sınıfı önce ve sonra bir yapılandırma değişikliği yükseltilmiş olayları aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="7c8da-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="7c8da-189">**[Değiştirme](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) olayı**</span><span class="sxs-lookup"><span data-stu-id="7c8da-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="7c8da-190">Merhaba yapılandırma değişikliği uygulanan tooa belirtilen gerekirse fırsat tootake hello rol örnekleri aşağı vermiş bir rol örneği önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="7c8da-191">**[Değiştirilen](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) olayı**</span><span class="sxs-lookup"><span data-stu-id="7c8da-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="7c8da-192">Merhaba yapılandırma değişikliği uygulanan tooa belirtilen bir rol örneği olduğunda oluşur.</span><span class="sxs-lookup"><span data-stu-id="7c8da-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="7c8da-193">Sertifika değişiklikleri her zaman bir rolün örnekleri hello çevrimdışına çünkü hello RoleEnvironment.Changing veya RoleEnvironment.Changed olayları yükseltmeyin.</span><span class="sxs-lookup"><span data-stu-id="7c8da-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="7c8da-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="7c8da-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="7c8da-195">bir uygulamayı Azure bulut hizmeti olarak toodeploy, ilk paketi Merhaba uygulaması hello uygun biçimde gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c8da-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="7c8da-196">Merhaba kullanabilirsiniz **CSPack** komut satırı aracı (Merhaba ile yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/)) toocreate hello paket dosyası alternatif bir tooVisual Studio olarak.</span><span class="sxs-lookup"><span data-stu-id="7c8da-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="7c8da-197">**CSPack** kullanır hello hello hizmet tanımı dosya ve hizmet yapılandırma dosyası toodefine hello hello paketinin içeriğini içeriğini.</span><span class="sxs-lookup"><span data-stu-id="7c8da-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="7c8da-198">**CSPack** hello kullanarak bir uygulama paketi dosyası (.cspkg tooAzure yükleyebilirsiniz) oluşturur [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="7c8da-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="7c8da-199">Varsayılan olarak, adlı hello paket `[ServiceDefinitionFileName].cspkg`, ancak hello kullanarak farklı bir ad belirtebilirsiniz `/out` seçeneği **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="7c8da-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="7c8da-200">**CSPack** bulunur</span><span class="sxs-lookup"><span data-stu-id="7c8da-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="7c8da-201">CSPack.exe (windows üzerinde) kullanılabilir hello çalıştırarak **Microsoft Azure komut istemi** hello SDK ile yüklenen kısayol.</span><span class="sxs-lookup"><span data-stu-id="7c8da-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="7c8da-202">Hello CSPack.exe programını tek başına toosee belgelerine tüm hello olası anahtarları ve komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c8da-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="7c8da-203">Bulut hizmetinizi yerel olarak çalıştırma hello **Microsoft Azure işlem öykünücüsü**, hello kullan **/copyonly** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7c8da-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="7c8da-204">Bu seçenek hello hello uygulama tooa dizin düzenini içinden hello işlem öykünücüsü çalıştırılabilmesi için ikili dosyaları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7c8da-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="7c8da-205">Örnek komut toopackage bir bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="7c8da-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="7c8da-206">Merhaba aşağıdaki örnek bir web rolü hello bilgilerini içeren bir uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7c8da-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="7c8da-207">Merhaba hizmet tanımı dosyası toouse Hello komutu belirtir, ikili dosyaları burada olabilir hello dizin bulundu ve hello paket dosyasının adı hello.</span><span class="sxs-lookup"><span data-stu-id="7c8da-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="7c8da-208">Merhaba uygulama bir web rolü ve çalışan rolü içeriyorsa, hello aşağıdaki komutu kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7c8da-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="7c8da-209">Burada hello değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7c8da-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="7c8da-210">Değişken</span><span class="sxs-lookup"><span data-stu-id="7c8da-210">Variable</span></span> | <span data-ttu-id="7c8da-211">Değer</span><span class="sxs-lookup"><span data-stu-id="7c8da-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7c8da-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-212">\[DirectoryName\]</span></span> |<span data-ttu-id="7c8da-213">Merhaba alt hello .csdef dosyası hello Azure projesi, içerir hello kök proje dizini altında.</span><span class="sxs-lookup"><span data-stu-id="7c8da-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="7c8da-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="7c8da-215">Merhaba hizmet tanımı dosyası Hello adı.</span><span class="sxs-lookup"><span data-stu-id="7c8da-215">hello name of hello service definition file.</span></span> <span data-ttu-id="7c8da-216">Varsayılan olarak, bu dosyayı ServiceDefinition.csdef olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="7c8da-217">\[Çıkışdosyaadı\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-217">\[OutputFileName\]</span></span> |<span data-ttu-id="7c8da-218">Merhaba adı hello için paket dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7c8da-218">hello name for hello generated package file.</span></span> <span data-ttu-id="7c8da-219">Genellikle, bu Merhaba uygulaması toohello adına ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7c8da-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="7c8da-220">Hiçbir dosya adı belirtilirse, hello uygulama paketi olarak oluşturuldu \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="7c8da-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="7c8da-221">\[Rol adı\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-221">\[RoleName\]</span></span> |<span data-ttu-id="7c8da-222">Merhaba hizmet tanımı dosyasında tanımlanan hello rolünün Hello adı.</span><span class="sxs-lookup"><span data-stu-id="7c8da-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="7c8da-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="7c8da-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="7c8da-224">hello ikili dosyaları hello rolü için başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="7c8da-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="7c8da-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-225">\[VirtualPath\]</span></span> |<span data-ttu-id="7c8da-226">Merhaba hello siteler bölümünde hello hizmet tanımı tanımlanan her sanal yol için fiziksel dizinler.</span><span class="sxs-lookup"><span data-stu-id="7c8da-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="7c8da-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="7c8da-228">Merhaba hello site düğümünde hello hizmet tanımı tanımlanan her sanal yol için hello içeriğinin fiziksel dizinleri.</span><span class="sxs-lookup"><span data-stu-id="7c8da-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="7c8da-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="7c8da-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="7c8da-230">Merhaba rolü için ikili dosya hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="7c8da-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c8da-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c8da-231">Next steps</span></span>
<span data-ttu-id="7c8da-232">Bulut hizmeti paket oluşturma ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="7c8da-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="7c8da-233">[Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="7c8da-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="7c8da-234">[Bir bulut hizmeti projesini dağıtma][deploy]</span><span class="sxs-lookup"><span data-stu-id="7c8da-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="7c8da-235">Visual Studio kullanarak ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="7c8da-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="7c8da-236">[Yeni bir bulut hizmeti oluştur][vs_create]</span><span class="sxs-lookup"><span data-stu-id="7c8da-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="7c8da-237">[Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="7c8da-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="7c8da-238">[Bir bulut hizmeti projesini dağıtma][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="7c8da-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="7c8da-239">[Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="7c8da-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
