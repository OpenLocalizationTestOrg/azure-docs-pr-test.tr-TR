---
title: "aaaTroubleshoot ağ güvenlik grupları - PowerShell | Microsoft Docs"
description: "Azure PowerShell kullanarak nasıl tootroubleshoot ağ güvenlik grupları'hello Azure Resource Manager dağıtımında model öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Ağ güvenlik grupları Azure PowerShell kullanarak sorun giderme
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Ağ güvenlik grupları (Nsg'ler), sanal makine (VM) üzerinde yapılandırılmış ve VM bağlantı sorunları yaşıyorsanız, bu makalede Nsg'ler toohelp daha fazla sorun giderme için tanılama özelliklerine genel bakış sağlar.

Nsg'ler toocontrol hello trafik türlerini ve sanal makineleri (VM'ler) dışındaki akan sağlar. Nsg'ler uygulanan toosubnets bir Azure sanal ağı (VNet), ağ arabirimleri (NIC) veya her ikisi de olabilir. bir toplama bağlı hello uygulanan Nsg'ler tooa NIC ve hello alt ağda bulunan hello kuralların Hello uygulanacak etkili kurallar tooa NIC var. Bu Nsg'ler arasında kuralları bazen birbiriyle çelişen ve bir sanal makinenin ağ bağlantısını etkileyebilir.  

VM Nıc'lerde uygulanan olarak Nsg'lerinizi tüm hello etkin güvenlik kuralları görüntüleyebilirsiniz. Bu makalede Azure Resource Manager dağıtım modeli bu kuralları kullanmak tootroubleshoot VM bağlantı sorunları nasıl hello gösterilmektedir. VNet ve NSG kavramlarına alışık değilseniz, hello okuma [sanal ağ](virtual-networks-overview.md) ve [ağ güvenlik grupları](virtual-networks-nsg.md) genel bakış makaleleri.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Etkin güvenlik kuralları tootroubleshoot VM trafik akışı kullanma
izleyen hello senaryo, ortak bir bağlantı sorunu örneğidir:

Adlı bir VM'den *VM1* adlı bir alt ağın parçası olan *Subnet1* adlı bir sanal ağ içindeki *WestUS VNet1*. Bir deneme tooconnect toohello 3389 numaralı TCP bağlantı noktası üzerinden RDP kullanarak VM başarısız olur. Nsg'ler NIC hem hello uygulanan *VM1 nıc1* ve alt ağ hello *Subnet1*. Trafik tooTCP 3389 numaralı bağlantı noktasını hello hello ağ arabirimiyle ilişkilendirilmiş NSG izin verilen *VM1 nıc1*, TCP ping ancak tooVM1'ın bağlantı noktası 3389 başarısız olur.

Bu örnek 3389 numaralı TCP bağlantı noktasını kullanır, ancak adımları hello kullanılan toodetermine herhangi bir bağlantı noktası gelen ve giden bağlantı hataları olabilir.

## <a name="detailed-troubleshooting-steps"></a>Ayrıntılı sorun giderme adımları
Bir VM için adımları tootroubleshoot Nsg'ler aşağıdaki hello tamamlayın:

