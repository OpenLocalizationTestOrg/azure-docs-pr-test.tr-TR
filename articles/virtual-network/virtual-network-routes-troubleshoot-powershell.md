---
title: aaaTroubleshoot yollar - PowerShell | Microsoft Docs
description: "Azure PowerShell kullanarak hello Azure Resource Manager dağıtım modelinde tootroubleshoot nasıl yönlendirir öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Azure PowerShell kullanarak yolları sorun giderme
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

Azure sanal makine (VM) gelen ağ bağlantısı sorunları tooor karşılaşıyorsanız, yolları VM trafik akışına etkiliyor olabilir. Bu makalede rotalar toohelp daha fazla sorun giderme için tanılama özelliklerine genel bakış sağlar.

Yönlendirme tabloları alt ağ ile ilişkili ve tüm ağ arabirimlerindeki (NIC) bu alt ağdaki etkili olur. şu yolların türlerini hello uygulanan tooeach ağ arabirimi olabilir:

* **Sistem yolları:** varsayılan olarak, yerel VNet trafiği, VPN ağ geçitleri üzerinden şirket içi trafik ve Internet trafiğini izin sistem yönlendirme tabloları bir Azure sanal ağı (VNet) içinde oluşturulan her alt ağ vardır. Sistem yolları da eşlenmiş Vnet'ler için mevcut.
* **BGP yolları:** toonetwork arabirimleri ExpressRoute veya siteden siteye VPN bağlantıları üzerinden yayılır. Merhaba okuyarak BGP yönlendirme hakkında daha fazla bilgi [VPN gateways ile BGP'ye](../vpn-gateway/vpn-gateway-bgp-overview.md) ve [ExpressRoute genel bakış](../expressroute/expressroute-introduction.md) makaleleri.
* **Kullanıcı tanımlı yolları (UDR):** ağ sanal Gereçleri kullanıyorsanız veya zorlamalı tünel olan trafik tooan içi ağınıza bir siteden siteye VPN aracılığıyla alt yol tablosu ile ilişkili kullanıcı tanımlı yollar (Udr'ler) olabilir. İle Udr'ler bilmiyorsanız hello okuma [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md#user-defined-routes) makalesi.

Merhaba ile uygulanan tooa ağ arabirimi, olabilecek çeşitli yollar, zor toodetermine toplama hangi rotalar etkili olabilir. toohelp VM ağ bağlantısı sorunlarını giderme, bir ağ arabirimi için tüm hello etkili yollar hello Azure Resource Manager dağıtım modelinde görüntüleyebilirsiniz.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Etkin yollar tootroubleshoot VM trafik akışı kullanma
Bu makalede nasıl tootroubleshoot hello etkili bir ağ arabirimi için yönlendiren bir örnek tooillustrate olarak senaryo aşağıdaki hello kullanır:

Bir VM'yi (*VM1*) toohello VNet bağlı (*VNet1*, öneki: 10.9.0.0/16) tooconnect tooa VM(VM3) yeni vnet'teki başarısız (*VNet3*, 10.10.0.0/16 öneki). Uygulanan tooVM1 nıc1 ağ arabirimi bağlı toohello VM Udr'ler ya da BGP yolları, yalnızca sistem yolları uygulanır vardır.

Bu makalede nasıl toodetermine hello neden hello bağlantı hatası, Azure kaynak yönetimi dağıtım modelinde etkili yollar özelliği kullanarak, açıklanmaktadır.
Yalnızca sistem yolları Hello örnek kullanıyor, ancak aynı adımları hello kullanılan toodetermine herhangi bir rota türü gelen ve giden bağlantı hataları olabilir.

> [!NOTE]
> VM bağlı birden çok NIC varsa, her hello NIC toodiagnose ağ bağlantısı sorunları tooand bir VM'den etkili yolları denetleyin.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>Bir sanal makine için Görünüm etkili yolları
uygulanan tooa VM, aşağıdaki adımları tam hello olan toosee hello toplama yollar:

### <a name="view-effective-routes-for-a-network-interface"></a>Bir ağ arabirimi için Görünüm etkili yolları
uygulanan tooa ağ arabirimi, aşağıdaki adımları tam hello olan toosee hello toplama yollar:

1. Bir Azure PowerShell oturumu ve oturum açma tooAzure başlatın. Azure PowerShell ile bilmiyorsanız hello okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.
2. Merhaba aşağıdaki komut döndürür tüm yollar uygulanan tooa ağ arabirimi adlı *VM1 nıc1* hello kaynak grubunda *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Bir ağ arabirimi hello adını bilmiyorsanız, bir kaynak group.* tüm ağ arabirimlerini komut tooretrieve hello adlarını aşağıdaki hello yazın
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Merhaba aşağıdaki çıkış benzer toohello çıkış NIC bağlı her uygulanan rota toohello alt hello arar:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Merhaba çıktısında Hello aşağıdakilere dikkat edin:
   
   * **Ad**: açıkça belirtilen, kullanıcı tanımlı yollar için sürece hello etkili rotanın adı boş olabilir. 
   * **Durum**: hello etkin yönlendirme durumunu gösterir. "Active" veya "Geçersiz" olası değerler şunlardır:
   * **AddressPrefixes**: CIDR gösteriminde hello etkin yönlendirme hello adres öneki belirtir. 
   * **nextHopType**: yol verilen hello için sonraki atlama hello gösterir. Olası değerler şunlardır: *değerinin VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, veya *Null*. Değerini *Null* için **nextHopType** bir UDR geçersiz bir yol gösteriyor olabilir. Örneğin, varsa **nextHopType** olan *değerinin VirtualAppliance* ve hello ağ sanal gereç VM sağlanan çalışıyor durumda değil. Varsa **nextHopType** olan *VPNGateway* ve VNet verilen hello sağlanan/çalışan ağ geçidi yok ise, hello yol geçersiz hale gelebilir.
   * **Nexthopıpaddress**: hello etkili yolunun sonraki atlama hello hello IP adresini belirtir.
   
   Merhaba aşağıdaki komut hello yolları daha kolay bir tooview tabloda döndürür:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Merhaba aşağıdaki çıkış daha önce açıklanan hello senaryosu için alınan hello çıkış bazıları verilmiştir:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Listelenen rota toohello yok *WestUS VNet3* VNet (10.10.0.0/16)** gelen önek *WestUS VNet1* (10.9.0.0/16 önek) hello önceki adımdaki hello çıkışı. Hello resim aşağıdaki gösterildiği gibi VNet eşleme bağlantısı ile Merhaba hello *WestUS VNet3* VNet olan hello *bağlantı kesildi* durumu.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    Merhaba çift yönlü bağlantı hello eşliği bozuk için açıklayan neden VM1 hello tooVM3 bağlanamadı *WestUS VNet3* VNet. Çift yönlü bir VNet eşleme bağlantısı yeniden için Kurulum *WestUS VNet1* ve *WestUS VNet3* sanal ağlar. Merhaba VNet eşleme bağlantısı doğru kurulduktan sonra döndürülen hello çıktı aşağıdaki gibidir:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Ekleyebilir, hello sorunu belirledikten sonra kaldırmak veya yolları değiştirmek ve tabloları rota. Merhaba komutu toosee hello kullanılan komutlar toodo listesini şekilde aşağıdaki komutu yazın:
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Merhaba yolların listesini gözden geçirirken aklınızda birkaç şey tookeep döndürdü:

* Yönlendirme üzerinde en uzun ön ek eşleşmesi (LPM) Udr'ler arasında temel BGP ve sistem yolları. Hello sahip birden fazla yol varsa aynı LPM eşleşmesi, sonra da bir yol, özgün sırasının hello göre seçilir:
  
  * Kullanıcı tanımlı yol
  * BGP yolu
  * Sistem (varsayılan) yolu
    
    Etkin yollar ile LPM eşleşmesine tüm hello kullanılabilir yollarına bağlı olduğundan geçerlilik yollar yalnızca görebilirsiniz. Nasıl hello yollar için belirli bir NIC gerçekte değerlendirildiği göstererek bu VM/gruptan bağlantı etkileyen çok daha kolay tootroubleshoot belirli yollar sağlar.
* Udr'ler varsa ve trafik tooa ağ sanal gereç (NVA) ile gönderiyor *değerinin VirtualAppliance* olarak **nextHopType**, IP iletimini hello NVA alıcı hello trafiği üzerinde etkinleştirildiğinden emin olun veya paket bırakılır. 
* Zorlamalı tünel etkinleştirildiğinde tüm giden Internet trafiği yönlendirilmiş tooon içi olur. RDP/SSH VM nasıl hello şirket içi bağlı olarak bu ayar ile çalışmayabilir Internet tooyour bu trafiği işler. 
  Zorlamalı tünel etkinleştirilebilir:
  * Siteden siteye VPN, VPN ağ geçidi olarak nextHopType ile bir kullanıcı tanımlı yönlendirme (UDR) ayarlayarak kullanıyorsanız
  * Varsayılan rota BGP Tanıtımı
* Sanal ağ trafiğini toowork doğru eşleme bir sistem rotası için **nextHopType** *VNetPeering* sanal ağınızın önek aralığı hello eşlenen için mevcut olması gerekir. Böyle bir yol mevcutsa değil ve VNet eşlemesi hello bağlantı Tamam görünür:
  * Birkaç saniye bekleyin ve yeni oluşturulmuş bir eşleme bağlantısı ise, yeniden deneyin. Bazen uzun toopropagate yollar tooall hello ağ arabirimleri bir alt ağdaki alır.
  * Ağ güvenlik grubu (NSG) kuralları hello trafik akışına etkiliyor olabilir. Merhaba daha fazla bilgi için bkz: [sorun giderme ağ güvenlik grupları](virtual-network-nsg-troubleshoot-powershell.md) makalesi.

