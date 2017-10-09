---
title: "Azure şablonları arasındaki aaaPass karmaşık değerleri | Microsoft Docs"
description: "Gösterir karmaşık nesneler tooshare durumu verilerinin Azure Resource Manager şablonları ile bağlı şablonları kullanma yaklaşım önerilir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Paylaşım durumu tooand Azure Resource Manager şablonları
Bu konu, yönetme ve şablonlar içindeki durumu paylaşımı için en iyi uygulamaları gösterir. Hello parametreler ve değişkenler bu konuda gösterilen örnekler tanımlayabilirsiniz nesnelerin hello türü tooconveniently Dağıtım gereksinimlerinizi düzenleyin. Bu örnekler, ortamınız için anlamlı özellik değerlerini kendi nesneleriyle uygulayabilirsiniz.

Bu konuda daha büyük bir Teknik İnceleme bir parçasıdır. tam kağıt tooread hello karşıdan [World sınıfı Resource Manager şablonları konuları ve kanıtlanmış yöntemler](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Standart yapılandırma ayarlarını belirtin
Toplam esneklik ve sayısız Çeşitlemeler sağlayan bir şablon sunmak yerine, genel bir desen tooprovide bilinen yapılandırmaları Seçimi ' dir. Etkin kullanıcılar korumalı alan, küçük, Orta ve büyük gibi standart ısı boyutları seçebilirsiniz. Diğer ısı boyutları community edition veya enterprise edition gibi ürün teklifleri gösterilebilir. Diğer durumlarda, harita azaltmak gibi iş yüküne özgü yapılandırmaları bir teknolojisi – olabilir veya hiç sql.

Karmaşık nesneler ile bazen "özellik paketleri" bilinen veri topluluklarını değişkenleri oluşturun ve o veri toodrive hello kaynak bildirimi şablonunuzda kullanın. Bu yaklaşım, müşteri için yapılandırılmış farklı boyutlarda iyi, bilinen yapılandırmaları sağlar. Bilinen yapılandırmaları hello şablon kullanıcılarının gerekir küme boyutlandırma platform kaynak kısıtlamaları kendi faktörünü üzerinde belirlemek ve depolama hesapları ve diğer kaynakların bölümleme matematik tooidentify hello kaynaklanan yapın (toocluster boyutu nedeniyle ve Kaynak sınırlamaları). Ayrıca toomaking hello müşteri için daha iyi bir deneyim, birkaç bilinen yapılandırmaları daha kolay toosupport olan ve yoğunluğu daha yüksek düzeyde sunmanıza yardımcı olabilir.

örnekte gösterildiği nasıl aşağıdaki hello veri koleksiyonları için karmaşık nesneler içeren toodefine değişkenleri. Merhaba koleksiyonları, sanal makine boyutu, ağ ayarları, işletim sistemi ayarlarını ve kullanılabilirlik ayarları için kullanılan değerleri tanımlayın.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Bu hello fark **tshirtSize** değişkeni, bir parametre aracılığıyla sağlanan hello ısı boyutu art arda ekler (**küçük**, **orta**, **büyük**) toohello metin **tshirtSize**. Bu değişken tooretrieve hello ilişkili karmaşık nesne değişkeni bu ısı boyut için kullanın.

Ardından hello şablondaki daha sonra bu değişkenleri başvuruda bulunabilir. Merhaba özelliği tooreference adlı-değişkenleri ve bunların özelliklerini hello şablon söz dizimi basitleştirir ve kolay toounderstand bağlamı kolaylaştırır. Aşağıdaki örneğine hello tooset değerleri daha önce gösterilen hello nesneleri kullanılarak bir kaynak toodeploy tanımlar. Örneğin, hello VM boyutu hello değeri alınırken tarafından ayarlanır `variables('tshirtSize').vmSize` hello disk boyutu alınır için hello değeri while `variables('tshirtSize').diskSize`. Ayrıca, bağlantılı bir şablon için hello değerle ayarlamak için URI hello `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Geçişi durumu tooa şablonu
Bir şablonu doğrudan dağıtım sırasında sağladığınız parametreler aracılığıyla içine durumu paylaşır.

şu Tablo listeleri yaygın olarak kullanılan parametreler şablonlarındaki hello.

| Ad | Değer | Açıklama |
| --- | --- | --- |
| location |Azure bölgeleri kısıtlanmış listesinden dize |Merhaba kaynakları dağıtıldığı hello konumu. |
| storageAccountNamePrefix |Dize |Merhaba hello VM'in disklerini yerleştirildiği depolama hesabı için benzersiz DNS adı |
| domainName |Dize |Merhaba biçiminde hello genel olarak erişilebilir jumpbox VM etki alanı adı: **{domainName}. { konum}.cloudapp.com** örneğin: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |Dize |Merhaba VM'ler için kullanıcı adı |
| Admınpassword |Dize |Merhaba VM'ler için parola |
| tshirtSize |Sunulan ısı boyutları kısıtlanmış listesinden dize |Ölçek birimi boyutu tooprovision adlı hello. Örneğin, "Küçük", "Medium", "Büyük" |
| virtualNetworkName |Dize |Tüketici hello hello sanal ağın adını toouse istemektedir. |
| enableJumpbox |(Etkin/devre dışı) kısıtlanmış listeden dize |Tanımlayan parametresi olup olmadığını tooenable jumpbox hello ortamı için. Değerler: "etkin", "disabled" |

Merhaba **tshirtSize** hello önceki bölümünde kullanılan parametre olarak tanımlanır:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Durum toolinked şablonları geçirin
Toolinked şablonları bağlanırken genellikle statik bir karışımını kullanın ve değişkenleri oluşturulur.

### <a name="static-variables"></a>Statik değişkenler
Statik değişkenler genellikle kullanılan tooprovide temel gibi bir şablon kullanılan URL'leri değerlerdir.

Şablon alıntı aşağıdaki hello içinde `templateBaseUrl` Github'da hello şablon hello kök konumunu belirtir. Merhaba sonraki satıra yeni bir değişken oluşturur `sharedTemplateUrl` hello temel URL hello bilinen hello paylaşılan kaynakları şablonunun adını ile birleştirir. Bu satır, bir karmaşık nesne değişkeni kullanılan toostore ısı boyutu hello temel URL birleştirilmiş toohello olduğu bilinen yapılandırma şablon konumu ve hello depolanan `vmTemplate` özelliği.

Bu yaklaşımın avantajı Hello hello şablon konumu değişirse, yalnızca tüm bağlı hello şablonlarda geçirir tek bir yerde toochange hello statik değişken olmanızdır.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Oluşturulan değişkenleri
Toplama toostatic değişkenlerde çeşitli değişkenler dinamik olarak oluşturulur. Bu bölümde bazı oluşturulan değişkenlerin hello ortak türlerini tanımlar.

#### <a name="tshirtsize"></a>tshirtSize
Örnekler hello yukarıdaki ile oluşturulan bu değişken hakkında bilgi sahibi.

#### <a name="networksettings"></a>networkSettings
Bir kapasite, özelliği veya uçtan uca kapsamlı çözüm şablonu hello bağlı şablonları mevcut kaynaklar genellikle bir ağda oluşturun. Bir kolay yaklaşım karmaşık nesne toostore ağ ayarlarını toouse olduğu ve bunları toolinked şablonları geçirin.

Ağ Ayarları iletişim kurulurken bir örnek aşağıda görülebilir.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Bağlantılı şablonlarında oluşturulan kaynakları, genellikle bir kullanılabilirlik kümesine yerleştirilir. Merhaba, aşağıdaki örneğine içinde hello kullanılabilirlik kümesi adı belirtilen ve hata etki alanı da hello ve etki alanı sayısı toouse güncelleştirin.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Önek olarak bir ad kullanabilirsiniz birden çok kullanılabilirlik kümesine (örneğin, bir ana düğüm için) ve veri düğümlerini için başka bir gereksinim duyarsanız, birden çok kullanılabilirlik kümesine belirtin veya belirli bir ısı boyutu için bir değişken oluşturmak için daha önce gösterilen hello modeli izleyin.

#### <a name="storagesettings"></a>storageSettings
Depolama ayrıntıları genellikle bağlı şablonları ile paylaşılır. Aşağıda, hello örnekte bir *storageSettings* nesnesi, depolama hesabı ve kapsayıcı adları hello hakkında ayrıntılar sağlar.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Bağlantılı şablonlarıyla bilinen farklı yapılandırma türlerine toopass işletim sistemi ayarlarını toovarious düğümleri türlerini gerekebilir. Karmaşık bir nesne bir kolay bir yolu toostore ve paylaşımı işletim sistemi bilgileri ve ayrıca daha kolay toosupport kılar dağıtımı için birden çok işletim sistemi seçenekleri.

Merhaba aşağıdaki örnek gösteren bir nesne için *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Oluşturulan bir değişken *machineSettings* bir VM oluşturmak için çekirdek değişkenleri bir karışımını içeren karmaşık bir nesne. Merhaba değişkenleri yönetici kullanıcı adı ve parola, hello VM adları için bir önek ve bir işletim sistemi görüntüsü başvurusu içerir.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Unutmayın *osImageReference* alır hello hello değerlerinden *osSettings* hello ana şablonda tanımlanan değişken. Anlamı kolayca değiştirebilirsiniz hello işletim sistemi için bir VM — tamamen veya bir şablon tüketici hello tercihine göre.

#### <a name="vmscripts"></a>vmScripts
Merhaba *vmScripts* hello betikleri toodownload hakkında ayrıntılar içeren nesne ve dış ve iç başvuruları dahil olmak üzere bir VM örneğinde yürütün. Dışında hello altyapı başvurular içerir.
Merhaba yüklü yazılımı yüklü ve yapılandırma iç başvurular içerir.

Merhaba kullandığınız *scriptsToDownload* özelliği toolist hello toodownload toohello VM komut dosyaları. Bu nesne farklı türde eylemler için başvurular toocommand satırı değişkenlerini de içerir. Bu eylemler hello Varsayılan yüklemede tek tek her düğüm, tüm düğümler dağıtıldıktan sonra çalıştırılan bir yükleme ve şablon verilen belirli tooa olabilecek ek betik yürütme içerir.

Bu, bir şablon toodeploy arbiter toodeliver yüksek kullanılabilirlik gerektiren MongoDB örneğidir. Merhaba *arbiterNodeInstallCommand* çok eklenen*vmScripts* tooinstall hello arbiter.

Merhaba değişkenleri hello belirli metin tooexecute hello komut hello uygun değerlerle tanımlamak hello değişkenleri nerede bölümüdür.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Bir şablondan dönüş durumu
Yalnızca, bir şablona veri geçişi, paylaşım veri geri toohello arama şablonu de kullanabilirsiniz. Merhaba, **çıkarır** bölüm bağlantılı şablonu, hello kaynak şablonu tarafından kullanılabilecek anahtar/değer çiftleri sağlayabilir.

Merhaba aşağıdaki örnekte nasıl toopass bağlantılı bir şablonda oluşturulan özel IP adresi hello gösterilmektedir.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

Merhaba ana şablonda sözdizimi aşağıdaki hello ile bu verileri kullanabilirsiniz:

    "[reference('master-node').outputs.masterip.value]"

Bu ifadede hello çıkışları bölüm veya hello kaynakları hello ana şablon bölümünü kullanabilirsiniz. Merhaba ifade hello değişkenler bölümünde kullanamazsınız, çünkü hello çalışma zamanı durumuna dayanır. tooreturn bu değer şablondan hello ana kullanın:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Bağlantılı şablonu tooreturn veri diski bir sanal makine için bölüm hello kullanma örneği çıkarır için bkz: [bir sanal makine için birden fazla veri diski oluşturma](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Sanal makine için kimlik doğrulama ayarlarını tanımlayın
Merhaba kullanabileceğiniz yapılandırma ayarları toospecify hello kimlik doğrulama ayarları bir sanal makine için daha önce gösterilen aynı düzeni. Parametre geçirme için kimlik doğrulama hello türünü oluşturun.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Merhaba farklı kimlik doğrulama türleri ve hangi tür hello parametresinin hello değere göre bu dağıtım için kullanılan bir değişken toostore değişkenleri ekleyin.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Merhaba sanal makine tanımlarken hello ayarlamak **osProfile** oluşturduğunuz toohello değişkeni.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Sonraki adımlar
* toolearn hello şablon hello bölümlerini hakkında bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md)
* bir şablonu içinde kullanılabilir toosee hello işlevleri bkz [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md)
