---
title: "aaaAdd ağ arabirimleri tooor Azure sanal makinelerden kaldırmak | Microsoft Docs"
description: "Tooadd ağ arabirimleri tooor kaldırma ağ arabirimleri sanal makinelerden öğrenin."
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Ağ arabirimleri tooor sanal makinelerden kaldırmak ekleme

Varolan bir ağ VM oluşturulurken arabirim eklemek veya hello var olan bir VM'de ağ arabirimleri kaldırma tooadd (serbest bırakıldığında) durumu nasıl durduruldu öğrenin. Bir ağ arabirimi, Internet, Azure ve şirket içi kaynakları ile bir Azure sanal makine (VM) toocommunicate sağlar. Bir VM, bir veya daha fazla ağ arabirimine sahip olabilir. 

Tooadd gerekiyorsa, değiştirin ya da bir ağ arabirimi için IP adreslerini kaldırın okuma hello [ağ arabirimi IP adreslerini yönetmek](virtual-network-network-interface-addresses.md) makalesi. Toocreate gerekiyorsa, değiştirme veya ağ arabirimleri silme okuma hello [ağ arabirimlerini yönetme](virtual-network-network-interface.md) makalesi.

## <a name="before"></a>Başlamadan önce

Görevler herhangi tamamlamadan önce aşağıdaki tam hello herhangi bir bölümünü bu makalede adımlar:

