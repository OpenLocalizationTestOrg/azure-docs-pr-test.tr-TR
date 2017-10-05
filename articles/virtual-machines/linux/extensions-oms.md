---
title: "Linux için OMS Azure sanal makine uzantısı | Microsoft Docs"
description: "OMS Aracısı'nı bir sanal makine uzantısını kullanarak Linux sanal makine dağıtın."
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
ms.openlocfilehash: 138fc8c98ea6f409b28407b20851c96ecc618b09
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="b3756-103">Linux için OMS sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="b3756-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="b3756-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b3756-104">Overview</span></span>

<span data-ttu-id="b3756-105">Operations Management Suite (OMS) bulut izleme, uyarma ve uyarı düzeltme özellikleri sağlar ve şirket içi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="b3756-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="b3756-106">Linux için OMS Aracısı sanal makine uzantısı yayımlanan ve Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b3756-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="b3756-107">Uzantı Azure sanal makinelerde OMS Aracısı'nı yükler ve sanal makineleri olan bir OMS çalışma kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b3756-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="b3756-108">Bu belge, desteklenen platformlar, yapılandırmaları ve Linux için OMS sanal makine uzantısı için dağıtım seçeneklerini ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="b3756-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3756-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b3756-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="b3756-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="b3756-110">Operating system</span></span>

<span data-ttu-id="b3756-111">OMS Aracısı uzantısı bu Linux dağıtımları karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3756-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="b3756-112">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="b3756-112">Distribution</span></span> | <span data-ttu-id="b3756-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b3756-113">Version</span></span> |
|---|---|
| <span data-ttu-id="b3756-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="b3756-114">CentOS Linux</span></span> | <span data-ttu-id="b3756-115">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="b3756-115">5, 6, and 7</span></span> |
| <span data-ttu-id="b3756-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="b3756-116">Oracle Linux</span></span> | <span data-ttu-id="b3756-117">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="b3756-117">5, 6, and 7</span></span> |
| <span data-ttu-id="b3756-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="b3756-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="b3756-119">5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="b3756-119">5, 6 and 7</span></span> |
| <span data-ttu-id="b3756-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="b3756-120">Debian GNU/Linux</span></span> | <span data-ttu-id="b3756-121">6, 7 ve 8</span><span class="sxs-lookup"><span data-stu-id="b3756-121">6, 7, and 8</span></span> |
| <span data-ttu-id="b3756-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b3756-122">Ubuntu</span></span> | <span data-ttu-id="b3756-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b3756-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="b3756-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="b3756-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="b3756-125">11 ve 12</span><span class="sxs-lookup"><span data-stu-id="b3756-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="b3756-126">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="b3756-126">Internet connectivity</span></span>

<span data-ttu-id="b3756-127">Linux için OMS aracısının uzantısı hedef sanal makine internet'e bağlı olduğunu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b3756-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="b3756-128">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="b3756-128">Extension schema</span></span>

<span data-ttu-id="b3756-129">Aşağıdaki JSON şeması OMS Aracısı uzantısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3756-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="b3756-130">Uzantı çalışma alanı kimliği ve hedef OMS çalışma alanından bir çalışma alanı anahtarı gerektirir; Bu değerleri OMS Portalı'nda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-130">The extension requires the workspace ID and workspace key from the target OMS workspace; these values can be found in the OMS portal.</span></span> <span data-ttu-id="b3756-131">Çalışma alanı anahtarı hassas verileri olarak değerlendirilmesi için bir korumalı ayarı yapılandırmasında depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3756-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="b3756-132">Azure VM uzantısının korumalı ayarı veri şifrelenir ve yalnızca hedef sanal makineye şifresi.</span><span class="sxs-lookup"><span data-stu-id="b3756-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="b3756-133">Unutmayın **Workspaceıd** ve **workspaceKey** büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="b3756-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="b3756-134">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="b3756-134">Property values</span></span>

