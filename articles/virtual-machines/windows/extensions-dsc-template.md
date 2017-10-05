---
title: "İstenen durum yapılandırması Resource Manager şablonu | Microsoft Docs"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="352ef-103">Windows VMSS ve Azure Resource Manager şablonları ile istenen durum yapılandırması</span><span class="sxs-lookup"><span data-stu-id="352ef-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="352ef-104">Bu makalede Resource Manager şablonu [istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="352ef-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="352ef-105">Bir Windows VM için şablon örneği</span><span class="sxs-lookup"><span data-stu-id="352ef-105">Template example for a Windows VM</span></span>
<span data-ttu-id="352ef-106">Aşağıdaki kod parçacığında, şablonu kaynak bölüme gider.</span><span class="sxs-lookup"><span data-stu-id="352ef-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="352ef-107">Windows VMSS şablonu Örneğin</span><span class="sxs-lookup"><span data-stu-id="352ef-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="352ef-108">Bir VMSS düğümün "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle vardır.</span><span class="sxs-lookup"><span data-stu-id="352ef-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="352ef-109">DSC "Uzantılar altında" eklenir.</span><span class="sxs-lookup"><span data-stu-id="352ef-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="352ef-110">Ayrıntılı ayarları bilgileri</span><span class="sxs-lookup"><span data-stu-id="352ef-110">Detailed Settings Information</span></span>
<span data-ttu-id="352ef-111">Bir Azure Resource Manager şablonu Azure DSC uzantı ayarları bölümü aşağıdaki şema içindir.</span><span class="sxs-lookup"><span data-stu-id="352ef-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="352ef-112">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="352ef-112">Details</span></span>
| <span data-ttu-id="352ef-113">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="352ef-113">Property Name</span></span> | <span data-ttu-id="352ef-114">Tür</span><span class="sxs-lookup"><span data-stu-id="352ef-114">Type</span></span> | <span data-ttu-id="352ef-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="352ef-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="352ef-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="352ef-116">settings.wmfVersion</span></span> |<span data-ttu-id="352ef-117">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-117">string</span></span> |<span data-ttu-id="352ef-118">VM üzerinde yüklenmesi gereken Windows Management Framework'ün sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="352ef-119">Bu özellik için 'Son' yükler WMF en güncel sürümünü ayarlama.</span><span class="sxs-lookup"><span data-stu-id="352ef-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="352ef-120">Bu özellik için yalnızca geçerli olası değerler **'4.0', '5.0', ' 5.0PP' ve 'Son'**.</span><span class="sxs-lookup"><span data-stu-id="352ef-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="352ef-121">Olası değerler tabi güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="352ef-121">These possible values are subject to updates.</span></span> <span data-ttu-id="352ef-122">'Son' varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="352ef-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="352ef-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="352ef-123">settings.configuration.url</span></span> |<span data-ttu-id="352ef-124">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-124">string</span></span> |<span data-ttu-id="352ef-125">DSC yapılandırması zip dosyasını karşıdan yüklemek URL konumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="352ef-126">Sağlanan URL erişim için bir SAS belirteci gerektiriyorsa, protectedSettings.configurationUrlSasToken özelliği, SAS belirteci değerine ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="352ef-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="352ef-127">Settings.Configuration.Script ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="352ef-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="352ef-128">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="352ef-128">settings.configuration.script</span></span> |<span data-ttu-id="352ef-129">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-129">string</span></span> |<span data-ttu-id="352ef-130">DSC yapılandırması tanımını içeren komut dosyasının dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="352ef-131">Bu komut dosyası configuration.url özelliği tarafından belirtilen URL'den indirilen ZIP dosyasının kök dizininde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="352ef-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="352ef-132">Settings.Configuration.URL ve/veya settings.configuration.script tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="352ef-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="352ef-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="352ef-133">settings.configuration.function</span></span> |<span data-ttu-id="352ef-134">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-134">string</span></span> |<span data-ttu-id="352ef-135">DSC yapılandırması adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="352ef-136">Adlı yapılandırmasını configuration.script tarafından tanımlanan komut dosyasında yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="352ef-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="352ef-137">Settings.Configuration.URL ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="352ef-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="352ef-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="352ef-138">settings.configurationArguments</span></span> |<span data-ttu-id="352ef-139">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="352ef-139">Collection</span></span> |<span data-ttu-id="352ef-140">DSC yapılandırmanızı geçirmek istediğiniz herhangi bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="352ef-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="352ef-141">Bu özellik şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="352ef-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="352ef-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="352ef-142">settings.configurationData.url</span></span> |<span data-ttu-id="352ef-143">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-143">string</span></span> |<span data-ttu-id="352ef-144">DSC yapılandırmanız için giriş olarak kullanmak için yapılandırma verileri (.psd1) dosyanızı indirileceği URL'yi belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="352ef-145">Sağlanan URL erişim için bir SAS belirteci gerektiriyorsa, protectedSettings.configurationDataUrlSasToken özelliği, SAS belirteci değerine ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="352ef-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="352ef-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="352ef-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="352ef-147">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-147">string</span></span> |<span data-ttu-id="352ef-148">Etkinleştirir veya telemetri koleksiyonunu devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="352ef-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="352ef-149">Bu özellik yalnızca olası değerler **'Etkinleştir', 'Devre dışı', '', veya $null**.</span><span class="sxs-lookup"><span data-stu-id="352ef-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="352ef-150">Bu özellik boş ya da boş bırakarak telemetri sağlar.</span><span class="sxs-lookup"><span data-stu-id="352ef-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="352ef-151">Varsayılan değer ''.</span><span class="sxs-lookup"><span data-stu-id="352ef-151">The default value is ''.</span></span> [<span data-ttu-id="352ef-152">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="352ef-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="352ef-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="352ef-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="352ef-154">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="352ef-154">Collection</span></span> |<span data-ttu-id="352ef-155">WMF indirileceği alternatif konumlar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="352ef-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="352ef-156">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="352ef-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="352ef-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="352ef-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="352ef-158">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="352ef-158">Collection</span></span> |<span data-ttu-id="352ef-159">DSC yapılandırmanızı geçirmek istediğiniz herhangi bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="352ef-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="352ef-160">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="352ef-160">This property is encrypted.</span></span> |
| <span data-ttu-id="352ef-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="352ef-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="352ef-162">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-162">string</span></span> |<span data-ttu-id="352ef-163">Configuration.URL tarafından tanımlanan URL'yi erişmek için SAS belirteci belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="352ef-164">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="352ef-164">This property is encrypted.</span></span> |
| <span data-ttu-id="352ef-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="352ef-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="352ef-166">Dize</span><span class="sxs-lookup"><span data-stu-id="352ef-166">string</span></span> |<span data-ttu-id="352ef-167">ConfigurationData.url tarafından tanımlanan URL'yi erişmek için SAS belirteci belirtir.</span><span class="sxs-lookup"><span data-stu-id="352ef-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="352ef-168">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="352ef-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="352ef-169">Ayarları vs. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="352ef-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="352ef-170">Tüm ayarlar, VM'de ayarlarını metin dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="352ef-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="352ef-171">Ayarları metin dosyasında şifrelenmediğinden Özellikleri 'ayarlarında' ortak özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="352ef-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="352ef-172">Özellikleri 'protectedSettings' altında bir sertifika ile şifrelenir ve bu dosyayı VM düz metinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="352ef-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="352ef-173">Yapılandırma kimlik bilgileri gerektiriyorsa, protectedSettings içinde eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="352ef-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="352ef-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="352ef-174">Example</span></span>
<span data-ttu-id="352ef-175">Aşağıdaki örnekte "Başlarken" bölümünden türetilen [DSC uzantısı işleyici genel bakış sayfasında](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="352ef-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="352ef-176">Bu örnek uzantısını dağıtmak için cmdlet'leri yerine Resource Manager şablonları kullanır.</span><span class="sxs-lookup"><span data-stu-id="352ef-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="352ef-177">"IisInstall.ps1" yapılandırmasını kaydetmek, yerleştirileceği bir. ZIP dosyası ve erişilebilir bir URL dosyayı karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="352ef-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="352ef-178">Bu örnek, Azure blob depolama kullanır, ancak karşıdan yüklemek mümkündür. Herhangi bir rastgele konumdan ZIP dosyaları.</span><span class="sxs-lookup"><span data-stu-id="352ef-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="352ef-179">Azure Resource Manager şablonunda VM doğru dosyasını indirin ve uygun PowerShell işlevi çalıştırmak için aşağıdaki kodu bildirir:</span><span class="sxs-lookup"><span data-stu-id="352ef-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="352ef-180">Önceki biçimden güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="352ef-180">Updating from the Previous Format</span></span>
<span data-ttu-id="352ef-181">Önceki biçiminde (ortak özellikler ModulesUrl, ConfigurationFunction, SasToken veya özellikler içeren) otomatik olarak herhangi bir ayarı geçerli biçimine uyum ve yalnızca bunlar önce yaptığınız gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="352ef-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="352ef-182">Aşağıdaki şema gibi Aranan hangi önceki ayarları şeması şöyledir:</span><span class="sxs-lookup"><span data-stu-id="352ef-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="352ef-183">Önceki biçimi geçerli biçimine nasıl uyum aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="352ef-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="352ef-184">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="352ef-184">Property Name</span></span> | <span data-ttu-id="352ef-185">Önceki şema eşdeğerine</span><span class="sxs-lookup"><span data-stu-id="352ef-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="352ef-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="352ef-186">settings.wmfVersion</span></span> |<span data-ttu-id="352ef-187">Ayarlar. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="352ef-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="352ef-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="352ef-188">settings.configuration.url</span></span> |<span data-ttu-id="352ef-189">Ayarlar. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="352ef-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="352ef-190">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="352ef-190">settings.configuration.script</span></span> |<span data-ttu-id="352ef-191">Ayarları ilk kısmı. ConfigurationFunction (önce '\\\\')</span><span class="sxs-lookup"><span data-stu-id="352ef-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="352ef-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="352ef-192">settings.configuration.function</span></span> |<span data-ttu-id="352ef-193">Ayarları ikinci bölümü. ConfigurationFunction (sonra '\\\\')</span><span class="sxs-lookup"><span data-stu-id="352ef-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="352ef-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="352ef-194">settings.configurationArguments</span></span> |<span data-ttu-id="352ef-195">Ayarlar. Özellikleri</span><span class="sxs-lookup"><span data-stu-id="352ef-195">settings.Properties</span></span> |
| <span data-ttu-id="352ef-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="352ef-196">settings.configurationData.url</span></span> |<span data-ttu-id="352ef-197">protectedSettings.DataBlobUri (olmadan, SAS belirteci)</span><span class="sxs-lookup"><span data-stu-id="352ef-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="352ef-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="352ef-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="352ef-199">Ayarlar. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="352ef-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="352ef-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="352ef-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="352ef-201">Ayarlar. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="352ef-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="352ef-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="352ef-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="352ef-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="352ef-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="352ef-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="352ef-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="352ef-205">Ayarlar. SasToken</span><span class="sxs-lookup"><span data-stu-id="352ef-205">settings.SasToken</span></span> |
| <span data-ttu-id="352ef-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="352ef-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="352ef-207">SAS belirteci protectedSettings.DataBlobUri gelen</span><span class="sxs-lookup"><span data-stu-id="352ef-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="352ef-208">Sorun giderme - 1100 hata kodu</span><span class="sxs-lookup"><span data-stu-id="352ef-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="352ef-209">Hata kodu 1100 DSC uzantısı için kullanıcı girişi ile ilgili bir sorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="352ef-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="352ef-210">Bu hataların metin değişkendir ve değişebilir.</span><span class="sxs-lookup"><span data-stu-id="352ef-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="352ef-211">İçine çalışabilir hataları ve bunları düzeltmek nasıl bazıları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="352ef-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="352ef-212">Geçersiz değerler</span><span class="sxs-lookup"><span data-stu-id="352ef-212">Invalid Values</span></span>
<span data-ttu-id="352ef-213">"Privacy.dataCollection '{0}' dir.</span><span class="sxs-lookup"><span data-stu-id="352ef-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="352ef-214">Yalnızca olası değerler şunlardır: '' 'Enable' ve 'Disable' ""WmfVersion olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="352ef-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="352ef-215">Yalnızca olası değerler şunlardır:...</span><span class="sxs-lookup"><span data-stu-id="352ef-215">Only possible values are …</span></span> <span data-ttu-id="352ef-216">ve 'Son' "</span><span class="sxs-lookup"><span data-stu-id="352ef-216">and 'latest'"</span></span>

<span data-ttu-id="352ef-217">Sorun: Sağlanan değerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="352ef-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="352ef-218">Çözüm: geçersiz değer geçerli bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="352ef-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="352ef-219">Ayrıntılar bölümündeki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="352ef-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="352ef-220">Geçersiz URL</span><span class="sxs-lookup"><span data-stu-id="352ef-220">Invalid URL</span></span>
<span data-ttu-id="352ef-221">"ConfigurationData.url '{0}' dir.</span><span class="sxs-lookup"><span data-stu-id="352ef-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="352ef-222">Bu geçerli bir URL değil""DataBlobUri olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="352ef-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="352ef-223">Bu geçerli bir URL değil""Configuration.url olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="352ef-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="352ef-224">Bu geçerli bir URL değil"</span><span class="sxs-lookup"><span data-stu-id="352ef-224">This is not a valid URL"</span></span>

<span data-ttu-id="352ef-225">Sorun: Bir URL geçerli değil sağlanan.</span><span class="sxs-lookup"><span data-stu-id="352ef-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="352ef-226">Çözüm: sağlanan tüm URL'leri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="352ef-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="352ef-227">Tüm URL'leri geçerli konumlara uzantısı uzak makinede erişebilmesini çözmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="352ef-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="352ef-228">Geçersiz ConfigurationArgument türü</span><span class="sxs-lookup"><span data-stu-id="352ef-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="352ef-229">"Geçersiz configurationArguments türü {0}"</span><span class="sxs-lookup"><span data-stu-id="352ef-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="352ef-230">Sorun: Bir Hashtable nesnesine ConfigurationArguments özelliği çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="352ef-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="352ef-231">Çözüm: bir karma tablosu ConfigurationArguments özelliğinizi olun.</span><span class="sxs-lookup"><span data-stu-id="352ef-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="352ef-232">Önceki örnekte sağlanan biçimi izler.</span><span class="sxs-lookup"><span data-stu-id="352ef-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="352ef-233">Tırnak işareti, virgül ve küme ayraçları dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="352ef-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="352ef-234">Yinelenen ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="352ef-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="352ef-235">"Bağımsız değişken yinelenen '{0}' hem genel hem de korumalı configurationArguments bulunamadı"</span><span class="sxs-lookup"><span data-stu-id="352ef-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="352ef-236">Sorun: Genel Ayarları'nda ConfigurationArguments ve korumalı ayarlarında ConfigurationArguments aynı ada sahip özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="352ef-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="352ef-237">Çözüm: Yinelenen özellikler birini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="352ef-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="352ef-238">Özellikler eksik</span><span class="sxs-lookup"><span data-stu-id="352ef-238">Missing Properties</span></span>
<span data-ttu-id="352ef-239">"Configuration.function configuration.url veya configuration.module belirtilmesini gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="352ef-240">"Bu configuration.script belirtilen Configuration.url gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="352ef-241">"Bu configuration.url belirtilen Configuration.script gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="352ef-242">"Bu configuration.function belirtilen Configuration.url gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="352ef-243">"Bu configuration.url belirtilen ConfigurationUrlSasToken gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="352ef-244">"Bu configurationData.url belirtilen ConfigurationDataUrlSasToken gerektirir"</span><span class="sxs-lookup"><span data-stu-id="352ef-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="352ef-245">Sorun: Tanımlanmış bir özelliği eksik olan başka bir özellik olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="352ef-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="352ef-246">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="352ef-246">Solutions:</span></span> 

* <span data-ttu-id="352ef-247">Eksik özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="352ef-247">Provide the missing property.</span></span>
* <span data-ttu-id="352ef-248">Eksik özellik olması gerekiyor özelliğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="352ef-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="352ef-249">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="352ef-249">Next Steps</span></span>
<span data-ttu-id="352ef-250">DSC hakkında bilgi edinin ve sanal makine ölçek kümelerinin de [sanal makine ölçek kümeleri kullanma Azure DSC uzantısı](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="352ef-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="352ef-251">Daha fazla ayrıntı bulabilirsiniz [DSC'SİNİN güvenli kimlik bilgileri yönetimi](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="352ef-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="352ef-252">Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı işleyici giriş](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="352ef-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="352ef-253">PowerShell DSC hakkında daha fazla bilgi için [PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="352ef-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

