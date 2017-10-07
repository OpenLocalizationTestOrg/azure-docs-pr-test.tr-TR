---
title: "bir Azure sanal ağ (Klasik) birden fazla alt ağı aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir sanal ağ (Klasik) Azure içinde birden fazla alt ağı."
services: virtual-network
documentationcenter: 
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
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Bir sanal ağ ile birden fazla alt ağ (Klasik) oluşturun

> [!IMPORTANT]
> Azure sahip iki [farklı dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) oluşturmak ve kaynaklarla çalışmak için: Resource Manager ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft önerir hello üzerinden çoğu yeni sanal ağlar oluşturma [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) dağıtım modeli.

Bu öğreticide, nasıl toocreate olan bir temel Azure sanal ağ (Klasik) ayrı ortak ve özel alt ağlar hakkında bilgi edinin. Sanal makineler ve bir alt ağdaki bulut Hizmetleri gibi Azure kaynaklarını oluşturabilirsiniz. Sanal ağları (Klasik) oluşturulan kaynakları birbirleriyle ve diğer ağ bağlantılı tooa sanal ağınızdaki kaynaklara ile iletişim kurabilir.

Tüm hakkında daha fazla bilgi [sanal ağ](virtual-network-manage-network.md) ve [alt](virtual-network-manage-subnet.md) ayarlar.

