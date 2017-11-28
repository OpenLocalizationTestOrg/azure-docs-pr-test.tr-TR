---
title: "aaaConnect PowerShell kullanarak uygulama tooyour sanal ağınızı"
description: "Tooconnect tooand nasıl sanal ağlarla PowerShell kullanarak ilgili yönergeler"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="f9ec8-103">PowerShell kullanarak uygulama tooyour sanal ağınıza bağlamak</span><span class="sxs-lookup"><span data-stu-id="f9ec8-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="f9ec8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f9ec8-104">Overview</span></span>
<span data-ttu-id="f9ec8-105">Azure App Service'te uygulamanızı (web, mobil veya API) bağlanabilir tooan aboneliğinizde Azure sanal ağı (VNet).</span><span class="sxs-lookup"><span data-stu-id="f9ec8-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="f9ec8-106">Bu özellik, VNet tümleştirmesi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="f9ec8-107">Merhaba VNet tümleştirme özelliği, Azure App Service örneği sanal ağınızda toorun verir hello uygulama hizmeti ortamı özelliği ile karıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="f9ec8-108">Merhaba VNet tümleştirme özelliği, hello Klasik dağıtım modeli veya hello Azure Resource Manager dağıtım modeli kullanılarak dağıtılan sanal ağlarla toointegrate kullanabilirsiniz, hello yeni Portalı'nda bir kullanıcı arabirimi (UI) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f9ec8-109">Merhaba özelliği hakkında daha fazla toolearn istiyorsanız, bkz: [uygulamanızı Azure sanal ağı ile tümleştirmek](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9ec8-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="f9ec8-110">Bu makalede nasıl toouse hello UI ilgili değildir ancak bunun yerine konusunda olduğu PowerShell kullanarak tooenable tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="f9ec8-111">Her dağıtım modeli için Hello komutları farklı olduğundan, bu makalede her dağıtım modeli için bir bölüm vardır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="f9ec8-112">Bu makale ile devam etmeden önce şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="f9ec8-113">en son Azure PowerShell SDK'sı yüklü hello.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="f9ec8-114">Bu hello Web Platformu Yükleyicisi ile yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="f9ec8-115">Azure uygulama hizmetinde bir standart veya Premium SKU çalışan bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="f9ec8-116">Klasik sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="f9ec8-116">Classic virtual networks</span></span>
<span data-ttu-id="f9ec8-117">Bu bölümde, hello Klasik dağıtım modelini kullanan sanal ağlar için üç görevleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="f9ec8-118">Bir ağ geçidi ve noktadan siteye bağlantı için yapılandırılmış uygulama tooa önceden var olan sanal ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="f9ec8-119">Uygulamanız için sanal ağ tümleştirme bilgilerinizi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="f9ec8-120">Uygulamanızı, sanal ağ bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="f9ec8-121">Bir uygulama tooa bağlanmak Klasik VNet</span><span class="sxs-lookup"><span data-stu-id="f9ec8-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="f9ec8-122">tooconnect bir uygulama tooa sanal ağ bu üç adımı izleyin:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="f9ec8-123">Belirli bir sanal ağ katılacağı toohello web uygulaması bildirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="f9ec8-124">Merhaba uygulama toohello sanal ağ için noktadan siteye bağlantı verilen bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="f9ec8-125">Merhaba web uygulama sertifika toohello sanal ağ karşıya yükleyin ve sonra hello noktadan siteye VPN paketi URI alır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="f9ec8-126">Merhaba web uygulamanızın sanal ağ bağlantısı hello noktası site paket URI güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="f9ec8-127">Merhaba birinci ve üçüncü adımları yönüyle ancak hello ikinci adım, bir kerelik, el ile eylemi hello portal ya da erişim tooperform üzerinden gerektirir **PUT** veya **düzeltme eki** hello sanal ağda Eylemler Azure Kaynak Yöneticisi uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="f9ec8-128">Azure desteği toohave bu etkinleştirildiğinde başvurun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="f9ec8-129">Başlamadan önce noktadan siteye bağlantı zaten etkinleştirilmiş ve dağıtılan bir ağ geçidi klasik bir sanal ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="f9ec8-130">toocreate hello ağ geçidi ve etkinleştir noktadan siteye bağlanabilirlik toouse hello portal konusunda açıklandığı gibi gereken [bir VPN ağ geçidi oluşturma][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="f9ec8-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="f9ec8-131">Merhaba Klasik sanal ağ gerekiyor toobe hello uygulama hizmetiniz aynı abonelik planı ile tümleştirme, ayrı tutma hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="f9ec8-132">Azure PowerShell SDK ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f9ec8-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="f9ec8-133">Bir PowerShell penceresi açın ve kullanarak, Azure hesabınızı ve aboneliğinizi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="f9ec8-134">Bu komutu bir komut istemi tooget Azure kimlik bilgilerinizi açılır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="f9ec8-135">Oturum açtıktan sonra aşağıdaki komutları tooselect hello abonelik toouse istediğiniz hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="f9ec8-136">Sanal ağ ve uygulama hizmeti planı hello abonelik kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="f9ec8-137">or</span><span class="sxs-lookup"><span data-stu-id="f9ec8-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="f9ec8-138">Bu makalede kullanılan değişkenleri</span><span class="sxs-lookup"><span data-stu-id="f9ec8-138">Variables used in this article</span></span>
<span data-ttu-id="f9ec8-139">toosimplify komutlar, biz ayarlayacak bir **$Configuration** PowerShell değişkeni hello belirli yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="f9ec8-140">Bir değişken PowerShell'de şu parametreler hello ile aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="f9ec8-141">Merhaba uygulamasının konumuna hello konumu boşluk olmadan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="f9ec8-142">Örneğin, Batı ABD westus olur.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="f9ec8-143">Merhaba sonraki hello sertifika nereye yazılması gereken öğesidir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="f9ec8-144">Yerel bilgisayarınızda yazılabilir bir yol olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="f9ec8-145">Merhaba sonunda tooinclude .cer emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="f9ec8-146">toosee ne ayarlamanız türü **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="f9ec8-147">Bu bölümde Hello kalan biraz önce açıklandığı gibi oluşturulan değişken sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="f9ec8-148">Merhaba sanal ağ toohello uygulama bildirme</span><span class="sxs-lookup"><span data-stu-id="f9ec8-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="f9ec8-149">Bu belirli bir sanal ağ kullanacağınız komut tootell hello uygulama aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="f9ec8-150">Bu, gerekli sertifikaları hello uygulama toogenerate neden olur:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="f9ec8-151">Bu komutun başarılı olursa, **$vnet** olmalıdır bir **özellikleri** da değişken.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="f9ec8-152">Merhaba **özellikleri** değişkeni, hem bir sertifika parmak izi ve hello sertifika verileri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="f9ec8-153">Merhaba web uygulama sertifika toohello sanal ağ karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="f9ec8-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="f9ec8-154">El ile her abonelik ve sanal ağ bileşimi için tek seferlik adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="f9ec8-155">Diğer bir deyişle, abonelik A tooVirtual Ağ A uygulamalarında bağlanıyorsanız toodo bu adımı gerekir, yalnızca kaç uygulamalara bağımsız olarak yapılandırdığınız bir kez.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="f9ec8-156">Yeni bir uygulama tooanother sanal ağ ekliyorsanız, bu yeniden toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="f9ec8-157">Bunun nedeni Hello sertifikalar kümesini Azure App Service'te bir abonelik düzeyinde oluşturulur ve hello kümesi kez hello uygulamaları bağlanacağı her sanal ağ için oluşturulan ' dir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="f9ec8-158">Merhaba sertifikaları zaten adımları izlediyseniz veya hello ile aynı bütünleştirdiyseniz ayarlanan hello portalını kullanarak sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="f9ec8-159">Merhaba ilk adımı toogenerate hello .cer dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="f9ec8-160">Merhaba ikinci adım tooupload hello .cer dosyasını tooyour sanal ağdır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="f9ec8-161">toogenerate hello .cer hello hello API çağrısında dosyasından önceki adımda, hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="f9ec8-162">Merhaba sertifika hello konumda bulunan, **$Configuration.GeneratedCertificatePath** belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="f9ec8-163">tooupload hello sertifikayı el ile hello kullan [Azure portal] [ azureportal] ve **Gözat sanal ağ (Klasik)** > **VPNbağlantıları**  >  **Noktadan siteye** > **yönetmek sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="f9ec8-164">Buradan, sertifikanızı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="f9ec8-165">Başlangıç noktası site paketi alın</span><span class="sxs-lookup"><span data-stu-id="f9ec8-165">Get hello point-to-site package</span></span>
<span data-ttu-id="f9ec8-166">bir web uygulaması üzerinde bir sanal ağ bağlantısı kurma hello sonraki adım tooget hello noktadan siteye paketidir ve tooyour web uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="f9ec8-167">Aşağıdaki şablonu tooa dosyasına GetNetworkPackageUri.json herhangi bir yerde, bilgisayarınızda, örneğin, C:\Azure\Templates\GetNetworkPackageUri.json adlı hello kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="f9ec8-168">Giriş parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="f9ec8-169">Merhaba komut dosyasını çağırın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="f9ec8-170">Merhaba değişkeni **$output. Outputs.packageUri** tooyour web uygulaması verilen hello paket URI toobe şimdi içerecektir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="f9ec8-171">Başlangıç noktası site paket tooyour uygulamayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="f9ec8-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="f9ec8-172">Merhaba son adım tooprovide hello Paketle uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="f9ec8-173">Yalnızca hello sonraki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="f9ec8-174">Mevcut kaynağın üzerine tooconfirm soran bir ileti tooallow emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="f9ec8-175">Bu komutun başarılı olduktan sonra uygulamanızı artık bağlı toohello sanal ağ olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="f9ec8-176">tooconfirm başarı tooyour uygulama Konsolu gidin ve hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="f9ec8-177">Merhaba hedef sanal ağ hello adıyla eşleşen bir değere sahip WEBSITE_VNETNAME adlı bir ortam değişkeni ise, tüm yapılandırmaları başarılı olduğunu.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="f9ec8-178">Klasik VNet tümleştirme bilgilerini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="f9ec8-178">Update classic VNet integration information</span></span>
<span data-ttu-id="f9ec8-179">tooupdate veya bilgilerinizi yeniden eşitleme, yalnızca hello ilk yerinde hello tümleştirme oluşturduğunuzda, uyguladığınız hello adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="f9ec8-180">Bu adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-180">Those steps are:</span></span>

