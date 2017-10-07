---
title: "Azure uygulama ağ geçidi - şablonları aaaCreate | Microsoft Docs"
description: "Bu sayfa, hello Azure Resource Manager şablonu kullanarak bir Azure uygulama ağ geçidi yönergeleri toocreate sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Hello Azure Resource Manager şablonu kullanarak bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içi olup, yük devretme ve performans yönlendirme HTTP isteklerini, farklı sunucular arasında sağlar. Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar. toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)

Bu makalede, indirme ve var olan bir Azure Resource Manager şablonunu github'dan değiştirme ve hello şablonu GitHub, PowerShell ve Azure CLI hello dağıtma anlatılmaktadır.

Yalnızca hello Azure Resource Manager şablonu herhangi bir değişiklik yapmadan doğrudan github'dan dağıtıyorsanız, Github'dan şablon toodeploy atlayın.

## <a name="scenario"></a>Senaryo

Bu senaryoda:

* Bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturun.
* Ayrılmış 10.0.0.0/16 CIDR bloğu olan, VirtualNetwork1 adlı bir sanal ağ oluşturacaksınız.
* Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.
* Merhaba web sunucuları için önceden yapılandırılmış iki arka uç IP'leri ayarlamak tooload hello trafiği dengelemek istiyorsunuz. Bu şablon örneğinde hello arka uç IP de 10.0.1.10 ve 10.0.1.11.olacak.

> [!NOTE]
> Bu ayarlar, bu şablonu hello parametreleridir. toocustomize hello şablonu, kurallar, hello dinleyicisi, SSL ve diğer seçenekleri hello azuredeploy.json dosyasını değiştirebilirsiniz.