> [!WARNING]
> Sanal ağları (Klasik), Azure tarafından hemen silinir, bir [abonelik devre dışı](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Sanal ağları (Klasik) kaynakları hello sanal ağında mevcut bağımsız olarak silinir. Daha sonra hello aboneliği yeniden etkinleştirirseniz, hello sanal ağında varolan kaynakları yeniden oluşturulmalıdır.

Hello kullanarak bir sanal ağ (Klasik) oluşturabilirsiniz [Azure portal](#portal), hello [Azure komut satırı arabirimi (CLI) 1.0](#azure-cli), veya [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. Bir Internet tarayıcısında toohello Git [Azure portal](https://portal.azure.com). Kullanarak oturum açın, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Tıklatın **+ yeni** hello Portalı'nda.
3. Girin *sanal ağ* hello içinde **arama hello Market** kutusunu hello hello üstündeki **yeni** görünür dikey.  Tıklatın **sanal ağ** hello arama sonuçlarında görüntülendiğinde.
4. Seçin **Klasik** hello içinde **dağıtım modeli seçin** hello kutusunda **sanal ağ** görünür, ardından dikey **oluşturma**. 
5. Değerler üzerinde hello aşağıdaki hello girin **sanal ağ oluştur (Klasik)** dikey ve ardından **oluşturma**:

    |Ayar|Değer|
    |---|---|
    |Ad|myVnet|
    |Adres alanı|10.0.0.0/16|
    |Alt ağ adı|Genel|
    |Alt ağ adres aralığı|10.0.0.0/24|
    |Kaynak grubu|Bırakın **Yeni Oluştur** seçili yazıp enter **myResourceGroup**.|
    |Abonelik ve konum|Abonelik ve konum seçin.

    Yeni tooAzure değilseniz, hakkında daha fazla bilgi [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (tooas ya da *bölgeleri*).
4. Bir sanal ağ oluşturduğunuzda, hello Portalı'nda, yalnızca bir alt ağ oluşturabilirsiniz. Merhaba sanal ağ oluşturduktan sonra Bu öğreticide, ikinci bir alt ağ oluşturun. Daha sonra Internet'ten erişilebilen kaynaklara hello oluşturacağınız **ortak** alt ağ. Merhaba hello Internet üzerinden erişilebilir olmayan kaynakları de oluşturabilir **özel** alt ağ. toocreate ikinci alt ağ Merhaba, girin **myVnet** hello içinde **arama kaynakları** hello sayfanın üst kısmındaki hello kutusu. Tıklatın **myVnet** hello arama sonuçlarında görüntülendiğinde.
5. Tıklatın **alt ağlar** (Merhaba içinde **ayarları** bölüm) hello üzerinde **sanal ağ oluştur (Klasik)** görünür dikey.
6. Tıklatın **+ Ekle** hello üzerinde **myVnet - alt ağlar** görünür dikey.
7. Girin **özel** için **adı** hello üzerinde **alt ağ Ekle** dikey. Girin **10.0.1.0/24** için **adres aralığı**.  **Tamam** düğmesine tıklayın.
8. Merhaba üzerinde **myVnet - alt ağlar** dikey penceresinde hello görebilirsiniz **ortak** ve **özel** oluşturduğunuz alt ağlar.
9. **İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi yok, oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz:
    - Tıklatın **genel bakış** hello üzerinde **myVnet** dikey.
    - Merhaba tıklatın **silmek** hello simgesine **myVnet** dikey.
    - tooconfirm hello silme tıklatın **Evet** hello içinde **Delete sanal ağ** kutusu.

## <a name="azure-cli"></a>Azure CLI

1. Seçebilir ya da [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), veya hello Azure bulut Kabuk içinde hello CLI kullanın. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. CLI komutları için tooget Yardım yazın `azure <command> --help`. 
2. CLI oturumunda, aşağıdaki hello komutuyla tooAzure kaydedilir. Tıklatırsanız **deneyin** hello kutuya bir bulut Kabuğu'nu açar. Komutu aşağıdaki hello girmeden tooyour Azure aboneliği kaydedebilirsiniz:

    ```azurecli-interactive
    azure login
    ```

3. CLI Hizmet Yönetimi modundaysa tooensure hello hello aşağıdaki komutu girin:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Bir sanal ağ ile özel bir alt ağ oluşturun:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Ortak bir alt ağ içinde hello sanal ağ oluşturun:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Merhaba sanal ağ ve alt ağları gözden geçirin:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Hello CLI kullanarak bir kaynak grubu toocreate bir sanal ağ (Klasik) belirtemezsiniz olsa, Azure hello sanal ağ içinde adlı bir kaynak grubu oluşturur. *varsayılan ağ*.

## <a name="powershell"></a>PowerShell

1. Merhaba PowerShell Hello en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumu başlatın.
3. PowerShell'de tooAzure içinde hello girerek oturum `Add-AzureAccount` komutu.
4. Değiştirme hello şu yol ve dosya adı, uygun şekilde sonra varolan ağ yapılandırma dosyanızı aktarın:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate ortak ve özel alt ağları, sanal ağ kullanan herhangi bir metin düzenleyicisi tooadd hello **VirtualNetworkSite** toohello ağ yapılandırma dosyası izleyen öğesi.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Gözden geçirme hello tam [ağ yapılandırma dosyası şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Merhaba ağ yapılandırma dosyasını içeri aktarın:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir. Yalnızca hello önceki sanal ağ ekleme ve yok değiştirdiğinizde veya var olan tüm sanal ağları aboneliğinizden kaldırma emin olun. 

7. Merhaba sanal ağ ve alt ağları gözden geçirin:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz. toodelete hello sanal ağ, tam adımlar 4-6 yeniden, bu zaman kaldırma hello **VirtualNetworkSite** 5. adımda eklediğiniz öğesi.
 
> [!NOTE]
> Azure PowerShell kullanarak bir kaynak grubu toocreate bir sanal ağ (Klasik) belirtemezsiniz olsa adlı bir kaynak grubunda hello sanal ağ oluşturur *varsayılan ağ*.

---

## <a name="next-steps"></a>Sonraki adımlar

- tüm sanal ağ ve alt ağ ayarları hakkında toolearn bkz [sanal ağlarını yönetmeleri](virtual-network-manage-network.md) ve [sanal ağ alt ağlarını yönetin](virtual-network-manage-subnet.md). Sanal ağlar ve alt ağlar, bir üretim ortamında toomeet farklı gereksinimleri kullanmaya yönelik çeşitli seçenekleriniz vardır.
- gelen ve giden toofilter alt ağ trafiği, oluşturma ve uygulama [ağ güvenlik grubu](virtual-networks-nsg.md) toosubnets.
- Oluşturma bir [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine ve tooan varolan sanal ağa bağlayın.
- tooconnect iki sanal ağlar olarak Merhaba aynı Azure konumunda, oluşturma bir [sanal ağ eşlemesi](create-peering-different-deployment-models.md) hello sanal ağlar arasında. Bir sanal ağ (Resource Manager) tooa sanal ağ (Klasik) eşi, ancak iki sanal ağ (Klasik) arasında eşleme oluşturamazsınız.
- Kullanarak Hello sanal ağ tooan şirket ağına bağlanan bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hattı.
