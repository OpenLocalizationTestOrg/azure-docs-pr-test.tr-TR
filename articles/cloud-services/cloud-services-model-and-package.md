---
title: Bir bulut hizmeti modeli ve paket nedir | Microsoft Docs
description: "Bulut hizmeti modeli (.csdef, .cscfg) ve Azure paketine (.cspkg) açıklanır"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="a1c69-103">Bulut hizmeti modeli nedir ve nasıl paket?</span><span class="sxs-lookup"><span data-stu-id="a1c69-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="a1c69-104">Bir bulut hizmeti üç bileşenlerini hizmet tanımı oluşturulur *(.csdef)*, hizmet yapılandırması *(.cscfg)*ve bir hizmet paketi *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="a1c69-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="a1c69-105">Her iki **ServiceDefinition.csdef** ve **ServiceConfig.cscfg** dosyaları XML tabanlı ve topluca modeli olarak adlandırılan bulut hizmeti ve nasıl yapılandırıldığını; yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="a1c69-106">**ServicePackage.cspkg** oluşturulduğu bir zip dosyası **ServiceDefinition.csdef** ve bunun yanı sıra, ikili tabanlı tüm gerekli bağımlılıklar içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="a1c69-107">Azure hem de bir bulut hizmeti oluşturur **ServicePackage.cspkg** ve **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="a1c69-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="a1c69-108">Azure'da bulut hizmeti çalışır duruma geldiğinde üzerinden yapılandırabilirsiniz **ServiceConfig.cscfg** dosyası, ancak tanımı alter olamaz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="a1c69-109">Ne hakkında daha fazla bilgi edinmek istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="a1c69-109">What would you like to know more about?</span></span>
* <span data-ttu-id="a1c69-110">Daha fazla bilgi almak istiyorum [ServiceDefinition.csdef](#csdef) ve [ServiceConfig.cscfg](#cscfg) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a1c69-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="a1c69-111">Zaten bu hakkında bilebilirim ver [bazı örnekler](#next-steps) üzerinde ne ı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="a1c69-112">Oluşturmak istediğiniz [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="a1c69-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="a1c69-113">Visual Studio kullanarak ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="a1c69-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="a1c69-114">[Bir bulut hizmeti oluştur][vs_create]</span><span class="sxs-lookup"><span data-stu-id="a1c69-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="a1c69-115">[Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="a1c69-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="a1c69-116">[Bir bulut hizmeti projesini dağıtma][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="a1c69-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="a1c69-117">[Bir bulut hizmeti örneği içine Uzak Masaüstü][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="a1c69-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="a1c69-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="a1c69-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="a1c69-119">**ServiceDefinition.csdef** dosyasını bir bulut hizmeti yapılandırmak için Azure tarafından kullanılan ayarları belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="a1c69-120">[Azure Hizmet tanım Şeması (.csdef dosyası)](https://msdn.microsoft.com/library/azure/ee758711.aspx) Hizmet tanım dosyası için izin verilen biçim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="a1c69-121">Aşağıdaki örnek, Web ve çalışan rolleri için tanımlanan ayarları gösterir:</span><span class="sxs-lookup"><span data-stu-id="a1c69-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="a1c69-122">Başvurabilirsiniz [Hizmet tanım Şeması](https://msdn.microsoft.com/library/azure/ee758711.aspx) daha iyi burada kullanılan XML Şeması anlamak için Bununla birlikte, İşte bazı öğelerin hızlı bir açıklaması:</span><span class="sxs-lookup"><span data-stu-id="a1c69-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="a1c69-123">**Siteleri**</span><span class="sxs-lookup"><span data-stu-id="a1c69-123">**Sites**</span></span>  
<span data-ttu-id="a1c69-124">IIS7'de barındırılan Web siteleri veya web uygulamaları için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="a1c69-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="a1c69-125">**InputEndpoints**</span></span>  
<span data-ttu-id="a1c69-126">Bulut hizmeti ile iletişim kurmada kullanılan uç noktalar için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="a1c69-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="a1c69-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="a1c69-128">Rol örnekleri tarafından birbirleri ile iletişim kurmak için kullanılan uç noktalar için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="a1c69-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="a1c69-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="a1c69-130">Belirli bir rol özelliklerinin ayarı tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="a1c69-131">**Sertifikalar**</span><span class="sxs-lookup"><span data-stu-id="a1c69-131">**Certificates**</span></span>  
<span data-ttu-id="a1c69-132">Bir rol için gerekli sertifikaları için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="a1c69-133">Önceki kod örneğinde Azure Connect yapılandırma için kullanılan bir sertifika gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="a1c69-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="a1c69-134">**LocalResources**</span></span>  
<span data-ttu-id="a1c69-135">Yerel depolama alanı kaynakları için tanımları içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="a1c69-136">Yerel depolama kaynağı, bir rol örneği çalıştığı sanal makinenin dosya sisteminde ayrılmış bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="a1c69-137">**İçeri aktarmalar**</span><span class="sxs-lookup"><span data-stu-id="a1c69-137">**Imports**</span></span>  
<span data-ttu-id="a1c69-138">İçeri aktarılan modül tanımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="a1c69-139">Önceki kod örneğinde, Uzak Masaüstü Bağlantısı ve Azure bağlanmak için modülleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="a1c69-140">**Başlangıç**</span><span class="sxs-lookup"><span data-stu-id="a1c69-140">**Startup**</span></span>  
<span data-ttu-id="a1c69-141">Rol başladığında çalıştırılan görevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="a1c69-142">Görevler bir .cmd veya yürütülebilir dosya içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="a1c69-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="a1c69-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="a1c69-144">Bulut hizmetiniz için ayarları yapılandırma değerleri tarafından belirlenen **ServiceConfiguration.cscfg** dosya.</span><span class="sxs-lookup"><span data-stu-id="a1c69-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="a1c69-145">Bu dosyadaki her rol için dağıtmak istediğiniz örneklerinin sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1c69-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="a1c69-146">Hizmet tanımı dosyasında tanımlanan yapılandırma ayarları için değerleri service yapılandırma dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="a1c69-147">Bulut hizmeti ile ilişkilendirilmiş herhangi bir yönetim sertifika parmak izleri de dosyaya eklenir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="a1c69-148">[Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx) için bir hizmet yapılandırma dosyası izin verilen biçim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="a1c69-149">Hizmet yapılandırma dosyası uygulama ile paketlenmiştir değil, ancak ayrı bir dosya olarak Azure karşıya ve bulut hizmeti yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="a1c69-150">Bulut hizmetinizi gerek olmadan yeni bir hizmet yapılandırma dosyası karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="a1c69-151">Bulut hizmeti çalışırken bulut hizmeti için yapılandırma değerlerini değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="a1c69-152">Aşağıdaki örnek, Web ve çalışan rolleri için tanımlanan yapılandırma ayarlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="a1c69-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="a1c69-153">Başvurabilirsiniz [hizmet yapılandırma şeması](https://msdn.microsoft.com/library/azure/ee758710.aspx) daha iyi burada kullanılan XML Şeması anlamak için ancak öğeleri hızlı bir açıklaması aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a1c69-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="a1c69-154">**Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="a1c69-154">**Instances**</span></span>  
<span data-ttu-id="a1c69-155">Çalışan rolü için örnek sayısını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="a1c69-156">Bulut hizmetinizi olası yükseltmeleri sırasında kullanılamaz hale gelmesini önlemek için web dönük rollerinizi birden fazla örneğini dağıtmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="a1c69-157">Birden fazla örneği dağıtarak, yönergelere karşıladığınızdan [Azure işlem hizmet düzeyi sözleşmesi (SLA)](http://azure.microsoft.com/support/legal/sla/), garanti %99,95 harici bağlantı Internet'e yönelik rolleri, iki veya daha fazla rol örnekleri bir hizmet için dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="a1c69-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="a1c69-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="a1c69-159">Bir rolün çalışan örneklerini için ayarları yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="a1c69-160">Adını `<Setting>` öğeleri hizmet tanımı dosyası ayarı tanımlarında eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="a1c69-161">**Sertifikalar**</span><span class="sxs-lookup"><span data-stu-id="a1c69-161">**Certificates**</span></span>  
<span data-ttu-id="a1c69-162">Hizmet tarafından kullanılan sertifikalar yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="a1c69-163">Önceki kod örneğinde RemoteAccess modülü için sertifikayı tanımlayan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="a1c69-164">Değeri *parmak izi* özniteliği kullanmak için sertifika parmak izi için ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="a1c69-165">Sertifika parmak izini bir metin düzenleyicisi kullanarak yapılandırma dosyasına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="a1c69-166">Veya, değer üzerinde eklenebilir **sertifikaları** sekmesinde **özellikleri** Visual Studio'da rolünün sayfası.</span><span class="sxs-lookup"><span data-stu-id="a1c69-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="a1c69-167">Rol örnekleri için bağlantı noktalarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="a1c69-167">Defining ports for role instances</span></span>
<span data-ttu-id="a1c69-168">Azure web rolü için yalnızca bir giriş noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="a1c69-169">Tüm trafiği aracılığıyla bir IP adresi oluştuğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="a1c69-170">İstek doğru konuma yönlendirmek için ana bilgisayar üstbilgisi yapılandırarak bir bağlantı noktasını paylaşmak için Web sitelerinizi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="a1c69-171">IP adresi iyi bilinen bağlantı noktalarını dinlemek için uygulamalarınızı da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="a1c69-172">Aşağıdaki örnek bir Web sitesi ve web uygulaması içeren bir web rolü için yapılandırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="a1c69-173">Web sitesi bağlantı noktası 80 üzerinde varsayılan giriş konumu olarak yapılandırılmış ve web uygulamaları "mail.mysite.cloudapp.net" adlı bir alternatif ana bilgisayar üstbilgisi istekleri almak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="a1c69-174">Bir rolü yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a1c69-174">Changing the configuration of a role</span></span>
<span data-ttu-id="a1c69-175">Azure üzerinde hizmet çevrimdışı bırakmadan çalışırken, bulut hizmetinin yapılandırmasını güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="a1c69-176">Yapılandırma bilgilerini değiştirmek için yeni bir yapılandırma dosyası karşıya yükleme veya yerinde yapılandırma dosyasını düzenlemenize ve çalışan hizmetinize uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a1c69-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="a1c69-177">Bir hizmet yapılandırması için aşağıdaki değişiklikler yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="a1c69-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="a1c69-178">**Yapılandırma ayarlarının değerleri değiştirme**</span><span class="sxs-lookup"><span data-stu-id="a1c69-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="a1c69-179">Ne zaman bir yapılandırma değişiklikleri ayarı değişikliği örneği çevrimiçi veya çevrimdışı olduğunda örneğinin düzgün bir şekilde geri dönüşüm ve örnek değişikliği uygulamak için geçerliyken, bir rol örneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="a1c69-180">**Rol örneklerinin Hizmeti topolojisi değiştirme**</span><span class="sxs-lookup"><span data-stu-id="a1c69-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="a1c69-181">Topolojisi değişiklikleri bir örneği burada kaldırılmakta dışında çalışan örneklerini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="a1c69-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="a1c69-182">Tüm kalan örnekleri genellikle geri dönüştürülmesi gerekmez; Ancak, bir topoloji değişikliği yanıta rol örneklerinin geri dönüşüm seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="a1c69-183">**Sertifika parmak izini değiştirme**</span><span class="sxs-lookup"><span data-stu-id="a1c69-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="a1c69-184">Rol örneği çevrimdışı olduğunda, yalnızca bir sertifika güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c69-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="a1c69-185">Bir sertifika eklenmiş, silinmiş veya rol örneği çevrimiçi durumdayken değişti, Azure düzgün biçimde örneği çevrimdışı bir sertifikayı güncelleştirmek ve değişiklik tamamlandıktan sonra yeniden çevrimiçi duruma getirmek için alır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="a1c69-186">Yapılandırma değişiklikleriyle hizmeti çalışma zamanı olayları işleme</span><span class="sxs-lookup"><span data-stu-id="a1c69-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="a1c69-187">[Azure çalışma zamanı kitaplığı](https://msdn.microsoft.com/library/azure/mt419365.aspx) içeren [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) ad alanı bir rolden Azure ortamı ile etkileşim kurmaya yönelik sınıflar sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="a1c69-188">[RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) sınıfı önce ve sonra bir yapılandırma değişikliği yükseltilmiş aşağıdaki olaylar tanımlar:</span><span class="sxs-lookup"><span data-stu-id="a1c69-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="a1c69-189">**[Değiştirme](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) olayı**</span><span class="sxs-lookup"><span data-stu-id="a1c69-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="a1c69-190">Yapılandırma değişikliği bir iletmenize gerekirse rol örnekleri almak için bir rolün belirtilen bir örneğini uygulanmadan önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="a1c69-191">**[Değiştirilen](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) olayı**</span><span class="sxs-lookup"><span data-stu-id="a1c69-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="a1c69-192">Belirtilen bir rol örneği için yapılandırma değişikliği uygulandıktan sonra oluşur.</span><span class="sxs-lookup"><span data-stu-id="a1c69-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="a1c69-193">Sertifika değişiklikleri her zaman bir rolün örnekleri çevrimdışına çünkü RoleEnvironment.Changing veya RoleEnvironment.Changed olayları yükseltmeyin.</span><span class="sxs-lookup"><span data-stu-id="a1c69-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="a1c69-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="a1c69-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="a1c69-195">Bir uygulamayı Azure bulut hizmeti olarak dağıtmak için önce uygun biçimdeki uygulama paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="a1c69-196">Kullanabileceğiniz **CSPack** komut satırı aracı (yüklenmiş [Azure SDK'sı](https://azure.microsoft.com/downloads/)) Visual Studio alternatif olarak paket dosyasını oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a1c69-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="a1c69-197">**CSPack** Hizmet tanım dosyası ve hizmet yapılandırma dosyasının içeriğini paket içeriğini tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="a1c69-198">**CSPack** kullanarak Azure'a yükleyebileceğiniz bir uygulama paketi dosyası (.cspkg) oluşturur [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="a1c69-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="a1c69-199">Varsayılan olarak, adlı paket `[ServiceDefinitionFileName].cspkg`, ancak kullanarak farklı bir ad belirtebilirsiniz `/out` seçeneği **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="a1c69-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="a1c69-200">**CSPack** bulunur</span><span class="sxs-lookup"><span data-stu-id="a1c69-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="a1c69-201">CSPack.exe (windows üzerinde) kullanılabilir çalıştırarak **Microsoft Azure komut istemi** SDK ile birlikte yüklenen kısayol.</span><span class="sxs-lookup"><span data-stu-id="a1c69-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="a1c69-202">Tüm olası anahtarları ve komutları ile ilgili belgeler görmek için kendi başına CSPack.exe programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a1c69-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="a1c69-203">Bulut hizmetinizi yerel olarak çalıştırmak **Microsoft Azure işlem öykünücüsü**, kullanın **/copyonly** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a1c69-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="a1c69-204">Bu seçenek, uygulama, bunlar işlem öykünücüsü çalıştırılabilir bir dizin düzeni için ikili dosyaları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="a1c69-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="a1c69-205">Bir bulut hizmeti paketlemek için örnek komut</span><span class="sxs-lookup"><span data-stu-id="a1c69-205">Example command to package a cloud service</span></span>
<span data-ttu-id="a1c69-206">Aşağıdaki örnek, bir web rolü için bilgileri içeren bir uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1c69-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="a1c69-207">Komut, ikili dosyaları bulunabileceği, dizini kullanmak için hizmet tanımı dosyası ve paket dosyası adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1c69-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="a1c69-208">Uygulama bir web rolü ve çalışan rolü içeriyorsa, aşağıdaki komutu kullanılır:</span><span class="sxs-lookup"><span data-stu-id="a1c69-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="a1c69-209">Burada değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a1c69-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="a1c69-210">Değişken</span><span class="sxs-lookup"><span data-stu-id="a1c69-210">Variable</span></span> | <span data-ttu-id="a1c69-211">Değer</span><span class="sxs-lookup"><span data-stu-id="a1c69-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a1c69-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-212">\[DirectoryName\]</span></span> |<span data-ttu-id="a1c69-213">Azure projesi .csdef dosyası içeren kök proje dizini altında alt dizin.</span><span class="sxs-lookup"><span data-stu-id="a1c69-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="a1c69-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="a1c69-215">Hizmet tanımı dosyası adı.</span><span class="sxs-lookup"><span data-stu-id="a1c69-215">The name of the service definition file.</span></span> <span data-ttu-id="a1c69-216">Varsayılan olarak, bu dosyayı ServiceDefinition.csdef olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="a1c69-217">\[Çıkışdosyaadı\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-217">\[OutputFileName\]</span></span> |<span data-ttu-id="a1c69-218">Oluşturulan paket dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="a1c69-218">The name for the generated package file.</span></span> <span data-ttu-id="a1c69-219">Genellikle, bu uygulama adına ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a1c69-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="a1c69-220">Hiçbir dosya adı belirtilirse, uygulama paketi olarak oluşturuldu \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="a1c69-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="a1c69-221">\[Rol adı\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-221">\[RoleName\]</span></span> |<span data-ttu-id="a1c69-222">Hizmet tanımı dosyasında tanımlanan rolün adı.</span><span class="sxs-lookup"><span data-stu-id="a1c69-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="a1c69-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="a1c69-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="a1c69-224">Rolü için ikili dosyalarının konumu.</span><span class="sxs-lookup"><span data-stu-id="a1c69-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="a1c69-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-225">\[VirtualPath\]</span></span> |<span data-ttu-id="a1c69-226">Hizmet tanımı siteler bölümünde tanımlanan her sanal yol için fiziksel dizinler.</span><span class="sxs-lookup"><span data-stu-id="a1c69-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="a1c69-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="a1c69-228">Hizmet tanımı site düğümde tanımlanan her sanal yol için içerik fiziksel dizinleri.</span><span class="sxs-lookup"><span data-stu-id="a1c69-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="a1c69-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="a1c69-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="a1c69-230">Rolü için ikili dosya adı.</span><span class="sxs-lookup"><span data-stu-id="a1c69-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a1c69-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1c69-231">Next steps</span></span>
<span data-ttu-id="a1c69-232">Bulut hizmeti paket oluşturma ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="a1c69-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="a1c69-233">[Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="a1c69-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="a1c69-234">[Bir bulut hizmeti projesini dağıtma][deploy]</span><span class="sxs-lookup"><span data-stu-id="a1c69-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="a1c69-235">Visual Studio kullanarak ve istiyorum...</span><span class="sxs-lookup"><span data-stu-id="a1c69-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="a1c69-236">[Yeni bir bulut hizmeti oluştur][vs_create]</span><span class="sxs-lookup"><span data-stu-id="a1c69-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="a1c69-237">[Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="a1c69-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="a1c69-238">[Bir bulut hizmeti projesini dağıtma][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="a1c69-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="a1c69-239">[Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="a1c69-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
