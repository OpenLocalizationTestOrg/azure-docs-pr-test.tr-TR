---
title: "aaaDeploy MSDeploy ile ana bilgisayar adı ve ssl sertifikasını kullanarak bir web uygulaması"
description: "Bir Azure Resource Manager şablonu toodeploy MSDeploy kullanarak ve özel ana bilgisayar adı ve bir SSL sertifikası ayarlama bir web uygulaması kullanın"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>MSDeploy, özel ana bilgisayar adı ve SSL sertifikası ile bir web uygulaması dağıtma
Bu kılavuzda, bir uçtan uca dağıtımı için bir Azure Web uygulaması oluşturma, MSDeploy yararlanarak yanı sıra aracılığıyla özel bir ana bilgisayar adı ve bir SSL sertifikası toohello ARM şablonu ekleme anlatılmaktadır.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Örnek uygulaması oluşturma
ASP.NET web uygulaması dağıtma. Merhaba ilk adımı toocreate basit bir web uygulaması (veya mevcut bir toouse seçebilir - bu durumda, bu adımı atlayabilirsiniz).

Visual Studio 2015'ni açın ve Dosya > Yeni proje. Görüntülenen hello iletişim kutusunda Web seçin > ASP.NET Web uygulaması. Şablonlar altında Web seçin ve hello MVC şablonu seçin. Seçin *kimlik doğrulama türünü değiştirin* çok*doğrulaması yok*. Bu yalnızca toomake hello örnek olarak basit uygulamasıdır.

Bu noktada, dağıtım işleminin bir parçası bir temel ASP.Net web uygulaması hazır toouse sahip olur.

### <a name="create-msdeploy-package"></a>MSDeploy paketi oluşturma
Toocreate hello paket toodeploy hello web uygulama tooAzure sonraki adımdır. toodo Bu, projeyi kaydedin ve ardından hello aşağıdaki hello komut satırından çalıştırın:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Bu hello PackageLocation klasörü altında bir sıkıştırılmış paket oluşturur. Merhaba uygulama şimdi bir Azure Resource Manager şablonu toodo şimdi oluşturabilirsiniz dağıtıldı, toobe hazır olmasını.

### <a name="create-arm-template"></a>ARM şablonu oluşturma
İlk olarak, bir web uygulaması ve bir barındırma planı (parametreler ve değişkenler okumanızdır gösterilmez unutmayın) oluşturacak temel bir ARM şablonu ile başlayalım.

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

Ardından, toomodify hello web uygulaması kaynak tootake iç içe geçmiş MSDeploy kaynak gerekir. Bu, daha önce oluşturduğunuz, tooreference hello paketin izin ve Azure Resource Manager toouse MSDeploy toodeploy hello paket toohello Azure WebApp söyleyin. Merhaba aşağıdaki iç içe geçmiş hello MSDeploy kaynakla hello Microsoft.Web/sites kaynak gösterir:

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

Bu hello MSDeploy kaynak alır fark edeceksiniz artık bir **packageUri** şu şekilde tanımlanır özelliği:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Bu **packageUri** hello noktaları toohello depolama hesabını burada karşıya yüklediğiniz paketi zip için depolama hesabı URI alır. Hello Azure Resource Manager özelliğinden yararlanır [paylaşılan erişim imzaları](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello paketinden aşağı hello şablonu dağıttığınızda yerel olarak hello depolama hesabı. Bu işlem hello paketini karşıya yükleyin ve istenen hello Azure yönetim API'si toocreate hello anahtarları çağırın ve bu hello şablon içine parametreler olarak geçirin bir PowerShell komut dosyası aracılığıyla otomatik (*_artifactsLocation* ve *_artifactsLocationSasToken*). Filename hello paketidir karşıya yüklenen toounder hello depolama kapsayıcısı ve toodefine parametreleri için başlangıç klasörü gerekir.

Ardından başka bir iç içe kaynak toosetup hello konak adı bağlamaları tooleverage özel bir etki alanı içinde tooadd gerekir. Şunları yapacaksınız kendi hello ana bilgisayar adı ve toobe ayarlayın ilk gerek tooensure size ait olduğu Azure tarafından doğrulanan - bkz [Azure App Service'te özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md). Bu yapıldığında tooyour şablonu hello Microsoft.Web/sites kaynak bölümü altında aşağıdaki hello ekleyebilirsiniz:

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

Son olarak başka bir üst düzey kaynak, Microsoft.Web/certificates tooadd gerekir. Bu kaynak SSL sertifikanızı içerir ve aynı web uygulamanızı olarak düzeyi ve barındırma planı hello yer alır.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

Toohave sipariş tooset bu kaynağını içinde geçerli bir SSL sertifikası gerekir. Daha sonra bu geçerli bir sertifikası edindikten sonra bir base64 dizesi olarak tooextract hello pfx bayt gerekir. Bir seçenek tooextract bu PowerShell komutunu aşağıdaki toouse hello olur:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Bu parametre tooyour ARM dağıtım şablonu olarak sonra geçirebilirdiniz.

Bu noktada hello ARM şablonu hazırdır.

### <a name="deploy-template"></a>Şablon dağıtma
Son adımlar hello toopiece bu tüm baştan sona tam dağıtım birbirine. toomake dağıtım hello yararlanabilirsiniz daha kolay **dağıtma AzureResourceGroup.ps1** Visual Studio toohelp gerekli yapıların karşıya yükleme ile bir Azure kaynak grubu projesi oluşturduğunuzda, eklediğiniz PowerShell Betiği Merhaba şablonu. Önceden toouse istediğiniz bir depolama hesabı oluşturuldu toohave gerektirir. Bu örnekte, karşıya hello package.zip toobe için bir paylaşılan depolama hesabı oluşturdum. Merhaba betik AzCopy tooupload hello paket toohello depolama hesabı özelliğinden yararlanır. Yapı klasörü konumunuz geçirebilir ve hello betik depolama kapsayıcısı adlı bu dizin toohello içindeki tüm dosyaları otomatik olarak yükler. Dağıtma-AzureResourceGroup.ps1 çağrıldıktan sonra toothen güncelleştirme hello SSL bağlamaları toomap hello özel ana bilgisayar adı, SSL sertifikası ile sahip.

PowerShell gösterir aşağıdaki hello hello tam dağıtım arama hello dağıtma-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

Bu noktada, uygulamanız dağıtıldıktan ve mümkün toobrowse tooit https://www.yourcustomdomain.com aracılığıyla olmalıdır

