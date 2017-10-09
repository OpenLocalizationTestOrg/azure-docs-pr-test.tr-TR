---
title: "Azure sanal ağ eşlemesi bir - aaaCreate Resource Manager - aynı abonelik | Microsoft Docs"
description: "Nasıl Resource Manager aracılığıyla aynı hello mevcut bir sanal ağ sanal ağlar arasında eşlemeyi toocreate oluşturulacağını öğrenin Azure aboneliği."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Bir sanal ağ eşlemesi - oluşturmak Resource Manager, aynı abonelik

Bu öğreticide, bir sanal ağ Resource Manager aracılığıyla oluşturulan sanal ağlar arasında eşleme toocreate öğrenin. Her iki sanal ağlar hello aynı mevcut abonelik. Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ. Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md). 

Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla. Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:

|Azure dağıtım modeli  | Azure aboneliği  |
|--------- |---------|
|[Her iki kaynak yöneticisi](create-peering-different-subscriptions.md) |Farklı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models.md) |Aynı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models-subscriptions.md) |Farklı|

Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor. Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi. Her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlar tooconnect gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar. 

Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) Azure [PowerShell](#powershell), veya bir [Azure Resource Manager şablonu](#template) toocreate bir sanal ağ eşlemesi. Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.

## <a name="portal"></a>Eşlemesi - oluşturmak Azure portalı

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
4. Adım 2-3 yeniden değerleri adım 3'te aşağıdaki hello belirtme tamamlayın:
    - **Ad**: *myVnet2*
    - **Adres alanı**: *10.1.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.1.0.0/24*
    - **Abonelik**: aboneliğinizi seçin
    - **Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*
    - **Konum**: *Doğu ABD*
5. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myResourceGroup*. Tıklatın **myResourceGroup** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myresourcegroup** kaynak grubu. Merhaba kaynak grubu, önceki adımlarda oluşturduğunuz hello iki sanal ağ içeriyor.
6. Tıklatın **myVNet1**.
7. Merhaba, **myVnet1** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.
8. Merhaba, **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**
9. Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:
     - **Ad**: *myVnet1ToMyVnet2*
     - **Sanal ağ dağıtım modeli**: seçin **Resource Manager**. 
     - **Abonelik**: aboneliğinizi seçin
     - **Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.
     - **Sanal ağ erişimine izin ver:** emin **etkin** seçilir.
    Diğer bir ayarları, bu öğreticide kullanılır. Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).
10. ' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden. Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir. **Başlatılan** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu. Vnet1 tooVnet2 eşlenen, ancak şimdi myVnet2 toomyVnet1 eş gerekir. Merhaba eşliği her iki yönde de hello sanal ağlar toocommunicate tooenable kaynaklarında birbirleri ile oluşturulması gerekir.
11. Yeniden myVnet2 için 5-10 adımları tamamlayın.  Merhaba ad eşlemesi *myVnet2ToMyVnet1*.
12. ' I tıklattıktan sonra birkaç saniye **Tamam** toocreate hello MyVnet2 için hello eşliği **myVnet2ToMyVnet1** , yeni oluşturduğunuz eşliği ile listelendiğini **bağlı** hello içinde **Eşleme durumu** sütun.
13. Adım 5-7 MyVnet1 için yeniden tamamlayın. Merhaba **EŞLİĞİ durumu** hello için **myVnet1ToVNet2** eşliği olan şimdi de **bağlı**. Merhaba eşliği başarıyla kuruldu gördükten sonra **bağlı** hello içinde **EŞLİĞİ durum** hello eşlemesindeki her iki sanal ağlar için sütun.
14. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
15. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.

Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Eşlemesi - oluşturmak Azure CLI

komut dosyası izleyen hello:

- Hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Merhaba çalıştırmak toofind hello sürüm `az --version` komutu. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Bir Bash kabuğunda çalışır. Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Merhaba CLI ve bağımlılıklarını yüklemek yerine, hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. Merhaba tıklatın **deneyin** Azure hesabı düğmesini hello betikteki, oturumu bir bulut Kabuk çağırır aşağıdaki tooyour oturum açabilir. tooexecute Merhaba komut dosyası, hello tıklatın **kopyalama** düğmesine tıklayın ve bulut kabuğundan hello içeriğini yapıştırın.

1. Bir kaynak grubu ve iki sanal ağ oluşturun.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Merhaba iki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Merhaba betiği çalıştırdıktan sonra her bir sanal ağ hello eşlemeleri gözden geçirin. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Değiştirme Hello önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*. her ikisi de Hello çıktısını gösterir komutları **bağlı** hello içinde **PeeringState** sütun.

     Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
5. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.


## <a name="powershell"></a>Eşlemesi - oluşturmak PowerShell

1. Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. bir PowerShell oturumu toostart Git çok**Başlat**, girin **powershell**ve ardından **PowerShell**.
3. PowerShell'de tooAzure içinde hello girerek oturum `login-azurermaccount` komutu. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
4. Bir kaynak grubu ve iki sanal ağ oluşturun. tooexecute hello komut dosyası, kopyalama hello aşağıdaki komut, PowerShell içinde yapıştırın ve tuşuna basarak `Enter` hello son satırında Merhaba ekranında göründükten sonra:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Merhaba iki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun. Kopya hello aşağıdaki komut, tooPowerShell içinde yapıştırın ve tuşuna basarak `Enter` hello son satırında Merhaba ekranında göründükten sonra:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello hello sanal ağ alt ağları, kopyalama hello aşağıdaki komutu, içinde tooPowerShell yapıştırın ve tuşuna basın `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Değiştirme Hello önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*. her ikisi de Hello çıktısını gösterir komutları **bağlı** hello içinde **PeeringState** sütun.
7. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
8. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.

Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Eşlemesi - oluşturmak Resource Manager şablonu

1. Başvuru [bir sanal ağ eşlemesi oluşturma](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager şablonu. Merhaba şablonu dağıtmak için hello şablonuyla kullanarak hello Azure portal, PowerShell veya Azure CLI hello yönergeler sağlanmıştır. Günlük toodeploy hello şablonla, sahip bir hesap kullanarak seçtiğiniz toowhichever aracında bir sanal ağ eşlemesi gerekli izinleri toocreate hello. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
2. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
3. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete) kullanarak, bu makalenin bölümüne hello Azure portal, PowerShell veya Azure CLI hello.

## <a name="permissions"></a>İzinleri

bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir. Örneğin, VNet1 ve VNet2 adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:
    
|Sanal ağ|Rol|İzinler|
|---|---|---|
|VNet1|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|Vnet2'ye|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).

## <a name="delete"></a>Kaynakları silin
Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz. Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.

### <a name="delete-portal"></a>Azure portalı

1. Merhaba portal arama kutusuna **myResourceGroup**. Merhaba arama sonuçlarında tıklatın **myResourceGroup**.
2. Merhaba üzerinde **myResourceGroup** dikey penceresinde hello tıklatın **silmek** simgesi.
3. Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.

### <a name="delete-cli"></a>Azure CLI

Merhaba aşağıdaki komutu girin:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Merhaba aşağıdaki komutu girin:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Sonraki adımlar

- Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.
- Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).
- Nasıl çok öğrenin[bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.
