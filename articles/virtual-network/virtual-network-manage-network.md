---
title: "aaaCreate, değiştirme veya bir Azure sanal ağı silme | Microsoft Docs"
description: "Nasıl toocreate, değiştirme veya Azure sanal ağında silme öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Oluşturma, değiştirme veya bir sanal ağı silme

Nasıl toocreate ve Sil gibi bir sanal ağ ve değişiklik ayarlar öğrenin DNS sunucuları ve IP adresi alanlarını, varolan bir sanal ağı.

Bir sanal ağ kendi ağ hello bulutta gösterimidir. Bir sanal ağ hello ayrılmış tooyour Azure aboneliği olan Azure bulut mantıksal yalıtımının ' dir. Oluşturduğunuz her sanal ağ için şunları yapabilirsiniz:
- Bir adres alanı tooassign seçin. Bir adres alanı 10.0.0.0/16 gibi sınıfsız etki alanları arası yönlendirme (CIDR) gösterimi kullanılarak tanımlanmış bir veya daha fazla adres aralıklarını oluşur.
- Toouse hello Azure tarafından sağlanan DNS sunucusu seçmeniz veya kendi DNS sunucusu kullanın. Bağlı toohello sanal ağ olan tüm kaynakların bu DNS sunucusu tooresolve adları hello sanal ağ içinde atanır.
- Segment hello sanal ağınıza alt ağlar, her biri kendi adres aralığında hello hello sanal ağın adres alanı. toocreate, değiştirme ve silme alt ağlara nasıl görürüm toolearn [Ekle, değiştirme veya silme alt ağlar](virtual-network-manage-subnet.md).

Bu makalede nasıl toocreate, değiştirme ve sanal ağlar hello Azure Resource Manager dağıtım modelini kullanarak silme açıklanmaktadır.

## <a name="before"></a>Başlamadan önce

Bu makalede açıklanan hello görevleri başlamadan önce aşağıdaki önkoşullar hello tamamlayın:

