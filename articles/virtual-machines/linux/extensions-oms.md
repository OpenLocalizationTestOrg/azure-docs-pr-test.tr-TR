---
title: "Linux için Azure sanal makine uzantısı aaaOMS | Microsoft Docs"
description: "Merhaba OMS Aracısı'nı bir sanal makine uzantısını kullanarak Linux sanal makine dağıtın."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="2ec34-103">Linux için OMS sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="2ec34-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="2ec34-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2ec34-104">Overview</span></span>

<span data-ttu-id="2ec34-105">Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="2ec34-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="2ec34-106">Merhaba OMS Aracısı sanal makine uzantısı Linux için yayımlanan ve Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2ec34-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="2ec34-107">Merhaba uzantısı Azure sanal makinelerde hello OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2ec34-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="2ec34-108">Bu belge ayrıntıları hello platformları, yapılandırmaları ve dağıtım seçenekleri Linux için OMS sanal makine uzantısı hello için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ec34-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ec34-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="2ec34-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="2ec34-110">Operating system</span></span>

<span data-ttu-id="2ec34-111">Merhaba OMS Aracısı uzantısı bu Linux dağıtımları karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ec34-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="2ec34-112">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="2ec34-112">Distribution</span></span> | <span data-ttu-id="2ec34-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="2ec34-113">Version</span></span> |
|---|---|
| <span data-ttu-id="2ec34-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="2ec34-114">CentOS Linux</span></span> | <span data-ttu-id="2ec34-115">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="2ec34-115">5, 6, and 7</span></span> |
| <span data-ttu-id="2ec34-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="2ec34-116">Oracle Linux</span></span> | <span data-ttu-id="2ec34-117">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="2ec34-117">5, 6, and 7</span></span> |
| <span data-ttu-id="2ec34-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="2ec34-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="2ec34-119">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="2ec34-119">5, 6 and 7</span></span> |
| <span data-ttu-id="2ec34-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="2ec34-120">Debian GNU/Linux</span></span> | <span data-ttu-id="2ec34-121">6, 7 ve 8</span><span class="sxs-lookup"><span data-stu-id="2ec34-121">6, 7, and 8</span></span> |
| <span data-ttu-id="2ec34-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2ec34-122">Ubuntu</span></span> | <span data-ttu-id="2ec34-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2ec34-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="2ec34-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="2ec34-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="2ec34-125">11 ve 12</span><span class="sxs-lookup"><span data-stu-id="2ec34-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="2ec34-126">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="2ec34-126">Internet connectivity</span></span>

<span data-ttu-id="2ec34-127">Linux için OMS aracısının uzantısı Hello gerektirir hello hedef sanal makinenin bağlı toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="2ec34-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="2ec34-128">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="2ec34-128">Extension schema</span></span>

<span data-ttu-id="2ec34-129">Merhaba aşağıdaki JSON hello OMS Aracısı uzantısı için hello şema gösterir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="2ec34-130">Merhaba uzantısı hello hedef OMS çalışma alanından hello çalışma alanı kimliği ve çalışma alanı anahtarı gerekiyor; Bu değerleri hello OMS portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="2ec34-131">Merhaba çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="2ec34-132">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hello hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="2ec34-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="2ec34-133">Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="2ec34-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="2ec34-134">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="2ec34-134">Property values</span></span>

| <span data-ttu-id="2ec34-135">Ad</span><span class="sxs-lookup"><span data-stu-id="2ec34-135">Name</span></span> | <span data-ttu-id="2ec34-136">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="2ec34-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="2ec34-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2ec34-137">apiVersion</span></span> | <span data-ttu-id="2ec34-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="2ec34-138">2015-06-15</span></span> |
| <span data-ttu-id="2ec34-139">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="2ec34-139">publisher</span></span> | <span data-ttu-id="2ec34-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="2ec34-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="2ec34-141">type</span><span class="sxs-lookup"><span data-stu-id="2ec34-141">type</span></span> | <span data-ttu-id="2ec34-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="2ec34-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="2ec34-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="2ec34-143">typeHandlerVersion</span></span> | <span data-ttu-id="2ec34-144">1.4</span><span class="sxs-lookup"><span data-stu-id="2ec34-144">1.4</span></span> |
| <span data-ttu-id="2ec34-145">Workspaceıd (örneğin)</span><span class="sxs-lookup"><span data-stu-id="2ec34-145">workspaceId (e.g)</span></span> | <span data-ttu-id="2ec34-146">6f680a37-00c6-41C7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="2ec34-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="2ec34-147">workspaceKey (örneğin)</span><span class="sxs-lookup"><span data-stu-id="2ec34-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="2ec34-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="2ec34-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="2ec34-149">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="2ec34-149">Template deployment</span></span>

