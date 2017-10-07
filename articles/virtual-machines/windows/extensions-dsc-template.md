---
title: "aaaDesired durumu yapılandırma Resource Manager şablonu | Microsoft Docs"
description: "İstenen durum yapılandırması örnekleri içeren Azure ve sorun giderme için Resource Manager şablonu tanımı"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Windows VMSS ve Azure Resource Manager şablonları ile istenen durum yapılandırması
Bu makalede hello Resource Manager şablonu hello için [istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Bir Windows VM için şablon örneği
Merhaba aşağıdaki kod parçacığında kaynak bölümü hello şablonunun hello gider.

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a>Windows VMSS şablonu Örneğin
Bir VMSS düğümün hello "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle vardır. DSC "Uzantılar altında" eklenir. 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a>Ayrıntılı ayarları bilgileri
Merhaba aşağıdaki şema hello Azure DSC uzantısı'nda bir Azure Resource Manager şablonu hello ayarları bölümü içindir.

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a>Ayrıntılar
| Özellik adı | Tür | Açıklama |
| --- | --- | --- |
| settings.wmfVersion |Dize |Hello VM üzerinde yüklenmesi gereken bir Windows Management Framework'ün Hello sürümünü belirtir. Bu özellik too'latest ayarı ' yükler hello en güncel sürümünü WMF. Bu özellik için yalnızca geçerli olası değerler Hello **'4.0', '5.0', ' 5.0PP' ve 'Son'**. Konu tooupdates bu olası değerler. Merhaba varsayılan değer 'Son' dir. |
| Settings.Configuration.URL |Dize |Hangi toodownload Hello URL konumdan DSC yapılandırma zip dosyası belirtir. Sağlanan hello URL erişim için bir SAS belirteci gerektiriyorsa, tooset hello protectedSettings.configurationUrlSasToken özelliği toohello değeri, SAS belirteci gerekir. Settings.Configuration.Script ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir. |
| Settings.Configuration.Script |Dize |DSC yapılandırması hello tanımını içeren hello betik Hello dosya adını belirtir. Bu komut dosyası hello hello configuration.url özelliği tarafından belirtilen hello URL'den indirilen hello zip dosyasının kök klasöründe olması gerekir. Settings.Configuration.URL ve/veya settings.configuration.script tanımlanmışsa, bu özellik gereklidir. |
| Settings.Configuration.Function |Dize |DSC yapılandırması Hello adını belirtir. adlı hello yapılandırması configuration.script tarafından tanımlanan hello komut dosyasında yer almalıdır. Settings.Configuration.URL ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir. |
| settings.configurationArguments |Koleksiyon |Toopass tooyour DSC yapılandırması istediğiniz herhangi bir parametre tanımlar. Bu özellik şifrelenmez. |
| settings.configurationData.url |Dize |DSC yapılandırması için giriş olarak hangi toodownload yapılandırma verilerinizi (.psd1) toouse dosya hello URL'yi belirtir. Sağlanan hello URL erişim için bir SAS belirteci gerektiriyorsa, tooset hello protectedSettings.configurationDataUrlSasToken özelliği toohello değeri, SAS belirteci gerekir. |
| settings.privacy.dataEnabled |Dize |Etkinleştirir veya telemetri koleksiyonunu devre dışı bırakır. Merhaba yalnızca bu özellik için olası değerler: **'Etkinleştir', 'Devre dışı', '', veya $null**. Bu özellik boş ya da boş bırakarak telemetri sağlar. Merhaba varsayılan değer ''. [Daha fazla bilgi](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Koleksiyon |Hangi toodownload WMF hello alternatif konumlar tanımlar. [Daha fazla bilgi](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Koleksiyon |Toopass tooyour DSC yapılandırması istediğiniz herhangi bir parametre tanımlar. Bu özellik şifrelenir. |
| protectedSettings.configurationUrlSasToken |Dize |Configuration.URL tarafından tanımlanan hello SAS belirteci tooaccess hello URL'yi belirtir. Bu özellik şifrelenir. |
| protectedSettings.configurationDataUrlSasToken |Dize |ConfigurationData.url tarafından tanımlanan hello SAS belirteci tooaccess hello URL'yi belirtir. Bu özellik şifrelenir. |

## <a name="settings-vs-protectedsettings"></a>Ayarları vs. ProtectedSettings
Tüm ayarlar hello VM üzerinde ayarlarını metin dosyasına kaydedilir.
Hello ayarları metin dosyasında şifrelenmediğinden Özellikleri 'ayarlarında' ortak özelliklerdir.
Özellikleri 'protectedSettings' altında bir sertifika ile şifrelenir ve bu dosyayı hello VM düz metinde gösterilmez.

Merhaba yapılandırma kimlik bilgileri gerektiriyorsa, protectedSettings içinde eklenebilir:

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a>Örnek
Merhaba aşağıdaki örnek türetilen hello "Başlarken" bölümünden hello [DSC uzantısı işleyici genel bakış sayfasında](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Bu örnek cmdlet toodeploy hello uzantısı yerine Resource Manager şablonları kullanır. Merhaba "IisInstall.ps1" yapılandırmasını kaydetmek, yerleştirileceği bir. Dosya ve karşıya yükleme hello erişilebilir bir URL dosyasında ZIP. Bu örnek, Azure blob depolama kullanır, ancak olası toodownload değil. Herhangi bir rastgele konumdan ZIP dosyaları.

Hello Azure Resource Manager şablonunda hello aşağıdaki kodu hello VM toodownload hello doğru dosya bildirir ve hello uygun PowerShell işlevi çalıştırın:

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a>Önceki biçiminde Hello güncelleştiriliyor
Herhangi bir ayarı (Merhaba ortak özellikler ModulesUrl, ConfigurationFunction, SasToken veya özellikler içeren biçiminde) hello önceki otomatik olarak toohello geçerli biçim uyum ve yalnızca bunlar önce yaptığınız gibi çalıştırın.

Şema aşağıdaki hello gibi Aranan hangi hello önceki ayarları şeması şöyledir:

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

Merhaba önceki biçimi toohello geçerli biçim nasıl uyum aşağıda verilmiştir:

| Özellik adı | Önceki şema eşdeğerine |
| --- | --- |
| settings.wmfVersion |Ayarlar. WMFVersion |
| Settings.Configuration.URL |Ayarlar. ModulesUrl |
| Settings.Configuration.Script |Ayarları ilk kısmı. ConfigurationFunction (önce '\\\\') |
| Settings.Configuration.Function |Ayarları ikinci bölümü. ConfigurationFunction (sonra '\\\\') |
| settings.configurationArguments |Ayarlar. Özellikleri |
| settings.configurationData.url |protectedSettings.DataBlobUri (olmadan, SAS belirteci) |
| settings.privacy.dataEnabled |Ayarlar. Privacy.DataEnabled |
| settings.advancedOptions.downloadMappings |Ayarlar. AdvancedOptions.DownloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |Ayarlar. SasToken |
| protectedSettings.configurationDataUrlSasToken |SAS belirteci protectedSettings.DataBlobUri gelen |

## <a name="troubleshooting---error-code-1100"></a>Sorun giderme - 1100 hata kodu
Hata kodu 1100 hello kullanıcı girişi toohello DSC uzantısı ile ilgili bir sorun olduğunu gösterir.
Bu hataların Hello metin değişkendir ve değişebilir.
Merhaba hataları içine çalıştırabilir ve bunları düzeltmek nasıl bazıları aşağıda verilmiştir.

### <a name="invalid-values"></a>Geçersiz değerler
"Privacy.dataCollection '{0}' dir. Merhaba yalnızca olası değerler şunlardır: '' 'Enable' ve 'Disable' ""WmfVersion olan '{0}'. Yalnızca olası değerler şunlardır:... ve 'Son' "

Sorun: Sağlanan değerine izin verilmez.

Çözüm: hello geçersiz değer tooa geçerli değeri değiştirin. Merhaba ayrıntıları bölümü Hello tabloya bakın.

### <a name="invalid-url"></a>Geçersiz URL
"ConfigurationData.url '{0}' dir. Bu geçerli bir URL değil""DataBlobUri olan '{0}'. Bu geçerli bir URL değil""Configuration.url olan '{0}'. Bu geçerli bir URL değil"

Sorun: Bir URL geçerli değil sağlanan.

Çözüm: sağlanan tüm URL'leri denetleyin. Tüm URL'leri hello uzantısı hello uzak makinede erişebilirsiniz toovalid konumları çözmek emin olun.

### <a name="invalid-configurationargument-type"></a>Geçersiz ConfigurationArgument türü
"Geçersiz configurationArguments türü {0}"

Sorun: Merhaba ConfigurationArguments özelliği tooa Hashtable nesnesi çözümlenemiyor. 

Çözüm: bir karma tablosu ConfigurationArguments özelliğinizi olun. Merhaba önceki örnekte sağlanan hello biçimi izler. Tırnak işareti, virgül ve küme ayraçları dikkat edin.

### <a name="duplicate-configurationarguments"></a>Yinelenen ConfigurationArguments
"Bağımsız değişken yinelenen '{0}' hem genel hem de korumalı configurationArguments bulunamadı"

Sorun: ConfigurationArguments ortak ayarlarında hello ve hello ConfigurationArguments korumalı ayarlarında içermelidir özellikleri hello ile aynı adı.

Çözüm: hello yinelenen özellikler birini kaldırın.

### <a name="missing-properties"></a>Özellikler eksik
"Configuration.function configuration.url veya configuration.module belirtilmesini gerektirir"

"Bu configuration.script belirtilen Configuration.url gerektirir"

"Bu configuration.url belirtilen Configuration.script gerektirir"

"Bu configuration.function belirtilen Configuration.url gerektirir"

"Bu configuration.url belirtilen ConfigurationUrlSasToken gerektirir"

"Bu configurationData.url belirtilen ConfigurationDataUrlSasToken gerektirir"

Sorun: Tanımlanmış bir özelliği eksik olan başka bir özellik olması gerekiyor.

Çözüm: 

* Merhaba eksik özellik sağlar.
* Merhaba eksik özellik olması gerekiyor hello özelliğini kaldırın.

## <a name="next-steps"></a>Sonraki Adımlar
DSC hakkında bilgi edinin ve sanal makine ölçek kümelerinin de [sanal makine ölçek kümeleri kullanma hello Azure DSC uzantısı ile](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Daha fazla ayrıntı bulabilirsiniz [DSC'SİNİN güvenli kimlik bilgileri yönetimi](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview). 

