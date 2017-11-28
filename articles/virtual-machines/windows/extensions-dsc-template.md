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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="a19b3-103">Windows VMSS ve Azure Resource Manager şablonları ile istenen durum yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a19b3-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="a19b3-104">Bu makalede hello Resource Manager şablonu hello için [istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a19b3-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="a19b3-105">Bir Windows VM için şablon örneği</span><span class="sxs-lookup"><span data-stu-id="a19b3-105">Template example for a Windows VM</span></span>
<span data-ttu-id="a19b3-106">Merhaba aşağıdaki kod parçacığında kaynak bölümü hello şablonunun hello gider.</span><span class="sxs-lookup"><span data-stu-id="a19b3-106">hello following snippet goes into hello Resource section of hello template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="a19b3-107">Windows VMSS şablonu Örneğin</span><span class="sxs-lookup"><span data-stu-id="a19b3-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="a19b3-108">Bir VMSS düğümün hello "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle vardır.</span><span class="sxs-lookup"><span data-stu-id="a19b3-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="a19b3-109">DSC "Uzantılar altında" eklenir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="a19b3-110">Ayrıntılı ayarları bilgileri</span><span class="sxs-lookup"><span data-stu-id="a19b3-110">Detailed Settings Information</span></span>
<span data-ttu-id="a19b3-111">Merhaba aşağıdaki şema hello Azure DSC uzantısı'nda bir Azure Resource Manager şablonu hello ayarları bölümü içindir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="a19b3-112">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="a19b3-112">Details</span></span>
| <span data-ttu-id="a19b3-113">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="a19b3-113">Property Name</span></span> | <span data-ttu-id="a19b3-114">Tür</span><span class="sxs-lookup"><span data-stu-id="a19b3-114">Type</span></span> | <span data-ttu-id="a19b3-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a19b3-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a19b3-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a19b3-116">settings.wmfVersion</span></span> |<span data-ttu-id="a19b3-117">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-117">string</span></span> |<span data-ttu-id="a19b3-118">Hello VM üzerinde yüklenmesi gereken bir Windows Management Framework'ün Hello sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="a19b3-119">Bu özellik too'latest ayarı ' yükler hello en güncel sürümünü WMF.</span><span class="sxs-lookup"><span data-stu-id="a19b3-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="a19b3-120">Bu özellik için yalnızca geçerli olası değerler Hello **'4.0', '5.0', ' 5.0PP' ve 'Son'**.</span><span class="sxs-lookup"><span data-stu-id="a19b3-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="a19b3-121">Konu tooupdates bu olası değerler.</span><span class="sxs-lookup"><span data-stu-id="a19b3-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="a19b3-122">Merhaba varsayılan değer 'Son' dir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="a19b3-123">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="a19b3-123">settings.configuration.url</span></span> |<span data-ttu-id="a19b3-124">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-124">string</span></span> |<span data-ttu-id="a19b3-125">Hangi toodownload Hello URL konumdan DSC yapılandırma zip dosyası belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="a19b3-126">Sağlanan hello URL erişim için bir SAS belirteci gerektiriyorsa, tooset hello protectedSettings.configurationUrlSasToken özelliği toohello değeri, SAS belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="a19b3-127">Settings.Configuration.Script ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a19b3-128">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="a19b3-128">settings.configuration.script</span></span> |<span data-ttu-id="a19b3-129">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-129">string</span></span> |<span data-ttu-id="a19b3-130">DSC yapılandırması hello tanımını içeren hello betik Hello dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="a19b3-131">Bu komut dosyası hello hello configuration.url özelliği tarafından belirtilen hello URL'den indirilen hello zip dosyasının kök klasöründe olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="a19b3-132">Settings.Configuration.URL ve/veya settings.configuration.script tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="a19b3-133">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="a19b3-133">settings.configuration.function</span></span> |<span data-ttu-id="a19b3-134">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-134">string</span></span> |<span data-ttu-id="a19b3-135">DSC yapılandırması Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="a19b3-136">adlı hello yapılandırması configuration.script tarafından tanımlanan hello komut dosyasında yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="a19b3-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="a19b3-137">Settings.Configuration.URL ve/veya settings.configuration.function tanımlanmışsa, bu özellik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a19b3-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a19b3-138">settings.configurationArguments</span></span> |<span data-ttu-id="a19b3-139">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="a19b3-139">Collection</span></span> |<span data-ttu-id="a19b3-140">Toopass tooyour DSC yapılandırması istediğiniz herhangi bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a19b3-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a19b3-141">Bu özellik şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="a19b3-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="a19b3-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a19b3-142">settings.configurationData.url</span></span> |<span data-ttu-id="a19b3-143">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-143">string</span></span> |<span data-ttu-id="a19b3-144">DSC yapılandırması için giriş olarak hangi toodownload yapılandırma verilerinizi (.psd1) toouse dosya hello URL'yi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="a19b3-145">Sağlanan hello URL erişim için bir SAS belirteci gerektiriyorsa, tooset hello protectedSettings.configurationDataUrlSasToken özelliği toohello değeri, SAS belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="a19b3-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a19b3-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a19b3-147">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-147">string</span></span> |<span data-ttu-id="a19b3-148">Etkinleştirir veya telemetri koleksiyonunu devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a19b3-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="a19b3-149">Merhaba yalnızca bu özellik için olası değerler: **'Etkinleştir', 'Devre dışı', '', veya $null**.</span><span class="sxs-lookup"><span data-stu-id="a19b3-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="a19b3-150">Bu özellik boş ya da boş bırakarak telemetri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a19b3-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="a19b3-151">Merhaba varsayılan değer ''.</span><span class="sxs-lookup"><span data-stu-id="a19b3-151">hello default value is ''.</span></span> [<span data-ttu-id="a19b3-152">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a19b3-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="a19b3-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a19b3-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a19b3-154">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="a19b3-154">Collection</span></span> |<span data-ttu-id="a19b3-155">Hangi toodownload WMF hello alternatif konumlar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a19b3-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="a19b3-156">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a19b3-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="a19b3-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a19b3-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a19b3-158">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="a19b3-158">Collection</span></span> |<span data-ttu-id="a19b3-159">Toopass tooyour DSC yapılandırması istediğiniz herhangi bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a19b3-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a19b3-160">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-160">This property is encrypted.</span></span> |
| <span data-ttu-id="a19b3-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a19b3-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a19b3-162">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-162">string</span></span> |<span data-ttu-id="a19b3-163">Configuration.URL tarafından tanımlanan hello SAS belirteci tooaccess hello URL'yi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="a19b3-164">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-164">This property is encrypted.</span></span> |
| <span data-ttu-id="a19b3-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a19b3-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a19b3-166">Dize</span><span class="sxs-lookup"><span data-stu-id="a19b3-166">string</span></span> |<span data-ttu-id="a19b3-167">ConfigurationData.url tarafından tanımlanan hello SAS belirteci tooaccess hello URL'yi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="a19b3-168">Bu özellik şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="a19b3-169">Ayarları vs. ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="a19b3-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="a19b3-170">Tüm ayarlar hello VM üzerinde ayarlarını metin dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="a19b3-171">Hello ayarları metin dosyasında şifrelenmediğinden Özellikleri 'ayarlarında' ortak özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="a19b3-172">Özellikleri 'protectedSettings' altında bir sertifika ile şifrelenir ve bu dosyayı hello VM düz metinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="a19b3-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="a19b3-173">Merhaba yapılandırma kimlik bilgileri gerektiriyorsa, protectedSettings içinde eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="a19b3-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="a19b3-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="a19b3-174">Example</span></span>
<span data-ttu-id="a19b3-175">Merhaba aşağıdaki örnek türetilen hello "Başlarken" bölümünden hello [DSC uzantısı işleyici genel bakış sayfasında](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a19b3-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="a19b3-176">Bu örnek cmdlet toodeploy hello uzantısı yerine Resource Manager şablonları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a19b3-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="a19b3-177">Merhaba "IisInstall.ps1" yapılandırmasını kaydetmek, yerleştirileceği bir. Dosya ve karşıya yükleme hello erişilebilir bir URL dosyasında ZIP.</span><span class="sxs-lookup"><span data-stu-id="a19b3-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="a19b3-178">Bu örnek, Azure blob depolama kullanır, ancak olası toodownload değil. Herhangi bir rastgele konumdan ZIP dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a19b3-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="a19b3-179">Hello Azure Resource Manager şablonunda hello aşağıdaki kodu hello VM toodownload hello doğru dosya bildirir ve hello uygun PowerShell işlevi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a19b3-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

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

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="a19b3-180">Önceki biçiminde Hello güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="a19b3-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="a19b3-181">Herhangi bir ayarı (Merhaba ortak özellikler ModulesUrl, ConfigurationFunction, SasToken veya özellikler içeren biçiminde) hello önceki otomatik olarak toohello geçerli biçim uyum ve yalnızca bunlar önce yaptığınız gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a19b3-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="a19b3-182">Şema aşağıdaki hello gibi Aranan hangi hello önceki ayarları şeması şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a19b3-182">hello following schema is what hello previous settings schema looked like:</span></span>

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

<span data-ttu-id="a19b3-183">Merhaba önceki biçimi toohello geçerli biçim nasıl uyum aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a19b3-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="a19b3-184">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="a19b3-184">Property Name</span></span> | <span data-ttu-id="a19b3-185">Önceki şema eşdeğerine</span><span class="sxs-lookup"><span data-stu-id="a19b3-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="a19b3-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a19b3-186">settings.wmfVersion</span></span> |<span data-ttu-id="a19b3-187">Ayarlar. WMFVersion</span><span class="sxs-lookup"><span data-stu-id="a19b3-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="a19b3-188">Settings.Configuration.URL</span><span class="sxs-lookup"><span data-stu-id="a19b3-188">settings.configuration.url</span></span> |<span data-ttu-id="a19b3-189">Ayarlar. ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="a19b3-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="a19b3-190">Settings.Configuration.Script</span><span class="sxs-lookup"><span data-stu-id="a19b3-190">settings.configuration.script</span></span> |<span data-ttu-id="a19b3-191">Ayarları ilk kısmı. ConfigurationFunction (önce '\\\\')</span><span class="sxs-lookup"><span data-stu-id="a19b3-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="a19b3-192">Settings.Configuration.Function</span><span class="sxs-lookup"><span data-stu-id="a19b3-192">settings.configuration.function</span></span> |<span data-ttu-id="a19b3-193">Ayarları ikinci bölümü. ConfigurationFunction (sonra '\\\\')</span><span class="sxs-lookup"><span data-stu-id="a19b3-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="a19b3-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a19b3-194">settings.configurationArguments</span></span> |<span data-ttu-id="a19b3-195">Ayarlar. Özellikleri</span><span class="sxs-lookup"><span data-stu-id="a19b3-195">settings.Properties</span></span> |
| <span data-ttu-id="a19b3-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a19b3-196">settings.configurationData.url</span></span> |<span data-ttu-id="a19b3-197">protectedSettings.DataBlobUri (olmadan, SAS belirteci)</span><span class="sxs-lookup"><span data-stu-id="a19b3-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="a19b3-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a19b3-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a19b3-199">Ayarlar. Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="a19b3-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="a19b3-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a19b3-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a19b3-201">Ayarlar. AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="a19b3-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="a19b3-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a19b3-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a19b3-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="a19b3-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="a19b3-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a19b3-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a19b3-205">Ayarlar. SasToken</span><span class="sxs-lookup"><span data-stu-id="a19b3-205">settings.SasToken</span></span> |
| <span data-ttu-id="a19b3-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a19b3-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a19b3-207">SAS belirteci protectedSettings.DataBlobUri gelen</span><span class="sxs-lookup"><span data-stu-id="a19b3-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="a19b3-208">Sorun giderme - 1100 hata kodu</span><span class="sxs-lookup"><span data-stu-id="a19b3-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="a19b3-209">Hata kodu 1100 hello kullanıcı girişi toohello DSC uzantısı ile ilgili bir sorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="a19b3-210">Bu hataların Hello metin değişkendir ve değişebilir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="a19b3-211">Merhaba hataları içine çalıştırabilir ve bunları düzeltmek nasıl bazıları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="a19b3-212">Geçersiz değerler</span><span class="sxs-lookup"><span data-stu-id="a19b3-212">Invalid Values</span></span>
<span data-ttu-id="a19b3-213">"Privacy.dataCollection '{0}' dir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="a19b3-214">Merhaba yalnızca olası değerler şunlardır: '' 'Enable' ve 'Disable' ""WmfVersion olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a19b3-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="a19b3-215">Yalnızca olası değerler şunlardır:...</span><span class="sxs-lookup"><span data-stu-id="a19b3-215">Only possible values are …</span></span> <span data-ttu-id="a19b3-216">ve 'Son' "</span><span class="sxs-lookup"><span data-stu-id="a19b3-216">and 'latest'"</span></span>

<span data-ttu-id="a19b3-217">Sorun: Sağlanan değerine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a19b3-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="a19b3-218">Çözüm: hello geçersiz değer tooa geçerli değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a19b3-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="a19b3-219">Merhaba ayrıntıları bölümü Hello tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="a19b3-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="a19b3-220">Geçersiz URL</span><span class="sxs-lookup"><span data-stu-id="a19b3-220">Invalid URL</span></span>
<span data-ttu-id="a19b3-221">"ConfigurationData.url '{0}' dir.</span><span class="sxs-lookup"><span data-stu-id="a19b3-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="a19b3-222">Bu geçerli bir URL değil""DataBlobUri olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a19b3-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="a19b3-223">Bu geçerli bir URL değil""Configuration.url olan '{0}'.</span><span class="sxs-lookup"><span data-stu-id="a19b3-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="a19b3-224">Bu geçerli bir URL değil"</span><span class="sxs-lookup"><span data-stu-id="a19b3-224">This is not a valid URL"</span></span>

<span data-ttu-id="a19b3-225">Sorun: Bir URL geçerli değil sağlanan.</span><span class="sxs-lookup"><span data-stu-id="a19b3-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="a19b3-226">Çözüm: sağlanan tüm URL'leri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a19b3-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="a19b3-227">Tüm URL'leri hello uzantısı hello uzak makinede erişebilirsiniz toovalid konumları çözmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="a19b3-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="a19b3-228">Geçersiz ConfigurationArgument türü</span><span class="sxs-lookup"><span data-stu-id="a19b3-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="a19b3-229">"Geçersiz configurationArguments türü {0}"</span><span class="sxs-lookup"><span data-stu-id="a19b3-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="a19b3-230">Sorun: Merhaba ConfigurationArguments özelliği tooa Hashtable nesnesi çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="a19b3-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="a19b3-231">Çözüm: bir karma tablosu ConfigurationArguments özelliğinizi olun.</span><span class="sxs-lookup"><span data-stu-id="a19b3-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="a19b3-232">Merhaba önceki örnekte sağlanan hello biçimi izler.</span><span class="sxs-lookup"><span data-stu-id="a19b3-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="a19b3-233">Tırnak işareti, virgül ve küme ayraçları dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a19b3-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="a19b3-234">Yinelenen ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="a19b3-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="a19b3-235">"Bağımsız değişken yinelenen '{0}' hem genel hem de korumalı configurationArguments bulunamadı"</span><span class="sxs-lookup"><span data-stu-id="a19b3-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="a19b3-236">Sorun: ConfigurationArguments ortak ayarlarında hello ve hello ConfigurationArguments korumalı ayarlarında içermelidir özellikleri hello ile aynı adı.</span><span class="sxs-lookup"><span data-stu-id="a19b3-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="a19b3-237">Çözüm: hello yinelenen özellikler birini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a19b3-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="a19b3-238">Özellikler eksik</span><span class="sxs-lookup"><span data-stu-id="a19b3-238">Missing Properties</span></span>
<span data-ttu-id="a19b3-239">"Configuration.function configuration.url veya configuration.module belirtilmesini gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="a19b3-240">"Bu configuration.script belirtilen Configuration.url gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="a19b3-241">"Bu configuration.url belirtilen Configuration.script gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="a19b3-242">"Bu configuration.function belirtilen Configuration.url gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="a19b3-243">"Bu configuration.url belirtilen ConfigurationUrlSasToken gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="a19b3-244">"Bu configurationData.url belirtilen ConfigurationDataUrlSasToken gerektirir"</span><span class="sxs-lookup"><span data-stu-id="a19b3-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="a19b3-245">Sorun: Tanımlanmış bir özelliği eksik olan başka bir özellik olması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a19b3-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="a19b3-246">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="a19b3-246">Solutions:</span></span> 

* <span data-ttu-id="a19b3-247">Merhaba eksik özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="a19b3-247">Provide hello missing property.</span></span>
* <span data-ttu-id="a19b3-248">Merhaba eksik özellik olması gerekiyor hello özelliğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a19b3-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a19b3-249">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a19b3-249">Next Steps</span></span>
<span data-ttu-id="a19b3-250">DSC hakkında bilgi edinin ve sanal makine ölçek kümelerinin de [sanal makine ölçek kümeleri kullanma hello Azure DSC uzantısı ile](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="a19b3-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="a19b3-251">Daha fazla ayrıntı bulabilirsiniz [DSC'SİNİN güvenli kimlik bilgileri yönetimi](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a19b3-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a19b3-252">Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a19b3-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a19b3-253">PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="a19b3-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