- Kaç tane ağ arabirimleri hakkındaki hello gözden geçirerek her Linux ve Windows VM boyutu destekler öğrenin [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri.
- Toohello Azure oturum [portal](https://portal.azure.com), Azure komut satırı arabirimi (CLI) ya da Azure PowerShell ile bir Azure hesabı. Zaten bir Azure hesabınız yoksa, kaydolun bir [ücretsiz deneme sürümü hesabı](https://azure.microsoft.com/free).
- Bu makalede, toocomplete görevleri komutları PowerShell kullanarak, [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Hello en son sürümünü hello Azure PowerShell cmdlet'leri yüklü olduğundan emin olun. tooget Yardım için örneklerle PowerShell komutlarını yazın `get-help <command> -full`.
- Bu makalede, toocomplete görevleri komutları Azure komut satırı arabirimi (CLI) kullanarak, [hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuğu'nu tıklatın hello bulut Kabuk **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com).

## <a name="about"></a>Ağ arabirimleri ve sanal makineleri hakkında

Ekleyebileceğiniz (Ekle) var olan bir ağ arabirimi tooa hello ağ arabirimi şu anda sağlandığında hello VM oluşturduğunuzda VM tooanother VM bağlı. Bir ağ arabirimi ekleme veya kaldırma (detach) bir ağ arabiriminin toofrom mevcut bir VM'yi hello VM hello (serbest bırakıldığında) durumu durduruldu sağlanan. Hello Azure portal kullanarak bir VM'i oluşturursanız, hello portalı bir ağ arabirimi sizin için varsayılan ayarlarla oluşturur. Merhaba portal için izin vermez:

- Varolan bir ağ arabirimi tooadd hello VM oluştururken belirtin
- Birden çok ağ arabirimi ile VM oluşturma
- Merhaba ağ arabirimi için bir ad belirtin (Merhaba portal oluşturur hello ağ arabirimi bir varsayılan ad ile)

Merhaba portalı kullanamazsınız tüm hello önceki özniteliklere sahip Azure PowerShell veya hello CLI toocreate bir ağ arabirimi ya da VM kullanabilirsiniz. Aşağıdaki bölümlerde hello Hello görevleri tamamlamadan önce hello aşağıdakileri göz önünde bulundurun kısıtlamaları ve davranışları:

- Tüm VM boyutları en az iki ağ arabirimi destekler ancak ikiden fazla ağ arabirimleri bazı VM boyutlarını destekler. Merhaba geçmiş, bazı VM boyutları yalnızca bir ağ arabirimi desteklenir. toolearn her VM boyutu destekliyorsa, kaç tane ağ arabirimleri okuma hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri. 
- Geçmiş Hello içinde ağ arabirimleri yalnızca desteklenen birden çok ağ arabirimleri ve en az iki ağ arabirimi ile oluşturulan eklenen tooVMs olabilir. Birden çok ağ arabirimi Hello VM boyutu desteklenen olsa bile bir ağ arabirimi tooa bir ağ arabirimi ile oluşturulan VM eklenemedi. Buna karşılık, bir VM'den en az üç ağ arabirimlerine sahip ağ arabirimleri yalnızca kaldırabilirsiniz, her zaman en az iki ağ arabirimi ile oluşturulan VM'ler toohave sahip olduğunuz için en az iki ağ arabirimleri. Bu kısıtlamaların hiçbiri artık geçerli. Şimdi ağ arabirimlerinin (yukarı toohello numarası hello VM boyutu tarafından desteklenen) herhangi bir sayı ile bir VM oluşturun ve da ekleyebilir veya hello VM her zaman en az bir ağ arabirimine sahip olduğu sürece herhangi bir sayıda ağ arabirimlerinden (Merhaba durduruldu (serbest bırakıldı) Vm'lerde durumu), kaldırabilirsiniz.
- Varsayılan olarak, hello ilk ağ arabirimi bir VM'de hello tanımlanan *birincil* ağ arabirimi. Merhaba VM diğer tüm ağ arabirimlerini olan *ikincil* ağ arabirimleri.
- Birincil ağ arabirimine bir varsayılan ağ geçidi hello Azure DHCP sunucuları tarafından atanmış, ancak ikincil ağ arabirimlerine değildir. İkincil ağ arabirimlerine bir varsayılan ağ geçidi atanmamış olduğundan, bunlar kendi alt dışında kaynaklarla varsayılan olarak iletişim kuramıyor. bir Windows VM toocommunicate kendi alt ağı dışından kaynaklarla tooenable ikincil ağ arabirimi ekleyin hello kullanarak yolları toohello işletim sistemi `route add` bir Windows komut satırından komutu. Merhaba varsayılan davranışı yönlendirme, zayıf konak kullandığından Linux VM'ler için ikincil ağ arabirimleri tooa tek alt ağ trafiği kısıtlama öneririz. İçin ikincil ağ arabirimleri, etkinleştirme ilke tabanlı, giriş tooensure yönlendirme hello alt dışında bağlantı gerektirir ve çıkış trafiği hello kullanıyorsa aynı arabirimi ağ.
- Varsayılan olarak, tüm giden trafiği VM hello IP adresini gönderilen hello toohello hello birincil ağ arabirimi birincil IP yapılandırmasının atanır. Hangi IP adresi hello VM'ın işletim sistemi içinde giden trafik için kullanılan denetim ancak isteğe bağlı olarak varsayılan olarak hello birincil ağ arabirimi üzerinden yapılır.
- Merhaba geçmiş hello içindeki tüm sanal makineleri aynı kullanılabilirlik kümesinde bulunduğunuz tek veya birden çok ağ arabirimleri gerekli toohave. Ağ arabirimleri şimdi bulunabilir herhangi bir sayıda olan VM'ler hello VM boyutu tarafından desteklenen toohello numarasını aynı kullanılabilirlik kümesinde hello. Yalnızca bir VM tooan kullanılabilirlik ancak oluşturulduğunda kümesi ekleyebilirsiniz. Kullanılabilirlik kümeleri, hello okuma hakkında daha fazla toolearn [VM'ler için Azure'da hello kullanılabilirliğini yönetme](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) makale.
- İçinde ağ arabirimleri sırada hello aynı VM bir sanal ağ içindeki alt ağlara bağlı toodifferent olabilir, hello ağ arabirimleri tüm olmalıdır bağlı toohello aynı sanal ağı.
- Herhangi bir birincil veya ikincil ağ arabirimi tooan Azure yük dengeleyici arka uç havuzu IP yapılandırması için herhangi bir IP adresi ekleyebilirsiniz. Hello geçmiş, yalnızca hello birincil IP adresi için hello birincil ağ arabirimi tooa arka uç havuzu eklenemedi. IP adresleri ve hello okuma yapılandırmaları hakkında daha fazla toolearn [Ekle, Değiştir veya Kaldır IP adresleri](virtual-network-network-interface-addresses.md) makalesi.
- Bir VM silme ekli tooit olan hello ağ arabirimleri silmez. Bir VM silindiğinde, hello ağ arabirimleri VM hello ayrılır. Merhaba ağ arabirimleri toodifferent sanal makineleri ekleyin veya silin.
- Bir ağ arabirimi özel bir IPv6 adresi atanmış tooit varsa, hello VM oluştururken, onu tooa VM ekleyebilirsiniz. Merhaba VM oluşturulduktan sonra bir ağ arabirimine atanmış bir IPv6 adresi tooa VM ile eklenemiyor. Bir sanal makine oluşturulurken özel bir IPv6 adresi atanmış bir ağ arabirimiyle eklerseniz, bu ağ arabirimi toohello sanal makine, kaç tane ağ arabirimleri hello VM boyutu destekler ne olursa olsun yalnızca ekleyebilirsiniz. Bkz: [ağ arabirimi IP adresleri](virtual-network-network-interface-addresses.md) IP atama hakkında daha fazla toolearn toonetwork arabirimleri giderir.

## <a name="vm-create"></a>Mevcut ağ arabirimleri tooa ekleme yeni VM

Bir VM hello portal üzerinden oluşturduğunuzda, hello portalı varsayılan ayarlarla bir ağ arabirimi oluşturur ve toohello VM sizin için ekler. Mevcut ağ arabirimleri tooa ekleyemezsiniz yeni VM veya birden çok ağ arabirimleri hello Azure portal kullanarak bir VM oluşturun. Her ikisini birden yapın CLI veya PowerShell hello kullanarak. VM boyutu destekler oluşturmakta olduğunuz hello birçok arabirimleri tooa VM ağ olarak ekleyebilirsiniz. kaç tane ağ hakkında daha fazla toolearn arabirimleri hello okuma her VM boyutu destekler [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri. Merhaba ağ arabirimleri tooa VM eklediğiniz şu anda ekli tooanother VM olamaz. Ağ arabirimleri, hello okuma oluşturma hakkında daha fazla toolearn [ağ arabirimlerini yönetme](virtual-network-network-interface.md#create-a-network-interface) makale.

> [!WARNING]
> Bir ağ arabirimi tooit atanan özel bir IPv6 adresi varsa, hello sanal makine oluştururken yalnızca hello ağ arabirimi toohello sanal makine ekleyebilirsiniz. Bir IPv6 adresi tooa ağ arabirimi bağlı tooa sanal makineye atanan sürece hello sanal makine oluşturduğunuzda ya da hello sonra sanal makine oluşturulur mu, birden fazla ağ arabirimi toohello sanal makine eklenemez. Bkz: [ağ arabirimi IP adresleri](virtual-network-network-interface-addresses.md) IP atama hakkında daha fazla toolearn toonetwork arabirimleri giderir.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az vm oluşturma](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>VM var olan bir ağ arabirimi tooan Ekle

Birçok ağ arabirimleri toosupports eklediğiniz VM boyutu hello arabirimleri tooa VM ağ olarak ekleyebilirsiniz. toolearn her VM boyutu destekliyorsa, kaç tane ağ arabirimleri okuma hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri. Merhaba tooadd bir ağ arabirimi toomust hello tooadd istediğiniz ve durdurulmuş hello olmalıdır ağ arabirimlerinin sayısını desteklemek istediğiniz VM (durumu Serbest). Merhaba ağ arabirimleri tooadd istediğiniz şu anda ekli tooanother VM olamaz. Ağ arabirimleri tooan hello Azure portal kullanarak VM varolan ekleyemezsiniz. VM varolan tooan tooadd ağ arabirimleri, hello CLI veya PowerShell kullanmanız gerekir. 

> [!WARNING]
> Bir ağ arabirimi tooit atanan özel bir IPv6 adresi varsa, tooan varolan sanal makine eklenemez. Bir sanal makine oluşturduğunuzda, yalnızca bir ağ arabirimi bir atanan özel IPv6 adresi tooa sanal makineyle ekleyebilirsiniz. Bkz: [ağ arabirimi IP adresleri](virtual-network-network-interface-addresses.md) IP atama hakkında daha fazla toolearn toonetwork arabirimleri giderir.

|Aracı|Komut|
|---|---|
|CLI|[az vm NIC eklemeniz](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (başvuru) veya [ayrıntılı adımları](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (başvuru) veya [ayrıntılı adımları](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>Bir VM için görünümü ağ arabirimleri

Tooeach ağ arabirimine atanmış hello IP adresleri ve hello ağ arabirimleri şu anda ekli tooa VM toolearn her ağ arabiriminin yapılandırması hakkında görüntüleyebilir. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) aboneliğiniz için hello sahibi, katkıda bulunan veya ağ Katılımcısı rolüne atanmış bir hesap ile. rolleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *sanal makineleri*. Zaman **sanal makineleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **sanal makineleri** görünür, dikey hello tooview ağ arabirimleri için istediğiniz VM hello adını tıklayın.
4. Merhaba, **ayarları** görünen hello sanal makine için dikey hello Seçtiğiniz VM bölümüne tıklatın **ağ arabirimleri**. toolearn ağ arabirimi ayarları hakkında ve nasıl toochange bunları, okuma hello [ağ arabirimlerini yönetme](virtual-network-network-interface.md) makalesi. değiştirerek veya kaldırarak tooa ağ arabirimi, atanan IP adresleri ekleme hakkında toolearn bkz [yönetmek IP adresleri](virtual-network-network-interface-addresses.md).

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az vm Göster](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>Bir ağ arabirimi bir sanal makineden kaldırın

Merhaba tooremove istediğiniz (veya detach) bir ağ arabiriminden VM durduruldu (serbest bırakıldığında) durumu hello ve en az iki ağ arabirimleri tooit şu anda ekli gerekir olması gerekir. Herhangi bir ağ arabirimi kaldırabilirsiniz, ancak hello VM her zaman en az bir ağ arabirimi bağlı tooit olması gerekir. Birincil Ağ arabirimi kaldırırsanız, Azure ekli toohello VM hello uzun bırakıldı hello birincil öznitelik toohello ağ arabirimi atar. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) aboneliğiniz için hello sahibi, katkıda bulunan veya ağ Katılımcısı rolüne atanmış bir hesap ile. rolleri tooaccounts atama hakkında daha fazla toolearn bkz [Azure rol tabanlı erişim denetimi için yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *sanal makineleri*. Zaman **sanal makineleri** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **sanal makineleri** görünür, dikey hello bir ağ arabirimi için tooremove istediğiniz VM hello adını tıklayın.
4. Merhaba, **ayarları** görünen hello sanal makine için dikey hello Seçtiğiniz VM bölümüne tıklatın **ağ arabirimleri**. toolearn ağ arabirimi ayarları hakkında ve nasıl toochange bunları, okuma hello [ağ arabirimlerini yönetme](virtual-network-network-interface.md) makalesi. değiştirerek veya kaldırarak tooa ağ arabirimi, atanan IP adresleri ekleme hakkında toolearn bkz [yönetmek IP adresleri](virtual-network-network-interface-addresses.md).
5. Görüntülenen hello ağ arabirimleri dikey penceresinde hello tıklayın **...**  toohello sağ hello ağ arabiriminin toodetach istiyor.
6. Tıklatın **Detach**. Yalnızca bir ağ arabirimi bağlı toohello sanal makine varsa, hello **ayırma** seçeneği kullanılamaz. Tıklatın **Evet** görünür hello onay kutusunda.

**Komutları**

|Aracı|Komut|
|---|---|
|CLI|[az vm NIC kaldırmak](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (başvuru) veya [ayrıntılı adımları](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (başvuru) veya [ayrıntılı adımları](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Sonraki adımlar
toocreate birden çok ağ arabirimlerine sahip bir VM veya IP adresleri, makaleler hello okuyun:

**Komutları**

|Görev|Aracı|
|---|---|
|Birden çok NIC ile VM oluşturma|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Birden çok IPv4 adresleriyle tek bir NIC VM oluşturma|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Özel bir IPv6 adresi (arkasında bir Azure yük dengeleyici) ile tek bir NIC VM oluşturma|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager şablonu](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