| <span data-ttu-id="b3756-135">Ad</span><span class="sxs-lookup"><span data-stu-id="b3756-135">Name</span></span> | <span data-ttu-id="b3756-136">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="b3756-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="b3756-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b3756-137">apiVersion</span></span> | <span data-ttu-id="b3756-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="b3756-138">2015-06-15</span></span> |
| <span data-ttu-id="b3756-139">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="b3756-139">publisher</span></span> | <span data-ttu-id="b3756-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="b3756-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="b3756-141">type</span><span class="sxs-lookup"><span data-stu-id="b3756-141">type</span></span> | <span data-ttu-id="b3756-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="b3756-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="b3756-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="b3756-143">typeHandlerVersion</span></span> | <span data-ttu-id="b3756-144">1.4</span><span class="sxs-lookup"><span data-stu-id="b3756-144">1.4</span></span> |
| <span data-ttu-id="b3756-145">Workspaceıd (örneğin)</span><span class="sxs-lookup"><span data-stu-id="b3756-145">workspaceId (e.g)</span></span> | <span data-ttu-id="b3756-146">6f680a37-00c6-41C7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="b3756-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="b3756-147">workspaceKey (örneğin)</span><span class="sxs-lookup"><span data-stu-id="b3756-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="b3756-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ ==</span><span class="sxs-lookup"><span data-stu-id="b3756-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="b3756-149">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="b3756-149">Template deployment</span></span>

<span data-ttu-id="b3756-150">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="b3756-151">Şablonları, bir veya daha fazla OMS ekleme gibi dağıtım yapılandırma sonrası gerektiren sanal makineler dağıtırken idealdir.</span><span class="sxs-lookup"><span data-stu-id="b3756-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="b3756-152">OMS Aracısı VM uzantısı içeren bir örnek Resource Manager şablonunu bulunabilir [Azure hızlı başlangıç Galerisi](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="b3756-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="b3756-153">Sanal makine uzantısı JSON yapılandırması içinde sanal makine kaynağı iç içe geçmiş veya kök veya Resource Manager JSON şablonu en üst düzeyinde yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-153">The JSON configuration for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="b3756-154">JSON yapılandırma yerleşimini kaynak adı ve türü değeri etkiler.</span><span class="sxs-lookup"><span data-stu-id="b3756-154">The placement of the JSON configuration affects the value of the resource name and type.</span></span> <span data-ttu-id="b3756-155">Daha fazla bilgi için bkz: [Ayarla alt kaynakları için ad ve tür](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b3756-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="b3756-156">Aşağıdaki örnek, OMS uzantısı içinde sanal makine kaynağı iç içe geçmiş varsayar.</span><span class="sxs-lookup"><span data-stu-id="b3756-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="b3756-157">Uzantı kaynak iç içe geçirme sırasında JSON yerleştirilir `"resources": []` sanal makinenin nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b3756-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

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

<span data-ttu-id="b3756-158">JSON uzantısı şablon kökünde yerleştirirken, kaynak adı üst sanal makine için referans içeriyor ve iç içe geçmiş yapılandırma türü yansıtır.</span><span class="sxs-lookup"><span data-stu-id="b3756-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

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

## <a name="azure-cli-deployment"></a><span data-ttu-id="b3756-159">Azure CLI dağıtım</span><span class="sxs-lookup"><span data-stu-id="b3756-159">Azure CLI deployment</span></span>

<span data-ttu-id="b3756-160">Azure CLI OMS Aracısı VM uzantısı olan bir sanal makineyi dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="b3756-161">OMS anahtarı ve OMS kimliği bu OMS çalışma alanınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b3756-161">Replace the OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="b3756-162">Sorun giderme ve Destek</span><span class="sxs-lookup"><span data-stu-id="b3756-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="b3756-163">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b3756-163">Troubleshoot</span></span>

<span data-ttu-id="b3756-164">Veri uzantısı dağıtımları durumuyla ilgili Azure portalından ve Azure CLI kullanarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-164">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="b3756-165">İçin belirli bir VM uzantıları dağıtım durumunu görmek için Azure CLI kullanarak şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b3756-165">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="b3756-166">Uzantı yürütme çıktısını aşağıdaki dosyasına kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="b3756-166">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="b3756-167">Hata kodları ve anlamları</span><span class="sxs-lookup"><span data-stu-id="b3756-167">Error codes and their meanings</span></span>

