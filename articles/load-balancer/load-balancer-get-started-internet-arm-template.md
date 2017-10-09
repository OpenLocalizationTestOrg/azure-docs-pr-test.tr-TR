---
title: "aaaCreate bir Internet'e yönelik Yük Dengeleyici - Azure şablonu | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici kaynak bir şablon kullanarak Yöneticisi'nde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Şablon kullanarak İnternet’e yönelik yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Klasik dağıtım modeli kullanarak bilgi edinin](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Kullanarak Hello şablonu dağıtma toodeploy tıklatın

Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır. toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](http://go.microsoft.com/fwlink/?LinkId=544801), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell kullanarak Hello şablonu dağıtma

PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.

1. Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.
2. Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hello şablonu dağıtma

hello Azure CLI kullanarak toodeploy hello şablon hello adımları izleyin.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.

    ```azurecli
    azure config mode arm
    ```

    Yukarıdaki hello komut için beklenen hello çıktı şöyledir:

        info:    New mode is arm

3. Tarayıcınızdan çok gidin[hızlı başlatma şablonunu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)hello hello json dosyasının içeriğini kopyalayın ve bilgisayarınızı yeni bir dosyaya yapıştırın. Bu senaryo için adlı tooa dosya altındaki hello değerler kopyaladığınız **c:\lb\azuredeploy.parameters.json**.
4. Merhaba çalıştırmak **azure Grup dağıtımı oluşturmak** hello şablonu ve parametre kullanarak cmdlet toodeploy hello Yeni Yük Dengeleyici, yukarıda indirdiğiniz ve değiştirdiğiniz dosyaları. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
