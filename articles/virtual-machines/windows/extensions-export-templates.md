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
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>VM uzantıları içeren kaynak grupları dışarı aktarma

Azure kaynak gruplarını daha sonra yeniden dağıtılması yeni bir Resource Manager şablonuna aktarılabilir. Hello verme işlemi var olan kaynakların yorumlar ve Resource Manager şablonu dağıtıldığında oluşturan benzer bir kaynak grubunda neden olur. Sanal makine uzantıları içeren bir kaynak grubu karşı Hello kaynak grubunu dışarı aktarma seçeneğini kullanırken, çeşitli öğeleri gerek toobe uzantısı uyumluluk gibi kabul ve ayarların korumalı.

Uzantıları listesi dahil olmak üzere sanal makine uzantıları ile ilgili hello kaynak grubunu dışarı aktarma işlemini nasıl çalıştığını bu belge ayrıntıları desteklenir ve işleme ayrıntıları verilerin güvenliği.

## <a name="supported-virtual-machine-extensions"></a>Desteklenen sanal makine uzantıları

Çok sayıda sanal makine uzantıları kullanılabilir. Tüm uzantıları hello "Otomasyon betiğini" özelliğini kullanarak bir Resource Manager şablonu aktarılabilir. Bir sanal makine uzantısı desteklenmiyorsa hello dışarı aktarılan şablona el ile yerleştirilen toobe gerekir.

Merhaba aşağıdaki uzantılar hello Otomasyon betik özelliğiyle aktarılabilir.

| Dahili numara ||||
|---|---|---|---|
| Acronis yedekleme | Datadog Windows Aracısı | Linux için düzeltme eki uygulama işletim sistemi | VM anlık görüntü Linux
| Acronis yedekleme Linux | Docker uzantısı | Puppet aracı |
| BG bilgisi | DSC Uzantısı | Site 7 x 24 Apm Insight |
| BMC CTM Aracısı Linux | Dynatrace Linux | Site 7 x 24 Linux sunucusu |
| BMC CTM Aracısı Windows | Dynatrace Windows | Site 7 x 24 Windows sunucusu |
| Chef istemci | HPE güvenlik uygulama Defender | Eğilim mikro DSA |
| Özel bir komut dosyası | Iaas kötü amaçlı yazılımdan koruma | Eğilim mikro DSA Linux |
| Özel Betik Uzantısı | Iaas tanılama | Linux VM erişim |
| Linux için özel bir komut dosyası | Linux Chef istemci | Linux VM erişim |
| Datadog Linux Aracısı | Linux tanılama | VM anlık görüntü |

## <a name="export-hello-resource-group"></a>Merhaba kaynak grubunu dışarı aktarma

bir kaynak grubuna yeniden kullanılabilir bir şablonu, aşağıdaki adımları tam hello tooexport:

1. Toohello Azure portalında oturum açın
2. Hello Hub menüsünde, kaynak grupları'nı tıklatın.
3. Merhaba listeden Hello hedef kaynak grubu seçin
4. Otomasyon betiğini Hello kaynak grubu dikey penceresinde tıklayın

![Şablonu dışarı aktarma](./media/extensions-export-templates/template-export.png)

Resource Manager şablonu, bir parametre dosyası ve PowerShell ve Azure CLI gibi birkaç örnek dağıtım betikleri Hello Azure Resource Manager otomasyonlara komut dosyası oluşturur. Bu noktada, hello dışarı aktarılan şablonu yeni bir şablon toohello Şablon kitaplığı eklendiğinde veya hello kullanarak imzalanmasını hello İndir düğmesini kullanarak indirilebilir Dağıt düğmesi.

## <a name="configure-protected-settings"></a>Korumalı ayarlarını yapılandırma

Kimlik bilgileri ve yapılandırma dizeleri gibi hassas verileri şifreler korumalı ayarlarını yapılandırma, çok sayıda Azure sanal makine uzantıları içerir. Korumalı ayarları ile Merhaba Otomasyon betiğini dışarı aktarılmaz. Gerekirse, korumalı ayarlarını hello yeniden toobe gerekiyorsa şablonlu verildi.

### <a name="step-1---remove-template-parameter"></a>1. adım - Kaldır şablon parametresi

Kaynak grubu verilir, hello tek şablon parametresi tooprovide oluşturulduğunda değeri toohello korumalı ayarları dışarı. Bu parametre kaldırılabilir. tooremove hello parametresi hello parametre listesine bakın ve benzer toothis JSON örnek görünür hello parametre silin.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>2. adım - Get ayarları özellikleri korumalı

Her korunan ayarın gerekli özellikler kümesi olduğundan, bu özelliklerin listesini toplanan toobe gerekir. Merhaba korumalı ayarlarını yapılandırma, her bir parametreyi hello bulunabilir [github'da Azure Resource Manager şema](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Bu şemayı hello genel bakış bölümünde bu belgenin listelenen hello uzantıları için hello parametre kümeleri yalnızca içerir. 

Öğesinden Bu örnek için istenen hello uzantısı hello şema deposu içinde arama `IaaSDiagnostics`. Bir kez Uzantıları'nı hello `protectedSettings` nesne bulunduğu açıldı, her bir parametreyi not edin. Merhaba hello örneğinde `IaasDiagnostic` uzantısı hello gerektiren parametreleri `storageAccountName`, `storageAccountKey`, ve `storageAccountEndPoint`.

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

### <a name="step-3---re-create-hello-protected-configuration"></a>3. adım - korumalı hello yapılandırmasını yeniden oluşturma

Üzerinde Merhaba dışarı aktarılan şablon, arama `protectedSettings` ve gerekli hello uzantısı parametreleri ve her biri için bir değer içeren yeni bir hello dışarı aktarılan korumalı ayar nesnesini değiştirin.

Merhaba hello örneğinde `IaasDiagnostic` uzantısı hello yeni korumalı ayarını yapılandırma uygulamamız görünecektir aşağıdaki örneğine hello gibi:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

Merhaba son uzantısı kaynak aşağıdaki JSON örneğine benzer toohello arar:

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

Şablon parametreleri tooprovide özellik değerlerini kullanarak, bu oluşturulan toobe gerekir. Şablon parametreleri değerlerini ayarlama korumalı oluştururken, emin toouse hello edin `SecureString` parametre türü hassas değerleri güvenli hale getirilir. Parametreleri kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).

Merhaba hello örneğinde `IaasDiagnostic` uzantısı şu parametreler hello hello Parametreler bölümünde hello Resource Manager şablonu oluşturulacaktır.

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

Bu noktada, hello şablonu herhangi bir şablon dağıtım yöntemini kullanılarak dağıtılabilir.