| <span data-ttu-id="b3756-168">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="b3756-168">Error Code</span></span> | <span data-ttu-id="b3756-169">Anlamı</span><span class="sxs-lookup"><span data-stu-id="b3756-169">Meaning</span></span> | <span data-ttu-id="b3756-170">Olası eylemi</span><span class="sxs-lookup"><span data-stu-id="b3756-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="b3756-171">10</span><span class="sxs-lookup"><span data-stu-id="b3756-171">10</span></span> | <span data-ttu-id="b3756-172">VM zaten bir OMS çalışma alanına bağlı</span><span class="sxs-lookup"><span data-stu-id="b3756-172">VM is already connected to an OMS workspace</span></span> | <span data-ttu-id="b3756-173">VM uzantısı şemasında belirtilen çalışma alanına bağlanmak için stopOnMultipleConnections genel ayarları'nda false olarak ayarlayın veya bu özelliği kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b3756-173">To connect the VM to the workspace specified in the extension schema, set stopOnMultipleConnections to false in public settings or remove this property.</span></span> <span data-ttu-id="b3756-174">Bu VM için bağlı her çalışma alanı için bir kez fatura.</span><span class="sxs-lookup"><span data-stu-id="b3756-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="b3756-175">11</span><span class="sxs-lookup"><span data-stu-id="b3756-175">11</span></span> | <span data-ttu-id="b3756-176">Uzantı için sağlanan geçersiz yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3756-176">Invalid config provided to the extension</span></span> | <span data-ttu-id="b3756-177">Dağıtım için gereken tüm özellik değerlerini ayarlamak için Yukarıdaki örneklerde izleyin.</span><span class="sxs-lookup"><span data-stu-id="b3756-177">Follow the preceding examples to set all property values necessary for deployment.</span></span> |
| <span data-ttu-id="b3756-178">12</span><span class="sxs-lookup"><span data-stu-id="b3756-178">12</span></span> | <span data-ttu-id="b3756-179">Dpkg Paket Yöneticisi kilitli</span><span class="sxs-lookup"><span data-stu-id="b3756-179">The dpkg package manager is locked</span></span> | <span data-ttu-id="b3756-180">Tamamlandı ve yeniden deneyin tüm dpkg güncelleştirme makine üzerindeki işlemleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="b3756-180">Make sure all dpkg update operations on the machine have finished and retry.</span></span> |
| <span data-ttu-id="b3756-181">20</span><span class="sxs-lookup"><span data-stu-id="b3756-181">20</span></span> | <span data-ttu-id="b3756-182">Erken adlı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b3756-182">Enable called prematurely</span></span> | <span data-ttu-id="b3756-183">[Azure Linux Aracısı güncelleştirme](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) sürüme en son kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b3756-183">[Update the Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to the latest available version.</span></span> |
| <span data-ttu-id="b3756-184">51</span><span class="sxs-lookup"><span data-stu-id="b3756-184">51</span></span> | <span data-ttu-id="b3756-185">Bu uzantı sanal makinenin işletim sistemi üzerinde desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="b3756-185">This extension is not supported on the VM's operation system</span></span> | |
| <span data-ttu-id="b3756-186">55</span><span class="sxs-lookup"><span data-stu-id="b3756-186">55</span></span> | <span data-ttu-id="b3756-187">Microsoft Operations Management Suite hizmetine bağlanamıyor</span><span class="sxs-lookup"><span data-stu-id="b3756-187">Cannot connect to the Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="b3756-188">Sistem ya da Internet erişimi veya geçerli bir HTTP proxy sağlanmış sahip denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b3756-188">Check that the system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="b3756-189">Ayrıca, çalışma alanı kimliği doğruluğunu denetleyin</span><span class="sxs-lookup"><span data-stu-id="b3756-189">Additionally, check the correctness of the workspace ID.</span></span> |

<span data-ttu-id="b3756-190">Ek sorun giderme bilgileri bulunabilir [Linux için OMS Aracısı sorun giderme kılavuzu](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="b3756-190">Additional troubleshooting information can be found on the [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="b3756-191">Destek</span><span class="sxs-lookup"><span data-stu-id="b3756-191">Support</span></span>

<span data-ttu-id="b3756-192">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b3756-192">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="b3756-193">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="b3756-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b3756-194">Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="b3756-194">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="b3756-195">Azure desteği hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="b3756-195">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
