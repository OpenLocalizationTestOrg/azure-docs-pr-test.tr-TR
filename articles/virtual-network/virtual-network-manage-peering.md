---
title: "aaaCreate, değiştirme veya bir Azure sanal ağ eşlemesi silme | Microsoft Docs"
description: "Nasıl toocreate, değiştirme veya bir sanal ağ eşlemesi silme öğrenin."
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Oluşturma, değiştirme veya bir sanal ağ eşlemesi silme

Nasıl toocreate, değiştirme veya bir sanal ağ eşlemesi silme öğrenin. Sanal ağ eşleme etkinleştirir, tooconnect iki sanal ağlarda aynı Azure konumuna hello Azure omurga ağı hello. Eşlendikten sonra iki sanal ağ hello hala ayrı kaynaklar olarak yönetilir. Her iki sanal ağ kaynaklarında iletişim hello ile aynı gecikme süresi ve bant genişliği hello kaynakları içinde değilmiş gibi hello aynı sanal ağ. Sanal Ağ eşlemesi ile bilmiyorsanız hello okumanız önerilir [sanal ağ eşleme genel bakış](virtual-network-peering-overview.md) hello tamamlayarak [bir sanal ağ eşleme öğretici oluşturma](virtual-network-create-peering.md), tamamlanmadan önce Bu makalede Hello görevler.

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalenin herhangi bir bölümdeki adımları gerçekleştirmeden önce görevleri aşağıdaki hello tamamlayın:

