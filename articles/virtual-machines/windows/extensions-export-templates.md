---
title: "VM uzantıları içeren Azure kaynak gruplarını dışa aktarma | Microsoft Docs"
description: "Sanal makine uzantıları dahil Resource Manager şablonları dışarı aktarın."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cc3c705f1c9123de75ced016a5b39eb1a86b0f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="84c88-103">VM uzantıları içeren kaynak grupları dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="84c88-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="84c88-104">Azure kaynak gruplarını daha sonra yeniden dağıtılması yeni bir Resource Manager şablonuna aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="84c88-105">Dışa aktarma işlemi var olan kaynakların yorumlar ve Resource Manager şablonu dağıtıldığında oluşturan benzer bir kaynak grubunda neden olur.</span><span class="sxs-lookup"><span data-stu-id="84c88-105">The export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="84c88-106">Sanal makine uzantıları içeren bir kaynak grubu karşı kaynak grubunu dışarı aktarma seçeneğini kullanırken, birden çok öğe uzantısı uyumluluk gibi ele alınması gereken ve ayarların korumalı.</span><span class="sxs-lookup"><span data-stu-id="84c88-106">When using the Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need to be considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="84c88-107">Bu belge ayrıntıları listesi dahil olmak üzere sanal makine uzantıları ile ilgili kaynak grubunu dışarı aktarma işleminin nasıl çalıştığı uzantıları desteklenir ve işleme ayrıntıları verilerin güvenli.</span><span class="sxs-lookup"><span data-stu-id="84c88-107">This document details how the Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="84c88-108">Desteklenen sanal makine uzantıları</span><span class="sxs-lookup"><span data-stu-id="84c88-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="84c88-109">Çok sayıda sanal makine uzantıları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="84c88-110">Tüm uzantıları "Otomasyon betiğini" özelliğini kullanarak bir Resource Manager şablonu aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-110">Not all extensions can be exported into a Resource Manager template using the “Automation Script” feature.</span></span> <span data-ttu-id="84c88-111">Bir sanal makine uzantısı desteklenmiyorsa, dışarı aktarılan şablona el ile yerleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="84c88-111">If a virtual machine extension is not supported, it needs to be manually placed back into the exported template.</span></span>

<span data-ttu-id="84c88-112">Aşağıdaki uzantılar Otomasyon betik özelliğiyle aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-112">The following extensions can be exported with the automation script feature.</span></span>

