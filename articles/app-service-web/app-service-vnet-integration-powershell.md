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
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>PowerShell kullanarak uygulama tooyour sanal ağınıza bağlamak
## <a name="overview"></a>Genel Bakış
Azure App Service'te uygulamanızı (web, mobil veya API) bağlanabilir tooan aboneliğinizde Azure sanal ağı (VNet). Bu özellik, VNet tümleştirmesi adı verilir. Merhaba VNet tümleştirme özelliği, Azure App Service örneği sanal ağınızda toorun verir hello uygulama hizmeti ortamı özelliği ile karıştırılmamalıdır.

Merhaba VNet tümleştirme özelliği, hello Klasik dağıtım modeli veya hello Azure Resource Manager dağıtım modeli kullanılarak dağıtılan sanal ağlarla toointegrate kullanabilirsiniz, hello yeni Portalı'nda bir kullanıcı arabirimi (UI) sahiptir. Merhaba özelliği hakkında daha fazla toolearn istiyorsanız, bkz: [uygulamanızı Azure sanal ağı ile tümleştirmek](web-sites-integrate-with-vnet.md).

Bu makalede nasıl toouse hello UI ilgili değildir ancak bunun yerine konusunda olduğu PowerShell kullanarak tooenable tümleştirme. Her dağıtım modeli için Hello komutları farklı olduğundan, bu makalede her dağıtım modeli için bir bölüm vardır.  

Bu makale ile devam etmeden önce şunları yapın:

* en son Azure PowerShell SDK'sı yüklü hello. Bu hello Web Platformu Yükleyicisi ile yükleyebilirsiniz.
* Azure uygulama hizmetinde bir standart veya Premium SKU çalışan bir uygulama.

## <a name="classic-virtual-networks"></a>Klasik sanal ağlar
Bu bölümde, hello Klasik dağıtım modelini kullanan sanal ağlar için üç görevleri açıklanmaktadır:

1. Bir ağ geçidi ve noktadan siteye bağlantı için yapılandırılmış uygulama tooa önceden var olan sanal ağınıza bağlayın.
2. Uygulamanız için sanal ağ tümleştirme bilgilerinizi güncelleştirin.
3. Uygulamanızı, sanal ağ bağlantısını kesin.

### <a name="connect-an-app-tooa-classic-vnet"></a>Bir uygulama tooa bağlanmak Klasik VNet
tooconnect bir uygulama tooa sanal ağ bu üç adımı izleyin:

1. Belirli bir sanal ağ katılacağı toohello web uygulaması bildirin. Merhaba uygulama toohello sanal ağ için noktadan siteye bağlantı verilen bir sertifika oluşturur.
2. Merhaba web uygulama sertifika toohello sanal ağ karşıya yükleyin ve sonra hello noktadan siteye VPN paketi URI alır.
3. Merhaba web uygulamanızın sanal ağ bağlantısı hello noktası site paket URI güncelleştirin.

Merhaba birinci ve üçüncü adımları yönüyle ancak hello ikinci adım, bir kerelik, el ile eylemi hello portal ya da erişim tooperform üzerinden gerektirir **PUT** veya **düzeltme eki** hello sanal ağda Eylemler Azure Kaynak Yöneticisi uç noktası. Azure desteği toohave bu etkinleştirildiğinde başvurun. Başlamadan önce noktadan siteye bağlantı zaten etkinleştirilmiş ve dağıtılan bir ağ geçidi klasik bir sanal ağ olduğundan emin olun. toocreate hello ağ geçidi ve etkinleştir noktadan siteye bağlanabilirlik toouse hello portal konusunda açıklandığı gibi gereken [bir VPN ağ geçidi oluşturma][createvpngateway].

Merhaba Klasik sanal ağ gerekiyor toobe hello uygulama hizmetiniz aynı abonelik planı ile tümleştirme, ayrı tutma hello uygulama.

##### <a name="set-up-azure-powershell-sdk"></a>Azure PowerShell SDK ayarlayın
Bir PowerShell penceresi açın ve kullanarak, Azure hesabınızı ve aboneliğinizi ayarlayın:

    Login-AzureRmAccount

Bu komutu bir komut istemi tooget Azure kimlik bilgilerinizi açılır. Oturum açtıktan sonra aşağıdaki komutları tooselect hello abonelik toouse istediğiniz hello birini kullanın. Sanal ağ ve uygulama hizmeti planı hello abonelik kullandığınızdan emin olun.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

