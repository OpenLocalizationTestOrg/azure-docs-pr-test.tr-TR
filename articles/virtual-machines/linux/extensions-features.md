---
title: "aaaVirtual Linux için uzantıları ve özellikleri makine | Microsoft Docs"
description: "Hangi uzantıları ne bunlar sağlayın veya geliştirmek tarafından gruplandırılmış Azure sanal makineler için kullanılabilir olduğunu öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Sanal makine uzantıları ve Linux için özellikleri

Azure sanal makine uzantıları Azure sanal makinelerde dağıtım sonrası yapılandırma ve Otomasyon görevlerini sağlayan küçük uygulamalardır. Örneğin, bir sanal makineye yazılım yükleme, virüsten koruma veya Docker yapılandırma gerektiriyorsa, VM uzantısı için kullanılan toocomplete bu görevleri olabilir. Azure VM uzantıları ve Azure portal hello hello Azure CLI, PowerShell, Azure Resource Manager şablonları kullanarak çalıştırabilirsiniz. Uzantıları ile yeni bir sanal makine dağıtımı paketlenebilir veya varolan bir sistemle bağlantılı çalıştırın.

Bu belge VM uzantıları, Azure VM uzantıları ve Kılavuzu nasıl toodetect, yönetme ve VM uzantıları kaldırma üzerinde kullanma önkoşulları genel bir bakış sağlar. Birçok VM uzantıları bulunduğundan, bu belgede genelleştirilmiş bilgiler sağlanmaktadır her potansiyel olarak benzersiz bir yapılandırmaya sahip. Uzantı özel ayrıntıları her belge belirli toohello tek tek uzantısı'nda bulunabilir.

## <a name="use-cases-and-samples"></a>Kullanım örnekleri ve örnekler

Birkaç farklı Azure VM uzantıları kullanılabilir, her biri belirli bir kullanım örneği. Bazı örnekler şunlardır:

