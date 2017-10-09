---
title: "aaaCreate, değiştirmek veya bir Azure ağı arabirimi silme | Microsoft Docs"
description: "Ne öğrenin bir ağ arabirimi ve toocreate, ayarlarını değiştirmek ve silmek."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Oluşturma, değiştirme veya bir ağ arabirimi silme

Nasıl toocreate, ayarlarını değiştirin ve ağ arabirimini silmek öğrenin. Bir ağ arabirimi, Internet, Azure ve şirket içi kaynakları ile bir Azure sanal makine toocommunicate sağlar. Hello Azure portal kullanarak bir sanal makine oluştururken, hello portal sizin için varsayılan ayarlarla bir ağ arabirimi oluşturur. Bunun yerine, ağ arabirimleri özel ayarlarla toocreate seçin ve oluşturduğunuzda bir veya daha fazla ağ arabirimleri tooa sanal makine eklemek. Varolan bir ağ arabirimi için toochange varsayılan ağ arabirimi ayarları da isteyebilirsiniz. Bu makalede nasıl toocreate bir ağ arabirimi özel ayarlarla ağ filtre (ağ güvenlik grubu) ataması, alt ağ ataması, DNS sunucusu ayarlarını ve IP iletimini gibi varolan ayarlarını değiştirin ve ağ arabirimini silmek açıklanmaktadır.

Tooadd gerekiyorsa, değiştirin ya da bir ağ arabirimi için IP adreslerini kaldırın okuma hello [yönetmek IP adresleri](virtual-network-network-interface-addresses.md) makalesi. Tooadd ağ arabirimlerine gerekir veya ağ arabirimleri sanal makinelerden kaldırırsanız, hello okuma [ekleme veya kaldırma ağ arabirimleri](virtual-network-network-interface-vm.md) makalesi.


## <a name="before-you-begin"></a>Başlamadan önce

Görevler herhangi tamamlamadan önce aşağıdaki tam hello herhangi bir bölümünü bu makalede adımlar:

- Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makale toolearn ağ arabirimleri için sınırları hakkında.
- Toohello Azure oturum [portal](https://portal.azure.com), Azure komut satırı arabirimi (CLI) ya da Azure PowerShell ile bir Azure hesabı. Zaten bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede, toocomplete görevleri komutları PowerShell kullanarak, [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Hello en son sürümünü hello Azure PowerShell cmdlet'leri yüklü olduğundan emin olun. tooget Yardım için örneklerle PowerShell komutlarını yazın `get-help <command> -full`.
- Bu makalede, toocomplete görevleri komutları Azure komut satırı arabirimi (CLI) kullanarak, [hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuğu'nu tıklatın hello bulut Kabuk **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Bir ağ arabirimi oluştur

Hello Azure portal kullanarak bir sanal makine oluştururken, hello portal sizin için varsayılan ayarlarla bir ağ arabirimi oluşturur. Bunun yerine tüm ağ arabirimi ayarlarını belirtmeniz gerekir, bir ağ arabirimi ile özel ayarları oluşturmak ve (PowerShell veya hello Azure CLI kullanarak) hello sanal makine oluştururken hello ağ arabirimi tooa sanal makine ekleyin. Ayrıca, bir ağ arabirimi oluştur ve tooan varolan sanal makine (PowerShell veya hello Azure CLI kullanarak) ekleyebilirsiniz. toolearn toocreate varolan bir sanal makine ağ arabirimi veya tooadd için ya da var olan sanal makinelerden ağ arabirimleri Kaldır nasıl hello okuma [ekleme veya kaldırma ağ arabirimleri](virtual-network-network-interface-vm.md) makalesi. Bir ağ arabirimi oluşturmadan önce varolan olmalıdır [sanal ağ](virtual-networks-create-vnet-arm-pportal.md) içinde aynı konum ve bir ağ arabiriminde oluşturduğunuz abonelik hello.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey tıklayın **+ Ekle**.
4. Merhaba, **oluşturma ağ arabirimi** görünür, dikey girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:

    |Ayar|Gerekli mi?|Ayrıntılar|
    |---|---|---|
    |Ad|Evet|Merhaba adı seçtiğiniz hello kaynak grubunda benzersiz olmalıdır. Zamanla, Azure aboneliğinizde büyük olasılıkla birden fazla ağ arabirimleri sahip olacaksınız. Okuma hello [adlandırma kuralları](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) birkaç yönetme bir adlandırma kuralı toomake oluştururken önerileri ağ arabirimleri kolaylaştırmak için makalesi. Merhaba adı Hello ağ arabirimi oluşturulduktan sonra değiştirilemez.|
    |Sanal ağ|Evet|Merhaba ağ arabirimi için Hello sanal ağı seçin. Hello aynı adda bir ağ arabirimi tooa sanal ağ yalnızca atayabilirsiniz abonelik ve konumda hello ağ arabirimi. Bir ağ arabirimi oluşturulduktan sonra atandığı hello sanal ağ değiştirilemiyor. Merhaba hello ağ arabirimi toomust eklediğiniz sanal makine de mevcut hello aynı konumu ve abonelik hello ağ arabirimi.|
    |Alt ağ|Evet|Seçtiğiniz hello sanal ağ içindeki bir alt ağ seçin. Merhaba alt değiştirebileceğiniz hello ağ arabirimi oluşturulan tooafter atanır.|
    |Özel IP adresi ataması|Evet| Bu ayarda hello IPv4 adresi için hello atama yöntemini seçme. Atama yöntemlerinin aşağıdaki hello seçin: **dinamik:** bu seçeneğin belirlenmesi, Azure hello adres alanından seçtiğiniz hello alt ağının kullanılabilir bir adresi otomatik olarak atar.. Durduruldu (serbest bırakıldığında) durumu Hello edilmiş sonra hello sanal makine içinde başlatıldığında azure farklı bir adres tooa ağ arabirimi atayabilir. durduruldu (serbest bırakıldığında) durumu Hello edilmiş olmadan hello sanal makine yeniden başlatılırsa hello adres kalır aynı hello. **Statik:** bu seçeneğin belirlenmesi, bir kullanılabilir IP adresi hello adres alanı, seçtiğiniz hello alt ağının içinde el ile atamanız gerekir. Statik adresler, bunları değiştirebilir veya hello ağ arabirimi silinene kadar değiştirmeyin. Merhaba ağ arabirimi oluşturulduktan sonra hello atama yöntemi değiştirebilirsiniz. Hello Azure DHCP sunucusu bu adresi toohello ağ arabirimi hello sanal makine hello işletim sistemi içinde atar.|
    |Ağ güvenlik grubu|Hayır| İzin ayarlama çok**hiçbiri**, var olan seçin [ağ güvenlik grubu](virtual-networks-nsg.md), veya [bir ağ güvenlik grubu oluşturun](virtual-networks-create-nsg-arm-pportal.md). Ağ güvenlik grupları toofilter ağ trafiği bir ağ arabirimi ve etkinleştirin. Sıfır veya bir ağ güvenlik grubu tooa ağ arabirimi uygulayabilirsiniz. Sıfır veya bir ağ güvenlik grubu da uygulanabilir toohello alt hello ağ arabirimi atanır. Bir ağ güvenlik grubu uygulanan tooa ağ arabirimi ve hello alt hello ağ arabirimi olduğunda, bazen beklenmeyen sonuçlar ortaya atanır. tootroubleshoot ağ güvenlik grubu uygulanan toonetwork arabirimleri ve alt ağlar, okuma hello [ağ güvenlik grupları sorun giderme](virtual-network-nsg-troubleshoot-portal.md#nsg) makalesi.|
    |Abonelik|Evet|Azure birini [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Merhaba sanal makine, bağlandığınız bir ağ arabirimi tooand hello sanal ağ ekleme toomust mevcut hello aynı abonelik.|
    |Özel IP adresi (IPv6)|Hayır| Bu onay kutusunu seçerseniz, bir IPv6 adresi atanmış toohello ağ arabirimi, ayrıca toohello ağ arabirimi toohello IPv4 adresi atanmış. Merhaba bkz [IPv6](#IPv6) hakkında önemli bilgiler için kullanım IPv6 ağ arabirimi ile bu makalenin. Merhaba IPv6 adresi için bir atama yöntemi seçemezsiniz. Bir IPv6 adresi tooassign seçerseniz, hello dinamik yöntemiyle atanır.
    |IPv6 adı (yalnızca hello görünür **özel IP adresi (IPv6)** onay kutusu işaretli) |Evet, hello varsa **özel IP adresi (IPv6)** onay kutusu işaretli.| Bu ad tooa ikincil IP yapılandırması hello ağ arabirimi için atanır. Merhaba IP yapılandırmaları hakkında daha fazla bilgi [görünüm ağ arabirimi ayarları](#view-network-interface-settings) bu makalenin.|
    |Kaynak grubu|Evet|Var olan seçin [kaynak grubu](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) veya bir tane oluşturun. Bir ağ arabirimi aynı hello mevcut veya hello sanal makine için iliştirmek daha farklı bir kaynak grubu veya hello sanal ağa bağlanma.|
    |Konum|Evet|Merhaba sanal makine, bağlandığınız bir ağ arabirimi tooand hello sanal ağ ekleme toomust mevcut hello aynı [konumu](https://azure.microsoft.com/regions), tooas bir bölge da denir.|

hello portal Hello portal genel bir IP adresi oluşturun ve hello portalı kullanarak bir sanal makine oluşturduğunuzda tooa ağ arabirimi atayın olsa da, oluşturduğunuzda, bir ortak IP adresi toohello ağ arabirimi hello seçeneği tooassign sağlamaz. toolearn tooadd bir ortak IP adresi toohello ağ arabirim nasıl, oluşturduktan sonra hello okuma [yönetmek IP adresleri](virtual-network-network-interface-addresses.md) makalesi. Toocreate bir genel IP adresine sahip bir ağ arabirimi istiyorsanız hello CLI veya PowerShell toocreate hello ağ arabirimini kullanmanız gerekir.

>[!Note]
> Yalnızca hello ağ arabirimine ekli tooa sanal makine ve hello sanal makine tamamlandıktan sonra bir MAC adresi toohello ağ arabirimi azure atar hello ilk kez başlatılır. Azure toohello ağ arabirimi atar hello MAC adresi belirtemezsiniz. MAC adresi atanmış kalır toohello ağ arabirimi Hello ağ arabirimi silinene kadar hello veya hello toohello hello birincil ağ arabirimi birincil IP yapılandırmasının atanan özel IP adresi değiştirilemez. IP adresleri ve hello okuma IP yapılandırmaları hakkında daha fazla toolearn [yönetmek IP adresleri](virtual-network-network-interface-addresses.md) makalesi.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC oluşturun](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Ağ arabirimi ayarlarını görüntüleme

Görüntüleyin ve oluşturulduktan sonra bir ağ arabirimi için çoğu ayarlarını değiştirin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooview istediğiniz veya ayarlarını değiştirmek hello ağ arabirimi'ı tıklatın.
4. Merhaba aşağıdaki ayarları görünür hello dikey penceresinde hello ağ arabiriminin seçtiğiniz listelenmiştir:
    - **Genel Bakış:** tooit atanmış hello IP adresleri, hello sanal ağ alt hello ağ arabirimi atanır ve hello sanal makine hello ağ arabirimi çok bağlı gibi hello ağ arabirimi hakkında bilgi sağlar (IF bağlı olduğu tooone). Merhaba aşağıdaki resimde hello genel bakış için ayarları adlı ağ arabirimi gösterir **mywebserver256**: ![ağ arabirimi genel bakış](./media/virtual-network-network-interface/nic-overview.png) ağ arabirimi tooa farklı bir kaynak grubu taşıyabilirsiniz veya Abonelik tıklayarak (**değiştirme**) sonraki toohello **kaynak grubu** veya **abonelik adı**. Merhaba ağ arabirimi taşırsanız, onu sahip tüm kaynakları ilgili toohello ağ arabirimi taşımanız gerekir. Örneğin, Hello ağ arabirimine ekli tooa sanal makine ise, ayrıca hello sanal makine ve diğer ilgili sanal makine kaynakları taşımalısınız. Merhaba okuma toomove bir ağ arabirimi [kaynak tooa yeni kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) makalesi. Önkoşullar ve nasıl kullanarak toomove kaynakları hello Azure portalı, PowerShell ve Azure CLI hello Hello makalede listelenmektedir.
    - **IP yapılandırması:** tooIP yapılandırmaları atanan genel ve özel IPv4 ve IPv6 adresleri burada listelenir. Bir IPv6 adresi tooan IP yapılandırması atanmışsa hello adresi görüntülenmez. IP yapılandırmaları ve nasıl hello tooadd ekleme ve kaldırma IP adresleri hakkında daha fazla bilgi [yapılandırma IP adresleri için bir Azure ağı arabirimi](virtual-network-network-interface-addresses.md) makalesi. IP iletimi ve alt ağ ataması, bu bölümde de yapılandırılır. toolearn hello okuyun, bu ayarlar hakkında daha fazla [etkinleştirmek veya IP iletimini devre dışı](#enable-or-disable-ip-forwarding) ve [değiştirme alt ağ ataması](#change-subnet-assignment) bu makalenin bölümler.
    - **DNS sunucuları:** hangi DNS sunucusunun bir ağ arabirimi Azure DHCP sunucuları tarafından hello atanır belirtebilirsiniz. Merhaba ağ arabirimi hello ayarı devrettiği hello sanal ağ hello ağ arabirimi için atanan veya atanan için hello sanal ağ için hello ayarını geçersiz kılar özel bir ayar vardır. ne görüntülenir toomodify tam hello adımları hello [değişiklik DNS sunucuları](#change-dns-servers) bu makalenin.
    - **Ağ güvenlik grubu (NSG):** NSG olan görüntüler ilişkili toohello ağ arabirimi (varsa). Bir NSG'yi hello ağ arabirimi için gelen ve giden kuralları toofilter ağ trafiğini içerir. Bir NSG'yi ilişkili toohello ağ arabirimi, ilişkili NSG görüntülenen hello hello adı ise. ne görüntülenir toomodify tam hello adımları hello [ağ güvenlik grubu ilişkileri yönetme](virtual-network-manage-nsg-arm-portal.md#manage-associations) makalesi.
    - **Özellikler:** anahtar hello ağ arabirimi, MAC adresini (Merhaba ağ arabirimine ekli tooa sanal makine yoksa boş) dahil olmak üzere ilgili ayarları ve hello içinde var. abonelik görüntüler.
    - **Etkin güvenlik kuralları:** güvenlik kuralları hello ağ arabirimi sanal makine çalışırken ekli tooa ve ilişkili toohello ağ arabirimi, atanan için hello alt ağ veya her ikisini bir NSG ise listelenir. görüntülenenleri, hakkında daha fazla toolearn okuma hello [ağ güvenlik grupları sorun giderme](virtual-network-nsg-troubleshoot-portal.md#nsg) makalesi. Merhaba okuma Nsg'ler hakkında daha fazla toolearn [ağ güvenlik grupları](virtual-networks-nsg.md) makalesi.
    - **Etkin yollar:** hello ağ arabirimi sanal makine çalışırken ekli tooa ise yolları listelenir. Merhaba yollar hello Azure varsayılan yollar, tüm kullanıcı tanımlı yolları (UDR) ve hello alt hello ağ arabirimi atandığı için bulunabilecek BGP yollarını birleşimidir. görüntülenenleri, hakkında daha fazla toolearn okuma hello [sorun giderme yolları](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) makalesi. Azure varsayılan ve hello okuma Udr'ler hakkında daha fazla toolearn [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makalesi.
    - **Ortak Azure Resource Manager ayarları:** toolearn hello okuma ortak Azure Resource Manager ayarları hakkında daha fazla [etkinlik günlüğü](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [erişim denetimi (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [etiketleri ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Kilitler](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ve [Otomasyon betiğini](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) makaleleri.

**Komutları**

Bir IPv6 adresi tooa ağ arabirimi atanmışsa hello PowerShell çıkış hello adresi atanmış, ancak atanan hello adresi döndürmez hello olgu döndürür. Benzer şekilde, CLI döndürür adresi hello hello olgu atandı, ancak döndürür hello *null* çıktısını hello adresi içinde.

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC listesi](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview ağ arabirimleri hello Abonelikteki; [az ağ NIC Göster](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) bir ağ arabirimi için tooview ayarları|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview ağ arabirimlerini hello abonelik görünüm ayarlarını veya bir ağ arabirimi|

## <a name="change-dns-servers"></a>DNS sunucularını değiştirme

Merhaba DNS sunucusu hello Azure DHCP sunucusu toohello ağ arabirimi hello sanal makine işletim sistemi içinde atanır. atanan hello DNS ne olursa olsun hello DNS sunucusu için bir ağ arabirimi ayarıdır sunucusudur. bir ağ arabirimi için ad çözümleme ayarları hakkında daha fazla toolearn bkz [ad çözümlemesi için sanal makineler](virtual-networks-name-resolution-for-vms-and-role-instances.md). Merhaba ağ arabirimi hello sanal ağdan hello ayarlarını devralmak veya hello sanal ağ için hello ayarını geçersiz kılmak kendi benzersiz ayarları kullanın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooview istediğiniz veya ayarlarını değiştirmek hello ağ arabirimi'ı tıklatın.
4. Seçtiğiniz hello ağ arabirimi için Hello dikey penceresinde tıklayın **DNS sunucuları** altında **ayarları**.
5. Şunlardan birini tıklatın:
    - **Sanal ağ (varsayılan) devralmak**: hello sanal ağ hello ağ arabiriminin atandığı için tanımlanan bu seçeneği tooinherit hello DNS sunucusu ayarını seçin. Merhaba sanal ağ düzeyinde bir özel DNS sunucusu veya hello Azure tarafından sağlanan DNS sunucusu tanımlanır. Hello Azure tarafından sağlanan DNS sunucusu ana bilgisayar adları için atanan kaynakların toohello çözümleyebilir aynı sanal ağ. FQDN toodifferent sanal ağlar atanmış kaynaklar için kullanılan tooresolve olması gerekir.
    - **Özel**: birden çok sanal ağlarda kendi DNS sunucu tooresolve adları yapılandırabilirsiniz. Başlangıç IP adresi girin hello server'ın bir DNS sunucusu olarak toouse istiyor. Belirttiğiniz hello DNS sunucusu adresi, yalnızca toothis ağ arabirimi ve herhangi bir DNS ayar hello sanal ağ hello ağ arabirimi için atandığı geçersiz kılmalar atanır.
6. **Kaydet** düğmesine tıklayın.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC güncelleştirme](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Etkinleştirmek veya IP iletimini devre dışı bırakma

IP iletimi hello sanal makine bir ağ arabirimi iliştirildiği sağlar:
- Ağ trafiği tooany toohello ağ arabirimine atanmış hello IP yapılandırmalarının atanmış hello IP adreslerini biri için hedeflemeyen alırsınız.
- Ağ trafiği bir ağ arabiriminin IP yapılandırmalarının bir atanan tooone hello daha farklı bir kaynak IP adresine sahip gönderin.

Merhaba ayarı sanal makine gereksinimlerini tooforward hello trafiği alır, ekli toohello sanal makinenin her ağ arabirimi için etkinleştirilmesi gerekir. Birden çok ağ arabirimlerine veya tek bir ağ arabirimi bağlı tooit olup bir sanal makine trafik gönderebilir. IP iletimi Azure bir ayar olmakla birlikte, hello sanal makine da güvenlik duvarı, WAN iyileştirmesi ve Yük Dengeleme uygulamalar gibi bir uygulama mümkün tooforward hello trafiğini çalıştırmanız gerekir. Bir sanal makine ağ uygulamaları çalıştırırken hello sanal makine başvurulan tooas ağ sanal gereç görülür. Hello hazır toodeploy ağ sanal Gereçleri listesini görüntüleyebileceğiniz [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). IP iletimi genellikle kullanıcı tanımlı yollar ile kullanılır. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makalesi.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooenable istediğiniz ya da devre dışı bırakmak için iletme IP hello ağ arabirimi'ı tıklatın.
4. Seçtiğiniz hello ağ arabirimi için Hello dikey penceresinde tıklayın **IP yapılandırmaları** hello içinde **ayarları** bölümü.
5. Tıklatın **etkin** veya **devre dışı** (varsayılan ayar) toochange hello ayarı.
6. **Kaydet** düğmesine tıklayın.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC güncelleştirme](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Alt ağ ataması değiştirme

Merhaba alt ağ, ancak bir ağ arabirimi atandığı hello sanal ağda değil, değiştirebilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **ağ arabirimleri** görünür, dikey penceresinde, tooview istediğiniz veya ayarlarını değiştirmek hello ağ arabirimi'ı tıklatın.
4. Tıklatın **IP yapılandırmaları** altında **ayarları** hello dikey penceresinde, seçtiğiniz hello ağ arabirimi için. Tüm özel IP adresleri IP yapılandırmaları için listelenen varsa **(statik)** sonraki toothem izleyin hello adımları izleyerek başlangıç IP adresi ataması yöntemi toodynamic değiştirmelisiniz. Tüm özel IP adresleri hello dinamik atama yöntemi toochange hello alt ağ ataması hello ağ arabirimi için atanması gerekir. Merhaba adresleri hello dinamik yöntemiyle atanmışsa toostep beş devam edin. Merhaba statik atama yöntemi ile herhangi bir IPv4 adresi atanmışsa adımları toochange hello atama yöntemi toodynamic aşağıdaki hello tamamlayın:
    - Toochange hello Itanium tabanlı sistemler için IPv4 adres atama yöntemi için IP yapılandırmaları hello listesinden istediğiniz hello IP Yapılandırması'nı tıklatın.
    - Görüntülenen hello dikey penceresinde hello IP yapılandırması için tıklayın **dinamik** hello için **atama** yöntemi. Bir IPv6 adresi hello statik atama yöntemiyle atayamazsınız.
    - **Kaydet** düğmesine tıklayın.
5. Tooconnect hello ağ arabirimi toofrom hello istediğiniz hello alt ağ seçin **alt** aşağı açılan liste.
6. **Kaydet** düğmesine tıklayın. Yeni dinamik adresleri hello alt ağ adres aralığından hello yeni alt ağ için atanır. Seçerseniz hello ağ arabirimi tooa yeni alt atadıktan sonra statik bir IPv4 adresi hello yeni alt ağ adres aralığından atayabilirsiniz. ekleme, değiştirme ve hello okuma bir ağ arabirimi için IP adresleri kaldırma hakkında daha fazla toolearn [yönetmek IP adresleri](virtual-network-network-interface-addresses.md) makalesi.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC IP yapılandırmasını güncelleştir](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Bir ağ arabirimi Sil

Ekli tooa sanal makine olmadığı sürece, bir ağ arabirimi silebilirsiniz. Ekli tooa sanal makine varsa, ilk yer hello (serbest bırakıldı) sanal makine durdurulmuş hello içinde durumu gerekir, hello ağ arabirimi silmeden önce hello ağ arabirimi hello sanal makineden ayırın. bir ağ arabirimi bir sanal makineden toodetach, tam hello adımları hello [bir sanal makineden ağ arabirimini Ayır](virtual-network-network-interface-vm.md#vm-remove-nic) hello bölümünü [ekleme veya kaldırma ağ arabirimleri](virtual-network-network-interface-vm.md) makale. Bir sanal makine silinmesi, tüm ağ arabirimleri ekli tooit ayırır ancak hello ağ arabirimleri silmez.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. Okuma hello [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) makale toolearn rolleri ve izinleri tooaccounts atama hakkında daha fazla bilgi.
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *ağ arabirimleri*. Zaman **ağ arabirimleri** görünür hello arama sonuçlarında tıklatın.
3. Toodelete istediğiniz sağ hello ağ arabirimi **silmek**.
4. Tıklatın **Evet** hello ağ arabiriminin tooconfirm silme.

Ne zaman bir ağ arabirimi, tüm MAC silin veya atanmış IP adresleri tooit yayınladı.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ NIC Sil](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Sonraki adımlar
toocreate bir sanal makine birden çok ağ arabirimleri veya IP adresleri, makaleler hello okuyun:

**Komutları**

|Görev|Aracı|
|---|---|
|Birden çok NIC ile VM oluşturma|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Birden çok IPv4 adresleriyle tek bir NIC VM oluşturma|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Özel bir IPv6 adresi (arkasında bir Azure yük dengeleyici) ile tek bir NIC VM oluşturma|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager şablonu](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