- Yeni tooworking sanal ağlara sahip değilseniz, hello alıştırmada gözden geçirmenizi öneririz [ilk Azure sanal ağınızı oluşturmak](virtual-network-get-started-vnet-subnet.md). Bu alıştırmada sanal ağlar ile daha öğrenmenize yardımcı olabilir.
- sanal ağlar, gözden geçirme için sınırları hakkında toolearn [Azure sınırları](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Toohello Azure portalında oturum, Azure hesabınızı kullanarak Azure komut satırı aracı (Azure CLI) ya da Azure PowerShell hello. Bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede açıklanan toocomplete hello görevleri PowerShell komutları toouse düşünüyorsanız, öncelikle [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba hello Azure PowerShell cmdlet'lerinin yüklü en son sürümüne sahip olduğunuzdan emin olun. Merhaba örneklerde, PowerShell komutları için tooget Yardım girin `get-help <command> -full`.
- Azure CLI komutları bu makalede açıklanan toocomplete hello görevleri toouse düşünüyorsanız, öncelikle [Azure CLI'yi yükleme ve yapılandırma](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Azure CLI yüklenmiş hello en son sürümüne sahip olduğunuzdan emin olun. Azure CLI komutları tooget Yardım girin `az <command> --help`.


## <a name="create-vnet"></a>Bir sanal ağ oluşturma

bir sanal ağ toocreate:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Tıklatın **yeni** > **ağ** > **sanal ağ**.
3. Merhaba üzerinde **sanal ağ** dikey penceresinde hello **dağıtım modeli seçin** kutusunda, bırakın **Resource Manager** seçili ve ardından **oluşturma**.
4. Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:
    - **Adı**: hello adının benzersiz olması gerekir hello [kaynak grubu](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) toocreate hello sanal ağı seçin. Merhaba sanal ağ oluşturulduktan sonra hello adını değiştiremezsiniz. Zaman içinde birden çok sanal ağlar oluşturabilir. Öneriler adlandırma için bkz: [adlandırma kuralları](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Bir adlandırma kuralı aşağıdaki yardımcı daha kolay toomanage olun birden çok sanal ağ.
    - **Adres alanı**: hello adres alanı CIDR gösteriminde belirtin. tanımladığınız hello adres alanı, ortak veya özel (RFC 1918) olabilir. Genel veya özel olarak hello adres alanını tanımlamak, hello adres alanı hello sanal ağ, birbirine bağlı sanal ağlar ve sanal ağ toohello bağlı şirket içi ağlara içinde yalnızca erişilebilir olup. Adres alanlarını aşağıdaki hello ekleyemezsiniz:
        - 224.0.0.0/4 (çok noktaya yayın)
        - 255.255.255.255/32 (yayın)
        - 127.0.0.0/8 (geri döngü)
        - 169.254.0.0/16 (bağlantı yerel)
        - 168.63.129.16/32 (iç DNS)

      Merhaba sanal ağ oluşturduğunuzda, yalnızca bir adres alanı tanımlayabilirsiniz rağmen hello sanal ağ oluşturulduktan sonra daha fazla adres alanları ekleyebilirsiniz. toolearn tooadd bir adres alanı nasıl tooan var olan sanal ağ bkz [ekleme veya kaldırma bir adres alanı](#add-address-spaces) bu makalede.

      >[!WARNING]
      >Bir sanal ağ ile başka bir sanal ağ veya şirket içi ağ çakışan adres alanları varsa, hello iki ağlara bağlanamaz. Bir adres alanı tanımlamadan önce tooconnect hello sanal ağ tooother sanal ağları veya şirket içi ağlarda hello gelecekteki isteyip istemediğinizi göz önünde bulundurun.
      >
      >

    - **Alt ağ adı**: hello alt ağ adı hello sanal ağ içinde benzersiz olmalıdır. Merhaba alt ağ oluşturulduktan sonra hello alt ağ adı değiştirilemiyor. Hello portal bir sanal ağ oluşturduğunuzda, bir sanal ağ gerekli toohave değil olsa da, bir alt ağı hiçbir alt ağ tanımlamanızı gerektirir. Bir sanal ağ oluşturduğunuzda, hello Portalı'nda, yalnızca bir alt ağ tanımlayabilirsiniz. Merhaba sanal ağ oluşturulduktan sonra daha fazla alt ağlar toohello sanal ağ, daha sonra ekleyebilirsiniz. tooadd bir alt tooa sanal ağ bkz [bir alt ağ oluşturmak](virtual-network-manage-subnet.md#create-subnet) içinde [oluşturma, değiştirme veya silme alt](virtual-network-manage-subnet.md). Azure CLI veya PowerShell kullanarak birden çok alt ağa sahip bir sanal ağ oluşturabilirsiniz.

      >[!TIP]
      >Bazı durumlarda, yöneticileri hello alt ağlar arasında yönlendirme toofilter veya denetim trafiğinin farklı alt ağlar oluşturun. Alt ağlar tanımlamadan önce nasıl toofilter istediğiniz ve, alt ağlar arasında trafiği yönlendirmek göz önünde bulundurun. alt ağlar arasındaki trafik filtreleme hakkında daha fazla toolearn bkz [ağ güvenlik grupları](virtual-networks-nsg.md). Azure otomatik olarak alt ağlar, ancak arasındaki yolları trafiği Azure varsayılan yolların geçersiz kılabilirsiniz. toolearn toooverride Azure varsayılan alt ağ trafik yönlendirme, bkz [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md).
      >

    - **Alt ağ adres aralığı**: hello aralığı hello sanal ağ için girdiğiniz hello adres alanı içinde olmalıdır. belirleyebileceğiniz hello en küçük /29, sekiz IP adresleri hello alt ağı için sağladığı aralıktır. Azure yedekleri ilk hello ve son Protokolü uyum için her bir alt ağ adresi. Üç ek adresleri Azure hizmetinin kullanım için ayrılmıştır. Sonuç olarak, bir sanal ağ /29 bir alt ağ adres aralığı ile yalnızca üç kullanılabilir IP adresleri vardır. Bir sanal ağ tooa VPN ağ geçidi tooconnect planlıyorsanız, ağ geçidi alt ağı oluşturmanız gerekir. Daha fazla bilgi edinmek [ağ geçidi alt ağları için belirli bir adresi aralığı konuları](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Belirli koşullar altında Hello alt ağ oluşturulduktan sonra başlangıç adresi aralığı değiştirebilirsiniz. toochange bir alt ağ adres aralığı nasıl görürüm toolearn [alt ağ ayarlarını değiştirme](#change-subnet) içinde [Ekle, değiştirme veya silme alt ağlar](virtual-network-manage-subnet.md).
    - **Abonelik**: seçin bir [abonelik](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Merhaba kullanamazsınız aynı sanal ağda birden fazla Azure aboneliği. Ancak, diğer abonelikler bir abonelik toovirtual ağlarda sanal bir ağa bağlanabilir. tooconnect sanal ağlar farklı Aboneliklerde Azure VPN ağ geçidi veya sanal ağ eşlemesi kullanın. Toohello sanal ağ bağlantı herhangi bir Azure kaynak hello olmalıdır hello sanal ağ aynı abonelik.
    - **Kaynak grubu**: Varolan seçin [kaynak grubu](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) veya yeni bir tane oluşturun. Bir Azure kaynağı toohello sanal ağ bağlanmak hello olabilir aynı kaynak grubu olarak hello sanal ağ veya farklı bir kaynak grubu.
    - **Konum**: Azure seçin [konumu](https://azure.microsoft.com/regions/), bir bölge olarak da bilinir. Bir sanal ağ içinde yalnızca bir Azure konumu olabilir. Ancak, bir VPN ağ geçidi kullanarak başka bir konumda bir konum tooa sanal ağ sanal bir ağa bağlanabilir. Toohello sanal ağ bağlantı herhangi bir Azure kaynak hello olmalıdır hello sanal ağ ile aynı konumda.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ vnet oluşturma](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Yeni-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Sanal ağları görüntüle ve ayarları

tooview sanal ağlar ve ayarları:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında tıklatın **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde tooview ayarlarını istediğiniz hello sanal ağ'ı tıklatın.
4. Hello aşağıdaki ayarlar seçtiğiniz hello sanal ağ için hello dikey penceresinde listelenir:
    - **Genel Bakış**: hello sanal ağ adres alanı ve DNS sunucuları da dahil olmak üzere hakkında bilgi sağlar. Merhaba aşağıdaki ekran görüntüsünde hello genel bakış için ayarları adlı bir sanal ağ gösterir **MyVNet**:

        ![Ağ arabirimi genel bakış](./media/virtual-network-manage-network/vnet-overview.png)

      Merhaba üzerinde **genel bakış** dikey penceresinde, sanal ağ tooa farklı bir abonelik veya Kaynak Grup taşıyabilirsiniz. toomove bir sanal ağ nasıl görürüm toolearn [kaynakları tooa farklı bir kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Önkoşullar ve Azure portalı, PowerShell ve Azure CLI kullanarak toomove kaynakları nasıl hello Hello makalede listelenmektedir. Bağlı toohello sanal ağ olan tüm kaynakların hello sanal ağ ile taşımanız gerekir.
    - **Adres alanı**: toohello sanal ağ atanan hello adres alanları listelenir. tooadd ekleme ve kaldırma bir adres alanı nasıl tamamlamak toolearn hello adımlarda [ekleme veya kaldırma bir adres alanı](#address-spaces) bu makalede.
    - **Bağlı cihazları**: bağlı toohello sanal ağı olan kaynaklar listelenir. Ekran görüntüsü önceki hello üç ağ arabirimleri ve bir yük dengeleyiciye bağlı toohello sanal ağ tabanlıdır. Oluşturun ve toohello sanal ağa bağlanmak herhangi yeni kaynaklar listelenir. Bağlı toohello sanal ağ olan bir kaynak silerseniz, artık hello listesinde görüntülenir.
    - **Alt ağlar**: hello sanal ağ içindeki mevcut alt ağların bir listesi gösterilir. tooadd ekleme ve kaldırma bir alt ağ nasıl görürüm toolearn [bir alt ağ oluşturmak](virtual-network-manage-subnet.md#create-subnet) ve [bir alt ağını silmek](virtual-network-manage-subnet.md#delete-subnet) içinde [Ekle, değiştirme veya silme alt ağlar](virtual-network-manage-subnet.md).
    - **DNS sunucuları**: hello Azure iç DNS sunucusu veya özel bir DNS sunucusu ad çözümlemesi bağlı toohello sanal ağ aygıtları için sağlayıp sağlamadığını belirtebilirsiniz. Hello Azure portal kullanarak bir sanal ağ oluşturduğunuzda, Azure'nın DNS sunucuları bir sanal ağ içinde ad çözümlemesi için varsayılan olarak kullanılır. tam hello toomodify hello DNS sunucuları, adımları [ekleme, değiştirme veya kaldırma bir DNS sunucusu](#dns-servers) bu makalede.
    - **Eşlemeler**: hello abonelikte varolan eşlemeler varsa, bunlar burada listelenir. Var olan eşlemeleri için ayarları görüntüleyin veya oluşturun, değiştirin veya eşlemeler silin. eşlemeler, hakkında daha fazla toolearn bkz [sanal ağ eşlemesi](virtual-network-peering-overview.md).
    - **Özellikleri**: Merhaba hello sanal ağın kaynak kimliği dahil olmak üzere sanal ağ ve Azure abonelik içinde hello hakkında görüntüler ayarları.
    - **Diyagram**: hello diyagramı bağlı toohello sanal ağı olan tüm aygıtları görsel bir gösterimini sağlar. Merhaba diyagramı hello aygıtlar hakkında bazı önemli bilgiler sahiptir. toomanage hello diyagramda, bu görünümde bir aygıtı hello aygıt'ı tıklatın.
    - **Ortak Azure ayarları**: toolearn ortak Azure ayarları hakkında daha fazla bilgi aşağıdaki hello bakın:
        *   [Etkinlik Günlüğü](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Erişim denetimi (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Etiketler](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Kilitler](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Otomasyon komut dosyası](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ vnet Göster](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Bir adres alanı Ekle Kaldır

Bir sanal ağ için adres alanları ekleyip çıkarabilirsiniz. Bir adres alanı CIDR gösteriminde belirtilmelidir ve diğer adres alanları hello içinde ile aynı çakışamaz sanal ağ. tanımladığınız hello adres alanları ortak veya özel (RFC 1918) olabilir. Genel veya özel olarak hello adres alanını tanımlamak, hello adres alanı hello sanal ağ, birbirine bağlı sanal ağlar ve sanal ağ toohello bağlı şirket içi ağlara içinde yalnızca erişilebilir olup. Adres alanlarını aşağıdaki hello ekleyemezsiniz:

- 224.0.0.0/4 (çok noktaya yayın)
- 255.255.255.255/32 (yayın)
- 127.0.0.0/8 (geri döngü)
- 169.254.0.0/16 (bağlantı yerel)
- 168.63.129.16/32 (iç DNS)

tooadd veya bir adres alanı Kaldır:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında seçin **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde, kendisi için tooadd istediğiniz veya bir adres alanı kaldırma hello sanal ağ'ı tıklatın.
4. Altında dikey penceresinde Hello sanal ağ **ayarları**, tıklatın **adres alanı**.
5. Merhaba dikey penceresinde hello adres alanı, aşağıdaki seçenekleri şu hello birini tamamlayın:
    - **Bir adres alanı Ekle**: hello yeni bir adres alanı girin. Merhaba adres alanı hello sanal ağ için tanımlı olan bir adres alanı ile çakışamaz.
    - **Bir adres alanı Kaldır**: bir adres alanı sağ tıklatın ve ardından **kaldırmak**. Bir alt ağ hello adres alanı varsa, hello adres alanı kaldırılamıyor. tooremove bir adres alanı, ilk silmelisiniz hiçbir alt ağ (ve bağlı toohello alt ağlardır herhangi bir kaynağa) hello adres alanı yok.
6. **Kaydet** düğmesine tıklayın.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|Yalnızca Kaynak Yöneticisi|[az ağ vnet güncelleştirme](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Ekleme, değiştirme veya bir DNS sunucusunu kaldırma

Merhaba sanal ağ için belirttiğiniz hello DNS sunucuları ile bağlı toohello sanal ağ olan tüm VM'ler kaydedin. Ayrıca belirtilen hello kullandıkları ad çözümlemesi için DNS sunucusu. Bir VM her bir ağ arabirimine (NIC), kendi DNS sunucu ayarları olabilir. Bir NIC kendi DNS sunucu ayarları varsa, sanal ağ hello hello DNS sunucusu ayarlarını geçersiz kılar. toolearn NIC DNS ayarları hakkında daha fazla bilgi görmek [ağ arabirimi görevleri ve ayarlar](virtual-network-network-interface.md#change-dns-servers). VM'ler ve Azure Cloud Services rol örnekleri için ad çözümlemesi hakkında daha fazla toolearn bkz [VM'ler ve rol örnekleri için ad çözümlemesi](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, değiştirmek veya bir DNS sunucusu kaldırabilirsiniz:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında seçin **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde hello sanal ağ için DNS ayarlarını toochange istediğiniz'ı tıklatın.
4. Altında dikey penceresinde Hello sanal ağ **ayarları**, tıklatın **DNS sunucuları**.
5. Aşağıdaki seçenekleri DNS sunucuları listeler hello dikey penceresinde şu hello birini seçin:
    - **Varsayılan (Azure tarafından sağlanan)**: tüm kaynak adları ve özel IP adresleri otomatik olarak kayıtlı toohello Azure DNS sunucularıdır. Bağlı toohello olan kaynaklar arasındaki adlarını çözümleyebildiğini aynı sanal ağ. Bu seçenek tooresolve adlarının sanal ağlar arasında kullanamazsınız. sanal ağlar arasında tooresolve adları, özel bir DNS sunucusu kullanmanız gerekir.
    - **Özel**: bir veya daha fazla sunucu eklemek, Azure toohello için bir sanal ağ sınırlayın. DNS sunucusu sınırları hakkında daha fazla toolearn bkz [Azure sınırları](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Seçenekler aşağıdaki hello vardır:
        - **Adres Ekle**: hello sunucu tooyour sanal ağ DNS sunucuları listesi ekler. Bu seçenek ayrıca Azure ile Merhaba DNS sunucusu kaydeder. Azure ile bir DNS sunucusu zaten kaydınız varsa, bu DNS sunucusuna hello listesinden seçebilirsiniz.
        - **Bir adresi kaldırmak**: tooremove, istediğiniz sonraki toohello server'ı **X**. Merhaba sunucu siliniyor hello sunucu yalnızca bu sanal ağ listesinden kaldırır. Merhaba DNS sunucusu Azure'da diğer sanal ağlar toouse için kayıtlı kalır.
        - **DNS sunucusu adresleri yeniden sıralamak**: Merhaba, DNS sunucularının listesi tooverify ortamınız için sipariş düzeltmek önemlidir. DNS sunucusu listeleri belirtildikleri hello sırada kullanılır. Hepsini ayarı olarak çalışmaz. Merhaba ilk DNS sunucusu hello listesinde ulaşılabiliyorsa hello istemci olup hello DNS sunucusu düzgün bağımsız olarak, DNS sunucusu kullanır. Listelenen tüm hello DNS sunucularını kaldırın ve sonra geri istediğiniz hello sırayla ekleyin.
        - **Adres değiştirme**: hello DNS sunucusu hello listesinde vurgulayın ve hello yeni bir ad girin.
6. **Kaydet** düğmesine tıklayın.
7. Merhaba yeni DNS sunucusu ayarlarını atanmaları için bağlı toohello sanal ağ olan hello VM'ler yeniden başlatın. Yeniden başlatılana kadar VM'ler toouse geçerli DNS ayarlarına devam edin.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ vnet güncelleştirme](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Bir sanal ağı silme

Yalnızca hiçbir kaynaklara bağlı tooit varsa, bir sanal ağ silebilirsiniz. Hello sanal ağ içindeki kaynaklara bağlı tooany alt ağı varsa, hello sanal ağ içindeki alt ağlara bağlı tooall hello kaynaklarını silmeniz gerekir. Merhaba adımlar toodelete, kaynak'hello kaynak bağlı olarak farklılık gösterir. bağlı toosubnets toodelete kaynaklarını nasıl okuma toolearn hello belgelerine toodelete istediğiniz her kaynak türü için. bir sanal ağ toodelete:

1. İçinde toohello oturum [portal](https://portal.azure.com) bir hesapla hello ağ katkıda bulunan rolü aboneliğiniz için diğer bir deyişle (en az) atanan izinlerini. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında tıklatın **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde, select hello sanal ağ toodelete istiyor.
4. Toohello sanal ağ, hiçbir cihaz olduğunu tooconfirm Hello sanal ağ dikey penceresinde altında bağlı **ayarları**, tıklatın **bağlı cihazları**. Bağlı cihazlarınız varsa, hello sanal ağı silmeden önce silmeniz gerekir. Hiçbir bağlı cihazlarınız varsa, tıklatın **genel bakış**.
5. Merhaba hello dikey penceresinde Hello üstünde tıklatın **silmek** simgesi.
6. tooconfirm hello silme hello sanal ağının'yi tıklatın **Evet**.


**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[Azure ağı vnet Sil](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Sonraki adımlar

- toocreate VM ve tooa sanal ağ bağlanmak, bkz: [bir sanal ağ oluşturmak ve sanal makineleri bağlanmak](virtual-network-get-started-vnet-subnet.md#create-vms).
- bir sanal ağ içindeki alt ağlara arasındaki ağ trafiğini toofilter bkz [ağ güvenlik grupları oluşturma](virtual-networks-create-nsg-arm-pportal.md).
- bir sanal ağ tooanother sanal ağ toopeer bkz [bir sanal ağ eşlemesi oluşturma](virtual-network-create-peering.md#portal).
- bir sanal ağ tooan şirket ağına bağlanmak için seçenekler hakkında toolearn bkz [VPN Gateway hakkında](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
