---
title: "bir Azure ağ arabirimi için IP adreslerini aaaConfigure | Microsoft Docs"
description: "Nasıl tooadd, değiştirmek ve ağ arabirimi için özel ve genel IP adreslerini kaldırın öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Ekleme, değiştirme veya bir Azure ağ arabirimi için IP adreslerini kaldırın

Nasıl tooadd, değiştirmek ve ağ arabirimi için genel ve özel IP adreslerini kaldırın öğrenin. Özel IP adresleri tooa ağ arabirimine atanmış bir Azure sanal ağı ve bağlı ağların diğer kaynaklara sahip bir sanal makine toocommunicate etkinleştirin. Özel bir IP adresi giden iletişim toohello Internet öngörülemeyen bir IP adresi kullanarak da sağlar. A [genel IP adresi](virtual-network-public-ip-address.md) tooa atanan hello Internet gelen iletişimi tooa sanal makineden ağ arabirimi sağlar. Başlangıç adresi ayrıca hello sanal makine toohello tahmin edilebilir bir IP adresi kullanarak Internet giden iletişimi sağlar. Ayrıntılar için bkz [azure'da giden bağlantılar anlama](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Toocreate gerekiyorsa, değiştirin ya da bir ağ arabirimini silmek okuma hello [bir ağ arabirimi yönetmek](virtual-network-network-interface.md) makalesi. Gerekirse tooadd ağ arabirimleri, bir sanal makineden tooor Kaldır ağ arabirimleri, hello okuma [ekleme veya kaldırma ağ arabirimleri](virtual-network-network-interface-vm.md) makalesi. 


## <a name="before-you-begin"></a>Başlamadan önce

Görevler herhangi tamamlamadan önce aşağıdaki tam hello herhangi bir bölümünü bu makalede adımlar:

- Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makale toolearn ortak ve özel IP adresleri için sınırları hakkında.
- Toohello Azure oturum [portal](https://portal.azure.com), Azure komut satırı arabirimi (CLI) ya da Azure PowerShell ile bir Azure hesabı. Zaten bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede, toocomplete görevleri komutları PowerShell kullanarak, [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Hello en son sürümünü hello Azure PowerShell cmdlet'leri yüklü olduğundan emin olun. tooget Yardım için örneklerle PowerShell komutlarını yazın `get-help <command> -full`.
- Bu makalede, toocomplete görevleri komutları Azure komut satırı arabirimi (CLI) kullanarak, [hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuğu'nu tıklatın hello bulut Kabuk **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>IP adreslerini ekleyin

Kadar ekleyebilirsiniz [özel](#private) ve [ortak](#public) [IPv4](#ipv4) adresleri hello sınırları içinde gerekli tooa ağ arabirimi olarak listelenen hello [Azure sınırları ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makalesi. (Merhaba ağ arabirimi oluşturduğunuzda, hello portal tooadd özel bir IPv6 adresi tooa ağ arabirim kullanabilmenize rağmen) hello portal tooadd bir IPv6 adresi tooan var olan ağ arabirimi kullanamazsınız. PowerShell veya CLI tooadd özel bir IPv6 adresi tooone hello kullanabilirsiniz [ikincil IP yapılandırması](#secondary) (var olduğu sürece hiçbir var olan ikincil IP yapılandırmaları) varolan bir ağ için değil arabirimi tooa sanal bağlı. Makine. Herhangi bir genel IPv6 adresi tooa ağ arabirimi aracı tooadd kullanamazsınız. Bkz: [IPv6](#ipv6) IPv6 adresleri kullanma hakkında ayrıntılı bilgi için. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooadd bir IPv4 adresi için istediğiniz hello ağ arabirimi'ı tıklatın.
4. Tıklatın **IP yapılandırmaları** hello içinde **ayarları** hello dikey seçtiğiniz hello ağ arabirimi için bölümü.
5. Tıklatın **+ Ekle** açar hello dikey penceresinde IP yapılandırmaları için.
6. Merhaba aşağıdakileri belirtin ve ardından **Tamam** tooclose hello **eklemek IP yapılandırması** dikey penceresinde:

    |Ayar|Gerekli mi?|Ayrıntılar|
    |---|---|---|
    |Ad|Evet|Merhaba ağ arabirimi için benzersiz olmalıdır|
    |Tür|Evet|IP yapılandırması tooan varolan ağ arabirimi eklediğiniz ve her bir ağ arabirimine sahip olmalıdır bu yana bir [birincil](#primary) IP yapılandırması, tek seçenektir **ikincil**.|
    |Özel IP adres ataması yöntemi|Evet|[**Dinamik** ](#dynamic) adresleri hello edilmiş durduruldu (serbest bırakıldığında) durumu sonra hello sanal makine yeniden başlatılırsa değiştirebilirsiniz. Kullanılabilir bir adresi hello alt hello ağ arabiriminin hello adres alanından bağlı olduğu Azure atar. [**Statik** ](#static) hello ağ arabirimi silinene kadar adresleri serbest değil. Şu anda başka bir IP yapılandırması tarafından kullanılmadığından hello alt ağ adres alanı aralığından bir IP adresi belirtin.|
    |Genel IP adresi|Hayır|**Devre dışı:** hiçbir ortak IP adresi kaynağı şu anda ilişkili toohello IP yapılandırmadır. **Etkin:** var olan bir IPv4 ortak IP adresi seçin veya yeni bir tane oluşturun. nasıl toocreate bir ortak IP adresi okuma toolearn hello [ortak IP adresleri](virtual-network-public-ip-address.md#create-a-public-ip-address) makalesi.|
7. Merhaba hello yönergeleri izleyerek ikincil özel IP adresleri toohello sanal makine işletim sistemini el ile eklemeniz [toovirtual makine işletim sistemlerini birden çok IP adresi atamak](virtual-network-multiple-ip-addresses-portal.md#os-config) makalesi. Bkz: [özel](#private) el ile IP adresleri tooa sanal makine işletim sistemi eklemeden önce özel konular için IP adresi. Bir ortak IP adresleri toohello sanal makine işletim sistemi eklemeyin.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC IP-config oluşturma](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Ekleme AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>IP adresi ayarlarını değiştirme

Toochange hello atama yöntemi Değiştir hello statik IPv4 adresi, bir IPv4 adresi gerekebilir veya tooa ağ arabirimi değişiklik hello genel IP adresi atanır. Merhaba özel bir IPv4 adresi, bir sanal makinede bir ikincil ağ arabirimi ile ilişkili bir ikincil IP yapılandırmasının değiştirirsiniz varsa (hakkında daha fazla bilgi [birincil ve ikincil ağ arabirimleri](virtual-network-network-interface-vm.md#about)), yer hello sanal Merhaba makineye aşağıdaki adımları hello tamamlamadan önce (serbest bırakıldığında) durumu durduruldu: 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooview istediğiniz ya da IP adresi ayarlarını değiştirme hello ağ arabirimi'ı tıklatın.
4. Tıklatın **IP yapılandırmaları** hello içinde **ayarları** hello dikey seçtiğiniz hello ağ arabirimi için bölümü.
5. IP yapılandırması için açılır hello dikey hello listesinden toomodify istediğiniz hello IP Yapılandırması'nı tıklatın.
6. Hello ayarları hello 6. adımında hello ayarları hakkında bilgi hello kullanarak, istediğiniz değiştirme [bir IP Yapılandırması Ekle](#create-ip-config) bu makalenin. Tıklatın **kaydetmek** tooclose hello dikey değiştirdiğiniz hello IP yapılandırması için.

>[!NOTE]
>Hello birincil ağ arabirimi birden çok IP yapılandırmaları olan ve hello birincil IP yapılandırmasının hello özel IP adresini değiştirmek, el ile hello birincil ve ikincil IP adreslerini toohello ağ arabirimi içinden Windows atamanız gerekir (değil Linux için gereklidir). Okuma hello toomanually atamak IP adreslerini tooa ağ arabirimi bir işletim sistemi içinde [toovirtual makineleri birden çok IP adresi atamak](virtual-network-multiple-ip-addresses-portal.md#os-config) makalesi. Bkz: [özel](#private) el ile IP adresleri tooa sanal makine işletim sistemi eklemeden önce özel konular için IP adresi. Bir ortak IP adresleri toohello sanal makine işletim sistemi eklemeyin.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC IP yapılandırmasını güncelleştir](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>IP adreslerini kaldırın

Kaldırabileceğiniz [özel](#private) ve [ortak](#public) IP adresleri bir ağ arabiriminden, ancak bir ağ arabirimi her zaman en az bir özel IPv4 adresi atanmış tooit olması gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooremove IP adreslerinden istediğiniz hello ağ arabirimi'ı tıklatın.
4. Tıklatın **IP yapılandırmaları** hello içinde **ayarları** hello dikey seçtiğiniz hello ağ arabirimi için bölümü.
5. Sağ tıklayın bir [ikincil](#secondary) IP yapılandırması (Merhaba silemezsiniz [birincil](#primary) yapılandırma) toodelete istiyorsanız,'ı tıklatın **silmek**, ardından **Evet**  tooconfirm hello silme. Merhaba yapılandırma olsaydı genel bir IP adresi kaynağı tooit ilişkili, hello kaynak hello IP yapılandırmasından ilkenin ilişkisi ancak hello kaynak silinmez.
6. Kapat hello **IP yapılandırmaları** dikey.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC IP-config Sil](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>IP yapılandırması

[Özel](#private) ve (isteğe bağlı) [ortak](#public) IP adreslerini tooone atanan veya daha fazla IP yapılandırmaları tooa ağ arabirimine atanmış. İki tür IP yapılandırmaları vardır:

### <a name="primary"></a>Birincil

Her bir ağ arabirimine bir birincil IP yapılandırmasına atanır. Birincil bir IP yapılandırması:

- Sahip bir [özel](#private) [IPv4](#ipv4) atanan adresi tooit. Özel atayamazsınız [IPv6](#ipv6) adresi tooa birincil IP yapılandırması.
- Ayrıca bir [ortak](#public) IPv4 adresi atanmış tooit. Bir genel IPv6 adresi tooa birincil veya ikincil IP yapılandırması atayamazsınız. Ancak, ortak bir IPv6 adresi yükleyebilir tooan Azure yük dengeleyici Ata Bakiye trafiği tooa sanal makinenin özel IPv6 adresi. Daha fazla bilgi için bkz: [ayrıntıları ve IPv6 için sınırlamalar](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>İkincil

Ayrıca tooa birincil IP yapılandırması, bir ağ arabirimi tooit atanan sıfır veya daha fazla ikincil IP yapılandırmasına sahip. İkincil bir IP yapılandırması:

- Özel bir IPv4 veya IPv6 adresi atanmış tooit olması gerekir. Başlangıç adresi IPv6 ise, hello ağ arabirimi yalnızca bir ikincil IP yapılandırmasına sahip olabilir. Başlangıç adresi IPv4 ise hello ağ arabirimi tooit atanmış birden fazla ikincil IP yapılandırması olabilir. kaç tane özel ve ortak IPv4 adresleri tooa ağ arabirimi, atanabilir hakkında daha fazla toolearn bkz hello [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makalesi.  
- Merhaba özel IP adresi IPv4 ise, genel bir IPv4 adresi atanmış tooit da sahip olabilirsiniz. Merhaba özel IP adresi IPv6 ise, bir ortak IPv4 veya IPv6 adresi toohello IP yapılandırması atayamazsınız. Birden çok IP adresleri tooa ağ arabirimi atama gibi senaryolarda kullanışlıdır:
    - Tek bir sunucuda farklı IP adreslerine ve SSL sertifikalarına sahip birden fazla web sitesi veya hizmetin barındırılması.
    - Bir Güvenlik Duvarı'nı veya yük dengeleyici gibi bir ağ sanal gereç olarak hizmet veren bir sanal makine.
    - özelliği tooadd herhangi bir hello ağ arabirimleri tooan Azure yük dengeleyici arka uç havuzu için özel IPv4 adreslerini hello hiçbirini hello. Hello geçmiş, yalnızca hello birincil IPv4 adresi için hello birincil ağ arabirimi tooa arka uç havuzu eklenemedi. nasıl tooload Bakiye birden çok IPv4 yapılandırmaları hakkında daha fazla toolearn bkz hello [Yük Dengeleme birden fazla IP yapılandırması](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi. 
    - Merhaba özelliği tooload bir IPv6 adresi atanmış tooa ağ arabirimi dengeleyin. nasıl tooload Bakiye tooa özel IPv6 adresi hakkında daha fazla toolearn bkz hello [Yük Dengelemesi IPv6 adresleri](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.


## <a name="address-types"></a>Adres türleri

Şu IP adresleri tooan türlerini hello atayabilirsiniz [IP yapılandırması](#ip-configurations):

### <a name="private"></a>Özel

Özel [IPv4](#ipv4) adresleri sanal ağ veya diğer bağlı ağlara diğer kaynaklara sahip bir sanal makine toocommunicate etkinleştirin. Bir sanal makine için gelen iletilen olamaz ya da hello sanal makine özel olan giden iletişim kurabilir [IPv6](#ipv6) adresiyle bir özel durum. Bir sanal makine, bir IPv6 adresi kullanarak hello Azure yük dengeleyici ile iletişim kurabilir. Daha fazla bilgi için bkz: [ayrıntıları ve IPv6 için sınırlamalar](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Varsayılan olarak, hello Azure DHCP sunucuları hello özel bir IPv4 adresi hello için Ata [birincil IP yapılandırmasının](#primary) hello ağ arabirimi toohello ağ arabiriminin hello sanal makine işletim sistemi içinde. Sürece gerekli, hiçbir zaman el ile başlangıç IP adresi ağ arabiriminin hello sanal makinenin işletim sistemi içinde ayarlamanız gerekir. 

> [!WARNING]
> Merhaba IPv4 adresi olarak ayarlarsanız bir ağ arabirimi bir sanal makinenin işletim sistemi içinde hello birincil IP adresi toohello hello birincil ağ arabirimi birincil IP yapılandırmasının atanan hello özel bir IPv4 adresi tooa bağlı herhangi bir zamanda farklı. sanal makine Azure içinde bağlantı toohello sanal makine kaybedersiniz.

Gerekli toomanually kümesi hello IP adresini bir ağ arabirimi hello sanal makinenin işletim sistemi içinde olduğu senaryolar vardır. Örneğin, el ile bir Windows işletim sistemi hello birincil ve ikincil IP adreslerini birden çok IP adresleri tooan Azure sanal makinesi eklerken ayarlamanız gerekir. Bir Linux sanal makine için toomanually kümesi hello ikincil IP adresleri yalnızca gerekebilir. Bkz: [eklemek IP adresleri tooa VM işletim sistemi](virtual-network-multiple-ip-addresses-portal.md#os-config) Ayrıntılar için. El ile başlangıç IP adresi hello işletim sistemi içinde ayarladığınızda, hello adresleri toohello IP yapılandırması hello statik (yerine dinamik) atama yöntemi kullanarak bir ağ arabirimi için her zaman atamanız önerilir. Merhaba statik yöntemini kullanarak hello adresi atayarak hello adresi Azure içinde değiştirmez sağlar. Tooan IP yapılandırması atanmış toochange hello adresi gerekiyorsa, bu önermiştir:

1. tooensure hello sanal makine bir adresi hello Azure DHCP sunucularından alıyor, başlangıç IP adresi geri tooDHCP hello işletim sistemi ve yeniden başlatma hello sanal makine içinde hello atamasını değiştirin.
2. Durdur (deallocate) hello sanal makine.
3. Azure içinde hello IP yapılandırması için Hello IP adresini değiştirin.
4. Merhaba sanal makineyi başlatın.
5. [El ile yapılandırmanız](virtual-network-multiple-ip-addresses-portal.md#os-config) ikincil IP adresleri hello işletim sistemi (ve ayrıca Windows içindeki birincil IP adresi hello) içinde toomatch hello Azure içinde ayarlayın.
 
Merhaba önceki adımları izleyerek Merhaba özel IP adresi atanmış toohello ağ arabirimi Azure içinde ve bir sanal makinenin işletim sistemi içinde kalan aynı hello. hangi Azure eklemeyi düşünün sanal makineler için bir işletim sistemi içindeki IP adresleri el ile ayarladınız, abonelik içindeki tookeep izleme [etiketi](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello sanal makineler. Kullanabileceğinize "IP adresi ataması: statik", örneğin. Bu şekilde hello işletim sistemi içinde başlangıç IP adresi için el ile ayarladınız, abonelik içindeki hello sanal makineleri kolayca bulabilirsiniz.

Ayrıca bir sanal makine toocommunicate giden toohello Internet tooenabling de aynı ya da bağlı sanal ağlar, özel bir IP adresi hello içindeki diğer kaynaklara sahip bir sanal makine toocommunicate sağlar. Giden bağlantılar, Azure tooan öngörülemeyen ortak IP adresine göre çevrilmiş kaynak ağ adresi gerçekleştirilir. Merhaba okuyun, Azure giden Internet bağlantısı hakkında daha fazla toolearn [Azure giden Internet bağlantısı](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi. Gelen tooa sanal makinenin özel IP adresinden hello Internet iletişim kuramıyor.

### <a name="public"></a>Genel

Genel IP adresleri hello Internet gelen bağlantı tooa sanal makineden etkinleştirin. Giden bağlantılar toohello Internet tahmin edilebilir bir IP adresi kullanın. Bkz: [azure'da giden bağlantılar anlama](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için. Bir ortak IP adresi tooan IP yapılandırması atayabilir, ancak gerekli değildir. Bir ortak IP adresi tooa sanal makine atamazsanız, hala giden toohello özel IP adresini kullanarak Internet iletişim kurabilir. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [genel IP adresi](virtual-network-public-ip-address.md) makalesi.

Ağ arabirimi tooa atayabilirsiniz ortak IP adreslerini ve özel toohello sayısı sınırları vardır. Ayrıntılar için hello okuma [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makalesi.

> [!NOTE]
> Azure sanal makineye ait özel IP adresi tooa ortak IP adresi çevirir. Sonuç olarak, hello işletim sistemi tooit atanan tüm ortak IP adresleri de farkında, bu yüzden hiçbir gerek tooever el ile Merhaba işletim sistemi içinde ortak bir IP adresi atayın.

## <a name="assignment-methods"></a>Atama yöntemleri

Ortak ve özel IP adresleri atama yöntemlerinin aşağıdaki hello kullanılarak atanır:

### <a name="dynamic"></a>Dinamik

(İsteğe bağlı) dinamik özel IPv4 ve IPv6 adresleri varsayılan olarak atanır. Dinamik adresler hello sanal makine hello yerleştirirseniz değiştirebilirsiniz (serbest bırakıldığında) durumu durduruldu sonra başlatıldı. Merhaba hello sanal makine süresince IPv4 adresleri toochange istemiyorsanız, hello statik yöntemini kullanarak hello adresleri atayın. Yalnızca hello dinamik atama yöntemini kullanarak özel bir IPv6 adresi atayabilirsiniz. Her iki yöntemi kullanarak bir genel IPv6 adresi tooan IP yapılandırması atayamazsınız.

### <a name="static"></a>Statik

Bir sanal makine silinene kadar hello statik yöntemini kullanarak atanan adresler değiştirmeyin. İçinde Hello alt hello ağ arabirimi için el ile statik özel IPv4 adresi tooan IP yapılandırması hello adres alanından atayın. Genel veya özel statik IPv4 adresi tooan IP yapılandırması (isteğe bağlı) atayabilirsiniz. Bir statik genel veya özel IPv6 adresi tooan IP yapılandırması atayamazsınız. statik genel IPv4 adresi, Azure nasıl atar hakkında daha fazla toolearn hello bkz [genel IP adresi](virtual-network-public-ip-address.md) makalesi.

## <a name="ip-address-versions"></a>IP adresi sürümleri

Sürümleri adresleri atarken aşağıdaki hello belirtebilirsiniz:

### <a name="ipv4"></a>IPv4

Her bir ağ arabirimine bir olmalıdır [birincil](#primary) atanmış bir IP yapılandırmasıyla [özel](#private) [IPv4](#ipv4) adresi. Bir veya daha fazla ekleyebilirsiniz [ikincil](#secondary) her sahip özel bir IPv4 ve (isteğe bağlı) bir IPv4 IP yapılandırmaları [ortak](#public) IP adresi.

### <a name="ipv6"></a>IPv6

Sıfır veya bir özel atayabilirsiniz [IPv6](#ipv6) bir ağ arabirimi adresi tooone ikincil IP yapılandırması. Merhaba ağ arabirimi var olan tüm ikincil IP yapılandırmaları sahip olamaz. Bir IP yapılandırması hello portalı kullanarak bir IPv6 adresiyle ekleyemezsiniz. PowerShell veya CLI tooadd bir IP yapılandırması hello özel IPv6 adresi tooan var olan ağ arabirimi ile kullanın. Merhaba ağ arabirimi var olan VM ekli tooan olamaz.

> [!NOTE]
> Merhaba portalı kullanarak bir IPv6 adresiyle bir ağ arabirimi oluşturabilirsiniz ancak hello portal kullanarak mevcut bir ağ arabirimi tooa yeni veya var olan sanal makine, ekleyemezsiniz. PowerShell veya Azure CLI 2.0 toocreate bir ağ arabirimi hello özel bir IPv6 adresiyle kullanın ve sonra bir sanal makine oluştururken hello ağ arabirimi ekleyin. Atanmış tooit tooan varolan sanal makine özel bir IPv6 adresi ile bir ağ arabirimine eklenemiyor. Bir özel IPv6 adresi tooan IP yapılandırması hiçbir ağ arabirimi bağlı tooa herhangi bir aracı (portal, CLI veya PowerShell) kullanarak sanal makine için eklenemiyor.

Bir genel IPv6 adresi tooa birincil veya ikincil IP yapılandırması atayamazsınız.

## <a name="next-steps"></a>Sonraki adımlar
toocreate makaleler hello okuma farklı IP yapılandırmaları olan bir sanal makine:

|Görev|Aracı|
|---|---|
|Birden çok NIC ile VM oluşturma|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Birden çok IPv4 adresleriyle tek bir NIC VM oluşturma|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Özel bir IPv6 adresi (arkasında bir Azure yük dengeleyici) ile tek bir NIC VM oluşturma|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager şablonu](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