| <span data-ttu-id="84c88-113">Dahili numara</span><span class="sxs-lookup"><span data-stu-id="84c88-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="84c88-114">Acronis yedekleme</span><span class="sxs-lookup"><span data-stu-id="84c88-114">Acronis Backup</span></span> | <span data-ttu-id="84c88-115">Datadog Windows Aracısı</span><span class="sxs-lookup"><span data-stu-id="84c88-115">Datadog Windows Agent</span></span> | <span data-ttu-id="84c88-116">Linux için düzeltme eki uygulama işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="84c88-116">OS Patching For Linux</span></span> | <span data-ttu-id="84c88-117">VM anlık görüntü Linux</span><span class="sxs-lookup"><span data-stu-id="84c88-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="84c88-118">Acronis yedekleme Linux</span><span class="sxs-lookup"><span data-stu-id="84c88-118">Acronis Backup Linux</span></span> | <span data-ttu-id="84c88-119">Docker uzantısı</span><span class="sxs-lookup"><span data-stu-id="84c88-119">Docker Extension</span></span> | <span data-ttu-id="84c88-120">Puppet aracı</span><span class="sxs-lookup"><span data-stu-id="84c88-120">Puppet Agent</span></span> |
| <span data-ttu-id="84c88-121">BG bilgisi</span><span class="sxs-lookup"><span data-stu-id="84c88-121">Bg Info</span></span> | <span data-ttu-id="84c88-122">DSC Uzantısı</span><span class="sxs-lookup"><span data-stu-id="84c88-122">DSC Extension</span></span> | <span data-ttu-id="84c88-123">Site 7 x 24 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="84c88-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="84c88-124">BMC CTM Aracısı Linux</span><span class="sxs-lookup"><span data-stu-id="84c88-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="84c88-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="84c88-125">Dynatrace Linux</span></span> | <span data-ttu-id="84c88-126">Site 7 x 24 Linux sunucusu</span><span class="sxs-lookup"><span data-stu-id="84c88-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="84c88-127">BMC CTM Aracısı Windows</span><span class="sxs-lookup"><span data-stu-id="84c88-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="84c88-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="84c88-128">Dynatrace Windows</span></span> | <span data-ttu-id="84c88-129">Site 7 x 24 Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="84c88-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="84c88-130">Chef istemci</span><span class="sxs-lookup"><span data-stu-id="84c88-130">Chef Client</span></span> | <span data-ttu-id="84c88-131">HPE güvenlik uygulama Defender</span><span class="sxs-lookup"><span data-stu-id="84c88-131">HPE Security Application Defender</span></span> | <span data-ttu-id="84c88-132">Eğilim mikro DSA</span><span class="sxs-lookup"><span data-stu-id="84c88-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="84c88-133">Özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="84c88-133">Custom Script</span></span> | <span data-ttu-id="84c88-134">Iaas kötü amaçlı yazılımdan koruma</span><span class="sxs-lookup"><span data-stu-id="84c88-134">IaaS Antimalware</span></span> | <span data-ttu-id="84c88-135">Eğilim mikro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="84c88-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="84c88-136">Özel Betik Uzantısı</span><span class="sxs-lookup"><span data-stu-id="84c88-136">Custom Script Extension</span></span> | <span data-ttu-id="84c88-137">Iaas tanılama</span><span class="sxs-lookup"><span data-stu-id="84c88-137">IaaS Diagnostics</span></span> | <span data-ttu-id="84c88-138">Linux VM erişim</span><span class="sxs-lookup"><span data-stu-id="84c88-138">VM Access For Linux</span></span> |
| <span data-ttu-id="84c88-139">Linux için özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="84c88-139">Custom Script for Linux</span></span> | <span data-ttu-id="84c88-140">Linux Chef istemci</span><span class="sxs-lookup"><span data-stu-id="84c88-140">Linux Chef Client</span></span> | <span data-ttu-id="84c88-141">Linux VM erişim</span><span class="sxs-lookup"><span data-stu-id="84c88-141">VM Access For Linux</span></span> |
| <span data-ttu-id="84c88-142">Datadog Linux Aracısı</span><span class="sxs-lookup"><span data-stu-id="84c88-142">Datadog Linux Agent</span></span> | <span data-ttu-id="84c88-143">Linux tanılama</span><span class="sxs-lookup"><span data-stu-id="84c88-143">Linux Diagnostic</span></span> | <span data-ttu-id="84c88-144">VM anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="84c88-144">VM Snapshot</span></span> |

## <a name="export-the-resource-group"></a><span data-ttu-id="84c88-145">Kaynak grubunu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="84c88-145">Export the Resource Group</span></span>

<span data-ttu-id="84c88-146">Bir kaynak grubu içinde yeniden kullanılabilir bir şablonu dışarı aktarmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="84c88-146">To export a Resource Group into a reusable template, complete the following steps:</span></span>

1. <span data-ttu-id="84c88-147">Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="84c88-147">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="84c88-148">Hub menüsünde, kaynak grupları'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="84c88-148">On the Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="84c88-149">Hedef kaynak grubu listeden seçin</span><span class="sxs-lookup"><span data-stu-id="84c88-149">Select the target resource group from the list</span></span>
4. <span data-ttu-id="84c88-150">Kaynak grubu dikey penceresinde Otomasyon betiğini tıklayın</span><span class="sxs-lookup"><span data-stu-id="84c88-150">In the Resource Group blade, click Automation Script</span></span>