1. Bir Azure PowerShell oturumu ve oturum açma tooAzure başlatın. Azure PowerShell ile bilmiyorsanız hello okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.
2. Tooreturn tüm NSG kuralları uygulanan tooa adlı NIC komutu aşağıdaki hello girin *VM1 nıc1* hello kaynak grubunda *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Bir NIC hello adını bilmiyorsanız, bir kaynak grubundaki tüm NIC'ler komut tooretrieve hello adlarını aşağıdaki hello girin: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Merhaba aşağıdaki metni Merhaba döndürülen hello etkili kuralları çıkış örneğidir *VM1 nıc1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Aşağıdaki bilgilerle hello çıktısında hello dikkat edin:
   
   * Var olan iki **NetworkSecurityGroup** bölümler: bir alt ağ ile ilişkili biridir (*Subnet1*) ve bir NIC ile ilişkili olduğu (*VM1 nıc1*). Bu örnekte, bir NSG uygulanan tooeach olmuştur.
   * **İlişkilendirme** hello kaynak (alt ağ veya NIC) belirli bir NSG ile ilişkili olduğunu gösterir. Merhaba NSG kaynağı hemen bu komutu çalıştırmadan önce taşınmış ve ilişkilendirmesi ise, birkaç saniye toowait hello değişiklik tooreflect hello komut çıktısında için gerekebilir. 
   * Merhaba ile başlayan kuralı adları *defaultSecurityRules*: olduğunda bir NSG oluşturulur, birkaç varsayılan güvenlik kuralları içinde oluşturulur. Varsayılan kurallar kaldırılamaz, ancak daha yüksek öncelik kuralları ile geçersiz kılınabilir.
     Okuma hello [NSG genel bakış](virtual-networks-nsg.md#default-rules) NSG hakkında daha fazla makale toolearn varsayılan güvenlik kuralları.
   * **ExpandedAddressPrefix** hello adres öneklerini NSG varsayılan etiketleri için genişletir. Etiketler, birden çok adres öneklerini temsil eder. Merhaba etiketleri genişlemesi denetleyicisinden belirli adres öneklerini VM bağlantı sorunlarını giderirken faydalı olabilir. Örneğin, VNET eşlemesi ile VIRTUAL_NETWORK etiketine tooshow genişletir VNet ön hello önceki çıktısında eşlenen.
     
     > [!NOTE]
     > bir NSG'yi bir alt ağ, bir NIC veya her ikisi ile ilişkili ise, komut yalnızca gösterir etkili kuralları hello. Bir VM uygulanan farklı Nsg'ler ile birden çok NIC olabilir. Sorunlarını giderirken, her bir NIC hello komutunu çalıştırın
     > 
     > 
3. NSG kuralları, fazla sayıda filtreleme tooease başka komutlar tootroubleshoot aşağıdaki hello girin: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    RDP trafiğine (TCP bağlantı noktası 3389) için bir filtre hello resim aşağıdaki gösterildiği gibi toohello Izgara Görünümü uygulanır:
   
    ![Kuralları listesi](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Merhaba ızgara görünümünde görebileceğiniz gibi vardır her ikisi de izin ver ve Reddet kurallarının için RDP. Merhaba 2. adım çıktısını gösterir, hello *DenyRDP* hello NSG uygulanır toohello alt kuralıdır. Gelen kuralları için uygulanan Nsg'ler toohello alt önce işlenir. Bir eşleşme bulunamazsa hello NSG uygulanır toohello ağ arabirimi işlenmedi. Bu durumda, hello *DenyRDP* kural hello alt ağından gelen RDP toohello VM engeller (**VM1**).
   
   > [!NOTE]
   > Bir VM birden çok NIC ekli tooit olabilir. Her bağlı tooa farklı alt olabilir. Merhaba komutlar hello önceki adımlarda karşı bir NIC çalıştırılır, belirttiğiniz tooensure hello hello bağlantı hatası yaşıyoruz NIC önemlidir. Emin değilseniz, her bağlı NIC toohello VM karşı her zaman hello komutları çalıştırabilirsiniz.
   > 
   > 
5. VM1, değişiklik hello içine tooRDP *Reddet RDP (3389)* çok kural*izin RDP(3389)* hello içinde **Subnet1 NSG** NSG. TCP bağlantı noktası 3389 RDP bağlantı toohello VM açma veya hello PsPing aracını kullanarak açık olduğundan emin olun. Okuma hello tarafından PsPing hakkında daha fazla bilgiyi [PsPing indirme sayfası](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Komutu aşağıdaki hello hello çıktısını hello bilgileri kullanarak bir NSG kuralları kaldırın ve yapabilirsiniz:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Bağlantı sorunları giderirken noktaları aşağıdaki hello göz önünde bulundurun:

* Varsayılan NSG kuralları hello'ten gelen erişim engeller Internet ve yalnızca izin VNet gelen trafiği. Kuralları açıkça eklenmesi tooallow gelen gerektiği gibi Internet'ten erişim.
* Bir sanal makinenin ağ bağlantısı toofail neden hiçbir NSG güvenlik kuralları varsa, hello sorun nedeniyle olabilir:
  * Merhaba VM'ın işletim sistemi içinde çalışan güvenlik duvarı yazılımı
  * Sanal gereçler veya şirket içi trafiği için yapılandırılmış yollar. Internet trafiğini yeniden yönlendirilen tooon içi zorlamalı tünel aracılığıyla olabilir. Merhaba Internet tooyour VM bir RDP/SSH bağlantısı nasıl hello şirket içi ağ donanımı bu trafiği işler bağlı olarak bu ayar ile çalışmayabilir. Okuma hello [sorun giderme yolları](virtual-network-routes-troubleshoot-powershell.md) makale toolearn içinde ve dışında trafik akışını engelleyen toodiagnose rota sorunları hello nasıl VM hello. 
* Varsayılan olarak sanal ağlar, eşlenen durumdaysa hello VIRTUAL_NETWORK etiketine tooinclude önekleri eşlenmiş Vnet'ler için otomatik olarak genişletin. Bu önekleri hello görüntüleyebilirsiniz **ExpandedAddressPrefix** listesi olan bağlantı eşliği sorunları ilgili tooVNet tootroubleshoot. 
* Etkin güvenlik kuralları, bir NSG hello VM'in NIC ve veya alt ağ ilişkili olup yalnızca gösterilir. 
* Merhaba NIC ile ilişkili hiçbir Nsg'ler vardır veya alt ağ ve tooyour VM atanan genel bir IP adresi varsa, tüm bağlantı noktalarına gelen ve giden erişimi açık olacaktır. Merhaba VM genel bir IP adresi varsa, Nsg'ler toohello NIC veya alt ağ uygulama önemle tavsiye edilir.  

