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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="7ef8b-104">Linux VM’leri için DHCPv6’yı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7ef8b-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="7ef8b-105">Merhaba Linux sanal makine görüntülerini hello Azure Marketi bazıları varsayılan olarak yapılandırılan DHCPv6 sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="7ef8b-106">IPv6, DHCPv6 toosupport kullanmakta olduğunuz hello Linux işletim sistemi dağıtım içinde yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="7ef8b-107">Farklı Linux dağıtımları farklı paketler kullandığından, DHCPv6 yapılandırma farklı yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="7ef8b-108">Hello Azure Marketi son SUSE Linux ve CoreOS görüntüleri DHCPv6 ile önceden yapılandırılmış olmuştur.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="7ef8b-109">Bu görüntüleri kullanırken, ek değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="7ef8b-110">Bu belgede açıklanan nasıl tooenable DHCPv6 böylece Linux sanal makine bir IPv6 adresi alır.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="7ef8b-111">Ağ yapılandırma dosyalarını yanlış düzenlenmesi, toolose ağ erişim tooyour VM neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="7ef8b-112">Üretim dışı sistemlere yapılandırma değişikliklerinizi test önerilir.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="7ef8b-113">Bu makaledeki yönergeleri Hello hello son hello Linux hello Azure Marketi görüntülerinde sürümlerinde test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="7ef8b-114">Sürümünüzün Linux daha ayrıntılı yönergeler için Hello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="7ef8b-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7ef8b-115">Ubuntu</span></span>

1. <span data-ttu-id="7ef8b-116">Merhaba dosyasını düzenleyin `/etc/dhcp/dhclient6.conf` ve hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="7ef8b-117">Merhaba hello eth0 arabirimi için ağ yapılandırması ile yapılandırma aşağıdaki hello düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="7ef8b-118">Üzerinde **Ubuntu 12.04 ve 14.04**, hello dosyasını düzenleyin`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="7ef8b-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="7ef8b-119">Üzerinde **Ubuntu 16.04**, hello dosyasını düzenleyin`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="7ef8b-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="7ef8b-120">IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="7ef8b-121">Debian</span><span class="sxs-lookup"><span data-stu-id="7ef8b-121">Debian</span></span>

1. <span data-ttu-id="7ef8b-122">Merhaba dosyasını düzenleyin `/etc/dhcp/dhclient6.conf` ve hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="7ef8b-123">Merhaba dosyasını düzenleyin `/etc/network/interfaces` ve yapılandırma aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="7ef8b-124">IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="7ef8b-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="7ef8b-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="7ef8b-126">Merhaba dosyasını düzenleyin `/etc/sysconfig/network` ve parametre aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="7ef8b-127">Merhaba dosyasını düzenleyin `/etc/sysconfig/network-scripts/ifcfg-eth0` ve şu iki parametreler hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="7ef8b-128">IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="7ef8b-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="7ef8b-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="7ef8b-130">Azure'nün en son SLES ve openSUSE görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="7ef8b-131">Bu görüntüleri kullanırken, ek değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="7ef8b-132">Bir özel veya eski SUSE görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="7ef8b-133">Merhaba yüklemek `dhcp-client` gerekiyorsa, paket:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="7ef8b-134">Merhaba dosyasını düzenleyin `/etc/sysconfig/network/ifcfg-eth0` ve parametre aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="7ef8b-135">Merhaba IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="7ef8b-136">SLES 12 ve openSUSE artık</span><span class="sxs-lookup"><span data-stu-id="7ef8b-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="7ef8b-137">Azure'nün en son SLES ve openSUSE görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="7ef8b-138">Bu görüntüleri kullanırken, ek değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="7ef8b-139">Bir özel veya eski SUSE görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="7ef8b-140">Merhaba dosyasını düzenleyin `/etc/sysconfig/network/ifcfg-eth0` ve bu parametre değiştirme</span><span class="sxs-lookup"><span data-stu-id="7ef8b-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="7ef8b-141">Aşağıdaki değeri hello ile:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="7ef8b-142">Parametre çok aşağıdaki hello eklemek`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="7ef8b-143">Merhaba IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="7ef8b-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7ef8b-144">CoreOS</span></span>

<span data-ttu-id="7ef8b-145">Azure son CoreOS görüntülerinde DHCPv6 ile önceden yapılandırılmış olmuştur.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="7ef8b-146">Bu görüntüleri kullanırken, ek değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ef8b-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="7ef8b-147">Bir özel veya eski CoreOS görüntüyü temel alarak bir VM'niz varsa, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="7ef8b-148">Merhaba dosyasını düzenleyin`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="7ef8b-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="7ef8b-149">Merhaba IPv6 adresi yenileme:</span><span class="sxs-lookup"><span data-stu-id="7ef8b-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