1. <span data-ttu-id="f9ec8-181">Yapılandırma bilgilerinizi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-181">Define your configuration information.</span></span>
2. <span data-ttu-id="f9ec8-182">Merhaba sanal ağ toohello uygulama bildirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="f9ec8-183">Başlangıç noktası site paketi alın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="f9ec8-184">Başlangıç noktası site paket tooyour uygulamasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="f9ec8-185">Uygulamanızı bir Klasik sanal ağdan bağlantısını kesme</span><span class="sxs-lookup"><span data-stu-id="f9ec8-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="f9ec8-186">toodisconnect hello uygulama, sanal ağ tümleştirmesinin sırasında ayarlandı hello yapılandırma bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="f9ec8-187">Bu bilgileri kullanarak, yoktur sonra bir komut toodisconnect sanal ağınızı uygulamanızdan.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="f9ec8-188">Kaynak Yöneticisi sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="f9ec8-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="f9ec8-189">Kaynak Yöneticisi sanal ağlar, Klasik sanal ağlar ile karşılaştırıldığında bazı işlemleri basitleştirmek Azure Resource Manager API'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="f9ec8-190">Merhaba aşağıdaki görevleri tamamlamanıza yardımcı olacak bir komut dosyası sunuyoruz:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="f9ec8-191">Resource Manager sanal ağ oluşturmak ve uygulamanızı ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="f9ec8-192">Bir ağ geçidi oluşturmak, önceden var olan bir Resource Manager sanal ağda noktadan siteye bağlantı yapılandırmak ve uygulamanızı ile tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="f9ec8-193">Uygulamanızı bir ağ geçidi ve noktası site bağlantısı etkin olan bir önceden var olan kaynak yöneticisi sanal ağ ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="f9ec8-194">Uygulamanızı, sanal ağ bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="f9ec8-195">Resource Manager Vnet'i uygulama hizmeti tümleştirme komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f9ec8-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="f9ec8-196">Aşağıdaki komut dosyası ve tooa dosyasını kaydedin hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="f9ec8-197">Toouse hello betik olmasını istemezseniz, boş toolearn dışarı toosee nasıl eşitleyerek Resource Manager sanal ağ ile tooset işlemleri.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="f9ec8-198">Merhaba komut dosyasının bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-198">Save a copy of hello script.</span></span> <span data-ttu-id="f9ec8-199">Bu makalede, V2VnetAllinOne.ps1 çağrıldı, ancak başka bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="f9ec8-200">Bu komut için bağımsız değişken vardır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-200">There are no arguments for this script.</span></span> <span data-ttu-id="f9ec8-201">Bu çalıştırmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-201">You simply run it.</span></span> <span data-ttu-id="f9ec8-202">Merhaba ilk şey hello betik ne yapacağını toosign de sor değil.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="f9ec8-203">Oturum açtıktan sonra hello komut dosyası, hesabınız hakkında ayrıntılar alır ve Aboneliklerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="f9ec8-204">Kimlik bilgilerinizi Hello talebi saymaz, hello ilk komut dosyası yürütme şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="f9ec8-205">Tanıtım abonelik (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="f9ec8-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="f9ec8-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="f9ec8-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="f9ec8-207">Mor Demo abonelik (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="f9ec8-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="f9ec8-208">Bir seçenek belirleyin: 3</span><span class="sxs-lookup"><span data-stu-id="f9ec8-208">Choose an option: 3</span></span>

    <span data-ttu-id="f9ec8-209">Hesap: ccompy@microsoft.com ortam: AzureCloud abonelik: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Kiracı: 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="f9ec8-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="f9ec8-210">Lütfen merhaba, uygulamanızın kaynak grubu girin: hcdemo rg Lütfen merhaba, uygulamanızın adı girin: v2vnetpowershell ne yapması, toodo istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="f9ec8-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="f9ec8-211">Yeni sanal ağ tooan uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="f9ec8-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="f9ec8-212">Varolan bir sanal ağı tooan uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="f9ec8-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="f9ec8-213">Bir sanal ağ bir uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="f9ec8-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="f9ec8-214">Bu bölümde Hello kalan üç bu seçeneklerin her biri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="f9ec8-215">Resource Manager Vnet'i oluşturun ve onu ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f9ec8-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="f9ec8-216">toocreate kullandığı hello Resource Manager dağıtım modeli ve uygulamanızı ile tümleştirmek yeni bir sanal ağı seçin **1) yeni bir sanal ağ tooan uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="f9ec8-217">Bu hello sanal ağ hello adını ister.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="f9ec8-218">My durumda hello ayarlarını, aşağıdaki görebileceğiniz gibi hello adı, v2pshell kullandım.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="f9ec8-219">Merhaba komut dosyası oluşturuluyor hello sanal ağla ilgili hello ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="f9ec8-220">İstiyorsam, hello değerleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="f9ec8-221">Bu örnek yürütme ayarları aşağıdaki hello olan bir sanal ağ oluşturduğum:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="f9ec8-222">Merhaba değerlerden herhangi birini toochange istiyorsanız yazın **Y** ve hello değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="f9ec8-223">Merhaba sanal ağ ayarlarıyla hazır olduğunuzda yazın **N** veya yalnızca hello ayarlarını değiştirme hakkında istendiğinde Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="f9ec8-224">Buradan üzerinde tamamlama kadar hello betik bazı neyin size bildirir ' toocreate hello sanal ağ geçidi başlatana kadar yapılması i's.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="f9ec8-225">Bu adım tooan saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-225">That step can take up tooan hour.</span></span> <span data-ttu-id="f9ec8-226">Bu aşamada hiçbir İlerleme göstergesi yoktur, ancak hello betik bunu ne zaman hello ağ geçidi oluşturulup oluşturulmadığını size bildirir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="f9ec8-227">Merhaba betik tamamlandığında söyleyin **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="f9ec8-228">Bu noktada, hello ada sahip bir kaynak yöneticisi sanal ağ ve seçtiğiniz ayarları sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="f9ec8-229">Bu yeni bir sanal ağ de uygulamanız ile entegre.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="f9ec8-230">Uygulamanızı önceden var olan bir Resource Manager Vnet'i ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f9ec8-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="f9ec8-231">Bir ağ geçidi veya noktadan siteye bağlantı yok Resource Manager sanal ağ sağlarsanız, önceden var olan bir sanal ağ ile tümleştirme zaman hello komut dosyası, kurar.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="f9ec8-232">Merhaba VNET ayarlanan Bunlar zaten varsa, hello betik düz toohello uygulama tümleştirmesi gider.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="f9ec8-233">toostart bu işlem, yalnızca select **2) bir varolan sanal ağ tooan uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="f9ec8-234">Bu seçenek yalnızca hello olan önceden var olan kaynak yöneticisi sanal ağ varsa çalışır, uygulamanızın aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="f9ec8-235">Hello seçeneği belirledikten sonra Resource Manager sanal ağların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="f9ec8-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="f9ec8-236">v2demonetwork</span></span>
    2) <span data-ttu-id="f9ec8-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="f9ec8-237">v2pshell</span></span>
    3) <span data-ttu-id="f9ec8-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="f9ec8-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="f9ec8-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="f9ec8-239">v2asenetwork</span></span>
    5) <span data-ttu-id="f9ec8-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="f9ec8-240">v2pshell2</span></span>

    <span data-ttu-id="f9ec8-241">Bir seçenek belirleyin: 5</span><span class="sxs-lookup"><span data-stu-id="f9ec8-241">Choose an option: 5</span></span>

