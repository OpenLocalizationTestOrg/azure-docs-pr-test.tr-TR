---
title: "aaaCreate, değiştirin ya da Azure ortak IP adresi silme | Microsoft Docs"
description: "Nasıl toocreate, değiştirme veya genel bir IP adresi silme öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Oluşturma, değiştirme veya genel bir IP adresi silme

Hakkında genel bir IP adresi ve toocreate, değiştirmek ve silmek öğrenin. Bir ortak IP adresi, kendi yapılandırılabilir ayarlar ile bir kaynaktır. Bir ortak IP adresi tooother Azure kaynaklarını atama sağlar:
- Internet bağlantısı tooresources Azure sanal makineler (VM), Azure sanal makine ölçek kümeleri, Azure VPN ağ geçidi, uygulama ağ geçitleri ve Internet'e yönelik Azure yük dengeleyici gibi gelen. Azure kaynaklarını hello Internet atanmış ortak IP adresi olmayan gelen trafiği gelen iletişimi alamaz. Bazı Azure kaynakları aracılığıyla ortak IP adresleri kendiliğinden erişilebilir olmasına karşın, diğer kaynakları toothem toobe Internet hello erişilebilir atanmış ortak IP adresleri olmalıdır.
- Giden bağlantı toohello tahmin edilebilir bir IP adresi kullanarak Internet. Örneğin, bir sanal makine bir ortak IP adresi atanmış tooit olmadan Giden toohello Internet iletişim kurabilir, ancak Azure tooan öngörülemeyen ortak adresiyle çevrilmiş ağ adresi kendi adresidir. Genel bir IP adresi tooa kaynağı atama hangi IP adresi hello giden bağlantı için kullanılan tooknow sağlar. Tahmin edilebilir olsa hello atama yöntemine bağlı olarak seçilen hello adres değiştirebilirsiniz. Daha fazla bilgi için bkz: [genel bir IP adresi oluşturma](#create-a-public-ip-address). toolearn hello okuma Azure kaynaklarından giden bağlantılar hakkında daha fazla [giden bağlantılar anlamak](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.

## <a name="before-you-begin"></a>Başlamadan önce

Görevler herhangi tamamlamadan önce aşağıdaki tam hello herhangi bir bölümünü bu makalede adımlar:

- Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makale toolearn genel IP adresleri için sınırları hakkında.
- Toohello Azure oturum [portal](https://portal.azure.com), Azure komut satırı arabirimi (CLI) ya da Azure PowerShell ile bir Azure hesabı. Zaten bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede, toocomplete görevleri komutları PowerShell kullanarak, [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Hello en son sürümünü hello Azure PowerShell cmdlet'leri yüklü olduğundan emin olun. tooget Yardım için örneklerle PowerShell komutlarını yazın `get-help <command> -full`.
- Bu makalede, toocomplete görevleri komutları Azure komut satırı arabirimi (CLI) kullanarak, [hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuğu'nu tıklatın hello bulut Kabuk **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com).

Nominal bir ücret ortak IP adresine sahip. Merhaba tooview fiyatlandırma okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. 

## <a name="create-a-public-ip-address"></a>Genel IP adresi oluşturma

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *genel IP adresi*. Zaman **ortak IP adresleri** görünür hello arama sonuçlarında tıklatın.
3. Tıklatın **+ Ekle** hello içinde **genel IP adresi** görünür dikey.
4. Girin veya seçin hello ayarlarında aşağıdaki hello değerlerini **ortak IP adresi oluştur** görünür, ardından dikey **oluşturma**:

    |Ayar|Gerekli mi?|Ayrıntılar|
    |---|---|---|
    |Ad|Evet|Merhaba adı seçtiğiniz hello kaynak grubunda benzersiz olmalıdır.|
    |IP sürümü|Evet| IPv4 veya IPv6 seçin. Ortak IPv4 adresleri olabilir tooseveral atanan Azure kaynakları olsa da, bir IPv6 ortak IP adresi tooan Internet'e yönelik Yük Dengeleyici yalnızca atanabilir. Merhaba yük dengeleyici IPv6 trafiği tooAzure sanal makinelerin yük dengelemesini yapabilir. Daha fazla bilgi edinmek [Yük Dengeleme IPv6 trafiği toovirtual makineler](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |IP adresi ataması|Evet|**Dinamik:** dinamik adresler yalnızca hello genel IP adresi ilişkilendirilen sonra tooa NIC bağlı tooa VM ve hello VM hello için ilk kez başlatıldığında atanır. Dinamik adresler hello VM hello NIC ekli toois durduruldu ise değiştirebilirsiniz (serbest bırakıldı). Merhaba VM yeniden veya durduruldu (ancak değil serbest varsa) hello adres kalır aynı hello. **Statik:** statik adresleri hello genel IP adresi oluşturulduğu zaman atanır. Statik adresler değil (serbest bırakıldı) hello ise VM durduruldu hello put bile değişiklik durumu yapın. Merhaba NIC silindiğinde hello adresi yalnızca yayımlanır. Merhaba NIC oluşturulduktan sonra hello atama yöntemi değiştirebilirsiniz. Merhaba IPv6 seçerseniz **IP sürüm**, hello yalnızca atama yöntemi **dinamik**.|
    |Boşta kalma zaman aşımı (dakika)|Hayır|Bir TCP veya HTTP bağlantı açmak istemcileri toosend etkin tutma iletileri kullanmadan tookeep kaç dakika. IPv6 için seçerseniz **IP sürüm**, bu değer değiştirilemez. |
    |DNS ad etiketi|Hayır|Merhaba hello adı (tüm abonelikleri ve tüm müşteriler arasında) oluşturmak Azure konumu içinde benzersiz olmalıdır. Merhaba adıyla tooa kaynak bağlanabilmesi için hello Azure ortak DNS hizmeti hello adı ve IP adresi otomatik olarak kaydeder. Azure ekler *location.cloudapp.azure.com* (konum seçtiğiniz hello konum olduğu) yetkili toohello adı sağladığınız toocreate hello tam DNS adı. Her iki adres sürümleri toocreate seçerseniz, hello aynı DNS adı tooboth hello IPv4 ve IPv6 adresleri atanır. Hello Azure DNS hizmeti bir IPv4 ve IPv6 AAAA ad kayıtlarını içerir ve hello DNS adı arandığında her iki kayıt ile yanıt verir. Merhaba istemci ile hangi adresi (IPv4 veya IPv6) toocommunicate seçer.|
    |Bir IPv6 (ya da IPv4) adresi oluşturma|Hayır| IPv6 ya da IPv4 görüntülenip görüntülenmeyeceğini ne için seçtiğiniz üzerinde bağımlı **IP sürüm**. Örneğin, **IPv4** için **IP sürüm**, **IPv6** burada görüntülenir.
    |Adı (Merhaba işaretlediyseniz görünür **bir IPv6 (ya da IPv4) adresi oluşturma** onay kutusunu)|Evet, hello seçerseniz **IPv6 oluşturmak** (veya IPv4) onay kutusu.|Merhaba adı girdiğiniz Merhaba ilk hello adından farklı olmalıdır **adı** bu listede. Bir IPv4 ve IPv6 adresi toocreate seçerseniz, iki ayrı ortak IP adresi kaynakları, tooit atanan her IP adresi sürümüne sahip bir hello portal oluşturur.|
    |IP adresi ataması (Merhaba işaretlediyseniz görünür **bir IPv6 (ya da IPv4) adresi oluşturma** onay kutusunu)|Evet, hello seçerseniz **IPv6 oluşturmak** (veya IPv4) onay kutusu.|Merhaba onay kutusunu diyorsa **bir IPv4 adresi oluşturma**, bir atama yöntemini seçin. Merhaba onay kutusunu diyorsa **bir IPv6 adresi oluşturma**, bunu olması gerektiği bir atama yöntemi seçemezsiniz **dinamik**.|
    |Abonelik|Evet|Hello aynı bulunmalıdır [abonelik](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) hello kaynak olarak tooassociate hello ortak IP adresini istiyor.|
    |Kaynak grubu|Evet|Merhaba aynı veya farklı bulunabilir [kaynak grubu](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) hello kaynak olarak tooassociate hello ortak IP adresini istiyor.|
    |Konum|Evet|Hello aynı bulunmalıdır [konumu](https://azure.microsoft.com/regions), tooas bölge tooassociate hello genel IP adresi için istediğiniz hello kaynak olarak da adlandırılır.|

**Komutları**

Hello portal, iki ortak IP adresi kaynakları (bir IPv4 ve bir IPv6) hello seçeneği toocreate sağlar ancak CLI ve PowerShell komutlarını aşağıdaki hello bir kaynak adresi için bir IP sürümü veya hello olan diğer oluşturun. İki ortak IP adresi kaynakları, her IP sürümü için bir tane isterseniz, farklı adlar ve sürümler hello ortak IP adresi kaynaklar için belirtme hello komutunu iki kez çalıştırmalısınız. 

|Aracı|Komut|
|---|---|
|CLI|[az ağ genel IP oluşturun](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Görüntüleme, ayarlarını değiştirmek veya bir ortak IP adresini Sil

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *genel IP adresi*. Zaman **ortak IP adresleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ortak IP adresleri** görünür, dikey tooview istediğiniz ayarlarını değiştirme veya silme hello genel IP adresi hello adını tıklayın.
4. Görüntülenen hello dikey penceresinde hello için genel IP adresi, aşağıdaki seçenekleri tooview, mi istediğinize bağlı olarak şu hello tam birini silin veya hello ortak IP adresini değiştirin.
    - **Görünüm**: Merhaba **genel bakış** hello dikey bölümü hello ortak IP adresi için anahtar ayarlarını gösterir, gibi hello ağ arabirimiyle ilişkilendirilmiş çok (Merhaba adresi ilişkili tooa ağ arabirimi ise). Merhaba portal hello adresi (IPv4 veya IPv6) hello sürümü görüntülemez. tooview hello sürüm bilgileri, kullanım hello PowerShell veya CLI komutu tooview hello genel IP adresi. Başlangıç IP adresi sürümü IPv6 ise, adresi atanmış hello hello portal, PowerShell veya CLI hello tarafından görüntülenmez. 
    - **Silme**: toodelete hello genel IP adresi,'ı tıklatın **silmek** hello içinde **genel bakış** hello dikey bölüm. Başlangıç adresi şu anda ilişkili tooan IP yapılandırması ise, silinemez. Başlangıç adresi şu anda bir yapılandırması ile ilişkili ise, tıklatın **ilişkiyi** toodissociate hello adresinden hello IP yapılandırması.
    - **Değişiklik**: tıklatın **yapılandırma**. Adım hello 4 hello bilgileri kullanarak ayarları değiştirme [genel bir IP adresi oluşturma](#create-a-public-ip-address) bu makalenin. toochange hello ataması statik toodynamic gelen bir IPv4 adresi için hello genel IPv4 adresi için ilişkili hello IP yapılandırmadan önce ilişkilendirmesini kaldırmanız gerekir. Merhaba atama yöntemi toodynamic değiştirin ve tıklatın **ilişkilendirmek** tooassociate başlangıç IP adresi toohello aynı IP yapılandırması, farklı bir yapılandırma veya, bırakabilir, ilkenin ilişkisi. toodissociate genel bir IP adresi, hello **genel bakış** 'yi tıklatın **ilişkiyi**.

>[!WARNING]
>Merhaba atama yöntemi statik toodynamic değiştirdiğinizde, toohello genel IP adresi atanmış hello IP adresi kaybedersiniz. Hello Azure ortak DNS sunucularını bakım statik veya dinamik adresleri ve (bir tanımladıysanız) tüm DNS ad etiketi arasında bir eşleme yaparken hello olan durduruldu (serbest bırakıldığında) durumu sonra hello VM başlatıldığında dinamik bir IP adresi değiştirebilirsiniz. değiştirmesini, tooprevent hello adresi statik bir IP adresi atayın.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ ortak IP listesi](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist genel IP adresleri, [az ağ ortak IP Göster](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow ayarları; [az ağ ortak IP güncelleştirmesi](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [az ağ ortak IP silme](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve genel bir IP adresi nesne ve ayarlarını görüntülemek [kümesi AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate ayarları; [Kaldır AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Sonraki adımlar
Azure kaynaklarını aşağıdaki hello oluştururken genel IP adresleri atayın:

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makineler
- [Internet'e yönelik Azure yük dengeleyici](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure uygulama ağ geçidi](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Bir Azure VPN ağ geçidi kullanarak siteden siteye bağlantı](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure sanal makine ölçek kümesi](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
