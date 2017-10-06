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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="a9adf-103">MSDeploy, özel ana bilgisayar adı ve SSL sertifikası ile bir web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="a9adf-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="a9adf-104">Bu kılavuzda, bir uçtan uca dağıtımı için bir Azure Web uygulaması oluşturma, MSDeploy yararlanarak yanı sıra aracılığıyla özel bir ana bilgisayar adı ve bir SSL sertifikası toohello ARM şablonu ekleme anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="a9adf-105">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a9adf-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="a9adf-106">Örnek uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9adf-106">Create Sample Application</span></span>
<span data-ttu-id="a9adf-107">ASP.NET web uygulaması dağıtma.</span><span class="sxs-lookup"><span data-stu-id="a9adf-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="a9adf-108">Merhaba ilk adımı toocreate basit bir web uygulaması (veya mevcut bir toouse seçebilir - bu durumda, bu adımı atlayabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="a9adf-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="a9adf-109">Visual Studio 2015'ni açın ve Dosya > Yeni proje.</span><span class="sxs-lookup"><span data-stu-id="a9adf-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="a9adf-110">Görüntülenen hello iletişim kutusunda Web seçin > ASP.NET Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a9adf-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="a9adf-111">Şablonlar altında Web seçin ve hello MVC şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="a9adf-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="a9adf-112">Seçin *kimlik doğrulama türünü değiştirin* çok*doğrulaması yok*.</span><span class="sxs-lookup"><span data-stu-id="a9adf-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="a9adf-113">Bu yalnızca toomake hello örnek olarak basit uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="a9adf-114">Bu noktada, dağıtım işleminin bir parçası bir temel ASP.Net web uygulaması hazır toouse sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a9adf-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="a9adf-115">MSDeploy paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9adf-115">Create MSDeploy package</span></span>
<span data-ttu-id="a9adf-116">Toocreate hello paket toodeploy hello web uygulama tooAzure sonraki adımdır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="a9adf-117">toodo Bu, projeyi kaydedin ve ardından hello aşağıdaki hello komut satırından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a9adf-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="a9adf-118">Bu hello PackageLocation klasörü altında bir sıkıştırılmış paket oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9adf-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="a9adf-119">Merhaba uygulama şimdi bir Azure Resource Manager şablonu toodo şimdi oluşturabilirsiniz dağıtıldı, toobe hazır olmasını.</span><span class="sxs-lookup"><span data-stu-id="a9adf-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="a9adf-120">ARM şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9adf-120">Create ARM Template</span></span>
<span data-ttu-id="a9adf-121">İlk olarak, bir web uygulaması ve bir barındırma planı (parametreler ve değişkenler okumanızdır gösterilmez unutmayın) oluşturacak temel bir ARM şablonu ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="a9adf-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="a9adf-122">Ardından, toomodify hello web uygulaması kaynak tootake iç içe geçmiş MSDeploy kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="a9adf-123">Bu, daha önce oluşturduğunuz, tooreference hello paketin izin ve Azure Resource Manager toouse MSDeploy toodeploy hello paket toohello Azure WebApp söyleyin.</span><span class="sxs-lookup"><span data-stu-id="a9adf-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="a9adf-124">Merhaba aşağıdaki iç içe geçmiş hello MSDeploy kaynakla hello Microsoft.Web/sites kaynak gösterir:</span><span class="sxs-lookup"><span data-stu-id="a9adf-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="a9adf-125">Bu hello MSDeploy kaynak alır fark edeceksiniz artık bir **packageUri** şu şekilde tanımlanır özelliği:</span><span class="sxs-lookup"><span data-stu-id="a9adf-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="a9adf-126">Bu **packageUri** hello noktaları toohello depolama hesabını burada karşıya yüklediğiniz paketi zip için depolama hesabı URI alır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="a9adf-127">Hello Azure Resource Manager özelliğinden yararlanır [paylaşılan erişim imzaları](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello paketinden aşağı hello şablonu dağıttığınızda yerel olarak hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a9adf-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="a9adf-128">Bu işlem hello paketini karşıya yükleyin ve istenen hello Azure yönetim API'si toocreate hello anahtarları çağırın ve bu hello şablon içine parametreler olarak geçirin bir PowerShell komut dosyası aracılığıyla otomatik (*_artifactsLocation* ve *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="a9adf-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="a9adf-129">Filename hello paketidir karşıya yüklenen toounder hello depolama kapsayıcısı ve toodefine parametreleri için başlangıç klasörü gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="a9adf-130">Ardından başka bir iç içe kaynak toosetup hello konak adı bağlamaları tooleverage özel bir etki alanı içinde tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="a9adf-131">Şunları yapacaksınız kendi hello ana bilgisayar adı ve toobe ayarlayın ilk gerek tooensure size ait olduğu Azure tarafından doğrulanan - bkz [Azure App Service'te özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a9adf-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="a9adf-132">Bu yapıldığında tooyour şablonu hello Microsoft.Web/sites kaynak bölümü altında aşağıdaki hello ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9adf-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="a9adf-133">Son olarak başka bir üst düzey kaynak, Microsoft.Web/certificates tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="a9adf-134">Bu kaynak SSL sertifikanızı içerir ve aynı web uygulamanızı olarak düzeyi ve barındırma planı hello yer alır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="a9adf-135">Toohave sipariş tooset bu kaynağını içinde geçerli bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="a9adf-136">Daha sonra bu geçerli bir sertifikası edindikten sonra bir base64 dizesi olarak tooextract hello pfx bayt gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="a9adf-137">Bir seçenek tooextract bu PowerShell komutunu aşağıdaki toouse hello olur:</span><span class="sxs-lookup"><span data-stu-id="a9adf-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="a9adf-138">Bu parametre tooyour ARM dağıtım şablonu olarak sonra geçirebilirdiniz.</span><span class="sxs-lookup"><span data-stu-id="a9adf-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="a9adf-139">Bu noktada hello ARM şablonu hazırdır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="a9adf-140">Şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="a9adf-140">Deploy Template</span></span>
<span data-ttu-id="a9adf-141">Son adımlar hello toopiece bu tüm baştan sona tam dağıtım birbirine.</span><span class="sxs-lookup"><span data-stu-id="a9adf-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="a9adf-142">toomake dağıtım hello yararlanabilirsiniz daha kolay **dağıtma AzureResourceGroup.ps1** Visual Studio toohelp gerekli yapıların karşıya yükleme ile bir Azure kaynak grubu projesi oluşturduğunuzda, eklediğiniz PowerShell Betiği Merhaba şablonu.</span><span class="sxs-lookup"><span data-stu-id="a9adf-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="a9adf-143">Önceden toouse istediğiniz bir depolama hesabı oluşturuldu toohave gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a9adf-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="a9adf-144">Bu örnekte, karşıya hello package.zip toobe için bir paylaşılan depolama hesabı oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="a9adf-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="a9adf-145">Merhaba betik AzCopy tooupload hello paket toohello depolama hesabı özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="a9adf-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="a9adf-146">Yapı klasörü konumunuz geçirebilir ve hello betik depolama kapsayıcısı adlı bu dizin toohello içindeki tüm dosyaları otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="a9adf-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="a9adf-147">Dağıtma-AzureResourceGroup.ps1 çağrıldıktan sonra toothen güncelleştirme hello SSL bağlamaları toomap hello özel ana bilgisayar adı, SSL sertifikası ile sahip.</span><span class="sxs-lookup"><span data-stu-id="a9adf-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="a9adf-148">PowerShell gösterir aşağıdaki hello hello tam dağıtım arama hello dağıtma-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="a9adf-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

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

<span data-ttu-id="a9adf-149">Bu noktada, uygulamanız dağıtıldıktan ve mümkün toobrowse tooit https://www.yourcustomdomain.com aracılığıyla olmalıdır</span><span class="sxs-lookup"><span data-stu-id="a9adf-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