<span data-ttu-id="2ec34-150">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="2ec34-151">Şablonları, bir veya daha fazla ekleme tooOMS gibi dağıtım yapılandırma sonrası gerektiren sanal makineler dağıtırken idealdir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="2ec34-152">Merhaba OMS Aracısı VM uzantısı içeren bir örnek Resource Manager şablonunu hello üzerinde bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="2ec34-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="2ec34-153">sanal makine uzantısı Hello JSON yapılandırması hello sanal makine kaynağı içinde iç içe geçmiş veya hello kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="2ec34-154">Merhaba JSON yapılandırma Hello yerleşimini hello değeri hello kaynak adı ve türü etkiler.</span><span class="sxs-lookup"><span data-stu-id="2ec34-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="2ec34-155">Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2ec34-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="2ec34-156">Merhaba aşağıdaki örneği hello OMS uzantısı hello sanal makine kaynağı içinde iç içe geçmiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="2ec34-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="2ec34-157">Merhaba uzantısı kaynak iç içe geçirme sırasında hello JSON hello yerleştirilir `"resources": []` hello sanal makinenin nesnesi.</span><span class="sxs-lookup"><span data-stu-id="2ec34-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="2ec34-158">Merhaba uzantısı JSON hello hello şablon kökünde yerleştirirken başvuru toohello üst sanal makinesini hello kaynak adı içerir ve hello türü hello iç içe geçmiş yapılandırma yansıtır.</span><span class="sxs-lookup"><span data-stu-id="2ec34-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="2ec34-159">Azure CLI dağıtım</span><span class="sxs-lookup"><span data-stu-id="2ec34-159">Azure CLI deployment</span></span>

<span data-ttu-id="2ec34-160">Hello Azure CLI kullanılan toodeploy hello OMS Aracısı VM uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="2ec34-161">Merhaba OMS anahtarı ve OMS kimliği bu OMS çalışma alanınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2ec34-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="2ec34-162">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="2ec34-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="2ec34-163">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2ec34-163">Troubleshoot</span></span>

<span data-ttu-id="2ec34-164">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure CLI kullanarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="2ec34-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="2ec34-165">toosee hello dağıtım durumu uzantılarının komutunu kullanarak aşağıdaki hello çalıştırmak, belirli bir VM için Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="2ec34-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="2ec34-166">Uzantı yürütme oturum toohello aşağıdaki dosyasına çıktı:</span><span class="sxs-lookup"><span data-stu-id="2ec34-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="2ec34-167">Hata kodları ve anlamları</span><span class="sxs-lookup"><span data-stu-id="2ec34-167">Error codes and their meanings</span></span>

| <span data-ttu-id="2ec34-168">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="2ec34-168">Error Code</span></span> | <span data-ttu-id="2ec34-169">Anlamı</span><span class="sxs-lookup"><span data-stu-id="2ec34-169">Meaning</span></span> | <span data-ttu-id="2ec34-170">Olası eylemi</span><span class="sxs-lookup"><span data-stu-id="2ec34-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="2ec34-171">10</span><span class="sxs-lookup"><span data-stu-id="2ec34-171">10</span></span> | <span data-ttu-id="2ec34-172">VM zaten bağlı tooan OMS çalışma</span><span class="sxs-lookup"><span data-stu-id="2ec34-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="2ec34-173">tooconnect hello VM toohello çalışma Hello uzantısı şemasında belirtilen stopOnMultipleConnections toofalse ortak ayarlar bölümünden veya bu özelliği kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2ec34-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="2ec34-174">Bu VM için bağlı her çalışma alanı için bir kez fatura.</span><span class="sxs-lookup"><span data-stu-id="2ec34-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="2ec34-175">11</span><span class="sxs-lookup"><span data-stu-id="2ec34-175">11</span></span> | <span data-ttu-id="2ec34-176">Sağlanan geçersiz config toohello uzantısı</span><span class="sxs-lookup"><span data-stu-id="2ec34-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="2ec34-177">Örnekler tooset dağıtımı için gerekli tüm özellik değerlerini önceki hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ec34-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="2ec34-178">12</span><span class="sxs-lookup"><span data-stu-id="2ec34-178">12</span></span> | <span data-ttu-id="2ec34-179">Merhaba dpkg Paket Yöneticisi kilitli</span><span class="sxs-lookup"><span data-stu-id="2ec34-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="2ec34-180">Tamamlandı ve yeniden deneyin tüm dpkg güncelleştirme makine üzerindeki işlemleri hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ec34-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="2ec34-181">20</span><span class="sxs-lookup"><span data-stu-id="2ec34-181">20</span></span> | <span data-ttu-id="2ec34-182">Erken adlı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2ec34-182">Enable called prematurely</span></span> | <span data-ttu-id="2ec34-183">[Güncelleştirme hello Azure Linux Aracısı](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello en son sürüme.</span><span class="sxs-lookup"><span data-stu-id="2ec34-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="2ec34-184">51</span><span class="sxs-lookup"><span data-stu-id="2ec34-184">51</span></span> | <span data-ttu-id="2ec34-185">Bu uzantı hello VM'in işlemi sistemde desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="2ec34-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="2ec34-186">55</span><span class="sxs-lookup"><span data-stu-id="2ec34-186">55</span></span> | <span data-ttu-id="2ec34-187">Toohello Microsoft Operations Management Suite hizmetine bağlanılamıyor</span><span class="sxs-lookup"><span data-stu-id="2ec34-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="2ec34-188">Hello sistem ya da Internet erişimi veya geçerli bir HTTP proxy sağlanmış sahip olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2ec34-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="2ec34-189">Ayrıca, hello çalışma alanı kimliği hello doğruluğunu denetleyin</span><span class="sxs-lookup"><span data-stu-id="2ec34-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="2ec34-190">Ek sorun giderme bilgileri hello üzerinde bulunabilir [Linux için OMS Aracısı sorun giderme kılavuzu](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="2ec34-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="2ec34-191">Destek</span><span class="sxs-lookup"><span data-stu-id="2ec34-191">Support</span></span>

<span data-ttu-id="2ec34-192">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz hello Azure uzmanlarıyla hello [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="2ec34-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="2ec34-193">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="2ec34-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="2ec34-194">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="2ec34-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="2ec34-195">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="2ec34-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
