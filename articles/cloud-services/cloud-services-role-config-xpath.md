---
title: "aaaCloud Hizmetleri rolünü config XPath kopya sayfası | Microsoft Docs"
description: "Merhaba bulut hizmeti rolünü yapılandırma tooexpose ayarlarında bir ortam değişkeni kullanabileceğiniz çeşitli XPath ayarları hello."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="fb78e-103">Rol yapılandırma ayarlarını XPath olan bir ortam değişkeni olarak kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="fb78e-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="fb78e-104">Merhaba bulut hizmeti çalışan veya web rolü Hizmet tanım dosyası, ortam değişkenleri olarak çalışma zamanı yapılandırma değerlerini getirebilir.</span><span class="sxs-lookup"><span data-stu-id="fb78e-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="fb78e-105">XPath değerleri aşağıdaki hello (hangi tooAPI değerler karşılık gelir) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fb78e-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="fb78e-106">Bu XPath değerleri de hello kullanılabilir [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="fb78e-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="fb78e-107">Öykünücüde çalışan uygulama</span><span class="sxs-lookup"><span data-stu-id="fb78e-107">App running in emulator</span></span>
<span data-ttu-id="fb78e-108">Bu hello uygulama hello öykünücüsünde çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb78e-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="fb78e-109">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-109">Type</span></span> | <span data-ttu-id="fb78e-110">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-111">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-111">XPath</span></span> |<span data-ttu-id="fb78e-112">XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="fb78e-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="fb78e-113">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-113">Code</span></span> |<span data-ttu-id="fb78e-114">var x RoleEnvironment.IsEmulated; =</span><span class="sxs-lookup"><span data-stu-id="fb78e-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="fb78e-115">Dağıtım kimliği</span><span class="sxs-lookup"><span data-stu-id="fb78e-115">Deployment ID</span></span>
<span data-ttu-id="fb78e-116">Merhaba örneğinin Hello dağıtım kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="fb78e-117">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-117">Type</span></span> | <span data-ttu-id="fb78e-118">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-119">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-119">XPath</span></span> |<span data-ttu-id="fb78e-120">XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="fb78e-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="fb78e-121">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-121">Code</span></span> |<span data-ttu-id="fb78e-122">var Deploymentıd = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="fb78e-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="fb78e-123">Rol Kimliği</span><span class="sxs-lookup"><span data-stu-id="fb78e-123">Role ID</span></span>
<span data-ttu-id="fb78e-124">Merhaba geçerli rol kimliği hello örneği alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="fb78e-125">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-125">Type</span></span> | <span data-ttu-id="fb78e-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-127">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-127">XPath</span></span> |<span data-ttu-id="fb78e-128">XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="fb78e-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="fb78e-129">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-129">Code</span></span> |<span data-ttu-id="fb78e-130">var kimliği = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="fb78e-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="fb78e-131">etki alanı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fb78e-131">Update domain</span></span>
<span data-ttu-id="fb78e-132">Merhaba örneğinin Hello güncelleştirme etki alanı alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="fb78e-133">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-133">Type</span></span> | <span data-ttu-id="fb78e-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-135">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-135">XPath</span></span> |<span data-ttu-id="fb78e-136">XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="fb78e-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="fb78e-137">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-137">Code</span></span> |<span data-ttu-id="fb78e-138">var ud RoleEnvironment.CurrentRoleInstance.UpdateDomain; =</span><span class="sxs-lookup"><span data-stu-id="fb78e-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="fb78e-139">hata etki alanı</span><span class="sxs-lookup"><span data-stu-id="fb78e-139">Fault domain</span></span>
<span data-ttu-id="fb78e-140">Merhaba örneğinin Hello hata etki alanı alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="fb78e-141">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-141">Type</span></span> | <span data-ttu-id="fb78e-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-143">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-143">XPath</span></span> |<span data-ttu-id="fb78e-144">XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="fb78e-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="fb78e-145">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-145">Code</span></span> |<span data-ttu-id="fb78e-146">var fd RoleEnvironment.CurrentRoleInstance.FaultDomain; =</span><span class="sxs-lookup"><span data-stu-id="fb78e-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="fb78e-147">Rol adı</span><span class="sxs-lookup"><span data-stu-id="fb78e-147">Role name</span></span>
<span data-ttu-id="fb78e-148">Merhaba örneklerinin Hello rol adını alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="fb78e-149">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-149">Type</span></span> | <span data-ttu-id="fb78e-150">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-151">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-151">XPath</span></span> |<span data-ttu-id="fb78e-152">XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="fb78e-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="fb78e-153">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-153">Code</span></span> |<span data-ttu-id="fb78e-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="fb78e-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="fb78e-155">Yapılandırma ayarı</span><span class="sxs-lookup"><span data-stu-id="fb78e-155">Config setting</span></span>
<span data-ttu-id="fb78e-156">Yapılandırma ayarı tanımlanmış hello hello değeri alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="fb78e-157">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-157">Type</span></span> | <span data-ttu-id="fb78e-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-159">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-159">XPath</span></span> |<span data-ttu-id="fb78e-160">XPath = "/ RoleEnvironment/currentınstance değerinin/ConfigurationSettings/ConfigurationSetting [@name'Setting1' =]/@value"</span><span class="sxs-lookup"><span data-stu-id="fb78e-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="fb78e-161">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-161">Code</span></span> |<span data-ttu-id="fb78e-162">değişken ayarı RoleEnvironment.GetConfigurationSettingValue("Setting1"); =</span><span class="sxs-lookup"><span data-stu-id="fb78e-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="fb78e-163">Yerel depolama alanı yolu</span><span class="sxs-lookup"><span data-stu-id="fb78e-163">Local storage path</span></span>
<span data-ttu-id="fb78e-164">Merhaba örneğin Hello yerel depolama yolunu alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="fb78e-165">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-165">Type</span></span> | <span data-ttu-id="fb78e-166">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-167">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-167">XPath</span></span> |<span data-ttu-id="fb78e-168">XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@path"</span><span class="sxs-lookup"><span data-stu-id="fb78e-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="fb78e-169">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-169">Code</span></span> |<span data-ttu-id="fb78e-170">var localResourcePath RoleEnvironment.GetLocalResource("LocalStore1") =. RootPath;</span><span class="sxs-lookup"><span data-stu-id="fb78e-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="fb78e-171">Yerel depolama boyutu</span><span class="sxs-lookup"><span data-stu-id="fb78e-171">Local storage size</span></span>
<span data-ttu-id="fb78e-172">Merhaba hello hello örneği için yerel depolama alanının boyutunu alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="fb78e-173">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-173">Type</span></span> | <span data-ttu-id="fb78e-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-175">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-175">XPath</span></span> |<span data-ttu-id="fb78e-176">XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="fb78e-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="fb78e-177">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-177">Code</span></span> |<span data-ttu-id="fb78e-178">var localResourceSizeInMB RoleEnvironment.GetLocalResource("LocalStore1") =. MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="fb78e-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="fb78e-179">Uç nokta Protokolü</span><span class="sxs-lookup"><span data-stu-id="fb78e-179">Endpoint protocol</span></span>
<span data-ttu-id="fb78e-180">Merhaba örneğe Hello uç nokta protokolünü alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="fb78e-181">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-181">Type</span></span> | <span data-ttu-id="fb78e-182">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-183">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-183">XPath</span></span> |<span data-ttu-id="fb78e-184">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@protocol"</span><span class="sxs-lookup"><span data-stu-id="fb78e-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="fb78e-185">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-185">Code</span></span> |<span data-ttu-id="fb78e-186">var KOR RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. Protokol;</span><span class="sxs-lookup"><span data-stu-id="fb78e-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="fb78e-187">Uç nokta IP</span><span class="sxs-lookup"><span data-stu-id="fb78e-187">Endpoint IP</span></span>
<span data-ttu-id="fb78e-188">Alır hello uç noktanın IP adresi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="fb78e-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="fb78e-189">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-189">Type</span></span> | <span data-ttu-id="fb78e-190">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-191">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-191">XPath</span></span> |<span data-ttu-id="fb78e-192">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@address"</span><span class="sxs-lookup"><span data-stu-id="fb78e-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="fb78e-193">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-193">Code</span></span> |<span data-ttu-id="fb78e-194">var adresi RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="fb78e-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="fb78e-195">uç nokta bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="fb78e-195">Endpoint port</span></span>
<span data-ttu-id="fb78e-196">Merhaba örneğinin Hello uç nokta bağlantı noktası alır.</span><span class="sxs-lookup"><span data-stu-id="fb78e-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="fb78e-197">Tür</span><span class="sxs-lookup"><span data-stu-id="fb78e-197">Type</span></span> | <span data-ttu-id="fb78e-198">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="fb78e-199">XPath</span><span class="sxs-lookup"><span data-stu-id="fb78e-199">XPath</span></span> |<span data-ttu-id="fb78e-200">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@port"</span><span class="sxs-lookup"><span data-stu-id="fb78e-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="fb78e-201">Kod</span><span class="sxs-lookup"><span data-stu-id="fb78e-201">Code</span></span> |<span data-ttu-id="fb78e-202">bağlantı noktası var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="fb78e-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="fb78e-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="fb78e-203">Example</span></span>
<span data-ttu-id="fb78e-204">Bir başlangıç görevi adında bir ortam değişkeni oluşturan çalışan rolü bir örneği burada verilmiştir `TestIsEmulated` ayarlamak toohello [ @emulated xpath değeri](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="fb78e-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="fb78e-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb78e-205">Next steps</span></span>
<span data-ttu-id="fb78e-206">Merhaba hakkında daha fazla bilgi [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) dosya.</span><span class="sxs-lookup"><span data-stu-id="fb78e-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="fb78e-207">Oluşturma bir [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) paket.</span><span class="sxs-lookup"><span data-stu-id="fb78e-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="fb78e-208">Etkinleştirme [Uzak Masaüstü](cloud-services-role-enable-remote-desktop.md) bir rol için.</span><span class="sxs-lookup"><span data-stu-id="fb78e-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