<span data-ttu-id="f9ec8-242">Yalnızca toointegrate ile istediğiniz hello sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="f9ec8-243">Noktadan siteye bağlantı etkin olan bir ağ geçidi zaten varsa, hello betik uygulamanızı sanal ağınızla yalnızca tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="f9ec8-244">Bir ağ geçidi yoksa toospecify hello ağ geçidi alt ağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="f9ec8-245">Ağ geçidi alt ağınızı, sanal ağ adres alanında olmalıdır ve herhangi bir alt ağda olamaz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="f9ec8-246">Bir ağ geçidi olmadan bir sanal ağ varsa ve bu adımın çalıştırılması, şeyler şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="f9ec8-247">Bu örnekte, ayarlar aşağıdaki hello sahip bir sanal ağ geçidi oluşturduğum:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="f9ec8-248">Bu ayarlardan herhangi birini toochange istiyorsanız, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="f9ec8-249">Aksi takdirde, Enter tuşuna basın ve hello komut dosyası, ağ geçidi oluşturmak ve uygulama tooyour sanal ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="f9ec8-250">Merhaba ağ geçidi oluşturma zamanı hala bir saat olsa, bu nedenle, göz önünde bulundurmanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="f9ec8-251">Her şeyi tamamlandığında hello betik sorar **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="f9ec8-252">Uygulamanızı bir Resource Manager sanal ağdan bağlantısını kesme</span><span class="sxs-lookup"><span data-stu-id="f9ec8-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="f9ec8-253">Uygulamanızı sanal ağ bağlantınızı kesmeden bırakmaz hello ağ geçidi alın veya noktadan siteye bağlantı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="f9ec8-254">Tüm, başka bir şey için kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="f9ec8-255">Bu da onu hello dışındaki diğer tüm uygulamalardan biri sağladığınız kesmez.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="f9ec8-256">tooperform Bu eylem, select **3) bir uygulamadan bir sanal ağı kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="f9ec8-257">Bunu yaptığınızda, şöyle bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="f9ec8-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="f9ec8-258">Delete Hello komut dosyası yazan rağmen hello sanal ağ silmez.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="f9ec8-259">Ayrıca, hello tümleştirme yalnızca kaldırıyor.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-259">It’s just removing hello integration.</span></span> <span data-ttu-id="f9ec8-260">Bu ne olduğunu doğruladıktan sonra toodo, hello komutu oldukça hızlı bir şekilde işlenir ve size bildirir **doğru** , ne zaman yapılır.</span><span class="sxs-lookup"><span data-stu-id="f9ec8-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
