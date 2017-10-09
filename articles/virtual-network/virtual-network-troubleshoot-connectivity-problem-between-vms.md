---
title: "Azure VM'ler arasında aaaTroubleshooting bağlantısı sorunları | Microsoft Docs"
description: "Nasıl tooTroubleshoot hello Azure VM'ler arasında bağlantı sorunları hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Azure VM'ler arasında bağlantı sorunlarını giderme

Azure VM'ler arasında bağlantı sorunları yaşayabilirsiniz. Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Belirti

Bir Azure VM tooanother Azure VM bağlanamıyor.

## <a name="troubleshooting-guidance"></a>Sorun giderme rehberi 

1. [NIC yanlış olmadığını denetleyin](#step-1-check-if-nic-is-misconfigured)
2. [Ağ trafiği NSG veya UDR tarafından bloke edilmiş olup olmadığını denetleyin](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Ağ trafiği bir VM Güvenlik Duvarı tarafından engellenir denetleyin](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını denetleyin](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Tarafından SNAT Hello soruna neden olup olmadığını denetleyin](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Onay trafiği için ACL'ler tarafından engellenmiş olup olmadığını hello Klasik VM](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Onay hello uç noktası için oluşturulup oluşturulmadığını hello Klasik VM](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [%S tooconnect tooa VM ağ paylaşımı](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Ağlar arası Vnet bağlantısı](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Sorun giderme adımları

Bu adımları tootroubleshoot hello sorunu izleyin. Her adımdan sonra Hello sorunun giderilmiş olup olmadığını denetleyin. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>1. adım: NIC yanlış olmadığını denetleyin

İzleyin [nasıl tooreset ağ arabirimi için Azure Windows VM](../virtual-machines/windows/reset-network-interface.md). 

Merhaba ağ arabirimi (NIC) değiştirdikten sonra hello sorun oluşursa, şu adımları izleyin:

**Mulit-NIC VM**

1. Bir NIC ekleme
2. Merhaba hatalı NIC veya kaldırma hatalı NIC Hello sorunları giderin  Merhaba NIC readd

Daha fazla bilgi için bkz: [Ekle ağ arabirimleri tooor sanal makinelerden kaldırmak](virtual-network-network-interface-vm.md).

**Tek NIC VM** 

- [Windows VM yeniden dağıtın](../virtual-machines/windows/redeploy-to-new-node.md)
- [Linux VM yeniden dağıtın](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>2. adım: ağ trafiği NSG veya UDR tarafından bloke edilmiş olup olmadığını denetleyin

Kullanan [Ağ İzleyicisi IP akış doğrulayın](../network-watcher/network-watcher-ip-flow-verify-overview.md) ve [NSG akış günlüğü](../network-watcher/network-watcher-nsg-flow-logging-overview.md) bir ağ güvenlik grubu veya kullanıcı tanımlı yol, trafik akışı ile engellemesini ise tooidentify.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>3. adım: ağ trafiği bir VM Güvenlik Duvarı tarafından engellenir denetleyin

Hello Güvenlik Duvarı'nı devre dışı bırakın ve ardından hello sonucunu sınayın. Merhaba sorunun giderilip giderilmediğini hello Güvenlik Duvarı'nda hello ayarlarını doğrulayın ve yeniden etkinleştirin.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>4. adım: VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını denetleyin

VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını yöntemleri toocheck aşağıdaki hello birini kullanabilirsiniz

- Merhaba sunucu bu bağlantı noktasında dinleme olup olmadığını komutları toocheck aşağıdaki hello çalıştırın.

**Windows VM**

    netstat –ano

**Linux VM**

    netstat -l

- Merhaba çalıştırmak **Telnet** hello VM tooitself tootest hello bağlantı noktası üzerinde komutu. Merhaba testi başarısız olursa, uygulama veya hizmet hello bağlantı noktasında yapılandırılmış toolisten değil.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>5. adım: SNAT tarafından hello soruna neden olup olmadığını denetleyin

Bazı senaryolarda hello VM kaynakların Azure dışında bir bağımlılığa sahip bir yük dengeleme çözümü arkasında yer alır. Aralıklı bağlantısı sorunlar yaşıyorsanız bu senaryolarda, hello sorunun nedeni olabilir [SNAT bağlantı noktası Tükenme](../load-balancer/load-balancer-outbound-connections.md). tooresolve hello sorun hello yük dengeleyicinin arkasına olan her bir VM için bir VIP (veya Klasik ILPIP) oluşturun ve NSG veya ACL ile güvenli. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>6. adım: Onay trafiği için ACL'ler tarafından engellenmiş olup olmadığını hello Klasik VM

Bir ACL veya bir sanal makine uç noktası için trafiği reddetmeye hello özelliği tooselectively izin sağlar. Daha fazla bilgi için bkz: [uç noktada Yönet hello ACL](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>7. adım: Onay hello uç noktası için oluşturulup oluşturulmadığını hello Klasik VM

Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz tüm sanal makineleri otomatik olarak hello içindeki diğer sanal makinelerle özel ağ kanalı üzerinden aynı hizmet veya sanal ağ bulut iletişim kurabilir. Ancak, diğer sanal ağlardaki bilgisayarlara uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir. Daha fazla bilgi için bkz: [nasıl tooset uç noktaları yukarı](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>8. adım: Oluşturulamıyor tooconnect tooa VM ağ paylaşımı

%S tooconnect tooa VM ağ paylaşımı varsa, hello VM içinde kullanılamaz NIC tarafından hello sorunu neden olabilir. toodelete kullanılamayan NICs Merhaba, bkz: [nasıl toodelete hello kullanılamaz NIC](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>9. adım: Arası Vnet bağlantısı

Kullanan [Ağ İzleyicisi IP akış doğrulayın](../network-watcher/network-watcher-ip-flow-verify-overview.md) ve [NSG akış günlüğü](../network-watcher/network-watcher-nsg-flow-logging-overview.md) bir ağ güvenlik grubu veya kullanıcı tanımlı yol, trafik akışı ile engellemesini ise tooidentify. Inter-Vnet yapılandırmasını doğrulamak için [burada](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