- Linux için hello DSC uzantısı kullanarak PowerShell istenen durum yapılandırması tooa sanal makine uygulayın. Daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Bir sanal makinenin hello Microsoft İzleme Aracısı VM uzantısı ile izlemeyi yapılandırma. Daha fazla bilgi için bkz: [nasıl toomonitor bir Linux VM](tutorial-monitoring.md).
- Azure altyapınızın hello Datadog uzantısı ile izlemeyi yapılandırma. Daha fazla bilgi için bkz: Merhaba [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Docker ana hello Docker VM uzantısı kullanılarak Azure sanal makinesi üzerinde yapılandırın. Daha fazla bilgi için bkz: [Docker VM uzantısı](dockerextension.md).

Ayrıca tooprocess özgü uzantılar, özel betik uzantısı hem Windows hem de Linux sanal makineler için kullanılabilir. Merhaba özel betik uzantısı Linux için bir sanal makine üzerinde çalışan tüm Bash betik toobe sağlar. Özel komut dosyaları, yerel hangi Azure araçlar sağlayabilir ötesinde yapılandırma gerektiren Azure dağıtımları tasarlamak için faydalıdır. Daha fazla bilgi için bkz: [Linux VM özel betik uzantısı](extensions-customscript.md).


## <a name="prerequisites"></a>Ön koşullar

Her sanal makine uzantısı önkoşulları kendi kümesi olabilir. Örneği için bir önkoşul desteklenen Linux dağıtım hello Docker VM uzantısı vardır. Tek tek uzantıların gereksinimlerini hello uzantıya özgü belgelerinde açıklanmıştır.

### <a name="azure-vm-agent"></a>Azure VM aracısı

Hello Azure VM Aracısı bir Azure sanal makinesi ve hello Azure yapı denetleyicisi arasındaki etkileşimler yönetir. Merhaba VM Aracısı dağıtma ve yönetme Azure sanal makineler, çalışan VM uzantıları dahil olmak üzere birçok işlevsel görünüşlere için sorumludur. Hello Azure VM Aracısı Azure Marketi görüntülerinde önceden yüklenmiş ve desteklenen işletim sistemlerinde el ile yüklenebilir.

Desteklenen işletim sistemleri ve yükleme yönergeleri hakkında daha fazla bilgi için bkz: [Azure sanal makine Aracısı](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>VM uzantıları Bul

Birçok farklı VM uzantıları, Azure sanal makineler ile kullanmak için kullanılabilir. tam bir listesi, toosee hello Azure CLI komutuyla izleyerek, tercih ettiğiniz hello konumla hello Örnek konum değiştirme hello çalıştırın.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>VM uzantıları çalıştırın

Azure sanal makine uzantıları toomake yapılandırma değişiklikleri gerekir ya da bağlantı zaten dağıtılmış bir VM'de kurtarmak bağlandığınızda yararlıdır ve mevcut sanal makineler üzerinde çalıştırılabilir. VM uzantıları, Azure Resource Manager şablonu dağıtımlarında da gönderilebilir. Resource Manager şablonları ile uzantıları kullanarak, Azure sanal makineleri dağıtılabilir ve dağıtım sonrası müdahalesi olmadan yapılandırılmış.

yöntemler aşağıdaki hello kullanılan toorun uzantı var olan bir sanal makineye karşı olabilir.

### <a name="azure-cli"></a>Azure CLI

Azure sanal makine uzantıları çalıştırılabilir karşı var olan bir sanal makine hello kullanarak `az vm extension set` komutu. Bu örnek, bir sanal makine hello özel betik uzantısı çalışır.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

komut dosyası oluşturduğu çıktı benzer toohello metin aşağıdaki hello:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Azure portalına

VM uzantıları hello Azure portal aracılığıyla uygulanan tooan varolan sanal makine olabilir. toodo hello sanal makine, bu nedenle, seçin seçin **uzantıları**, tıklatıp **Ekle**. Kullanılabilir uzantılar hello listeden istediğiniz ve hello hello sihirbazındaki yönergeleri izleyin hello uzantıyı seçin.

Merhaba aşağıdaki görüntüde hello Linux özel betik uzantısı hello Azure Portalı'ndan hello yüklemesini gösterir.

![Özel betik uzantısı yükleyin](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları

VM uzantıları eklenen tooan Azure Resource Manager şablonu olabilir ve hello şablon hello dağıtımı ile yürütüldü. Bir şablon uzantılı dağıttığınızda, tam olarak yapılandırılmış Azure dağıtımları oluşturamazsınız. Örneğin, aşağıdaki JSON bir Resource Manager şablondan alınmış hello. Merhaba şablonu bir dizi yük dengeli sanal makineler ve Azure SQL Veritabanını dağıtır ve ardından bir .NET Core uygulaması her VM yükler. Merhaba VM uzantısı hello yazılım yüklemesini mvc'deki.

Daha fazla bilgi için bkz: hello tam [Resource Manager şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>VM uzantısı verileri güvenli

VM uzantısı çalıştırırken kimlik bilgilerini, depolama hesabı adları ve depolama hesabı erişim anahtarlarını gibi hassas bilgileri gerekli tooinclude olabilir. Birçok VM uzantıları verileri şifreler ve yalnızca hello hedef sanal makine içinde şifresini çözer korumalı bir yapılandırmayı içerir. Belirli korumalı yapılandırma şeması her uzantısına sahip ve her uzantıya özgü belgelerinde ayrıntılı olarak gösterilmiştir.

Aşağıdaki örneğine hello Linux için hello özel betik uzantısı örneğini gösterir. Bu hello komutu tooexecute kimlik bilgileri kümesi içerir dikkat edin. Bu örnekte, hello komutu tooexecute şifrelenmez.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Taşıma hello **komutu tooexecute** özelliği toohello **korumalı** yapılandırma hello yürütme dize güvenliğini sağlar.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>VM uzantıları sorun giderme

Her VM uzantısı sorun giderme adımları belirli toohello uzantısına sahip olabilir. Örneğin, hello özel betik uzantısı kullanırken, komut dosyası yürütme ayrıntılarını yerel olarak hello uzantısı çalıştırıldığı hello sanal makine üzerinde bulunabilir. Uzantı özel sorun giderme işlemleri uzantıya özgü belgelerinde açıklanmıştır.

Aşağıdaki sorun giderme adımları hello tooall sanal makine uzantıları uygulayın.

### <a name="view-extension-status"></a>Uzantı durumunu görüntüle

Bir sanal makine uzantısı bir sanal makine çalıştırdıktan sonra Azure CLI komutu tooreturn uzantı durumunu izleyen hello kullanın. Örnek parametre adları kendi değerlerinizle değiştirin.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Merhaba çıktı hello metin aşağıdaki gibi görünür:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Uzantı yürütme durumu da hello Azure portalında bulunabilir. tooview hello durumu select hello sanal makine, bir uzantı seçin **uzantıları**, ve hello istenen uzantı seçin.

### <a name="rerun-a-vm-extension"></a>VM uzantısı yeniden çalıştırın

Bir sanal makine uzantısı toobe gereken durumlar olabilir yeniden çalıştırın. Uzantı, kaldırarak ve tercih ettiğiniz yürütme yöntemiyle hello uzantısı yeniden çalıştırma çalıştırabilirsiniz. bir uzantı tooremove hello Azure CLI komutuyla aşağıdaki hello çalıştırın. Örnek parametre adları kendi değerlerinizle değiştirin.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Uzantı hello Azure Portalı'ndaki adımları izleyerek hello kullanarak kaldırabilirsiniz:

1. Bir sanal makineyi seçin.
2. Seçin **uzantıları**.
3. İstenen hello uzantıyı seçin.
4. Seçin **kaldırma**.

## <a name="common-vm-extension-reference"></a>Ortak VM uzantısı başvurusu
| Uzantı adı | Açıklama | Daha fazla bilgi |
| --- | --- | --- |
| Linux için özel betik uzantısı |Bir Azure sanal makinesi karşı komut dosyalarını çalıştır |[Linux için özel betik uzantısı](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Docker uzantısı |Merhaba Docker arka plan programı toosupport uzak Docker komutları yükleyin. |[Docker VM uzantısı](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| VM Erişimi uzantısı |Erişim tooan Azure sanal makinesi yeniden elde |[VM Erişimi uzantısı](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Azure tanılama uzantısını |Azure tanılama yönetme |[Azure tanılama uzantısını](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM erişim uzantısı |Kullanıcılar ve kimlik bilgilerini yönetme |[Linux VM erişim uzantısı](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
