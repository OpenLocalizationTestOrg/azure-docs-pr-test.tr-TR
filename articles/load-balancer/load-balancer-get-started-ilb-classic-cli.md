---
title: "Klasik Azure CLI aaaCreate bir dahili yük dengeleyici - | Microsoft Docs"
description: "Nasıl bir iç yük dengeleyici kullanarak toocreate hello Azure CLI hello Klasik dağıtım modelinde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir iç yük dengeleyici (Klasik) oluşturmaya başlamak

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Bulut hizmetleri](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>sanal makineler için bir iç yük dengeleyici toocreate ayarlayın

bir iç yük dengeleyicisi ayarlayın ve hello kendi trafiği tooit göndereceğiniz sunucuları toocreate gerçekleştirmelisiniz hello aşağıdaki:

1. İç yük iş yükünün bir yük dengeli kümesi hello sunucular arasında dengeli gelen trafik toobe hello uç nokta olacak Dengeleme örneği oluşturun.
2. Merhaba gelen trafiği almak toohello sanal makineleri karşılık gelen uç noktalarını ekleyin.
3. Kendi trafiği toohello sanal IP (VIP) adresi iç Yük Dengeleme hello örneğinin toosend hello trafiği toobe yük dengeli gönderme hello sunucularını yapılandırın.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>CLI kullanarak iç yük dengeleyici oluşturma adımları

Bu kılavuz, nasıl bir iç yük dengeleyici toocreate yukarıdaki hello senaryosu üzerine temel gösterir.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooclassic modu.

    ```azurecli
    azure config mode asm
    ```

    Beklenen çıktı:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Uç nokta ve yük dengeleyici kümesi oluşturma

Merhaba senaryo hello sanal makineler "DB1" ve "DB2" "mytestcloud" adlı bir bulut hizmetinde varsayar. Her iki sanal makine de "subnet-1" alt ağına sahip "testvnet" adlı bir sanal ağ kullanmaktadır.

Bu kılavuzda hem özel hem de yerel bağlantı noktası olarak 1433 numaralı bağlantı noktası kullanılarak bir iç yük dengeleyici kümesi oluşturulmaktadır.

Bu, bir ortak IP adresini kullanarak doğrudan bir iç yük dengeleyici tooguarantee hello veritabanı sunucuları sunulan olmaz arka uç hello kullanarak SQL sanal makineleri sahip olduğu ortak bir senaryodur.

### <a name="step-1"></a>1. Adım

`azure network service internal-load-balancer add` kullanarak iç yük dengeleyici kümesi oluşturun.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Daha fazla bilgi için bkz. `azure service internal-load-balancer --help`.

Merhaba komutunu kullanarak hello iç yük dengeleyici özelliklerini kontrol edebilirsiniz `azure service internal-load-balancer list` *bulut hizmeti adı*.

Burada hello çıktısı örneği aşağıdaki gibidir:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>2. Adım

Merhaba iç yük dengeleyici hello Birinci uç nokta eklediğinizde Ayarla yapılandırın. Bu adımda ayarlama hello uç noktasını, sanal makine ve araştırma bağlantı noktası toohello iç yük dengeleyici ilişkilendireceğiniz.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>3. Adım

Merhaba yük dengeleyici Yapılandırması kullanılarak doğrulayın `azure vm show` *sanal makine adı*

```azurecli
azure vm show DB1
```

Merhaba çıkış olacaktır:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Bir sanal makine için uzak masaüstü uç noktası oluşturma

Uzak Masaüstü uç nokta tooforward ağ trafiğini kullanarak belirli bir sanal makine için bir genel bağlantı noktası tooa yerel bağlantı noktasından oluşturabileceğiniz `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Sanal makineyi yük dengeleyiciden kaldırma

İlişkili hello uç noktası siliniyor tarafından ayarlanmış bir iç yük dengeleyici sanal makine kaldırabilirsiniz. Merhaba endpoint kaldırıldıktan sonra hello sanal makine artık ayarlamak toohello yük dengeleyici ait olmaz.

Yukarıdaki Hello örneği kullanarak, "DB1" sanal makine için oluşturulmuş hello endpoint iç yük dengeleyiciden "ilbset" Merhaba komutunu kullanarak kaldırabilirsiniz `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Daha fazla bilgi için bkz. `azure vm endpoint --help`.

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
