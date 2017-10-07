---
title: "aaaCreate bir Azure sanal ağ eşleme - farklı dağıtım modellerini - aynı abonelik | Microsoft Docs"
description: "Nasıl hello aynı mevcut farklı Azure dağıtım modelleri arasında bir sanal ağ sanal ağlar arasında eşlemeyi toocreate oluşturulacağını öğrenin Azure aboneliği."
services: virtual-network
documentationcenter: 
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
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Sanal Ağ eşlemesi bir - farklı oluşturmak dağıtım modelleri, aynı abonelik 

Bu öğreticide, bir sanal ağ farklı dağıtım modeli oluşturulan sanal ağlar arasında eşleme toocreate öğrenin. Her iki sanal ağlar hello aynı mevcut abonelik. Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ. Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md). 

Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla. Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:

|Azure dağıtım modeli  | Azure aboneliği  |
|--------- |---------|
|[Her iki kaynak yöneticisi](virtual-network-create-peering.md) |Aynı|
|[Her iki kaynak yöneticisi](create-peering-different-subscriptions.md) |Farklı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models-subscriptions.md) |Farklı|

Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor. Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi. Her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlar tooconnect gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar. 

Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) veya Azure [PowerShell](#powershell) toocreate bir sanal ağ eşlemesi. Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.

## <a name="cli"></a>Eşlemesi - oluşturmak portalı

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
2. Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.
3. Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:
    - **Ad**: *myVnet1*
    - **Adres alanı**: *10.0.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.0.0.0/24*
    - **Abonelik**: aboneliğinizi seçin
    - **Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroup*
    - **Konum**: *Doğu ABD*
4. Tıklatın **+ yeni**. Merhaba, **arama hello Market** kutusuna *sanal ağ*. Tıklatın **sanal ağ** hello arama sonuçlarında görüntülendiğinde. 
5. Merhaba, **sanal ağ** dikey penceresinde, select **Klasik** hello içinde **dağıtım modeli seçin** kutusuna ve ardından **oluşturma**.
6. Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:
    - **Ad**: *myVnet2*
    - **Adres alanı**: *10.1.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.1.0.0/24*
    - **Abonelik**: aboneliğinizi seçin
    - **Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*
    - **Konum**: *Doğu ABD*
7. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myResourceGroup*. Tıklatın **myResourceGroup** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myresourcegroup** kaynak grubu. Merhaba kaynak grubu, önceki adımlarda oluşturduğunuz hello iki sanal ağ içeriyor.
8. Tıklatın **myVNet1**.
9. Merhaba, **myVnet1** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.
10. Merhaba, **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**
11. Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:
     - **Ad**: *myVnet1ToMyVnet2*
     - **Sanal ağ dağıtım modeli**: seçin **Klasik**. 
     - **Abonelik**: aboneliğinizi seçin
     - **Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.
     - **Sanal ağ erişimine izin ver:** emin **etkin** seçilir.
    Diğer bir ayarları, bu öğreticide kullanılır. Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).
12. ' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden. Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir. **Bağlı** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu.

    Merhaba eşliği şimdi oluşturulur. Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
14. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.

## <a name="cli"></a>Eşlemesi - oluşturmak Azure CLI

