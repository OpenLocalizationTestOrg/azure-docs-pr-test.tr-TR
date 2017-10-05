---
title: "Ana bilgisayar adı ve ssl sertifikasıyla MSDeploy kullanarak bir web uygulaması dağıtma"
description: "Özel ana bilgisayar adı ve bir SSL sertifikası ayarlama ve MSDeploy kullanarak bir web uygulaması dağıtmak için bir Azure Resource Manager şablonu kullanın"
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
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>MSDeploy, özel ana bilgisayar adı ve SSL sertifikası ile bir web uygulaması dağıtma
Bu kılavuzda bir uçtan uca dağıtımı için bir Azure Web uygulaması oluşturma, MSDeploy yararlanarak yanı sıra ARM şablonu için özel bir ana bilgisayar adı ve bir SSL sertifikası ekleme anlatılmaktadır.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Örnek uygulaması oluşturma
ASP.NET web uygulaması dağıtma. Basit bir web uygulaması oluşturmak için ilk adımdır (veya mevcut bir kullanmayı seçebilir - bu durumda, bu adımı atlayabilirsiniz).

Visual Studio 2015'ni açın ve Dosya > Yeni proje. Görüntülenen iletişim kutusunda Web seçin > ASP.NET Web uygulaması. Şablonlar altında Web seçin ve MVC şablonunu seçin. Seçin *kimlik doğrulama türünü değiştirin* için *doğrulaması yok*. Bu örnek uygulama yalnızca kadar basit hale getirmektir.

Bu noktada, temel bir ASP.Net web uygulama dağıtım işleminin bir parçası kullanıma hazır olacaktır.

### <a name="create-msdeploy-package"></a>MSDeploy paketi oluşturma
Sonraki adım, Azure için web uygulaması dağıtmak için paketi oluşturmaktır. Bunu yapmak için projeyi kaydedin ve ardından aşağıdaki komut satırından çalıştırın:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Bu PackageLocation klasörü altında bir sıkıştırılmış paket oluşturur. Uygulama, bunu yapmak için bir Azure Resource Manager şablonunu şimdi oluşturabilirsiniz dağıtılması hazır.

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

Ardından, bir iç içe geçmiş MSDeploy kaynağı olabilmesi için web uygulaması kaynak değiştirmeniz gerekir. Bu, paketi daha önce oluşturduğunuz ve Azure Resource Manager'ı Azure WebApp paketi dağıtmak için MSDeploy kullanılacak söyleyin başvurusuna izin verir. İç içe geçmiş MSDeploy kaynak Microsoft.Web/sites kaynakla gösterir:

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

MSDeploy kaynak sürdüğünü fark edeceksiniz artık bir **packageUri** şu şekilde tanımlanır özelliği:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Bu **packageUri** için paketi zip burada yükler depolama hesabına işaret depolama hesabı URI alır. Azure Resource Manager özelliğinden yararlanır [paylaşılan erişim imzaları](../storage/common/storage-dotnet-shared-access-signature-part-1.md) şablonu dağıttığınız zaman paketi yerel olarak depolama hesabından çekmesini. Bu işlem paketini karşıya yükleyin ve gerekli anahtarlar oluşturmak için Azure yönetim API çağrısı ve bu şablonu içine parametreler olarak geçirin bir PowerShell komut dosyası aracılığıyla otomatik (*_artifactsLocation* ve *_ artifactsLocationSasToken*). Klasörü parametrelerini tanımlamanız gerekir ve filename paket depolama kapsayıcısı altında yüklenir.

Sonraki özel bir etki alanı yararlanmak için konak adı bağlamaları kurulumu için başka bir iç içe kaynak eklemeniz gerekir. İlk ana bilgisayar adı ve bunun size - ait olduğu Azure tarafından doğrulanacak bkz kümesi sahip olmak gerekir [Azure App Service'te özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md). Bu yapıldığında, şablonu Microsoft.Web/sites kaynak bölümü altında aşağıdaki ekleyebilirsiniz:

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

Son olarak başka bir üst düzey kaynak Microsoft.Web/certificates eklemeniz gerekir. Bu kaynak SSL sertifikanızı içerir ve web uygulaması ve barındırma planı aynı düzeyde yer alır.

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

Bu kaynağı ayarladıysanız için geçerli bir SSL sertifikası olması gerekir. Bu geçerli bir sertifikası edindikten sonra bir base64 dizesi olarak pfx bayt ayıklamak gerekir. Bu ayıklamak için bir seçenek aşağıdaki PowerShell komutunu kullanmaktır:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Ardından bu parametre olarak ARM dağıtım şablonu geçirebilirdiniz.

Bu noktada ARM şablonu hazırdır.

### <a name="deploy-template"></a>Şablon dağıtma
Bu tam uçtan uca dağıtımı ile birlikte tüm parçası için son adımlardır bakın. Yararlanabilirsiniz dağıtımı daha kolay yapmak için **dağıtma AzureResourceGroup.ps1** gerekli yapıların karşıya yükleme ile yardımcı olmak için Visual Studio'da bir Azure kaynak grubu projesi oluşturduğunuzda eklediğiniz PowerShell Betiği Şablon. Önceden kullanmak istediğiniz bir depolama hesabı oluşturmuş olmanız gerekir. Bu örnekte, yüklenecek package.zip için bir paylaşılan depolama hesabı oluşturdum. Komut dosyası depolama hesabına paketini karşıya yüklemek için AzCopy özelliğinden yararlanır. Yapı klasörü konumunuz geçirebilir ve komut dosyası adlı depolama kapsayıcısı için otomatik olarak bu dizindeki tüm dosyaları karşıya yükler. Dağıtma-AzureResourceGroup.ps1 çağrıldıktan sonra özel ana bilgisayar adı, SSL sertifikası ile eşlemek için SSL bağlamaları güncelleştirmeniz gerekir.

Aşağıdaki PowerShell dağıtma çağırma tam dağıtım gösterir-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

Bu noktada, uygulamanız dağıtıldıktan ve https://www.yourcustomdomain.com göz olmalıdır

