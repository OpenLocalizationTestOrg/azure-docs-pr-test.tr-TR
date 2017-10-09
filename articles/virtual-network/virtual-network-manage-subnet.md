---
title: "aaaAdd, değiştirmek veya bir Azure sanal ağ alt ağını silmek | Microsoft Docs"
description: "Nasıl tooadd, değiştirme veya azure'da bir sanal ağ alt silme öğrenin."
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
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Ekleme, değiştirme veya bir sanal ağ alt ağı silme

Nasıl tooadd, değiştirme veya bir sanal ağ alt silme öğrenin. 

Ekleme, değiştirme veya bir alt ağ silme önce sanal ağlar ile bilmiyorsanız, okumanızı öneririz [Azure Virtual Network'e genel bakış](virtual-networks-overview.md) ve [oluşturma, değiştirme veya silme bir sanal ağ](virtual-network-manage-network.md). Bir sanal ağ içinde dağıtılan tüm Azure kaynaklarını bir sanal ağ içindeki bir alt ağ içinde dağıtılır. Genellikle, bir sanal ağ içinde birden fazla alt ağ oluşturulur:
- **Alt ağlar arasında trafiği filtrelemek**. Ağ güvenlik grupları toosubnets toofilter gelen ve giden uygulayabilirsiniz ağ trafiğini hello sanal ağdaki tüm kaynakların (örneğin, sanal makineler). toolearn nasıl toocreate bir ağ güvenlik grubu bkz hakkında daha fazla bilgi [ağ güvenlik grupları oluşturma](virtual-networks-create-nsg-arm-pportal.md).
- **Denetim alt ağlar arasında yönlendirme**. Azure varsayılan yolların oluşturur, böylece trafik alt ağlar arasında otomatik olarak yönlendirilir. Kullanıcı tanımlı yollar oluşturarak Azure varsayılan yolların geçersiz kılabilirsiniz. Kullanıcı tanımlı yollar hakkında daha fazla toolearn bkz [kullanıcı tanımlı yollar oluşturmayı](virtual-network-create-udr-arm-ps.md). 

Bu makalede nasıl tooadd, değiştirme ve hello Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş sanal ağlar için bir alt ağ silme açıklanmaktadır.
 
## <a name="before"></a>Başlamadan önce

Bu makalede açıklanan hello görevleri başlamadan önce aşağıdaki önkoşullar hello tamamlayın:

- Yeni tooworking sanal ağlara sahip değilseniz, hello alıştırmada gözden geçirmenizi öneririz [ilk Azure sanal ağınızı oluşturmak](virtual-network-get-started-vnet-subnet.md). Bu alıştırmada sanal ağlar ile daha öğrenmenize yardımcı olabilir.
- sanal ağlar, gözden geçirme için sınırları hakkında toolearn [Azure sınırları](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Toohello Azure portalında oturum, Azure hesabınızı kullanarak Azure komut satırı aracı (Azure CLI) ya da Azure PowerShell hello. Bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede açıklanan toocomplete hello görevleri PowerShell komutları toouse düşünüyorsanız, öncelikle [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba hello Azure PowerShell cmdlet'lerinin yüklü en son sürümüne sahip olduğunuzdan emin olun. Merhaba örneklerde, PowerShell komutları için tooget Yardım girin `get-help <command> -full`.
- Bu makalede açıklanan toocomplete hello görevleri Azure CLI komutları toouse düşünüyorsanız, aşağıdakilerden birini yapmanız gerekir:
    - [Hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Azure CLI yüklenmiş hello en son sürümüne sahip olduğunuzdan emin olun.
    - Hello Azure bulut Kabuğu'nu kullanın. Merhaba CLI ve bağımlılıklarını yüklemek yerine, hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuk hello bulut Kabuğu'nu tıklatın (**> _**) hello Azure portal hello üstündeki simgesi. 

  Azure CLI komutları tooget Yardım girin `az <command> --help`.

## <a name="create-subnet"></a>Bir alt ağ Ekle

tooadd bir alt ağ:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında tıklatın **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde hello sanal ağ alt ağına tooadd istediğiniz'ı tıklatın.
4. Merhaba sanal ağ dikey penceresinde **alt ağlar**.
5. Tıklatın **+ alt**.
6. Merhaba üzerinde **alt ağ Ekle** dikey penceresinde hello şu parametreler için değerler girin:
    - **Ad**: hello adı hello sanal ağ içinde benzersiz olmalıdır.
    - **Adres aralığı**: hello aralığı hello sanal ağın adres alanı hello içinde benzersiz olmalıdır. Merhaba aralığı hello sanal ağ içindeki diğer alt ağ adresi aralıklarıyla çakışamaz. Merhaba adres alanı, sınıfsız etki alanları arası yönlendirme (CIDR) gösterimini kullanarak belirtilmelidir. Örneğin, bir sanal ağda adres alanı 10.0.0.0/16, 10.0.0.0/24 alt ağ adres alanının tanımlayabilirsiniz. belirleyebileceğiniz hello en küçük /29, sekiz IP adresleri hello alt ağı için sağladığı aralıktır. Azure yedekleri ilk hello ve son Protokolü uyum için her bir alt ağ adresi. Üç ek adresleri Azure hizmetinin kullanım için ayrılmıştır. Sonuç olarak, bir alt ağ/29 ile tanımlama adres hello alt ağda üç kullanılabilir IP adresleri aralığı sonuçlanır. Bir sanal ağ tooa VPN ağ geçidi tooconnect planlıyorsanız, ağ geçidi alt ağı oluşturmanız gerekir. Daha fazla bilgi edinmek [ağ geçidi alt ağları için belirli bir adresi aralığı konuları](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Merhaba alt ağ, belirli koşullar altında ekledikten sonra hello adres aralığını değiştirebilirsiniz. toochange bir alt ağ adres aralığı nasıl görürüm toolearn [alt ağ ayarlarını değiştir](#change-subnet) bu makalede.
    - **Ağ güvenlik grubu**: isteğe bağlı olarak, varolan bir ağ güvenlik grubu ile Merhaba alt toocontrol ilişkilendirebilirsiniz gelen ve giden ağ trafiği için hello alt filtreleme. Merhaba ağ güvenlik grubu hello aynı bulunmalıdır abonelik ve konumda hello sanal ağı. Bu ayrıca hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş olması gerekir. toolearn nasıl toocreate bir ağ güvenlik grubu bkz hakkında daha fazla bilgi [ağ güvenlik grupları](virtual-networks-create-nsg-arm-pportal.md).
    - **Yol tablosu**: isteğe bağlı olarak, varolan bir yol tablosu ile Merhaba alt toocontrol ağ trafiği tooother ağlar ilişkilendirebilirsiniz. Merhaba yol tablosu hello aynı bulunmalıdır abonelik ve konumda hello sanal ağı. Bu ayrıca hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş olması gerekir. toolearn toocreate yol tablolarını nasıl görürüm hakkında daha fazla bilgi [kullanıcı tanımlı yollar](virtual-network-create-udr-arm-ps.md).
    - **Kullanıcıların**: yerleşik roller ya da kendi özel roller kullanarak erişim toohello alt kontrol edebilirsiniz. rolleri ve kullanıcılar, tooaccess hello alt ağ atama hakkında daha fazla toolearn bkz [rol ataması toomanage erişim tooyour Azure kullanmak kaynaklar](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. Seçtiğiniz tooadd hello alt toohello sanal ağa tıklayın **Tamam**.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ sanal alt oluşturma](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[AzureRmVirtualNetworkSubnetConfig yeni](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [ekleme AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Alt ağ ayarlarını değiştirme

Ağ güvenlik grupları, yol tablolarını ve kullanıcı erişim tooa alt ağ bir alt ağdaki kaynakları yöneterek değiştirebilirsiniz. Bu ayarlar hakkında toolearn içinde [bir alt ağ Ekle](#create-subnet), 6. adıma bakın. Toochange hello adres alanı, alt ağının istiyorsanız hello alt ağdaki herhangi bir kaynağa silmeniz gerekir. Merhaba adımlar toodelete, kaynak'hello kaynak bağlı olarak farklılık gösterir. toolearn toodelete istediğiniz alt ağlar, her kaynak için okuma hello belgelerine toodelete kaynaklarını nasıl yazın. bir alt ağ için toochange hello adres aralığı:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında tıklatın **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde hello sanal ağ toochange bir alt ağ adres aralığı istediğiniz'ı tıklatın.
4. Toochange hello adres aralığı istediğiniz hello alt ağına tıklayın.
5. Merhaba, hello alt dikey **adres aralığı** kutusuna, hello yeni adres aralığı girin. Merhaba aralığı hello sanal ağın adres alanı hello içinde benzersiz olmalıdır. Merhaba aralığı hello sanal ağ içindeki diğer alt ağ adresi aralıklarıyla çakışamaz. Merhaba adres alanı CIDR gösterimini kullanarak belirtilmelidir. Örneğin, bir sanal ağda adres alanı 10.0.0.0/16, 10.0.0.0/24 alt ağ adres alanının tanımlayabilirsiniz. belirleyebileceğiniz hello en küçük /29, sekiz IP adresleri hello alt ağı için sağladığı aralıktır. Azure yedekleri ilk hello ve son Protokolü uyum için her bir alt ağ adresi. Üç ek adresleri Azure hizmetinin kullanım için ayrılmıştır. Sonuç olarak, / 29 alt ağı adres aralığı üç kullanılabilir IP adresleri vardır. Bir sanal ağ tooa VPN ağ geçidi tooconnect planlıyorsanız, ağ geçidi alt ağı oluşturmanız gerekir. Daha fazla bilgi edinmek [ağ geçidi alt ağları için belirli bir adresi aralığı konuları](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Belirli koşullar altında Hello alt ağ oluşturulduktan sonra başlangıç adresi aralığı değiştirebilirsiniz. toochange bir alt ağ adres aralığı nasıl görürüm toolearn [alt ağ ayarlarını değiştir](#change-subnet) bu makalede.
6. **Kaydet** düğmesine tıklayın.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Bir alt ağı silme

Merhaba alt ağda kaynak varsa, bir alt ağ silebilirsiniz. Merhaba alt ağdaki kaynakları varsa hello alt ağı silmeden önce hello alt ağdaki hello kaynakları silmeniz gerekir. Merhaba adımlar toodelete, kaynak'hello kaynak bağlı olarak farklılık gösterir. toolearn toodelete istediğiniz alt ağlar, her kaynak için okuma hello belgelerine toodelete kaynaklarını nasıl yazın. toodelete bir alt ağ:

1. İçinde toohello oturum [portal](https://portal.azure.com) aboneliğiniz için hello ağ katkıda bulunan rolü (en az) için izinleri atanmış bir hesap ile. rolleri ve izinleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba portal arama kutusuna **sanal ağlar**. Merhaba arama sonuçlarında tıklatın **sanal ağlar**.
3. Merhaba üzerinde **sanal ağlar** dikey penceresinde hello sanal ağ alt ağından toodelete istediğiniz'ı tıklatın.
4. Altında dikey penceresinde Hello sanal ağ **ayarları**, tıklatın **alt ağlar**.
5. Merhaba alt ağlar dikey penceresinde, sağ hello alt görünen hello listesinde alt toodelete istediğiniz, tıklatın **silmek**ve ardından **Evet** toodelete hello alt ağ.

**Komutları**

|Aracı|Komut|
|---|---|
|Azure CLI|[az ağ vnet Sil](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Sonraki adımlar

toocreate bir alt ağ içindeki bir sanal makineye bkz [bir sanal ağ oluşturma ve VM'ler hello alt ağda dağıtma](virtual-network-get-started-vnet-subnet.md#create-vms).