or

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Bu makalede kullanılan değişkenleri
toosimplify komutlar, biz ayarlayacak bir **$Configuration** PowerShell değişkeni hello belirli yapılandırmasına sahip.

Bir değişken PowerShell'de şu parametreler hello ile aşağıdaki gibi ayarlayın:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

Merhaba uygulamasının konumuna hello konumu boşluk olmadan olmalıdır. Örneğin, Batı ABD westus olur.

    $Configuration.WebAppLocation = "[Your web app Location]"

Merhaba sonraki hello sertifika nereye yazılması gereken öğesidir. Yerel bilgisayarınızda yazılabilir bir yol olmalıdır. Merhaba sonunda tooinclude .cer emin olun.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee ne ayarlamanız türü **$Configuration**.

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

Bu bölümde Hello kalan biraz önce açıklandığı gibi oluşturulan değişken sahip olduğunuzu varsayar.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Merhaba sanal ağ toohello uygulama bildirme
Bu belirli bir sanal ağ kullanacağınız komut tootell hello uygulama aşağıdaki hello kullanın. Bu, gerekli sertifikaları hello uygulama toogenerate neden olur:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Bu komutun başarılı olursa, **$vnet** olmalıdır bir **özellikleri** da değişken. Merhaba **özellikleri** değişkeni, hem bir sertifika parmak izi ve hello sertifika verileri içermelidir.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Merhaba web uygulama sertifika toohello sanal ağ karşıya yükle
El ile her abonelik ve sanal ağ bileşimi için tek seferlik adım gereklidir. Diğer bir deyişle, abonelik A tooVirtual Ağ A uygulamalarında bağlanıyorsanız toodo bu adımı gerekir, yalnızca kaç uygulamalara bağımsız olarak yapılandırdığınız bir kez. Yeni bir uygulama tooanother sanal ağ ekliyorsanız, bu yeniden toodo gerekir. Bunun nedeni Hello sertifikalar kümesini Azure App Service'te bir abonelik düzeyinde oluşturulur ve hello kümesi kez hello uygulamaları bağlanacağı her sanal ağ için oluşturulan ' dir.

Merhaba sertifikaları zaten adımları izlediyseniz veya hello ile aynı bütünleştirdiyseniz ayarlanan hello portalını kullanarak sanal ağ.

Merhaba ilk adımı toogenerate hello .cer dosyası oluşturur. Merhaba ikinci adım tooupload hello .cer dosyasını tooyour sanal ağdır. toogenerate hello .cer hello hello API çağrısında dosyasından önceki adımda, hello aşağıdaki komutları çalıştırın.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

Merhaba sertifika hello konumda bulunan, **$Configuration.GeneratedCertificatePath** belirtir.

tooupload hello sertifikayı el ile hello kullan [Azure portal] [ azureportal] ve **Gözat sanal ağ (Klasik)** > **VPNbağlantıları**  >  **Noktadan siteye** > **yönetmek sertifikaları**. Buradan, sertifikanızı karşıya yükleyin.

##### <a name="get-hello-point-to-site-package"></a>Başlangıç noktası site paketi alın
bir web uygulaması üzerinde bir sanal ağ bağlantısı kurma hello sonraki adım tooget hello noktadan siteye paketidir ve tooyour web uygulaması sağlar.

Aşağıdaki şablonu tooa dosyasına GetNetworkPackageUri.json herhangi bir yerde, bilgisayarınızda, örneğin, C:\Azure\Templates\GetNetworkPackageUri.json adlı hello kaydedin.

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


Giriş parametreleri ayarlayın:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Merhaba komut dosyasını çağırın:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


Merhaba değişkeni **$output. Outputs.packageUri** tooyour web uygulaması verilen hello paket URI toobe şimdi içerecektir.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Başlangıç noktası site paket tooyour uygulamayı karşıya yüklemek
Merhaba son adım tooprovide hello Paketle uygulamasıdır. Yalnızca hello sonraki komutu çalıştırın:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Mevcut kaynağın üzerine tooconfirm soran bir ileti tooallow emin olun.