![Senaryo](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>İndirme ve hello Azure Resource Manager şablonu anlama

Merhaba mevcut Azure Resource Manager şablonu toocreate bir sanal ağ ve iki alt Github'dan indirdiğinizde, istediğiniz ve yeniden tüm değişiklikleri yapın. toodo, bu nedenle, hello aşağıdaki adımları kullanın:

1. Çok gidin[etkin web uygulaması güvenlik duvarı ile uygulama ağ geçidi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. **azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.
1. Merhaba dosya tooa yerel klasör bilgisayarınıza kaydedin.
1. Azure Resource Manager şablonları hakkında bilginiz varsa 7 toostep atlayın.
1. Kaydettiğiniz hello dosyasını açın ve altındaki hello içeriğe bakın **parametreleri** satırında
1. Azure Resource Manager şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için yer tutucu sağlar.

  | Parametre | Açıklama |
  | --- | --- |
  | **subnetPrefix** |Merhaba uygulama ağ geçidi alt ağının CIDR bloğu. |
  | **applicationGatewaySize** | Merhaba uygulama ağ geçidi boyutu.  WAF yalnızca orta ve büyük ölçekli izin verir. |
  | **backendIpaddress1** |Merhaba ilk web sunucusunun IP adresi. |
  | **backendIpaddress2** |Merhaba ikinci web sunucusunun IP adresi. |
  | **wafEnabled** | WAF etkinleştirilirse toodetermine ayarlama.|
  | **wafMode** | Merhaba web uygulaması güvenlik duvarı modu.  Kullanılabilir seçenekler **önleme** veya **algılama**.|
  | **wafRuleSetType** | WAF RuleSet türü.  Şu anda OWASP hello seçeneği yalnızca desteklenen değil. |
  | **wafRuleSetVersion** |RuleSet sürümü. Şu anda desteklenen hello seçenekler OWASP CRS 2.2.9 ve 3.0 belirtilmiştir. |

1. Merhaba içeriği altında denetleyin **kaynakları** ve bildirimi hello aşağıdaki özellikleri:

   * **type**. Merhaba şablon tarafından oluşturulan kaynak türü. Bu durumda, hello türüdür `Microsoft.Network/applicationGateways`, bir uygulama ağ geçidini temsil eder.
   * **name**. Merhaba kaynak adı. Bildirim hello kullanımını `[parameters('applicationGatewayName')]`, bu hello adı başka bir deyişle, girdi olarak sizin tarafınızdan veya bir parametre dosyası dağıtımı sırasında sağlanır.
   * **properties**. Merhaba kaynak özelliklerinin listesi. Bu şablon, uygulama ağ geçidi oluşturma sırasında hello sanal ağ ve genel IP adresini kullanır.

   > [!NOTE]
   > Şablonlar hakkında daha fazla bilgi için ziyaret edin: [Resource Manager şablonları başvurusu](/templates/)

1. Geri çok gidin[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Tıklatın **azuredeploy-parameters.json**ve ardından **RAW**.
1. Merhaba dosya tooa yerel klasör bilgisayarınıza kaydedin.
1. Kaydettiğiniz hello dosyasını açın ve hello parametreleri hello değerlerini düzenleyin. Senaryomuzda açıklanan değerleri toodeploy hello uygulama ağ geçidi aşağıdaki hello kullanın.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Merhaba dosyasını kaydedin. Merhaba JSON şablonunu ve parametre şablonunu gibi çevrimiçi JSON doğrulama araçlarını kullanarak test edebilirsiniz [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>PowerShell kullanarak Hello Azure Resource Manager şablonu dağıtma

Azure PowerShell'i hiç kullanmadıysanız, ziyaret edin: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) Azure'da hello yönergeleri toosign izleyin ve aboneliğinizi seçin.

1. Oturum açma tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Merhaba hesabının Hello abonelikleri kontrol edin.

    ```powershell
    Get-AzureRmSubscription
    ```

    Kimlik bilgilerinizle istendiğinde tooauthenticate var.

1. Azure abonelikleri toouse hangisinin seçin.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Gerekirse, hello kullanarak bir kaynak grubu oluşturma **New-AzureResourceGroup** cmdlet'i. Aşağıdaki örnek hello, Doğu ABD konumunda AppgatewayRG adlı bir kaynak grubu oluşturun.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını önceki hello kullanarak cmdlet toodeploy hello yeni sanal ağ.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hello Azure Resource Manager şablonu dağıtma

Azure CLI kullanarak indirdiğiniz toodeploy hello Azure Resource Manager şablonu hello aşağıdaki adımları izleyin:

1. Azure CLI hiç kullanmadıysanız bkz [yükleyin ve hello Azure CLI yapılandırma](/cli/azure/install-azure-cli) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.

1. Gerekli olduğunda, çalışma hello `az group create` komutu toocreate hello aşağıdaki kod parçacığında gösterildiği gibi bir kaynak grubu. Merhaba hello komutunun çıkışını dikkat edin. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md) sayfasını ziyaret edin.

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (veya --name)**. Merhaba yeni kaynak grubu adı. Senaryomuz için bu ad, *appgatewayRG*.
    
    **-l (veya --location)**. Merhaba yeni kaynak grubunun oluşturulduğu azure bölgesi. Bizim senaryomuz için sahip *westus*.

1. Merhaba çalıştırmak `az group deployment create` hello şablonu ve parametre kullanarak cmdlet toodeploy hello yeni sanal ağ indirdiğiniz ve değiştirdiğiniz adım önceki hello dosyaları. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Dağıtmak için kullanarak Hello Azure Resource Manager şablonu dağıtma

Dağıtmak için başka bir şekilde toouse Azure Resource Manager şablonları olur. Hello Azure portalında kolay bir yolu toouse şablonlarıyla olur.

1. Çok Git[web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Tıklatın **tooAzure dağıtmak**.

    ![TooAzure dağıtma](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Hello dağıtım şablonu hello portalındaki hello parametrelerini doldurun ve tıklayın **Tamam**.

    ![Parametreler](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Seçin **toohello hüküm ve koşullar yukarıda belirtildiği kabul** tıklatıp **satın alma**.

1. Merhaba özel dağıtım dikey penceresinde **oluşturma**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Sertifika verileri tooResource Manager şablonları sağlama

SSL sahip bir şablon kullanırken hello sertifikanın karşıya yüklenen yerine bir base64 dizesi sağlanan toobe gerekir. tooconvert bir .pfx veya .cer tooa base64 dizesi komutları aşağıdaki hello birini kullanın. Merhaba aşağıdaki komutları toohello şablonu sağlanan hello sertifika tooa base64 dizesi, dönüştürün. Merhaba çıktı bir değişkende depolanan ve hello şablonunda yapıştırılan bir dize bekleniyordu.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki adımları hello tam bir oluşturulan tüm kaynakları toodelete:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Sonraki adımlar

SSL boşaltma tooconfigure istiyorsanız, ziyaret edin: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).

Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, ziyaret edin: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

