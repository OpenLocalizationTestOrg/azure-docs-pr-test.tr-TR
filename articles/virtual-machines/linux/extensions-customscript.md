---
title: "Linux sanal makineleri Azure üzerinde aaaRun özel komut dosyaları | Microsoft Docs"
description: "Merhaba özel betik uzantısının kullanarak Linux VM yapılandırma görevleri otomatikleştirme"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Hello Azure özel betik uzantısı ile Linux sanal makineleri kullanma
Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır. Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi. Komut dosyaları Azure depolama veya diğer erişilebilir Internet konumdan indirilen veya çalışma zamanı toohello uzantısı sağlanan. Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.

Bu belge ayrıntıları nasıl toouse hello gelen özel betik uzantısının Azure CLI ve Azure Resource Manager şablonu ve ayrıca sorun giderme adımları Linux sistemlerde ayrıntılarını hello.

## <a name="extension-configuration"></a>Uzantı yapılandırması
Merhaba özel betik uzantısı yapılandırma komut dosyası konumunu ve hello komutu toobe çalıştırmak gibi belirtir. Bu yapılandırma hello komut satırında veya bir Azure Resource Manager şablonunda belirtilen yapılandırma dosyalarında depolanabilir. Duyarlı veri şifrelenir ve yalnızca hello sanal makine içinde şifresi bir korumalı bir yapılandırma depolanabilir. Merhaba korumalı yapılandırma, bir parola gibi gizli Hello yürütme komutu içerir yararlıdır.

### <a name="public-configuration"></a>Genel yapılandırma
Şema:

**Not** -bu özellik adları büyük/küçük harfe duyarlıdır. Merhaba adları tooavoid dağıtım sorunlarını görüldüğü gibi kullanın.

* **commandToExecute**: (gerekli, string) giriş noktası betik tooexecute hello
* **fileUris**: (isteğe bağlı, dize dizisi) dosyaları toobe hello URL'lerini indirilir.
* **zaman damgası** (isteğe bağlı, tamsayı) bu alanın değerini değiştirerek bu alan yalnızca tootrigger yeniden çalıştır hello komut dosyası kullanın.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Korumalı yapılandırma
Şema:

**Not** -bu özellik adları büyük/küçük harfe duyarlıdır. Merhaba adları tooavoid dağıtım sorunlarını görüldüğü gibi kullanın.

* **commandToExecute**: (isteğe bağlı, dize) giriş noktası betik tooexecute hello. Parolalar gibi gizli komutunuzu içeriyorsa, bu alan kullanın.
* **storageAccountName**: (isteğe bağlı, dize) depolama hesabının hello adı. Depolama kimlik belirtirseniz, tüm fileUris Azure BLOB'ları için URL'leri olması gerekir.
* **storageAccountKey**: (isteğe bağlı, dize) hello depolama hesabının erişim anahtarı.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
Hello Azure CLI toorun hello özel betik uzantısının kullanırken, bir yapılandırma dosyası veya en düşük hello dosya URI'si ve hello komut yürütme içeren dosyaları oluşturun.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

İsteğe bağlı olarak hello ayarları hello komutta JSON biçimli dize olarak belirtilebilir. Belirtilen yürütme sırasında ve ayrı yapılandırma dosyası olmadan hello yapılandırma toobe sağlar.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Azure CLI örnekleri

**Örnek 1** -komut dosyası ile genel yapılandırması.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Azure CLI komutu:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Örnek 2** -herhangi bir komut dosyası ile genel yapılandırması.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI komutu:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Örnek 3** - bir ortak yapılandırma dosyası kullanılan toospecify hello komut dosyası URI ve bir korumalı yapılandırma dosyası kullanılan toospecify hello komutu toobe yürütülür.

Genel yapılandırma dosyası:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Korumalı yapılandırma dosyası:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI komutu:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Resource Manager Şablonu
Hello Azure özel betik uzantısının Resource Manager şablonu kullanarak sanal makine dağıtımı aynı anda çalıştırabilirsiniz. toodo, bu nedenle, doğru biçimlendirilmiş JSON toohello Dağıtım şablonuna ekleyin.

### <a name="resource-manager-examples"></a>Resource Manager örnekleri
**Örnek 1** -genel yapılandırması.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Örnek 2** -korumalı yapılandırmasında yürütme komutu.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Hello .net Core müzik deposu görmek için tam bir örnek - Demo [müzik deposu Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Sorun giderme
Hello özel betik uzantısının çalıştığında, hello komut dosyası oluşturulur veya aşağıdaki örneğine bir dizin benzer toohello indirilir. Merhaba komutu çıktısı bu dizindeki INTO kaydedilmiş de `stdout` ve `stderr` dosya.

```bash
/var/lib/waagent/custom-script/download/0/
```

Hello Azure betik uzantısı burada bulunabilir bir günlük üretir.

```bash
/var/log/azure/custom-script/handler.log
```

Merhaba özel betik uzantısının Hello yürütme durumu da hello Azure CLI ile alınabilir.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

Merhaba çıktı hello metin aşağıdaki gibi görünür:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Sonraki Adımlar
Diğer VM betik uzantıları hakkında daha fazla bilgi için bkz: [Linux için Azure betik uzantısı genel bakış](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