Bu komutun başarılı olduktan sonra uygulamanızı artık bağlı toohello sanal ağ olması gerekir. tooconfirm başarı tooyour uygulama Konsolu gidin ve hello aşağıdakileri yazın:

    SET WEBSITE_

Merhaba hedef sanal ağ hello adıyla eşleşen bir değere sahip WEBSITE_VNETNAME adlı bir ortam değişkeni ise, tüm yapılandırmaları başarılı olduğunu.

### <a name="update-classic-vnet-integration-information"></a>Klasik VNet tümleştirme bilgilerini güncelleştirin
tooupdate veya bilgilerinizi yeniden eşitleme, yalnızca hello ilk yerinde hello tümleştirme oluşturduğunuzda, uyguladığınız hello adımları yineleyin. Bu adımlar şunlardır:

1. Yapılandırma bilgilerinizi tanımlayın.
2. Merhaba sanal ağ toohello uygulama bildirin.
3. Başlangıç noktası site paketi alın.
4. Başlangıç noktası site paket tooyour uygulamasını karşıya yükleyin.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Uygulamanızı bir Klasik sanal ağdan bağlantısını kesme
toodisconnect hello uygulama, sanal ağ tümleştirmesinin sırasında ayarlandı hello yapılandırma bilgileri gerekir. Bu bilgileri kullanarak, yoktur sonra bir komut toodisconnect sanal ağınızı uygulamanızdan.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Kaynak Yöneticisi sanal ağlar
Kaynak Yöneticisi sanal ağlar, Klasik sanal ağlar ile karşılaştırıldığında bazı işlemleri basitleştirmek Azure Resource Manager API'leri vardır. Merhaba aşağıdaki görevleri tamamlamanıza yardımcı olacak bir komut dosyası sunuyoruz:

* Resource Manager sanal ağ oluşturmak ve uygulamanızı ile tümleştirebilirsiniz.
* Bir ağ geçidi oluşturmak, önceden var olan bir Resource Manager sanal ağda noktadan siteye bağlantı yapılandırmak ve uygulamanızı ile tümleştirme.
* Uygulamanızı bir ağ geçidi ve noktası site bağlantısı etkin olan bir önceden var olan kaynak yöneticisi sanal ağ ile tümleştirin.
* Uygulamanızı, sanal ağ bağlantısını kesin.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Resource Manager Vnet'i uygulama hizmeti tümleştirme komut dosyası
Aşağıdaki komut dosyası ve tooa dosyasını kaydedin hello kopyalayın. Toouse hello betik olmasını istemezseniz, boş toolearn dışarı toosee nasıl eşitleyerek Resource Manager sanal ağ ile tooset işlemleri.

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

Merhaba komut dosyasının bir kopyasını kaydedin. Bu makalede, V2VnetAllinOne.ps1 çağrıldı, ancak başka bir ad kullanabilirsiniz. Bu komut için bağımsız değişken vardır. Bu çalıştırmanız yeterlidir. Merhaba ilk şey hello betik ne yapacağını toosign de sor değil. Oturum açtıktan sonra hello komut dosyası, hesabınız hakkında ayrıntılar alır ve Aboneliklerin listesini döndürür. Kimlik bilgilerinizi Hello talebi saymaz, hello ilk komut dosyası yürütme şöyle görünür:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Tanıtım abonelik (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Mor Demo abonelik (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Bir seçenek belirleyin: 3

    Hesap: ccompy@microsoft.com ortam: AzureCloud abonelik: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Kiracı: 722278f-fef1-499f-91ab-2323d011db47

    Lütfen merhaba, uygulamanızın kaynak grubu girin: hcdemo rg Lütfen merhaba, uygulamanızın adı girin: v2vnetpowershell ne yapması, toodo istiyorsunuz?

    1) Yeni sanal ağ tooan uygulama Ekle
    2) Varolan bir sanal ağı tooan uygulama Ekle
    3) Bir sanal ağ bir uygulamadan Kaldır

Bu bölümde Hello kalan üç bu seçeneklerin her biri açıklanmaktadır.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Resource Manager Vnet'i oluşturun ve onu ile tümleştirme
toocreate kullandığı hello Resource Manager dağıtım modeli ve uygulamanızı ile tümleştirmek yeni bir sanal ağı seçin **1) yeni bir sanal ağ tooan uygulama Ekle**. Bu hello sanal ağ hello adını ister. My durumda hello ayarlarını, aşağıdaki görebileceğiniz gibi hello adı, v2pshell kullandım.

