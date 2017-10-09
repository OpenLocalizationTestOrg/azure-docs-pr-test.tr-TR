---
title: "Linux VM'ler için DHCPv6 aaaConfiguring | Microsoft Docs"
description: "Nasıl tooconfigure DHCPv6 Linux VM'ler için."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>Linux VM’leri için DHCPv6’yı yapılandırma

Merhaba Linux sanal makine görüntülerini hello Azure Marketi bazıları varsayılan olarak yapılandırılan DHCPv6 sahip değilsiniz. IPv6, DHCPv6 toosupport kullanmakta olduğunuz hello Linux işletim sistemi dağıtım içinde yapılandırılmalıdır. Farklı Linux dağıtımları farklı paketler kullandığından, DHCPv6 yapılandırma farklı yolu vardır.

> [!NOTE]
> Hello Azure Marketi son SUSE Linux ve CoreOS görüntüleri DHCPv6 ile önceden yapılandırılmış olmuştur. Bu görüntüleri kullanırken, ek değişiklik gerekmez.

Bu belgede açıklanan nasıl tooenable DHCPv6 böylece Linux sanal makine bir IPv6 adresi alır.

> [!WARNING]
> Ağ yapılandırma dosyalarını yanlış düzenlenmesi, toolose ağ erişim tooyour VM neden olabilir. Üretim dışı sistemlere yapılandırma değişikliklerinizi test önerilir. Bu makaledeki yönergeleri Hello hello son hello Linux hello Azure Marketi görüntülerinde sürümlerinde test edilmiştir. Sürümünüzün Linux daha ayrıntılı yönergeler için Hello belgelerine başvurun.

## <a name="ubuntu"></a>Ubuntu

1. Merhaba dosyasını düzenleyin `/etc/dhcp/dhclient6.conf` ve hello aşağıdaki satırı ekleyin:

        timeout 10;

2. Merhaba hello eth0 arabirimi için ağ yapılandırması ile yapılandırma aşağıdaki hello düzenleyin:

   * Üzerinde **Ubuntu 12.04 ve 14.04**, hello dosyasını düzenleyin`/etc/network/interfaces.d/eth0.cfg`
   * Üzerinde **Ubuntu 16.04**, hello dosyasını düzenleyin`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6 adresi yenileme:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Merhaba dosyasını düzenleyin `/etc/dhcp/dhclient6.conf` ve hello aşağıdaki satırı ekleyin:

        timeout 10;

2. Merhaba dosyasını düzenleyin `/etc/network/interfaces` ve yapılandırma aşağıdaki hello ekleyin:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. IPv6 adresi yenileme:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Merhaba dosyasını düzenleyin `/etc/sysconfig/network` ve parametre aşağıdaki hello ekleyin:

        NETWORKING_IPV6=yes

2. Merhaba dosyasını düzenleyin `/etc/sysconfig/network-scripts/ifcfg-eth0` ve şu iki parametreler hello ekleyin:

        IPV6INIT=yes
        DHCPV6C=yes

3. IPv6 adresi yenileme:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

Azure'nün en son SLES ve openSUSE görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur. Bu görüntüleri kullanırken, ek değişiklik gerekmez. Bir özel veya eski SUSE görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:

1. Merhaba yüklemek `dhcp-client` gerekiyorsa, paket:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Merhaba dosyasını düzenleyin `/etc/sysconfig/network/ifcfg-eth0` ve parametre aşağıdaki hello ekleyin:

        DHCLIENT6_MODE='managed'

3. Merhaba IPv6 adresi yenileme:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 ve openSUSE artık

Azure'nün en son SLES ve openSUSE görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur. Bu görüntüleri kullanırken, ek değişiklik gerekmez. Bir özel veya eski SUSE görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:

1. Merhaba dosyasını düzenleyin `/etc/sysconfig/network/ifcfg-eth0` ve bu parametre değiştirme

        #BOOTPROTO='dhcp4'

    Aşağıdaki değeri hello ile:

        BOOTPROTO='dhcp'

2. Parametre çok aşağıdaki hello eklemek`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Merhaba IPv6 adresi yenileme:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Azure son CoreOS görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur. Bu görüntüleri kullanırken, ek değişiklik gerekmez. Bir özel veya eski CoreOS görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:

1. Merhaba dosyasını düzenleyin`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Merhaba IPv6 adresi yenileme:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
