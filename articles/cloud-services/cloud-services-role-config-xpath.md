---
title: "Bulut Hizmetleri rolünü config XPath kopya sayfası | Microsoft Docs"
description: "Çeşitli XPath ayarları bulut hizmeti rolünü yapılandırma ayarlarını bir ortam değişkeni göstermek için kullanabilirsiniz."
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
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="4f5c2-103">Rol yapılandırma ayarlarını XPath olan bir ortam değişkeni olarak kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="4f5c2-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="4f5c2-104">Bulut hizmeti çalışan ya da web rolü hizmet tanımı dosyası ortam değişkenleri olarak çalışma zamanı yapılandırma değerlerini getirebilir.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="4f5c2-105">Aşağıdaki XPath değerleri (hangi API değerlerine karşılık gelen) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="4f5c2-106">Bu XPath değerleri de aracılığıyla kullanılabilir [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="4f5c2-107">Öykünücüde çalışan uygulama</span><span class="sxs-lookup"><span data-stu-id="4f5c2-107">App running in emulator</span></span>
<span data-ttu-id="4f5c2-108">Uygulamayı öykünücüde çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="4f5c2-109">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-109">Type</span></span> | <span data-ttu-id="4f5c2-110">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-111">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-111">XPath</span></span> |<span data-ttu-id="4f5c2-112">XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="4f5c2-113">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-113">Code</span></span> |<span data-ttu-id="4f5c2-114">var x RoleEnvironment.IsEmulated; =</span><span class="sxs-lookup"><span data-stu-id="4f5c2-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="4f5c2-115">Dağıtım kimliği</span><span class="sxs-lookup"><span data-stu-id="4f5c2-115">Deployment ID</span></span>
<span data-ttu-id="4f5c2-116">Örneğin dağıtım kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="4f5c2-117">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-117">Type</span></span> | <span data-ttu-id="4f5c2-118">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-119">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-119">XPath</span></span> |<span data-ttu-id="4f5c2-120">XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="4f5c2-121">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-121">Code</span></span> |<span data-ttu-id="4f5c2-122">var Deploymentıd = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="4f5c2-123">Rol Kimliği</span><span class="sxs-lookup"><span data-stu-id="4f5c2-123">Role ID</span></span>
<span data-ttu-id="4f5c2-124">Örnek için geçerli rol kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="4f5c2-125">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-125">Type</span></span> | <span data-ttu-id="4f5c2-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-127">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-127">XPath</span></span> |<span data-ttu-id="4f5c2-128">XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="4f5c2-129">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-129">Code</span></span> |<span data-ttu-id="4f5c2-130">var kimliği = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="4f5c2-131">etki alanı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4f5c2-131">Update domain</span></span>
<span data-ttu-id="4f5c2-132">Güncelleştirme etki alanı örneği alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="4f5c2-133">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-133">Type</span></span> | <span data-ttu-id="4f5c2-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-135">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-135">XPath</span></span> |<span data-ttu-id="4f5c2-136">XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="4f5c2-137">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-137">Code</span></span> |<span data-ttu-id="4f5c2-138">var ud RoleEnvironment.CurrentRoleInstance.UpdateDomain; =</span><span class="sxs-lookup"><span data-stu-id="4f5c2-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="4f5c2-139">hata etki alanı</span><span class="sxs-lookup"><span data-stu-id="4f5c2-139">Fault domain</span></span>
<span data-ttu-id="4f5c2-140">Hata etki alanı örneği alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="4f5c2-141">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-141">Type</span></span> | <span data-ttu-id="4f5c2-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-143">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-143">XPath</span></span> |<span data-ttu-id="4f5c2-144">XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="4f5c2-145">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-145">Code</span></span> |<span data-ttu-id="4f5c2-146">var fd RoleEnvironment.CurrentRoleInstance.FaultDomain; =</span><span class="sxs-lookup"><span data-stu-id="4f5c2-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="4f5c2-147">Rol adı</span><span class="sxs-lookup"><span data-stu-id="4f5c2-147">Role name</span></span>
<span data-ttu-id="4f5c2-148">Bu rol adı örneği alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="4f5c2-149">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-149">Type</span></span> | <span data-ttu-id="4f5c2-150">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-151">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-151">XPath</span></span> |<span data-ttu-id="4f5c2-152">XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="4f5c2-153">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-153">Code</span></span> |<span data-ttu-id="4f5c2-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="4f5c2-155">Yapılandırma ayarı</span><span class="sxs-lookup"><span data-stu-id="4f5c2-155">Config setting</span></span>
<span data-ttu-id="4f5c2-156">Belirtilen yapılandırma ayarının değeri alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="4f5c2-157">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-157">Type</span></span> | <span data-ttu-id="4f5c2-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-159">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-159">XPath</span></span> |<span data-ttu-id="4f5c2-160">XPath = "/ RoleEnvironment/currentınstance değerinin/ConfigurationSettings/ConfigurationSetting [@name'Setting1' =]/@value"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="4f5c2-161">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-161">Code</span></span> |<span data-ttu-id="4f5c2-162">değişken ayarı RoleEnvironment.GetConfigurationSettingValue("Setting1"); =</span><span class="sxs-lookup"><span data-stu-id="4f5c2-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="4f5c2-163">Yerel depolama alanı yolu</span><span class="sxs-lookup"><span data-stu-id="4f5c2-163">Local storage path</span></span>
<span data-ttu-id="4f5c2-164">Örneğin yerel depolama yolunu alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="4f5c2-165">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-165">Type</span></span> | <span data-ttu-id="4f5c2-166">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-167">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-167">XPath</span></span> |<span data-ttu-id="4f5c2-168">XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@path"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="4f5c2-169">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-169">Code</span></span> |<span data-ttu-id="4f5c2-170">var localResourcePath RoleEnvironment.GetLocalResource("LocalStore1") =. RootPath;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="4f5c2-171">Yerel depolama boyutu</span><span class="sxs-lookup"><span data-stu-id="4f5c2-171">Local storage size</span></span>
<span data-ttu-id="4f5c2-172">Örneğin yerel depolama boyutunu alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="4f5c2-173">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-173">Type</span></span> | <span data-ttu-id="4f5c2-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-175">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-175">XPath</span></span> |<span data-ttu-id="4f5c2-176">XPath = "/ RoleEnvironment/currentınstance değerinin/LocalResources/LocalResource [@name'LocalStore1' =]/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="4f5c2-177">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-177">Code</span></span> |<span data-ttu-id="4f5c2-178">var localResourceSizeInMB RoleEnvironment.GetLocalResource("LocalStore1") =. MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="4f5c2-179">Uç nokta Protokolü</span><span class="sxs-lookup"><span data-stu-id="4f5c2-179">Endpoint protocol</span></span>
<span data-ttu-id="4f5c2-180">Örneği için uç nokta Protokolü alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="4f5c2-181">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-181">Type</span></span> | <span data-ttu-id="4f5c2-182">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-183">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-183">XPath</span></span> |<span data-ttu-id="4f5c2-184">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@protocol"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="4f5c2-185">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-185">Code</span></span> |<span data-ttu-id="4f5c2-186">var KOR RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. Protokol;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="4f5c2-187">Uç nokta IP</span><span class="sxs-lookup"><span data-stu-id="4f5c2-187">Endpoint IP</span></span>
<span data-ttu-id="4f5c2-188">Belirtilen uç noktanın IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="4f5c2-189">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-189">Type</span></span> | <span data-ttu-id="4f5c2-190">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-191">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-191">XPath</span></span> |<span data-ttu-id="4f5c2-192">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@address"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="4f5c2-193">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-193">Code</span></span> |<span data-ttu-id="4f5c2-194">var adresi RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="4f5c2-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="4f5c2-195">uç nokta bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="4f5c2-195">Endpoint port</span></span>
<span data-ttu-id="4f5c2-196">Örneği için uç nokta bağlantı noktası alır.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="4f5c2-197">Tür</span><span class="sxs-lookup"><span data-stu-id="4f5c2-197">Type</span></span> | <span data-ttu-id="4f5c2-198">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="4f5c2-199">XPath</span><span class="sxs-lookup"><span data-stu-id="4f5c2-199">XPath</span></span> |<span data-ttu-id="4f5c2-200">XPath = "/ RoleEnvironment/currentınstance değerinin/uç noktalar/uç noktanın [@name'Bitiş noktası 1' =]/@port"</span><span class="sxs-lookup"><span data-stu-id="4f5c2-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="4f5c2-201">Kod</span><span class="sxs-lookup"><span data-stu-id="4f5c2-201">Code</span></span> |<span data-ttu-id="4f5c2-202">bağlantı noktası var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 ="]. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="4f5c2-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="4f5c2-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="4f5c2-203">Example</span></span>
<span data-ttu-id="4f5c2-204">Bir başlangıç görevi adında bir ortam değişkeni oluşturan çalışan rolü bir örneği burada verilmiştir `TestIsEmulated` kümesine [ @emulated xpath değeri](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="4f5c2-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="4f5c2-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f5c2-205">Next steps</span></span>
<span data-ttu-id="4f5c2-206">Daha fazla bilgi edinmek [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) dosya.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="4f5c2-207">Oluşturma bir [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) paket.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="4f5c2-208">Etkinleştirme [Uzak Masaüstü](cloud-services-role-enable-remote-desktop.md) bir rol için.</span><span class="sxs-lookup"><span data-stu-id="4f5c2-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