![Şablonu dışarı aktarma](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="84c88-152">Azure Resource Manager otomasyonlara betik Resource Manager şablonu, bir parametre dosyası ve PowerShell ve Azure CLI gibi birkaç örnek dağıtım betikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84c88-152">The Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="84c88-153">Bu aşamada, dışarı aktarılan şablon, yeni bir şablon olarak Şablon Kitaplığı'na eklenen veya Dağıt düğmesi kullanılarak imzalanmasını karşıdan yükleme düğmesini kullanarak indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-153">At this point, the exported template can be downloaded using the download button, added as a new template to the template library, or redeployed using the deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="84c88-154">Korumalı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="84c88-154">Configure protected settings</span></span>

<span data-ttu-id="84c88-155">Kimlik bilgileri ve yapılandırma dizeleri gibi hassas verileri şifreler korumalı ayarlarını yapılandırma, çok sayıda Azure sanal makine uzantıları içerir.</span><span class="sxs-lookup"><span data-stu-id="84c88-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="84c88-156">Korumalı ayarları ile Otomasyon betiğini dışarı aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="84c88-156">Protected settings are not exported with the automation script.</span></span> <span data-ttu-id="84c88-157">Gerekirse, korumalı ayarlarını yeniden gerekiyorsa dışa aktarılan içine şablonlu.</span><span class="sxs-lookup"><span data-stu-id="84c88-157">If necessary, protected settings need to be reinserted into the exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="84c88-158">1. adım - Kaldır şablon parametresi</span><span class="sxs-lookup"><span data-stu-id="84c88-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="84c88-159">Kaynak grubunu dışarı aktardığınızda tek şablon parametresi dışarı aktarılan korumalı ayarlar için bir değer sağlamak için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="84c88-159">When the Resource Group is exported, a single template parameter is created to provide a value to the exported protected settings.</span></span> <span data-ttu-id="84c88-160">Bu parametre kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-160">This parameter can be removed.</span></span> <span data-ttu-id="84c88-161">Parametre kaldırmak için parametre listesine bakın ve bu JSON örneğe benzer parametre silin.</span><span class="sxs-lookup"><span data-stu-id="84c88-161">To remove the parameter, look through the parameter list and delete the parameter that looks similar to this JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="84c88-162">2. adım - Get ayarları özellikleri korumalı</span><span class="sxs-lookup"><span data-stu-id="84c88-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="84c88-163">Her korunan ayarın gerekli özellikler kümesi olduğundan, bu özelliklerin listesini gerekir toplanması.</span><span class="sxs-lookup"><span data-stu-id="84c88-163">Because each protected setting has a set of required properties, a list of these properties need to be gathered.</span></span> <span data-ttu-id="84c88-164">Korumalı ayarlarını yapılandırma, her bir parametreyi bulunabilir [github'da Azure Resource Manager şema](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="84c88-164">Each parameter of the protected settings configuration can be found in the [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="84c88-165">Bu şema, bu belgenin genel bakış bölümünde listelenen uzantıları için parametre kümeleri yalnızca içerir.</span><span class="sxs-lookup"><span data-stu-id="84c88-165">This schema only includes the parameter sets for the extensions listed in the overview section of this document.</span></span> 

<span data-ttu-id="84c88-166">Gelen istenen uzantısı, bu örnek için şema deposu içinde arama `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="84c88-166">From within the schema repository, search for the desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="84c88-167">Bir kez uzantıları `protectedSettings` nesne bulunduğu açıldı, her bir parametreyi not edin.</span><span class="sxs-lookup"><span data-stu-id="84c88-167">Once the extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="84c88-168">Örneğinde `IaasDiagnostic` uzantısı, Parametreler gerektiren `storageAccountName`, `storageAccountKey`, ve `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="84c88-168">In the example of the `IaasDiagnostic` extension, the require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-the-protected-configuration"></a><span data-ttu-id="84c88-169">3. adım - korumalı yapılandırmayı yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="84c88-169">Step 3 - Re-create the protected configuration</span></span>

<span data-ttu-id="84c88-170">Dışarı aktarılan şablona arama `protectedSettings` ve dışarı aktarılan korumalı ayar nesnesini gerekli uzantısı parametreleri ve her biri için bir değer içeren yeni bir tane ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="84c88-170">On the exported template, search for `protectedSettings` and replace the exported protected setting object with a new one that includes the required extension parameters and a value for each one.</span></span>

<span data-ttu-id="84c88-171">Örneğinde `IaasDiagnostic` uzantısı, yeni korumalı ayarını yapılandırma uygulamamız görünecektir aşağıdaki örnekteki gibi:</span><span class="sxs-lookup"><span data-stu-id="84c88-171">In the example of the `IaasDiagnostic` extension, the new protected setting configuration would look like the following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="84c88-172">Son uzantısı kaynak aşağıdaki JSON örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="84c88-172">The final extension resource looks similar to the following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="84c88-173">Şablon parametreleri özellik değerlerini sağlamak için kullanıyorsanız, bunlar oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84c88-173">If using template parameters to provide property values, these need to be created.</span></span> <span data-ttu-id="84c88-174">Şablon parametreleri değerlerini ayarlama korumalı oluştururken kullandığınızdan emin olun `SecureString` parametre türü hassas değerleri güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-174">When creating template parameters for protected setting values, make sure to use the `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="84c88-175">Parametreleri kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="84c88-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="84c88-176">Örneğinde `IaasDiagnostic` uzantısı, aşağıdaki parametreleri Resource Manager şablonu parametreleri bölümünde oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="84c88-176">In the example of the `IaasDiagnostic` extension, the following parameters would be created in the parameters section of the Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="84c88-177">Bu noktada, şablonu herhangi bir şablon dağıtım yöntemini kullanılarak dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="84c88-177">At this point, the template can be deployed using any template deployment method.</span></span>
