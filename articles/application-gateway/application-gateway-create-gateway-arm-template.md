---
title: "Azure uygulama ağ geçidi - şablonları oluşturma | Microsoft Docs"
description: "Bu sayfa, Azure Resource Manager şablonunu kullanarak, Azure uygulama ağ geçidi oluşturma yönergelerini verir."
documentationcenter: na
services: application-gateway
author: davidmu1
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: davidmu
ms.openlocfilehash: 0aa16e9d7472d2d8c3c251e60a506a7f4223ac1d
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/21/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a>Azure Resource Manager şablonunu kullanarak uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portalı](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ve performans yönlendirmeli HTTP istekleri sağlar. Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar. Desteklenen özelliklerin tam listesi için ziyaret edin [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)

Bu makalede indiriliyor ve var olan değiştirme aracılığıyla anlatılmaktadır [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md) GitHub ve şablonu GitHub, PowerShell ve Azure CLI dağıtma.

Sadece şablon herhangi bir değişiklik yapmadan doğrudan github'dan dağıtıyorsanız, github'dan şablon dağıtma bölümüne atlayın.

## <a name="scenario"></a>Senaryo

Bu senaryoda:

* Bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturun.
* Ayrılmış 10.0.0.0/16 CIDR bloğu olan, VirtualNetwork1 adlı bir sanal ağ oluşturacaksınız.
* Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.
* Trafik yük dengelemesi yapmak istediğiniz web sunucuları için, önceden yapılandırılmış iki arka uç IP’si ayarlayacaksınız. Bu şablon örneğinde arka uç IP’leri 10.0.1.10 ve 10.0.1.11’dir.

> [!NOTE]
> Bu ayarlar, bu şablonun parametreleridir. Şablonu özelleştirmek için kuralları, dinleyiciyi, SSL ve diğer seçenekleri azuredeploy.json dosyasını değiştirebilirsiniz.

![Senaryo](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a>Azure Resource Manager şablonu indirme ve anlama

GitHub’dan sanal ağ ve iki adet alt ağ oluşturmak için, mevcut Azure Resource Manager şablonunu indirebilir, istediğiniz değişikliği yapabilir ve yeniden kullanabilirsiniz. Bunu yapmak için aşağıdaki adımları kullanın:

1. Gidin [etkin web uygulaması güvenlik duvarı ile uygulama ağ geçidi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. **azuredeploy.json** ve **RAW** öğelerine sırayla tıklayın.
1. Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.
1. Eğer Azure Resource Manager şablonları hakkında bilginiz varsa, 7. adıma atlayın.
1. Kaydettiğiniz dosyayı açın ve altındaki içeriğe bakın **parametreleri** satırında
1. Azure Resource Manager şablonu parametreleri, dağıtım sırasında doldurulabilecek değerler için yer tutucu sağlar.

  | Parametre | Açıklama |
  | --- | --- |
  | **subnetPrefix** |Uygulama ağ geçidi alt ağının CIDR bloğu. |
  | **applicationGatewaySize** | Uygulama ağ geçidi boyutu.  WAF yalnızca orta ve büyük ölçekli izin verir. |
  | **backendIpaddress1** |İlk web sunucusunun IP adresi. |
  | **backendIpaddress2** |İkinci web sunucusunun IP adresi. |
  | **wafEnabled** | WAF etkin olup olmadığını belirlemek için ayarlama.|
  | **wafMode** | Web uygulaması güvenlik duvarı modu.  Kullanılabilir seçenekler **önleme** veya **algılama**.|
  | **wafRuleSetType** | WAF RuleSet türü.  Şu anda OWASP yalnızca desteklenen bir seçenektir. |
  | **wafRuleSetVersion** |RuleSet sürümü. Şu anda desteklenen seçenekler OWASP CRS 2.2.9 ve 3.0 belirtilmiştir. |

1. Altındaki içeriği denetleyin **kaynakları** ve aşağıdaki özelliklere dikkat edin:

   * **type**. Şablon tarafından oluşturulan kaynak türü. Bu durumda, türüdür `Microsoft.Network/applicationGateways`, bir uygulama ağ geçidini temsil eder.
   * **name**. Kaynağın adı. Kullanımına dikkat edin `[parameters('applicationGatewayName')]`, adı giriş olarak sizin tarafınızdan veya bir parametre dosyası dağıtımı sırasında sağlanan anlamına gelir.
   * **properties**. Kaynak özelliklerinin listesi. Bu şablon, uygulama ağ geçidi oluştururken sanal ağı ve genel IP adresini kullanır.

1. Geri gidin [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Tıklatın **azuredeploy-parameters.json**ve ardından **RAW**.
1. Dosyayı bilgisayarınızdaki yerel bir klasöre kaydedin.
1. Kaydettiğiniz dosyayı açın ve parametre değerlerini düzenleyin. Senaryomuzda açıklanan uygulama ağ geçidini dağıtmak için aşağıdaki değerleri kullanın.

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

1. Dosyayı kaydedin. JSON şablonunu ve parametre şablonunu, [JSlint.com](http://www.jslint.com/) gibi çevrimiçi JSON doğrulama araçlarını kullanarak test edebilirsiniz.

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a>PowerShell kullanarak Azure Resource Manager şablonu dağıtma

Azure PowerShell'i hiç kullanmadıysanız, ziyaret edin: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) ve Azure'da oturum açıp aboneliğinizi seçmek için yönergeleri izleyin.

1. PowerShell oturum açın

    ```powershell
    Login-AzureRmAccount
    ```

1. Hesapla ilişkili abonelikleri kontrol edin.

    ```powershell
    Get-AzureRmSubscription
    ```

    Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.

1. Hangi Azure aboneliğinizin kullanılacağını seçin.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Gerekirse, **New-AzureResourceGroup** cmdlet’ini kullanarak bir kaynak grubu oluşturun. Aşağıdaki örnekte Doğu ABD konumunda AppgatewayRG adlı yeni bir kaynak grubu oluşturacaksınız.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Önceden indirdiğiniz ve değiştirdiğiniz şablonu ve parametre dosyalarını kullanarak yeni sanal ağı dağıtmak için, **New-AzureRmResourceGroupDeployment** cmdlet’ini çalıştırın.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a>Azure CLI kullanarak Azure Resource Manager şablonu dağıtma

Azure CLI kullanarak indirdiğiniz Azure Resource Manager şablonu dağıtmak için aşağıdaki adımları izleyin:

1. Daha önce Azure CLI kullanmadıysanız, [Azure CLI yükleme ve yapılandırma](/cli/azure/install-azure-cli) sayfasına gidin ve Azure hesabınızı ve aboneliğinizi seçene kadar talimatları uygulayın.

1. Gerekirse, çalıştırmak `az group create` aşağıdaki kod parçacığında gösterildiği gibi bir kaynak grubu oluşturmak için komutu. Komutun çıktısına dikkat edin. Çıktıdan sonra gösterilen listede kullanılan parametreler açıklanmaktadır. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md) sayfasını ziyaret edin.

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (veya --name)**. Yeni kaynak grubunun adı. Senaryomuz için bu ad, *appgatewayRG*.
    
    **-l (veya --location)**. Yeni kaynak grubunun oluşturulduğu Azure bölgesi. Bizim senaryomuz için sahip *westus*.

1. Çalıştırma `az group deployment create` şablonu ve parametre kullanarak yeni sanal ağı dağıtmak için cmdlet indirdiğiniz ve değiştirdiğiniz önceki adımda dosyaları. Çıktıdan sonra gösterilen listede kullanılan parametreler açıklanmaktadır.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a>Dağıtmak için tıkla özelliğini kullanarak Azure Resource Manager şablonu dağıtma

Dağıtmak için tıkla, Azure Resource Manager şablonlarını kullanmanın başka bir yoludur. Kolay bir Azure portalıyla şablonları kullanma yoludur.

1. Git [web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. **Azure’a dağıt**’a tıklayın.

    ![Azure’a dağıtma](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Portalda, dağıtım şablonu parametrelerini doldurun ve **Tamam**’a tıklayın.

    ![Parametreler](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Seçin **hüküm ve koşulları yukarıda belirtildiği ediyorum** tıklatıp **satın alma**.

1. Özel dağıtım dikey penceresinde **Oluştur**’a tıklayın.

## <a name="providing-certificate-data-to-resource-manager-templates"></a>Resource Manager şablonları için sertifika verileri sağlayan

SSL sahip bir şablon kullanıldığında, sertifikanın karşıya yüklenen yerine bir base64 dizesi sağlanması gerekir. Dönüştürmek için bir .pfx veya base64 dizesi .cer kullanmak aşağıdaki komutlardan birini. Aşağıdaki komutları sertifika şablonu için sağlanan bir base64 dizesi dönüştürülemiyor. Beklenen çıktı bir değişkende depolanan ve şablonda yapıştırılan bir dizedir.

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

Bu makalede oluşturulan tüm kaynakları silmek için aşağıdaki adımlardan birini tamamlayın:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Sonraki adımlar

SSL yükü boşaltmayı yapılandırmak istiyorsanız [SSL yükü boşaltma için uygulama ağ geçidi yapılandırma](application-gateway-ssl.md) sayfasını ziyaret edin.

İç yük dengeleyiciyle kullanacağınız uygulama ağ geçidi yapılandırmak istiyorsanız [İç yük dengeleyici (ILB) ile uygulama ağ geçidi oluşturma](application-gateway-ilb.md) sayfasını ziyaret edin.

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