Merhaba komut dosyası oluşturuluyor hello sanal ağla ilgili hello ayrıntılarını verir. İstiyorsam, hello değerleri değiştirebilirsiniz. Bu örnek yürütme ayarları aşağıdaki hello olan bir sanal ağ oluşturduğum:

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

Merhaba değerlerden herhangi birini toochange istiyorsanız yazın **Y** ve hello değişiklikleri yapın. Merhaba sanal ağ ayarlarıyla hazır olduğunuzda yazın **N** veya yalnızca hello ayarlarını değiştirme hakkında istendiğinde Enter tuşuna basın. Buradan üzerinde tamamlama kadar hello betik bazı neyin size bildirir ' toocreate hello sanal ağ geçidi başlatana kadar yapılması i's. Bu adım tooan saat sürebilir. Bu aşamada hiçbir İlerleme göstergesi yoktur, ancak hello betik bunu ne zaman hello ağ geçidi oluşturulup oluşturulmadığını size bildirir.

Merhaba betik tamamlandığında söyleyin **tamamlandı**. Bu noktada, hello ada sahip bir kaynak yöneticisi sanal ağ ve seçtiğiniz ayarları sahip olacaktır. Bu yeni bir sanal ağ de uygulamanız ile entegre.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Uygulamanızı önceden var olan bir Resource Manager Vnet'i ile tümleştirme
Bir ağ geçidi veya noktadan siteye bağlantı yok Resource Manager sanal ağ sağlarsanız, önceden var olan bir sanal ağ ile tümleştirme zaman hello komut dosyası, kurar. Merhaba VNET ayarlanan Bunlar zaten varsa, hello betik düz toohello uygulama tümleştirmesi gider. toostart bu işlem, yalnızca select **2) bir varolan sanal ağ tooan uygulama Ekle**.

Bu seçenek yalnızca hello olan önceden var olan kaynak yöneticisi sanal ağ varsa çalışır, uygulamanızın aynı abonelik. Hello seçeneği belirledikten sonra Resource Manager sanal ağların bir listesini görürsünüz.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Bir seçenek belirleyin: 5

Yalnızca toointegrate ile istediğiniz hello sanal ağı seçin. Noktadan siteye bağlantı etkin olan bir ağ geçidi zaten varsa, hello betik uygulamanızı sanal ağınızla yalnızca tümleştirin. Bir ağ geçidi yoksa toospecify hello ağ geçidi alt ağı gerekir. Ağ geçidi alt ağınızı, sanal ağ adres alanında olmalıdır ve herhangi bir alt ağda olamaz. Bir ağ geçidi olmadan bir sanal ağ varsa ve bu adımın çalıştırılması, şeyler şöyle görünür:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

Bu örnekte, ayarlar aşağıdaki hello sahip bir sanal ağ geçidi oluşturduğum:

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

Bu ayarlardan herhangi birini toochange istiyorsanız, bunu yapabilirsiniz. Aksi takdirde, Enter tuşuna basın ve hello komut dosyası, ağ geçidi oluşturmak ve uygulama tooyour sanal ağınıza bağlayın. Merhaba ağ geçidi oluşturma zamanı hala bir saat olsa, bu nedenle, göz önünde bulundurmanız emin olun. Her şeyi tamamlandığında hello betik sorar **tamamlandı**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Uygulamanızı bir Resource Manager sanal ağdan bağlantısını kesme
Uygulamanızı sanal ağ bağlantınızı kesmeden bırakmaz hello ağ geçidi alın veya noktadan siteye bağlantı devre dışı bırakın. Tüm, başka bir şey için kullanıyor olabilir. Bu da onu hello dışındaki diğer tüm uygulamalardan biri sağladığınız kesmez. tooperform Bu eylem, select **3) bir uygulamadan bir sanal ağı kaldırmak**. Bunu yaptığınızda, şöyle bir şey görürsünüz:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Delete Hello komut dosyası yazan rağmen hello sanal ağ silmez. Ayrıca, hello tümleştirme yalnızca kaldırıyor. Bu ne olduğunu doğruladıktan sonra toodo, hello komutu oldukça hızlı bir şekilde işlenir ve size bildirir **doğru** , ne zaman yapılır.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
