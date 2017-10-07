---
title: "aaaTroubleshoot ağ güvenlik grupları - portalı | Microsoft Docs"
description: "Nasıl tootroubleshoot ağ güvenlik grupları'hello Azure Resource Manager dağıtımında hello Azure Portal kullanarak model öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Ağ güvenlik grupları hello Azure Portal kullanarak sorun giderme
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

### <a name="vm"></a>Bir sanal makine için etkili güvenlik kurallarını görüntüle
Bir VM için adımları tootroubleshoot Nsg'ler aşağıdaki hello tamamlayın:

Bir NIC'den hello VM kendisini hello etkin güvenlik kuralları tam listesini görüntüleyebilirsiniz. Ayrıca eklemek, değiştirmek ve bu işlemler izinleri tooperform varsa NIC ve alt ağ NSG kuralları hello etkili kuralları dikey penceresinden silin.

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **sanal makineleri** hello listesinde görünür.
3. VM tootroubleshoot görüntülenen hello listesinden seçin ve seçeneklerle bir VM dikey penceresi görünür.
4. Tıklatın **Tanıla & sorunları** ve ortak bir sorun seçin. Bu örnek için **toomy Windows VM bağlantı kurulamıyor** seçilir. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Adımları hello sorun altında hello resim aşağıdaki gösterildiği gibi görünür: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Tıklatın *etkin güvenlik grubu kuralları* önerilen adımları hello listesinde.
6. Merhaba **alma etkin güvenlik kuralları** hello resim aşağıdaki gösterildiği gibi dikey penceresi görünür:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Merhaba resim bölümlerini aşağıdaki hello dikkat edin:
   
   * **Kapsam:** çok ayarlamak*VM1*, 3. adımda seçtiğiniz VM hello.
   * **Ağ arabirimi:** *VM1 nıc1* seçilir. Bir VM birden çok ağ arabirimine (NIC) sahip. Her NIC'nin benzersiz etkin güvenlik kuralları olabilir. Sorunlarını giderirken, her bir NIC tooview hello etkin güvenlik kuralları gerekebilir.
   * **İlişkili Nsg'ler:** Nsg'ler NIC bağlı uygulanan tooboth hello NIC ve hello alt hello olabilir. Merhaba resimde, bir NSG bağlı uygulanan tooboth hello NIC ve hello alt olmuştur. Tıklayabilirsiniz hello NSG adları toodirectly hello Nsg'ler kurallarında değiştirin.
   * **VM1 nsg sekmesi:** hello hello resimde görüntülenen kuralları listesidir hello NSG toohello NIC uygulanan için Her bir NSG oluşturulduğunda birkaç varsayılan kuralları Azure tarafından oluşturulur. Merhaba varsayılan kuralları kaldırılamıyor, ancak daha yüksek öncelik kuralları ile geçersiz kılınabilir. Merhaba okuma varsayılan kuralları hakkında daha fazla toolearn [NSG genel bakış](virtual-networks-nsg.md#default-rules) makalesi.
   * **HEDEF sütun:** başkalarının adres öneklerini bulunurken hello kuralları bazıları metin hello sütununda vardır. oluşturulduğunda hello metin hello varsayılan uygulanan etiketleri toohello güvenlik kuralı adıdır. Başlangıç etiketleri birden çok önekleri temsil eden sistem tarafından sağlanan tanımlayıcılardır. Bir etiketi olan bir kural gibi seçerek *AllowInternetOutBound*, hello hello öneklerini listeler **adres önekleri** dikey.
   * **İndirin:** hello kurallarının listesini uzun olabilir. Hello kuralları çevrimdışı analiz için bir .csv dosyası tıklayarak indirebileceğiniz **karşıdan** ve hello dosyası kaydediliyor.
   * **AllowRDP** gelen kuralı: Bu kural RDP bağlantıları toohello VM izin verir.
7. Merhaba tıklatın **Subnet1 NSG** sekmesini tooview hello etkili kurallardan hello NSG uygulanan toohello alt hello resim aşağıdaki gösterildiği gibi: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Bildirim hello *denyRDP* **gelen** kuralı. Gelen kuralları Hello alt ağ uygulanan hello ağ arabiriminin uygulanan kurallardan önce değerlendirilir. Hello Reddet olduğundan kural hello alt ağ uygulanır, hello NIC hiçbir zaman değerlendirilen kural hello izin verdiğinden hello isteği tooconnect tooTCP 3389, başarısız olur. 
   
    Merhaba *denyRDP* kuralı hello neden neden hello RDP bağlantısı başarısız olur. Kaldırarak hello sorunu çözecektir.
   
   > [!NOTE]
   > Merhaba VM ilişkilendirirseniz ile Merhaba NIC çalışır durumda değil veya Nsg'ler uygulanan toohello NIC veya alt ağ yapmadıysanız, hiçbir kural gösterilir.
   > 
   > 
8. tooedit NSG kuralları'nı tıklatın *Subnet1 NSG* hello içinde **ilişkili Nsg'ler** bölümü.
   Merhaba açılır **Subnet1 NSG** dikey. Tıklayarak hello kuralları doğrudan düzenleyebilirsiniz **gelen güvenlik kuralları**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Merhaba kaldırdıktan sonra *denyRDP* hello gelen kuralı **Subnet1 NSG** ve ekleyerek bir *allowRDP* kural hello etkili kuralları listesi hello resim aşağıdaki gibi görünür:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    TCP bağlantı noktası 3389 RDP bağlantı toohello VM açma veya hello PsPing aracını kullanarak açık olduğundan emin olun. Okuma hello tarafından PsPing hakkında daha fazla bilgiyi [PsPing indirme sayfası](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Bir ağ arabirimi için etkili güvenlik kurallarını görüntüle
VM trafik akışı için belirli bir NIC etkilenir, hello aşağıdaki adımları tamamlayarak hello etkili kuralları hello NIC hello ağ arabirimleri bağlamından için tam bir listesini görüntüleyebilirsiniz:

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **ağ arabirimleri** hello listesinde görünür.
3. Bir ağ arabirimi seçin. Bir NIC resim aşağıdaki hello adlı *VM1 nıc1* seçilir.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Bu hello fark **kapsam** seçili toohello ağ arabirimi ayarlanır. 6. adımını hello okuma hakkında daha fazla bilgi toolearn hello gösterilen ek bilgiler **sorun giderme Nsg'leri bir VM için** bu makalenin.
   
   > [!NOTE]
   > Bir NSG'yi bir ağ arabiriminden kaldırılırsa, hello alt NSG NIC verilen hello üzerinde hala etkin Bu durumda, hello çıktı hello alt NSG kuralları yalnızca gösterir. Merhaba NIC ekli tooa VM ise kurallarını yalnızca görünür.
   > 
   > 
4. Kuralları, bir NIC ve bir alt ağ ile ilişkili Nsg'ler için doğrudan düzenleyebilirsiniz. toolearn nasıl okuma hello 8. adım **bir sanal makine için etkili güvenlik kuralları** bu makalenin.

## <a name="nsg"></a>Bir ağ güvenlik grubu (NSG) için etkili güvenlik kuralları görüntülemek
NSG kuralları değiştirirken tooreview hello hello kuralları belirli bir VM'de eklenmekte olan etkisini isteyebilirsiniz. Tüm belirli bir NSG uygulandığı NIC'ler hello için tam hello etkin güvenlik kuralları listesini görüntüleyebileceğiniz NSG dikey verilen hello tooswitch bağlamdan kalmadan. Aşağıdaki adımları tam hello bir NSG içinde tootroubleshoot etkili kuralları:

1. Oturum açma toohello https://portal.azure.com Azure portalında.
2. Tıklatın **daha fazla hizmet**, ardından **ağ güvenlik grupları** hello listesinde görünür.
3. Bir NSG'yi seçin. Resim aşağıdaki hello VM1 nsg adlı bir NSG seçilmedi.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Merhaba önceki resim bölümlerini aşağıdaki hello dikkat edin:
   
   * **Kapsam:** toohello seçili NSG ayarlayın.
   * **Sanal makine:** olduğunda bir NSG uygulanan tooa alt ağ, uygulanan tooall ağ arabirimleri ekli tooall VM'ler bağlı toohello alt ağı değil. Bu liste, bu NSG uygulandığı tüm sanal makineleri gösterir. Tüm VM hello listeden seçebilirsiniz.
     
     > [!NOTE]
     > Bir NSG uygulanan tooonly boş bir alt ağ, VM listelenmez. Bir NSG'yi bir VM ile ilişkili olmayan NIC uygulanan tooa ise, bu NIC'ler da listelenmez. 
     > 
     > 
   * **Ağ arabirimi:** VM birden çok ağ arabirimine sahip. Bir ağ arabirimi seçin ekli toohello seçili VM.
   * **AssociatedNSGs:** herhangi bir zamanda bir NIC tootwo olabilir etkili Nsg'ler toohello NIC uygulanan ve diğer toohello alt hello. Merhaba NIC etkin bir alt ağ NSG varsa hello kapsam VM1-nsg seçilen rağmen hello çıkış hem Nsg'ler gösterir.
4. Kuralları, bir NIC veya alt ağ ile ilişkili Nsg'ler için doğrudan düzenleyebilirsiniz. toolearn nasıl okuma hello 8. adım **bir sanal makine için etkili güvenlik kuralları** bu makalenin.

6. adımını hello okuma hakkında daha fazla bilgi toolearn hello gösterilen ek bilgiler **bir sanal makine için etkili güvenlik kuralları** bu makalenin.

> [!NOTE]
> Bir alt ağ ve NIC her yalnızca bir NSG uygulanır toothem kurabiliyor olsa bile, ilişkili toomultiple NIC ve birden çok alt ağa bir NSG olabilir.
> 
> 

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Bağlantı sorunları giderirken noktaları aşağıdaki hello göz önünde bulundurun:

* Varsayılan NSG kuralları hello'ten gelen erişim engeller Internet ve yalnızca izin VNet gelen trafiği. Kuralları açıkça eklenmesi tooallow gelen gerektiği gibi Internet'ten erişim.
* Bir sanal makinenin ağ bağlantısı toofail neden hiçbir NSG güvenlik kuralları varsa, hello sorun nedeniyle olabilir:
  * Merhaba VM'ın işletim sistemi içinde çalışan güvenlik duvarı yazılımı
  * Sanal gereçler veya şirket içi trafiği için yapılandırılmış yollar. Internet trafiğini yeniden yönlendirilen tooon içi zorlamalı tünel aracılığıyla olabilir. Merhaba Internet tooyour VM bir RDP/SSH bağlantısı nasıl hello şirket içi ağ donanımı bu trafiği işler bağlı olarak bu ayar ile çalışmayabilir. Okuma hello [sorun giderme yolları](virtual-network-routes-troubleshoot-powershell.md) makale toolearn içinde ve dışında trafik akışını engelleyen toodiagnose rota sorunları hello nasıl VM hello. 
* Varsayılan olarak sanal ağlar, eşlenen durumdaysa hello VIRTUAL_NETWORK etiketine tooinclude önekleri eşlenmiş Vnet'ler için otomatik olarak genişletin. Bu önekleri hello görüntüleyebilirsiniz **ExpandedAddressPrefix** listesi olan bağlantı eşliği sorunları ilgili tooVNet tootroubleshoot. 
* Etkin güvenlik kuralları, bir NSG hello VM'in NIC ve veya alt ağ ilişkili olup yalnızca gösterilir. 
* Merhaba NIC ile ilişkili hiçbir Nsg'ler vardır veya alt ağ ve tooyour VM atanan genel bir IP adresi varsa, tüm bağlantı noktalarına gelen ve giden erişimi açık olacaktır. Merhaba VM genel bir IP adresi varsa, Nsg'ler toohello NIC veya alt ağ uygulama önemle tavsiye edilir.

