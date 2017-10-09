---
title: "Resource Manager şablonları oluşturmak için aaaBest uygulamalar | Microsoft Docs"
description: "Azure Resource Manager şablonlarınızı basitleştirmeye yönelik yönergeler verilmiştir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Azure Resource Manager şablonları oluşturmak için en iyi uygulamalar
Bu yönergeleri, güvenilir ve kolay toouse olan Azure Resource Manager şablonları oluşturmanıza yardımcı olabilir. Merhaba, yalnızca önerileri yönergelerdir. Bunlar belirtilenler dışında gereksinimleri değildir. Senaryonuz hello birini çeşitlemesi gerektirebilir yaklaşımlar ve örnekler aşağıdaki.

## <a name="resource-names"></a>Kaynak adları
Genellikle, kaynak adları Kaynak Yöneticisi'nde üç türleri ile çalışır:

* Kaynak adları benzersiz olmalıdır.
* Toobe benzersiz olmayan kaynak adları gerekli, ancak tooprovide yardımcı olabilecek bir ad belirlemek bağlamına dayalı bir kaynak seçin.
* Genel kaynak adları.

 Kaynak adı kısıtlamaları hakkında daha fazla bilgi için bkz: [Azure kaynakları için adlandırma kurallarını önerilen](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Benzersiz kaynak adları
Veri erişim uç noktası olan herhangi bir kaynak türü için bir benzersiz kaynak adı sağlamanız gerekir. Benzersiz bir ad gerektiren bazı yaygın kaynak türleri şunlardır:

* Azure depolama<sup>1</sup> 
* Azure Uygulama Hizmeti’nin Web Apps özelliği
* SQL Server
* Azure Key Vault
* Azure Redis Cache
* Azure Batch
* Azure Traffic Manager
* Azure Search
* Azure Hdınsight

<sup>1</sup> depolama hesabı adları de küçük olmalıdır, 24 karakter veya daha az ve tire sahip değil.

Bir parametre için bir kaynak adı sağlarsanız, hello kaynak dağıttığınızda benzersiz bir ad sağlamanız gerekir. İsteğe bağlı olarak, hello kullanan bir değişken oluşturabilirsiniz [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate bir ad işlev. 

Ayrıca olabilir veya tooadd bir önek istediğiniz toohello soneki **uniqueString** sonucu. Değiştirme hello benzersiz bir ad daha fazla kolayca hello kaynak türü hello adından belirlemenize yardımcı olabilir. Örneğin, değişkeni aşağıdaki hello kullanarak bir depolama hesabı için benzersiz bir ad oluşturabilirsiniz:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Tanımlama için kaynak adları
Bazı kaynak türleri tooname isteyebilirsiniz, ancak adları benzersiz toobe sahip değil. Bu kaynak türleri için hello kaynak bağlamını ve hello kaynak türünü tanımlayan bir ad sağlayabilirsiniz. Merhaba kaynak kaynakların bir listesinde tanımanıza yardımcı olacak açıklayıcı bir ad sağlayın. Toouse farklı bir kaynak adı farklı dağıtımlar için gerekiyorsa, bir parametre için hello adı kullanabilirsiniz:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Dağıtım sırasında bir ad toopass ihtiyacınız yoksa, bir değişkeni kullanabilirsiniz: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

Bir sabit kodlu değer de kullanabilirsiniz:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Genel kaynak adları
Farklı bir kaynak çoğunlukla erişim kaynak türleri için hello şablonu sabit kodlanmış olan bir ad kullanabilirsiniz. Örneğin, bir SQL Server'da Güvenlik duvarı kuralları için standart, genel bir ad ayarlayabilirsiniz:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>Parametreler
parametrelerle çalışırken hello aşağıdaki bilgiler yararlı olabilir:

* Parametreleri kullanımını en aza indirin. Mümkün olduğunda, bir değişkeni veya hazır değer kullanın. Parametreleri için yalnızca bu senaryoları kullanın:
   
   * Tooenvironment (SKU, boyut, Kapasite) according, toouse Çeşitlemeler istediğiniz ayarları.
   * Kaynak adları için kolay bir şekilde tanımlanması toospecify istiyor.
   * Değerleri toocomplete sık diğer görevleri (örneğin, bir yönetici kullanıcı adı) kullanın.
   * Gizli (parolalar gibi).
   * Merhaba numarası veya bir kaynak türü birden çok örneğini oluşturduğunuzda değerleri toouse dizisi.
* Ortası büyük parametre adları için kullanın.
* Her parametre hello meta verilerindeki bir açıklama belirtin:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* (Dışında parolalar ve SSH anahtarları) parametrelerinin varsayılan değerleri tanımlayın:
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Kullanım **SecureString** tüm parolalar ve gizli anahtarları için: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Mümkün olduğunda, bir parametre toospecify konumu kullanmayın. Bunun yerine, hello kullanın **konumu** hello kaynak grubunun özelliği. Hello kullanarak **resourceGroup () .location** ifade tüm kaynaklarınız için hello şablon kaynaklarında içinde dağıtılan hello hello kaynak grubu ile aynı konumda:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Bir kaynak türü konumları, yalnızca sınırlı sayıda destekleniyorsa, toospecify geçerli bir konum hello şablonu doğrudan isteyebilirsiniz. Kullanmanız gerekiyorsa bir **konumu** parametresi mümkün olduğunca Bu parametre değeri Merhaba, büyük olasılıkla toobe kaynakları paylaşmak aynı konumu. Bu kullanıcılar tooprovide konum bilgileri sorulur hello sayı en aza indirir.
* Bir kaynak türü için hello API sürümü için bir parametre veya değişken kullanmaktan kaçının. Kaynak özellikleri ve değerlerini sürüm numarasına göre farklılık gösterebilir. Merhaba API sürümü tooa parametre veya değişken ayarlandığında bir kod düzenleyicisinde IntelliSense hello doğru şemayı belirleyemiyor. Bunun yerine, sabit kodlu hello hello şablonunda API sürümü.

## <a name="variables"></a>Değişkenler
değişkenlerle çalışırken hello aşağıdaki bilgiler yararlı olabilir:

* Toouse birden çok kez bir şablon ihtiyacınız olduğunu değerleri için değişkenlerini kullanın. Bir değer yalnızca bir kez kullanılır, sabit kodlanmış bir değer, şablonu daha kolay tooread yapar.
* Merhaba kullanamazsınız [başvuru](resource-group-template-functions-resource.md#reference) hello işlevinde **değişkenleri** hello şablonu bölümü. Merhaba **başvuru** işlevi hello kaynağın çalışma zamanı durumunu değerinden türetilir. Ancak, değişkenleri hello hello şablonunu ayrıştırma ilk sırasında çözümlenir. Merhaba gereken değerleri oluşturmak **başvuru** hello doğrudan işlevinde **kaynakları** veya **çıkarır** hello şablonu bölümü.
* Bölümünde açıklandığı gibi benzersiz kaynak adları için değişkenleri dahil [kaynak adları](#resource-names).
* Değişkenleri karmaşık nesneleri gruplayabilirsiniz. Kullanım hello **variable.subentry** tooreference karmaşık bir nesne arasında bir değer biçimlendirin. Değişkenleri gruplandırma ilgili değişkenleri izlemenize yardımcı olur. Ayrıca, hello şablon okunabilirliğini artırır. Örnek aşağıda verilmiştir:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Karmaşık bir nesne değeri karmaşık bir nesneden başvuran bir ifade içeremez. Bu amaç için ayrı bir değişken tanımlayın.
   > 
   > 
   
     Karmaşık nesne değişkenleri olarak kullanarak gelişmiş örnekler için bkz: [paylaşmak Azure Resource Manager şablonları durumda](best-practices-resource-manager-state.md).

## <a name="resources"></a>Kaynaklar
kaynaklarla çalışırken hello aşağıdaki bilgiler yararlı olabilir:

* toohelp diğer katkıda bulunanlar hello kaynak hello amacı anlamak, belirtin **açıklamaları** hello şablonundaki her bir kaynak için:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Etiketler tooadd meta veri tooresources kullanabilirsiniz. Kaynaklarınızın hakkında meta veri tooadd bilgileri kullanın. Örneğin, bir kaynak için meta veri toorecord fatura ayrıntılarına ekleyebilirsiniz. Daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).
* Kullanırsanız, bir *ortak uç nokta* şablonunuzda (örneğin, bir Azure Blob Depolama ortak uç nokta), *olmayan sabit kodlu* ad alanı hello. Kullanım hello **başvuru** işlevi toodynamically almak hello ad alanı. Bu yaklaşım toodeploy hello şablonu toodifferent genel ad alanı ortamlarında el ile Merhaba şablonunda hello endpoint değiştirmeden kullanabilirsiniz. Ayarlama hello API sürümü toohello şablonunuzda hello depolama hesabı için kullandığınız aynı sürüm:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Merhaba depolama hesabı hello dağıtılırsa oluşturmakta olduğunuz aynı şablonu gerektirmeyen toospecify hello sağlayıcı ad alanı hello kaynak başvurduğunuzda. Basitleştirilmiş hello sözdizimi şöyledir:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Yapılandırılmış toouse ortak bir ad alanı olan diğer değerleri şablonunuzda varsa, bu değerleri değiştirmek tooreflect hello aynı **başvuru** işlevi. Örneğin, hello ayarlayabilirsiniz **storageUri** hello sanal makine tanılama profili özelliği:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Ayrıca, farklı kaynak grubunda bulunan mevcut bir depolama hesabını başvurabilir:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Yalnızca bir uygulama gerektirdiğinde, ortak IP adresleri tooa sanal makine atayın. hata ayıklama için ya da Yönetim veya yönetim amacıyla tooconnect tooa sanal makine (VM) gelen NAT kuralları, bir sanal ağ geçidi ya da bir jumpbox kullanın.
   
     Toovirtual makineler bağlanma hakkında daha fazla bilgi için bkz:
   
   * [N katmanlı mimari Azure VM'ler çalıştırın](../guidance/guidance-compute-n-tier-vm.md)
   * [Azure Kaynak Yöneticisi'nde yer alan VM'ler için WinRM erişimini Ayarla](../virtual-machines/windows/winrm.md)
   * [Hello Azure portalını kullanarak dış erişim tooyour VM izin ver](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [PowerShell kullanarak dış erişim tooyour VM izin ver](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Azure CLI kullanarak dış erişim tooyour Linux VM izin ver](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Merhaba **domainNameLabel** özelliği genel IP adresleri için benzersiz olmalıdır. Merhaba **domainNameLabel** değeri gerekir 3 ile 63 karakter uzunluğunda olmalıdır ve bu normal bir ifadeyle belirtilen hello kurallarına: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Çünkü hello **uniqueString** işlevi hello 13 karakterden uzun olan bir dize oluşturur **dnsPrefixString** parametredir sınırlı too50 karakterler:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Bir parola tooa özel betik uzantısı eklediğinizde, hello kullan **commandToExecute** hello özelliğinde **protectedSettings** özelliği:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > gizli olan tooensure parametreleri tooVMs ve uzantıları geçirildiğinde şifrelenmiş hello kullan **protectedSettings** hello ilgili uzantılar özelliği.
   > 
   > 

## <a name="outputs"></a>Çıkışları
Bir şablon toocreate ortak IP adresleri kullanıyorsanız dahil bir **çıkarır** başlangıç IP adresi ve hello tam etki alanı adı (FQDN) ayrıntılarını döndürür bölümü. Dağıtımdan sonra çıktı değerleri tooeasily alma ayrıntılarını ortak IP adresleri ve FQDN'ler kullanabilirsiniz. Merhaba kaynağa başvuran toocreate kullanılan hello API sürümü kullanın: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>İç içe geçmiş şablonları karşılaştırması tek şablonu
toodeploy, çözümünüzün birden çok iç içe geçmiş şablonları ile tek bir şablon ya da ana şablon kullanabilirsiniz. İç içe geçmiş şablonları daha Gelişmiş senaryolar için yaygındır. Avantajları aşağıdaki hello iç içe geçmiş şablonu verir kullanma:

* Bir çözüm hedeflenen bileşenlere aşağı bozulabilir.
* Farklı ana şablonları ile iç içe geçmiş şablonlarını yeniden kullanabilirsiniz.

İç içe geçmiş toouse şablonları seçerseniz, yönergeleri izleyerek hello şablon tasarımı standartlaştırmak yardımcı olabilir. Bu yönergelere dayalı [Azure Resource Manager şablonları tasarlamak için desenleri](best-practices-resource-manager-design-templates.md). Şablonları aşağıdaki hello sahip bir tasarım öneririz:

* **Ana şablon** (azuredeploy.json). Merhaba giriş parametreleri için kullanın.
* **Paylaşılan kaynaklar şablon**. Kullanım toodeploy paylaşılan tüm diğer kaynakları kullanan kaynakları (örneğin, sanal ağ ve kullanılabilirlik kümeleri gibi). Kullanım hello **dependsOn** ifade tooensure bu şablonu önce diğer şablonlar dağıtılır.
* **İsteğe bağlı kaynakları şablon**. Kullanım tooconditionally bir parametre (örneğin, bir jumpbox) temel alarak kaynaklara dağıtın.
* **Üye kaynakları şablon**. Bir uygulama katmanı içindeki her örnek türü kendi yapılandırmasına sahip. Bir katman içinde farklı bir örnek türleri tanımlayabilirsiniz. (Örneğin, bir küme hello ilk örneği oluşturur ve ek örnekler toohello varolan bir kümeye eklenir.) Her örneği türü kendi dağıtım şablonu yok.
* **Komut dosyaları**. Yaygın olarak yeniden kullanılabilir komut dosyaları her örneği türü (örneğin, başlatma ve biçimi ek diskleri) için geçerlidir. Belirli özelleştirme amaçla oluşturduğunuz özel komut dosyaları hello örneği türüne göre farklı olabilir.

![İç içe geçmiş şablonu](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Daha fazla bilgi için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Koşullu toonested şablonları bağlantı
Bir parametre tooconditionally bağlantı toonested şablonları kullanabilirsiniz. Merhaba parametre hello URI hello şablonunun parçası haline gelir:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Şablon biçimi
İyi bir uygulama toopass olan şablonunuzu JSON Doğrulayıcı aracılığıyla. Bir doğrulayıcı yabancı virgül, parantez ve dağıtım sırasında bir hata neden olabilir parantezler kaldırmanıza yardımcı olabilir. Deneyin [JSONLint](http://jsonlint.com/) veya sık kullanılan için linter paketi düzenleme ortamı (Visual Studio Code, Atom, Sublime metin, Visual Studio).

Aynı zamanda bir fikir tooformat olan, JSON okunabilirliği. Bir JSON biçimlendirici paketi için yerel, Düzenleyicisi kullanabilirsiniz. Visual Studio'da tooformat hello belge basın **Ctrl + K, Ctrl + D**. Visual Studio Code basın **Alt + üst karakter + F**. Yerel düzenleyicinizi hello belge biçimlendirmez, kullanabileceğiniz bir [çevrimiçi biçimlendirici](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Sonraki adımlar
* Sanal makineler için çözüm mimarisi oluşturma ile ilgili yönergeler için bkz: [bir Windows VM Azure'da çalışan](../guidance/guidance-compute-single-vm.md) ve [Azure'da bir Linux VM çalışması](../guidance/guidance-compute-single-vm-linux.md).
* Bir depolama hesabı ayarlama hakkında yönergeler için bkz [Azure Storage performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage/common/storage-performance-checklist.md).
* Kuruluş Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında toolearn abonelikleri yönetmek için bkz [Azure enterprise iskele: Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

