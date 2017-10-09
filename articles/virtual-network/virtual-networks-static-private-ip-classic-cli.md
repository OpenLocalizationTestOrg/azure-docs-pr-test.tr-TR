---
title: "aaaConfigure özel IP adresleri VM'ler (Klasik) - Azure CLI 1.0 için | Microsoft Docs"
description: "Nasıl tooconfigure özel IP adresleri kullanarak sanal makineleri (Klasik) için Azure komut satırı arabirimi (CLI) 1.0 hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [hello Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-cli.md).

Merhaba aşağıdaki örnek Azure CLI komutları önceden oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken
toocreate adlı yeni bir VM *DNS01* adlı yeni bir bulut hizmetinde *TestService* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki adımları izleyin:

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure hizmet oluşturma** toocreate hello bulut hizmeti komutu.
   
        azure service create TestService --location uscentral
   
    Beklenen çıktı:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Merhaba çalıştırmak **azure vm oluşturma** komutu toocreate hello VM. Özel bir statik IP adresi için Hello değer dikkat edin. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Beklenen çıktı:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (veya --location)**. Merhaba VM oluşturulacağı azure bölgesi. Bizim senaryomuz için bu *centralus* ’tur.
   * **-n (veya--vm adı)**. Merhaba VM toobe oluşturulan adı.
   * **-w (veya--ağ adı sanal)**. Merhaba hello VM oluşturulacağı Vnet'in adı. 
   * **-S (veya--statik IP)**. Özel için statik IP adresi hello VM.
   * **TestService**. Merhaba VM oluşturulacağı hello bulut hizmeti adı.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Görüntü toocreate hello VM kullanılır.
   * **AdminUser**. Merhaba Windows VM için yerel yönetici.
   * **AdminP@ssw0rd**. Merhaba Windows VM için yerel yönetici parolası.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi
tooview hello statik özel IP adresi VM, Azure CLI komutu aşağıdaki hello çalıştırmak yukarıdaki hello betiği ile oluşturulan bilgi hello için ve hello değeri uyun *ağ StaticIP*:

    azure vm static-ip show DNS01

Beklenen çıktı:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Nasıl tooremove bir statik özel IP adresi bir sanal makineden
tooremove hello statik özel IP adresi, yukarıda, Azure CLI komutu aşağıdaki çalışma hello hello komut toohello VM eklendi:

    azure vm static-ip remove DNS01

Beklenen çıktı:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Nasıl tooadd statik özel bir IP tooan var olan VM
bir statik özel IP adresi toohello komutu aşağıdaki yukarıdaki çalışma hello komut dosyası kullanılarak oluşturulan VM tooadd:

    azure vm static-ip set DNS01 192.168.1.101

Beklenen çıktı:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

