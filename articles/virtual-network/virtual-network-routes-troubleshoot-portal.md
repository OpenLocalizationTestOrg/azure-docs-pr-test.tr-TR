---
title: "aaaTroubleshoot yollar - portalı | Microsoft Docs"
description: "Nasıl tootroubleshoot yollar'hello Azure Resource Manager dağıtım modelini kullanarak Azure Portal hello öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Yollar Hello Azure Portal kullanarak sorun giderme
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

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **sanal makineleri** hello listesinde görünür.
3. VM tootroubleshoot görüntülenen hello listesinden seçin ve seçeneklerle bir VM dikey penceresi görünür.
4. Tıklatın **Tanıla & sorunları** ve ortak bir sorun seçin. Bu örnek için **toomy Windows VM bağlantı kurulamıyor** seçilir.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Adımları hello sorun altında hello resim aşağıdaki gösterildiği gibi görünür:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Tıklatın *etkili yolları* önerilen adımları hello listesinde.
6. Merhaba **etkili yolları** hello resim aşağıdaki gösterildiği gibi dikey penceresi görünür:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Tek bir NIC VM varsa, varsayılan olarak seçilidir. Birden çok NIC varsa, tooview hello etkili yolları istediğiniz hello NIC seçin.

   > [!NOTE]
   > Merhaba VM ile ilişkili hello NIC çalışır durumda değil, etkin yollar gösterilmez. Yalnızca hello ilk 200 etkili yolları hello Portalı'nda gösterilmektedir. Merhaba tam listesi için tıklatın **karşıdan**. Daha fazla hello indirilen .csv dosyasından hello sonuçları filtreleyebilirsiniz.
   >
   >

    Merhaba çıktısında Hello aşağıdakilere dikkat edin:

   * **Kaynak**: hello rota türünü belirtir. Sistem yolları olarak gösterilir *varsayılan*, Udr'ler olarak gösterilir *kullanıcı* ve ağ geçidi yollarını (statik ya da BGP) olarak gösterilen *VPNGateway*.
   * **Durum**: hello etkin yönlendirme durumunu gösterir. Olası değerler şunlardır: *etkin* veya *geçersiz*.
   * **AddressPrefixes**: CIDR gösteriminde hello etkin yönlendirme hello adres öneki belirtir.
   * **nextHopType**: yol verilen hello için sonraki atlama hello gösterir. Olası değerler şunlardır: *değerinin VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, veya *Null*. Değerini *Null* için **nextHopType** bir UDR geçersiz bir yol gösteriyor olabilir. Örneğin, varsa **nextHopType** olan *değerinin VirtualAppliance* ve hello ağ sanal gereç VM sağlanan çalışıyor durumda değil. Varsa **nextHopType** olan *VPNGateway* ve VNet verilen hello sağlanan/çalışan ağ geçidi yok ise, hello yol geçersiz hale gelebilir.
7. Listelenen rota toohello yok *WestUS VNET3* hello (önek 10.10.0.0/16) ağdan *WestUS VNet1* (10.9.0.0/16 önek) hello önceki adımda hello resimdeki. Resim aşağıdaki hello hello hello eşleme bağlantısı olan *bağlantı kesildi* durumu:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    Merhaba çift yönlü bağlantı hello eşliği bozuk için açıklayan neden VM1 hello tooVM3 bağlanamadı *WestUS VNet3* VNet.
8. Merhaba aşağıdaki resimde hello yollar hello çift yönlü eşleme bağlantı kurulduktan sonra gösterilmiştir:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Zorlamalı tünel ve rota değerlendirme için daha fazla sorun giderme senaryoları için hello okuyun [konuları](virtual-network-routes-troubleshoot-portal.md#considerations) bu makalenin.

### <a name="view-effective-routes-for-a-network-interface"></a>Bir ağ arabirimi için Görünüm etkili yolları
Ağ trafiği akışını belirli bir ağ arabirimi (NIC) için etkilenen varsa etkili yolların tam bir listesi NIC üzerinde doğrudan görüntüleyebilirsiniz. uygulanan tooa NIC, aşağıdaki adımları tam hello olan toosee hello toplama yollar:

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **ağ arabirimleri**
3. Bir NIC hello adını Hello listede arama veya görüntülenen hello listesinden seçin. Bu örnekte, **VM1 nıc1** seçilir.
4. Seçin **etkili yolları** hello içinde **ağ arabirimi** hello resim aşağıdaki gösterildiği gibi dikey penceresinde:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Merhaba **kapsam** seçili Varsayılanları toohello ağ arabirimi.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Görünüm etkili yollar için bir yol tablosu
Kullanıcı tanımlı yollar (Udr'ler) rota tablosunda değiştirirken, belirli bir VM'de eklenmekte olan hello yolların tooreview hello etkisi isteyebilirsiniz. Bir yol tablosu alt ağlar herhangi bir sayı ile ilişkili olabilir. Tüm belirtilen yol tablosu uygulandığı NIC'ler hello için tüm hello etkili yollar artık görüntüleyebilirsiniz rota tablosu dikey verilen hello tooswitch bağlamdan kalmadan.

Bu örneğin, bir UDR (*UDRoute*) rota tablosunda belirtilen (*UDRouteTable*). Bu rotanın gelen tüm Internet trafiğini gönderir *Subnet1* hello içinde *WestUS VNet1* ağ sanal gereç (NVA) aracılığıyla VNet içinde *Altağ2* , aynı sanal ağı hello. Merhaba rota resim aşağıdaki hello gösterilir:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee hello toplama yollar için aşağıdaki adımları tam hello bir yol tablosu:

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **yol tablosu**
3. Merhaba yol tablosu için arama hello listesi, toosee toplama yollar için istediğiniz ve seçin. Bu örnekte, **UDRouteTable** seçilir. Dikey penceresinde seçili hello rota tablosu için hello resim aşağıdaki gösterildiği gibi görünür:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Seçin **etkili yolları** hello içinde **yol tablosu** dikey. Merhaba **kapsam** seçtiğiniz toohello yol tablosu ayarlanır.
5. Bir yol tablosu uygulanan toomultiple alt ağlar olabilir. Select hello **alt** hello listeden tooreview istiyor. Bu örnekte, **Subnet1** seçilir.
6. Seçin bir **ağ arabirimi**. Tüm NIC'ler seçili bağlı toohello alt listelenir. Bu örnekte, **VM1 nıc1** seçilir.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Merhaba NIC çalışan bir VM ile ilişkili değilse, etkili bir yol gösterilir.
   >
   >

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
  * Ağ güvenlik grubu (NSG) kuralları hello trafik akışına etkiliyor olabilir. Merhaba daha fazla bilgi için bkz: [sorun giderme ağ güvenlik grupları](virtual-network-nsg-troubleshoot-portal.md) makalesi.
