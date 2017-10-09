---
title: "VM uzantıları içeren Azure kaynak gruplarını aaaExporting | Microsoft Docs"
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
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="7fb71-103">VM uzantıları içeren kaynak grupları dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7fb71-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="7fb71-104">Azure kaynak gruplarını daha sonra yeniden dağıtılması yeni bir Resource Manager şablonuna aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="7fb71-105">Hello verme işlemi var olan kaynakların yorumlar ve Resource Manager şablonu dağıtıldığında oluşturan benzer bir kaynak grubunda neden olur.</span><span class="sxs-lookup"><span data-stu-id="7fb71-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="7fb71-106">Sanal makine uzantıları içeren bir kaynak grubu karşı Hello kaynak grubunu dışarı aktarma seçeneğini kullanırken, çeşitli öğeleri gerek toobe uzantısı uyumluluk gibi kabul ve ayarların korumalı.</span><span class="sxs-lookup"><span data-stu-id="7fb71-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="7fb71-107">Uzantıları listesi dahil olmak üzere sanal makine uzantıları ile ilgili hello kaynak grubunu dışarı aktarma işlemini nasıl çalıştığını bu belge ayrıntıları desteklenir ve işleme ayrıntıları verilerin güvenliği.</span><span class="sxs-lookup"><span data-stu-id="7fb71-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="7fb71-108">Desteklenen sanal makine uzantıları</span><span class="sxs-lookup"><span data-stu-id="7fb71-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="7fb71-109">Çok sayıda sanal makine uzantıları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="7fb71-110">Tüm uzantıları hello "Otomasyon betiğini" özelliğini kullanarak bir Resource Manager şablonu aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="7fb71-111">Bir sanal makine uzantısı desteklenmiyorsa hello dışarı aktarılan şablona el ile yerleştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="7fb71-112">Merhaba aşağıdaki uzantılar hello Otomasyon betik özelliğiyle aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="7fb71-113">Dahili numara</span><span class="sxs-lookup"><span data-stu-id="7fb71-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="7fb71-114">Acronis yedekleme</span><span class="sxs-lookup"><span data-stu-id="7fb71-114">Acronis Backup</span></span> | <span data-ttu-id="7fb71-115">Datadog Windows Aracısı</span><span class="sxs-lookup"><span data-stu-id="7fb71-115">Datadog Windows Agent</span></span> | <span data-ttu-id="7fb71-116">Linux için düzeltme eki uygulama işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="7fb71-116">OS Patching For Linux</span></span> | <span data-ttu-id="7fb71-117">VM anlık görüntü Linux</span><span class="sxs-lookup"><span data-stu-id="7fb71-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="7fb71-118">Acronis yedekleme Linux</span><span class="sxs-lookup"><span data-stu-id="7fb71-118">Acronis Backup Linux</span></span> | <span data-ttu-id="7fb71-119">Docker uzantısı</span><span class="sxs-lookup"><span data-stu-id="7fb71-119">Docker Extension</span></span> | <span data-ttu-id="7fb71-120">Puppet aracı</span><span class="sxs-lookup"><span data-stu-id="7fb71-120">Puppet Agent</span></span> |
| <span data-ttu-id="7fb71-121">BG bilgisi</span><span class="sxs-lookup"><span data-stu-id="7fb71-121">Bg Info</span></span> | <span data-ttu-id="7fb71-122">DSC Uzantısı</span><span class="sxs-lookup"><span data-stu-id="7fb71-122">DSC Extension</span></span> | <span data-ttu-id="7fb71-123">Site 7 x 24 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="7fb71-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="7fb71-124">BMC CTM Aracısı Linux</span><span class="sxs-lookup"><span data-stu-id="7fb71-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="7fb71-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="7fb71-125">Dynatrace Linux</span></span> | <span data-ttu-id="7fb71-126">Site 7 x 24 Linux sunucusu</span><span class="sxs-lookup"><span data-stu-id="7fb71-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="7fb71-127">BMC CTM Aracısı Windows</span><span class="sxs-lookup"><span data-stu-id="7fb71-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="7fb71-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="7fb71-128">Dynatrace Windows</span></span> | <span data-ttu-id="7fb71-129">Site 7 x 24 Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="7fb71-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="7fb71-130">Chef istemci</span><span class="sxs-lookup"><span data-stu-id="7fb71-130">Chef Client</span></span> | <span data-ttu-id="7fb71-131">HPE güvenlik uygulama Defender</span><span class="sxs-lookup"><span data-stu-id="7fb71-131">HPE Security Application Defender</span></span> | <span data-ttu-id="7fb71-132">Eğilim mikro DSA</span><span class="sxs-lookup"><span data-stu-id="7fb71-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="7fb71-133">Özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7fb71-133">Custom Script</span></span> | <span data-ttu-id="7fb71-134">Iaas kötü amaçlı yazılımdan koruma</span><span class="sxs-lookup"><span data-stu-id="7fb71-134">IaaS Antimalware</span></span> | <span data-ttu-id="7fb71-135">Eğilim mikro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="7fb71-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="7fb71-136">Özel Betik Uzantısı</span><span class="sxs-lookup"><span data-stu-id="7fb71-136">Custom Script Extension</span></span> | <span data-ttu-id="7fb71-137">Iaas tanılama</span><span class="sxs-lookup"><span data-stu-id="7fb71-137">IaaS Diagnostics</span></span> | <span data-ttu-id="7fb71-138">Linux VM erişim</span><span class="sxs-lookup"><span data-stu-id="7fb71-138">VM Access For Linux</span></span> |
| <span data-ttu-id="7fb71-139">Linux için özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7fb71-139">Custom Script for Linux</span></span> | <span data-ttu-id="7fb71-140">Linux Chef istemci</span><span class="sxs-lookup"><span data-stu-id="7fb71-140">Linux Chef Client</span></span> | <span data-ttu-id="7fb71-141">Linux VM erişim</span><span class="sxs-lookup"><span data-stu-id="7fb71-141">VM Access For Linux</span></span> |
| <span data-ttu-id="7fb71-142">Datadog Linux Aracısı</span><span class="sxs-lookup"><span data-stu-id="7fb71-142">Datadog Linux Agent</span></span> | <span data-ttu-id="7fb71-143">Linux tanılama</span><span class="sxs-lookup"><span data-stu-id="7fb71-143">Linux Diagnostic</span></span> | <span data-ttu-id="7fb71-144">VM anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="7fb71-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="7fb71-145">Merhaba kaynak grubunu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7fb71-145">Export hello Resource Group</span></span>