1. [Yükleme](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello sanal ağ (Klasik).
2. Bir komut oturumu açın ve içinde tooAzure hello kullanarak oturum `azure login` komutu.
3. Merhaba girerek Hello CLI Hizmet Yönetimi modunda çalışacak `azure config mode asm` komutu.
4. Toocreate hello sanal ağ (Klasik) komutu aşağıdaki hello girin:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun. Merhaba CLI 1.0 veya 2.0 kullanabilirsiniz ([yükleme](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). Kullanılan toocreate hello eşliği 2.0 olması gerektiğinden bu öğreticide, hello CLI 2.0 kullanılan toocreate hello sanal (Resource Manager) ağdır. Aşağıdaki yerel makinenize hello CLI 2.0.4 ile CLI betikten bash veya sonraki bir sürümü yüklü hello yürütün. Windows istemcisi üzerinde CLI betikleri çalıştırma seçenekleri bash için bkz: [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba betik hello Azure bulut Kabuğu'nu kullanarak da çalıştırabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. Merhaba tıklatın **deneyin** Azure hesabı düğmesini hello betikteki, oturumu bir bulut Kabuk çağırır aşağıdaki tooyour oturum açabilir. tooexecute Merhaba komut dosyası, hello tıklatın **kopya** düğmesi ve yapıştırma, bulut Kabuğunuzu Merhaba içeriğine tuşuna `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Merhaba farklı dağıtım modelleri arasında oluşturulan hello iki sanal ağlar arasında eşleme sanal ağ oluşturun. Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<subscription id>` aboneliğinizle kimliği. Merhaba, abonelik kimliği bilmiyorsanız, girin `az account show` komutu. Merhaba değeri **kimliği** hello çıktı, abonelik kimliği değil. Tooyour CLI oturumunda değiştiren hello betik yapıştırın ve tuşuna `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Merhaba betik yürütüldükten sonra hello sanal ağ (Resource Manager) hello eşlemesi gözden geçirin. Kopyalama hello aşağıdaki komutu, CLI oturumunuzda yapıştırın ve tuşuna `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Merhaba çıktısını gösterir **bağlı** hello içinde **PeeringState** sütun. 

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
9. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.

## <a name="powershell"></a>Eşlemesi - oluşturmak PowerShell

1. Merhaba PowerShell Hello en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) ve [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modüller. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumu başlatın.
3. PowerShell'de tooAzure içinde hello girerek oturum `Add-AzureAccount` komutu.
4. bir sanal ağ (Klasik) PowerShell ile toocreate, yeni bir, veya var olan değiştirmeniz gerekir ağ yapılandırma dosyası. Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md). Merhaba dosya hello aşağıdakileri içermelidir **VirtualNetworkSite** öğesi Bu öğreticide kullanılan hello sanal ağ için:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir. Yalnızca hello önceki sanal ağ ekleme ve yok değiştirdiğinizde veya var olan tüm sanal ağları aboneliğinizden kaldırma emin olun. 
5. Merhaba girerek tooAzure toocreate hello sanal ağında (Resource Manager) oturum `login-azurermaccount` komutu. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
6. Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun. Merhaba betiği kopyalayın, PowerShell içinde yapıştırın ve ardından basın `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Merhaba farklı dağıtım modelleri arasında oluşturulan hello iki sanal ağlar arasında eşleme sanal ağ oluşturun. Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<subscription id>` aboneliğinizle kimliği. Merhaba, abonelik kimliği bilmiyorsanız, girin `Get-AzureRmSubscription` komutu tooview onu. Merhaba değeri **kimliği** hello çıkış abonelik kimliğinizi döndürülür tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyasından metin düzenleyici, PowerShell oturumunuzda sağ tıklayın ve sonra basın `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Merhaba betik yürütüldükten sonra hello sanal ağ (Resource Manager) hello eşlemesi gözden geçirin. Kopyalama hello aşağıdaki komut, PowerShell oturumunuzda yapıştırın ve tuşuna `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Merhaba çıktısını gösterir **bağlı** hello içinde **PeeringState** sütun.

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
10. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.
 
## <a name="permissions"></a>İzinleri

bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir. Örneğin, myVnet1 ve myVnet2 adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:
    
|Sanal ağ|Dağıtım modeli|Rol|İzinler|
|---|---|---|---|
|myVnet1|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Yok|
|myVnet2|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).

## <a name="delete"></a>Kaynakları silin
Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz. Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.

### <a name="delete-portal"></a>Azure portalı

1. Merhaba portal arama kutusuna **myResourceGroup**. Merhaba arama sonuçlarında tıklatın **myResourceGroup**.
2. Merhaba üzerinde **myResourceGroup** dikey penceresinde hello tıklatın **silmek** simgesi.
3. Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.

### <a name="delete-cli"></a>Azure CLI

1. Hello Azure CLI 2.0 toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello ile kullanın:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Hello Azure CLI 1.0 toodelete hello sanal ağ (Klasik) ile Merhaba aşağıdaki komutları kullanın:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello girin:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello sanal ağ (Klasik) PowerShell ile varolan bir ağ yapılandırma dosyasını değiştirmeniz gerekir. Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md). Bu öğreticide kullanılan hello sanal ağ için VirtualNetworkSite öğesi aşağıdaki hello kaldırın:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir. Yalnızca hello önceki sanal ağı kaldırmak ve yok değiştirdiğinizde veya diğer varolan sanal ağlara aboneliğinizden kaldırma emin olun. 

## <a name="next-steps"></a>Sonraki adımlar

- Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.
- Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).
- Nasıl çok öğrenin[bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.