- Gözden geçirme hello [Azure sınırlar](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) makale toolearn eşleme için sınırları hakkında.
- Toohello Azure portal, Azure komut satırı arabirimi (CLI) veya Azure PowerShell bir Azure hesabı ile oturum açın. Zaten bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede, toocomplete görevleri komutları PowerShell kullanarak, [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure PowerShell cmdlet'lerinin yüklü olduğundan emin olun. tooget Yardım için örneklerle PowerShell komutlarını yazın `get-help <command> -full`.
- Bu makalede, toocomplete görevleri komutları Azure komut satırı arabirimi (CLI) kullanarak, [hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Merhaba bulut Kabuk Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuğu'nu tıklatın hello bulut Kabuk **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Bir eşleme oluşturma

>[!NOTE]
>Birkaç gereksinimi, kısıtlamaları vardır ve konuları toosuccessfully oluşturma bir sanal ağ eşlemesi. Bir eşleme oluşturmadan önce familiarized kendiniz ile Merhaba olun [gereksinimleri ve kısıtlamaları](#requirements-and-constraints) ve [gerekli izinleri](#permissions).
>

1. İçinde toohello oturum [portal](https://portal.azure.com) hello gerekli atanmış bir hesap ile [rol veya izinleri](#permissions).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *sanal ağlar*. Zaman **sanal ağlar** görünür hello arama sonuçlarında tıklatın. Seçmeyin **sanal ağları (Klasik)** hello Klasik dağıtım modeli aracılığıyla dağıtılan bir sanal ağ eşlemesi oluşturulamıyor gibi hello listesinde görünüp görünmeyeceğini.
3. Merhaba, **sanal ağlar** görünür, dikey hello sanal ağ için bir eşleme toocreate istediğiniz tıklayın.
4. Seçtiğiniz hello için sanal ağ görüntülenen hello bölmesinde **eşlemeler** hello içinde **ayarları** bölümü.
5. Tıklatın **+ Ekle**. 
6. <a name="add-peering"></a>Merhaba, **eklemek eşliği** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin:
    - **Ad:** hello eşleme için hello adı hello sanal ağ içinde benzersiz olmalıdır.
    - **Sanal ağ dağıtım modeli:** hangi dağıtım modeli hello sanal ağ seçin istediğiniz ile toopeer aracılığıyla dağıtıldı.
    - **Kaynak Kimliğimi biliyorum:** toopeer ile istediğiniz okuma erişimi toohello sanal ağınız varsa, bu onay kutusunun işaretini kaldırın. Okuma erişimi toohello sanal ağ veya toopeer ile istediğiniz abonelik yoksa, bu kutuyu işaretleyin. Merhaba sanal ağ ile toopeer hello içinde istediğiniz Hello tam kaynak Kimliğini girin **kaynak kimliği** hello kutusu işaretlendiğinde, görünen kutusu. Girdiğiniz kimliği var. bir sanal ağ için olmalıdır hello kaynak hello aynı Azure [konumu](https://azure.microsoft.com/regions) bu sanal ağ olarak. Merhaba tam kaynak kimliği arar benzerçok/abonelikleri/<Id>/resourceGroups/ < kaynak grubu adı > /providers/Microsoft.Network/virtualNetworks/ < sanal ağ-adı >. Bir sanal ağ hello özelliklerini görüntüleyerek hello kaynak kimliği için bir sanal ağ elde edebilirsiniz. nasıl bir sanal ağ tooview hello özelliklerini görmek toolearn [sanal ağlarını yönetmeleri](virtual-network-manage-network.md#view-vnet).
    - **Abonelik:** Select hello [abonelik](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) hello sanal ağı ile toopeer istiyor. Kaç tane abonelikleri hesabınızın okuma erişimine sahip bağlı olarak bir veya daha fazla abonelik listelenir. Merhaba işaretlediyseniz **kaynak kimliği** onay kutusu, bu ayar kullanılamaz. Her iki sanal ağlar Resource Manager aracılığıyla oluşturulan sürece farklı Aboneliklerdeki sanal ağlar eş. Farklı dağıtım modelleri arasında oluşturulan Aboneliklerdeki Hello özelliği toopeer Önizleme sürümünde ' dir. Farklı Aboneliklerde mevcut farklı dağıtım modeli üzerinden sanal ağlar arasında eşleme oluşturmadan önce hello Önizleme kaydolun. Hakkında daha fazla bilgi için hello önizlemesi tooregister ve [eş farklı Aboneliklerde farklı dağıtım modellerinde aracılığıyla oluşturulan sanal ağlar](create-peering-different-deployment-models-subscriptions.md).
    - **Sanal ağ:** hello toopeer ile istediğiniz sanal ağı seçin. Ya da Azure dağıtım modeliyle oluşturulan bir sanal ağ seçebilirsiniz, ancak hello sanal ağ başlatma hello sanal ağ ile aynı konumda hello gelen eşliği hello olması gerekir. Erişim toohello sanal ağ için toobe hello listesinde görünür okuduğunuz gerekir. Bir sanal ağ listeleniyorsa, gri ancak hello sanal ağın adres alanı hello hello bu sanal ağın adres alanı ile çakıştığından olabilir. Sanal ağ adres alanları, çakışma varsa, bunlar eşlenen olamaz. Merhaba işaretlediyseniz **kaynak kimliği** onay kutusu, bu ayar kullanılamaz.
    - **Sanal ağ erişimine izin ver:** seçin **etkin** (Merhaba iki sanal ağlar arası tooenable iletişimi istiyorsanız varsayılan). Sanal ağlar arasındaki iletişimi etkinleştirme sağlar bağlı kaynaklar tooeither sanal ağ toocommunicate birbirleri ile birlikte, aynı bant genişliği ve gecikme bağlı toohello değilmiş gibi hello aynı sanal ağ. Merhaba iki sanal ağlarda bulunan kaynaklar arasındaki tüm iletişimi hello Azure özel ağ ' dir. Merhaba **VirtualNetwork** hello sanal ağ ile eşlenen sanal ağ ağ güvenlik grupları için varsayılan etiket kapsar. hakkında daha fazla bilgi toolearn ağ güvenlik grubu varsayılan etiketleri okuma hello [ağ güvenlik gruplarını genel bakış](virtual-networks-nsg.md#default-tags) makalesi.  Seçin **devre dışı** trafiği tooflow toohello eşlenen sanal ağ istemiyorsanız. Seçtiğiniz **devre dışı** , bir sanal ağ başka bir sanal ağ ile eşlenen, ancak bazen hello iki sanal ağlar arasındaki trafik akışını toodisable istediğiniz olması gerekir. Etkinleştirme/devre dışı bırakma silinmesi ve yeniden eşlemeleri oluşturma daha rahat bulabilirsiniz. Bu ayar devre dışı bırakıldığında, trafiği arasında akan değil hello eşlenen sanal ağlar.
    - **İletilen trafiğe izin:** bu kutusunu tooallow iletilen trafik toohello eşlenen sanal ağ (trafiği hello eşlenen sanal ağında kaynaklanan değil) denetleyin tooflow toothis sanal ağ. Trafik yönlendirme ile eşleme yapıyorsanız ve kullanıcı tanımlı yollar tooforward trafiği hello ağ sanal gereç aracılığıyla oluşturulan hello sanal ağ içindeki ağ sanal gerecin dağıttıktan sonra yaygındır. Bu kutu işaretli (varsayılan) bırakırsanız hello eşlenen sanal ağ üzerinden iletilen trafik toothis sanal ağ geçirilemez. Bu özellik etkinleştirme hello eşleme aracılığıyla iletilen hello trafiği sağlar, ancak bunu oluşturmaz tüm kullanıcı tanımlı yollar veya sanal gereçler ağ. Kullanıcı tanımlı yollar ve ağ sanal Gereçleri ayrı olarak oluşturulur. Hakkında bilgi edinin [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md).
    - **Ağ geçidi transit izin ver:** bir sanal ağ geçidi ekli toothis sanal ağ varsa ve istediğiniz tooallow hello trafiğinden eşlenen sanal ağ tooflow hello ağ geçidi üzerinden bu kutuyu işaretleyin. Örneğin, bu sanal ağa ekli tooan şirket içi ağ üzerinden bir sanal ağ geçidi olabilir. Bu kutu hello gelen trafiğe izin verir denetimi hello ağ geçidi ekli toothis sanal ağ üzerinden sanal ağ tooflow eşlenen. Merhaba eşlenen sanal ağ, bu onay kutusunu işaretlerseniz, yapılandırılmış bir ağ geçidi sahip olamaz. Merhaba eşlenen sanal ağ hello olmalıdır **uzak ağ geçidini kullan** onay kutusu işaretli olduğunda gelen hello eşliği yukarı ayarı izin ver hello diğer sanal ağ toothis sanal ağ. Bu kutu işaretli (varsayılan) bırakırsanız hello eşlenen sanal ağ trafiğinden hala toothis sanal ağ akışlar, ancak sanal ağ geçidi ekli toothis aracılığıyla bir sanal ağ geçirilemez. Daha fazla bilgi edinmek [sanal ağ geçitlerini](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    (Resource Manager) bir sanal ağ (Klasik) ile bir sanal ağ eşlemesi varsa bu seçeneği etkinleştirilemiyor. Merhaba trafik hello iki sanal ağ arasında akan olsa hello sanal ağ (Klasik) trafiği bir ağ geçidi ekli toohello aracılığıyla sanal ağ (Resource Manager) geçirilemez.
    - **Uzak ağ geçitleri kullanın:** bu bu sanal ağ tooflow eşliği ile bir sanal ağ geçidi ekli toohello sanal ağ üzerinden gelen kutusu tooallow trafiği denetleyin. Örneğin, hello sanal ağ ile eşliği bağlı bir VPN ağ geçidi tooan şirket içi ağ iletişimi sağlayan sahiptir.  Bu kutuyu işaretleyerek bu sanal ağ tooflow hello VPN ağ geçidi ekli toohello eşlenmiş sanal ağ üzerinden gelen trafiğe izin verir. Bu kutuyu işaretleyin, hello eşlenen sanal ağ bir sanal ağ geçidi bağlı tooit olmalıdır ve hello olmalıdır **ağ geçidi transit izin** onay kutusu işaretli. Bu kutu işaretli (varsayılan) bırakırsanız hello eşlenen sanal ağ trafiğinden hala toothis sanal akabilir ağ, ancak sanal ağ geçidi ekli toothis aracılığıyla bir sanal ağ geçirilemez. 
    
    (Resource Manager) bir sanal ağ (Klasik) ile bir sanal ağ eşlemesi varsa bu seçeneği etkinleştirilemiyor. Merhaba trafik hello iki sanal ağ arasında akan olsa hello (Resource Manager) sanal ağ trafiği bir ağ geçidi ekli toohello aracılığıyla sanal ağ (Klasik) geçirilemez.
7. Merhaba tıklatın **Tamam** seçtiğiniz düğmesi tooadd hello alt toohello sanal ağ.

### <a name="commands"></a>Komutlar

|Aracı|Komut|
|---|---|
|CLI|[az ağ vnet eşlemesi oluşturma](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Ekleme AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Senaryolar

Bir sanal ağ eşlemesi aynı hello oluşturulan sanal ağlar arasında oluşturulur veya aynı ya da farklı Aboneliklerde bulunan farklı dağıtım modellerini hello. Aşağıdaki senaryolar hello biri için adım adım öğretici tamamlayın:
 
|Azure dağıtım modeli  | Abonelik  |
|---------|---------|
|Her ikisi de Resource Manager |[Aynı](virtual-network-create-peering.md)|
| |[Farklı](create-peering-different-subscriptions.md)|
|Biri Resource Manager, diğeri klasik     |[Aynı](create-peering-different-deployment-models.md)|
| |[Farklı](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Eşleme ayarlarını görüntülemek veya değiştirmek

1. İçinde toohello oturum [portal](https://portal.azure.com) hello gerekli atanmış bir hesap ile [rol veya izinleri](#permissions).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *sanal ağlar*. Zaman **sanal ağlar** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **sanal ağlar** görünür, dikey hello sanal ağ için bir eşleme toocreate istediğiniz tıklayın.
4. Seçtiğiniz hello için sanal ağ görüntülenen hello bölmesinde **eşlemeler** hello içinde **ayarları** bölümü.
5. Merhaba eşliği tıklatın tooview istediğiniz veya ayarlarını değiştirin.
6. Merhaba uygun ayarını değiştirin. Her bir ayarın hello seçenekleri hakkında bilgi [adım 6](#add-peering) Merhaba bu makalenin eşleme bir bölüm oluşturun. 

    >[!NOTE]
    >Birkaç gereksinimi, kısıtlamaları vardır ve konuları toosuccessfully oluşturma bir sanal ağ eşlemesi. Bir eşleme oluşturmadan önce familiarized kendiniz ile Merhaba olun [gereksinimleri ve kısıtlamaları](#requirements-and-constraints) ve [gerekli izinleri](#permissions).
    >

7. **Kaydet** düğmesine tıklayın.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ vnet eşleme listesi](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist eşlemeler sanal bir ağ için [az ağ vnet eşleme Göster](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) bir özel eşleme için tooshow ayarları ve [az ağ vnet eşleme güncelleştirmesi](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) toochange eşleme ayarları.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve eşleme ayarlarını görüntüleyin ve [kümesi AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange ayarlar.|

## <a name="delete-a-peering"></a>Bir eşleme Sil
Bir eşleme silindiğinde, bir sanal ağ trafiğinden artık toohello eşlenmiş sanal ağ akar. Resource Manager aracılığıyla dağıtılan sanal ağlar eşlendikleri, her sanal ağ eşleme toohello diğer sanal ağ vardır. Merhaba iletişimi hello sanal ağlar arasındaki bir sanal ağdan Hello eşliği silme devre dışı bırakır, ancak onu hello hello eşliği silmez diğer sanal ağ. Merhaba, eşliği hello var. için eşleme durumu hello diğer sanal ağ **bağlantı kesildi**. Merhaba hello hello ilk sanal ağ eşlemesi, yeniden oluşturmak ve hello eşleme durumunu sanal ağları değişiklikleri çok kadar eşliği yeniden oluşturulamaz*bağlı*. 

Sanal ağlar toocommunicate bazen istiyor, ancak her zaman, bir eşleme silme yerine hello ayarlayabileceğiniz **sanal ağ erişimine izin ver** çok ayarı**devre dışı** yerine. toolearn nasıl okuma hello 6. adım [bir eşlemesi oluşturmak](#create-peering) bu makalenin. Devre dışı bırakma ve ağ erişimi silme ve eşlemeler yeniden daha kolay bulabilirsiniz.

1. İçinde toohello oturum [portal](https://portal.azure.com) hello gerekli atanmış bir hesap ile [rol veya izinleri](#permissions).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *sanal ağlar*. Zaman **sanal ağlar** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **sanal ağlar** görünür, dikey, gelen eşliği toodelete istediğiniz hello sanal ağ'ı tıklatın.
4. Görüntülenen hello dikey penceresinde hello sanal ağın seçtiğiniz tıklayın **eşlemeler** altında **ayarları**.
5. İstediğiniz toodelete hello eşlemeler dikey penceresinde, sizin eşlemeyi sağ hello görünür eşlemeler Hello listesinde tıklayın **silmek**, ardından **Evet** toodelete hello hello ilk sanal ağdan eşleme.
6. Gelen eşliği tam hello önceki adımları toodelete hello hello hello eşlemesi içindeki diğer sanal ağ.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az ağ vnet eşleme Sil](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Gereksinimleri ve kısıtlamaları 

- Merhaba sanal ağlar, eş IP adresi alanları çakışmayan olması gerekir.
- Adres alanlarını eklemek veya başka bir sanal ağ ile sanal ağ eşlendikten sonra sanal ağdan adres alanları silin. tooadd veya kaldırma adres alanları delete hello eşliği, eklemek veya hello adres alanlarını kaldırın ve sonra hello eşliği yeniden oluşturun. tooadd adres alanları için veya sanal ağlardan adres alanlarını kaldırma hello okuma [oluşturma, değiştirme veya silme sanal ağlar](virtual-network-manage-network.md#add-address-spaces) makalesi. 
- Resource Manager veya hello Klasik dağıtım modeli aracılığıyla dağıtılan bir sanal ağ ile Resource Manager aracılığıyla dağıtılan bir sanal ağ üzerinden dağıtılan iki sanal ağ eş. Merhaba Klasik dağıtım modeli aracılığıyla oluşturulan iki sanal ağ eş olamaz. Azure dağıtım modelleri bilmiyorsanız hello okuma [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi. Kullanabileceğiniz bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect iki sanal ağlar hello Klasik dağıtım modeli oluşturuldu.
- Resource Manager aracılığıyla oluşturulan iki sanal ağ eşlemesi, bir eşleme hello eşlemesindeki her sanal ağ için yapılandırılmış olması gerekir. Merhaba ilk sanal ağdan hello eşleme toohello ikinci sanal ağ oluşturduğunuzda, hello eşleme durumudur *başlatılan*.  Merhaba hello ikinci sanal ağ toohello ilk sanal ağdan eşliği oluşturduğunuzda, eşleme durumundadır *bağlı*. Merhaba hello ilk sanal ağ eşleme durumunu görüntüleyin, değiştirildi durumu bakın *başlatılan* çok*bağlı*. Merhaba eşliği değil başarıyla kuruldu hello eşleme durumu için her iki sanal ağ eşlemesi bulunabilir kadar *bağlı*. 
- Resource Manager aracılığıyla hello Klasik dağıtım modeliyle oluşturulan bir sanal ağ ile oluşturulan bir sanal ağ eşlemesi olduğunda, yalnızca bir Resource Manager aracılığıyla dağıtılan hello sanal ağ eşlemesini yapılandırın. Bir sanal ağ (Klasik) veya hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağlar arasında eşleme yapılandıramazsınız. Merhaba hello sanal ağ (Resource Manager) toohello sanal ağdan (Klasik) eşliği oluşturduğunuzda, hello eşleme durumudur *güncelleştirme*, ardından kısa süre içinde çok değiştirir*bağlı*.   
- Bir eşleme iki sanal ağ arasında oluşturulur. Eşlemeler geçişli değildir. Arasındaki eşlemeler oluşturursanız:
    - VirtualNetwork1 & VirtualNetwork2
    - VirtualNetwork2 & VirtualNetwork3

  Hiçbir VirtualNetwork1 ve VirtualNetwork3 VirtualNetwork2 aracılığıyla arasında eşleme yoktur. Bir sanal ağ VirtualNetwork1 ve VirtualNetwork3 arasında eşleme toocreate istiyorsanız bir VirtualNetwork1 ve VirtualNetwork3 arasında eşleme toocreate gerekir.
- Varsayılan Azure ad çözümlemesi kullanarak eşlenen sanal ağları adlarında çözümlenemiyor. diğer sanal ağlar adlarında tooresolve, özel bir DNS sunucusu kullanmanız gerekir. kendi DNS sunucusu tooset nasıl okuma toolearn hello [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) makalesi.
- Merhaba eşlemesindeki her iki sanal ağ kaynaklarında iletişim kurabilir birbirleri ile Merhaba ile aynı bant genişliği ve gecikme süresi içinde oldukları gibi hello aynı sanal ağ. Her sanal makine boyutu ancak kendi maksimum ağ bant genişliği vardır. başka bir sanal makine boyutları, hello okumak için maksimum ağ bant genişliği hakkında daha fazla toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine boyutları makaleleri.
- İçinde aynı hello olan Resource Manager aracılığıyla dağıtılan sanal ağlar eş ya da farklı Aboneliklerde.
- İçinde aynı hello olan farklı dağıtım modelleri arasında dağıtılmış sanal ağları eş ya da farklı Aboneliklerde (Önizleme). 
- Merhaba her iki sanal ağlar aboneliklerin ilişkili toohello olmalıdır aynı Azure Active Directory kiracısı. Bir AD kiracısıyla zaten sahip değilseniz, hızlı bir şekilde yapabilecekleriniz [oluşturmak](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Kullanabileceğiniz bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) farklı Aboneliklerde mevcut tooconnect iki sanal ağlar toodifferent Active Directory kiracıları ilişkilendirilmiş.
- Bir sanal ağ eşlenmiş tooanother sanal ağı ve bağlı tooanother sanal ağ bir Azure sanal ağ geçidi ile de. Sanal ağlar eşliği ve ağ geçidi bağlandığında hello sanal ağlar arasında trafiği hello ağ geçidi yerine hello eşleme yapılandırmasını akar.
- Sanal ağ eşlemesi kullanan girdi ve çıktı trafiği için nominal bir ücret uygulanır. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>İzinler

bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir. Örneğin, myVnetA ve myVnetB adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:
    
|Sanal ağ|Dağıtım modeli|Rol|İzinler|
|---|---|---|---|
|myVnetA|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Yok|
|myVnetB|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl toocreate bir [hub ve bağlı bileşen ağ topolojisi](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