<span data-ttu-id="7fb71-146">bir kaynak grubuna yeniden kullanılabilir bir şablonu, aşağıdaki adımları tam hello tooexport:</span><span class="sxs-lookup"><span data-stu-id="7fb71-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="7fb71-147">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="7fb71-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="7fb71-148">Hello Hub menüsünde, kaynak grupları'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7fb71-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="7fb71-149">Merhaba listeden Hello hedef kaynak grubu seçin</span><span class="sxs-lookup"><span data-stu-id="7fb71-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="7fb71-150">Otomasyon betiğini Hello kaynak grubu dikey penceresinde tıklayın</span><span class="sxs-lookup"><span data-stu-id="7fb71-150">In hello Resource Group blade, click Automation Script</span></span>

![Şablonu dışarı aktarma](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="7fb71-152">Resource Manager şablonu, bir parametre dosyası ve PowerShell ve Azure CLI gibi birkaç örnek dağıtım betikleri Hello Azure Resource Manager otomasyonlara komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fb71-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="7fb71-153">Bu noktada, hello dışarı aktarılan şablonu yeni bir şablon toohello Şablon kitaplığı eklendiğinde veya hello kullanarak imzalanmasını hello İndir düğmesini kullanarak indirilebilir Dağıt düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7fb71-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="7fb71-154">Korumalı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7fb71-154">Configure protected settings</span></span>

<span data-ttu-id="7fb71-155">Kimlik bilgileri ve yapılandırma dizeleri gibi hassas verileri şifreler korumalı ayarlarını yapılandırma, çok sayıda Azure sanal makine uzantıları içerir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="7fb71-156">Korumalı ayarları ile Merhaba Otomasyon betiğini dışarı aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="7fb71-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="7fb71-157">Gerekirse, korumalı ayarlarını hello yeniden toobe gerekiyorsa şablonlu verildi.</span><span class="sxs-lookup"><span data-stu-id="7fb71-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="7fb71-158">1. adım - Kaldır şablon parametresi</span><span class="sxs-lookup"><span data-stu-id="7fb71-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="7fb71-159">Kaynak grubu verilir, hello tek şablon parametresi tooprovide oluşturulduğunda değeri toohello korumalı ayarları dışarı.</span><span class="sxs-lookup"><span data-stu-id="7fb71-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="7fb71-160">Bu parametre kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-160">This parameter can be removed.</span></span> <span data-ttu-id="7fb71-161">tooremove hello parametresi hello parametre listesine bakın ve benzer toothis JSON örnek görünür hello parametre silin.</span><span class="sxs-lookup"><span data-stu-id="7fb71-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="7fb71-162">2. adım - Get ayarları özellikleri korumalı</span><span class="sxs-lookup"><span data-stu-id="7fb71-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="7fb71-163">Her korunan ayarın gerekli özellikler kümesi olduğundan, bu özelliklerin listesini toplanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="7fb71-164">Merhaba korumalı ayarlarını yapılandırma, her bir parametreyi hello bulunabilir [github'da Azure Resource Manager şema](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="7fb71-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="7fb71-165">Bu şemayı hello genel bakış bölümünde bu belgenin listelenen hello uzantıları için hello parametre kümeleri yalnızca içerir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="7fb71-166">Öğesinden Bu örnek için istenen hello uzantısı hello şema deposu içinde arama `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="7fb71-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="7fb71-167">Bir kez Uzantıları'nı hello `protectedSettings` nesne bulunduğu açıldı, her bir parametreyi not edin.</span><span class="sxs-lookup"><span data-stu-id="7fb71-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="7fb71-168">Merhaba hello örneğinde `IaasDiagnostic` uzantısı hello gerektiren parametreleri `storageAccountName`, `storageAccountKey`, ve `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="7fb71-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

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

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="7fb71-169">3. adım - korumalı hello yapılandırmasını yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fb71-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="7fb71-170">Üzerinde Merhaba dışarı aktarılan şablon, arama `protectedSettings` ve gerekli hello uzantısı parametreleri ve her biri için bir değer içeren yeni bir hello dışarı aktarılan korumalı ayar nesnesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7fb71-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="7fb71-171">Merhaba hello örneğinde `IaasDiagnostic` uzantısı hello yeni korumalı ayarını yapılandırma uygulamamız görünecektir aşağıdaki örneğine hello gibi:</span><span class="sxs-lookup"><span data-stu-id="7fb71-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="7fb71-172">Merhaba son uzantısı kaynak aşağıdaki JSON örneğine benzer toohello arar:</span><span class="sxs-lookup"><span data-stu-id="7fb71-172">hello final extension resource looks similar toohello following JSON example:</span></span>

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

<span data-ttu-id="7fb71-173">Şablon parametreleri tooprovide özellik değerlerini kullanarak, bu oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="7fb71-174">Şablon parametreleri değerlerini ayarlama korumalı oluştururken, emin toouse hello edin `SecureString` parametre türü hassas değerleri güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="7fb71-175">Parametreleri kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7fb71-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="7fb71-176">Merhaba hello örneğinde `IaasDiagnostic` uzantısı şu parametreler hello hello Parametreler bölümünde hello Resource Manager şablonu oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7fb71-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

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

<span data-ttu-id="7fb71-177">Bu noktada, hello şablonu herhangi bir şablon dağıtım yöntemini kullanılarak dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fb71-177">At this point, hello template can be deployed using any template deployment method.</span></span>
