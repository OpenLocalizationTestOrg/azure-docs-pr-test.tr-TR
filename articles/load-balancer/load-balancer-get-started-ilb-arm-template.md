---
title: "bir iç yük dengeleyici - Azure şablonu aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir iç yük dengeleyici Kaynak Yöneticisi'nde bir şablon kullanarak bilgi edinin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>Şablon kullanarak iç yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Kullanarak Hello şablonu dağıtma toodeploy tıklatın

Merhaba örnek şablonunda kullanılabilir hello genel depo yukarıda açıklanan hello varsayılan kullanılan değerler toogenerate hello senaryosu içeren bir parametre dosyası kullanır. toodeploy tıklatın toodeploy, bu şablonu kullanarak izleyin [bu bağlantıyı](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin.

## <a name="deploy-hello-template-by-using-powershell"></a>PowerShell kullanarak Hello şablonu dağıtma

PowerShell kullanarak yüklediğiniz toodeploy hello şablonunu hello adımları izleyin.

1. Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.
2. Merhaba parametreleri dosya tooyour yerel disk indirin.
3. Merhaba dosyasını düzenleyin ve kaydedin.
4. Merhaba çalıştırmak **New-AzureRmResourceGroupDeployment** kullanarak bir kaynak grubu cmdlet toocreate hello şablonu.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
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

3. Merhaba parametre dosyasını açın, içeriğini seçin ve tooa dosyayı bilgisayarınıza kaydedin. Bu örnekte, hello parametreler dosyası çok kaydettik*parameters.json*.
4. Merhaba çalıştırmak **azure Grup dağıtımı oluşturmak** toodeploy hello şablonu ve parametre kullanarak yeni iç yük dengeleyici hello komut dosyaları, yukarıda indirdiğiniz ve değiştirdiğiniz. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

