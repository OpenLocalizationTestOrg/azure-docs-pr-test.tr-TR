---
title: "aaaCreate bir Azure sanal ağ - Resource Manager - eşliği farklı Aboneliklerde | Microsoft Docs"
description: "Toocreate sanal ağlar arasında eşlemeyi bir sanal ağ kaynak farklı Azure aboneliklerinde bulunmayan Yöneticisi aracılığıyla nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Bir sanal ağ eşlemesi - oluşturma, farklı Aboneliklerde Kaynak Yöneticisi'ni 

Bu öğreticide, bir sanal ağ Resource Manager aracılığıyla oluşturulan sanal ağlar arasında eşleme toocreate öğrenin. Merhaba sanal ağlar farklı Aboneliklerde mevcut. Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ. Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md). 

Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla. Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:

|Azure dağıtım modeli  | Azure aboneliği  |
|--------- |---------|
|[Her iki kaynak yöneticisi](virtual-network-create-peering.md) |Aynı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models.md) |Aynı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models-subscriptions.md) |Farklı|

Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor. Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi. Farklı Aboneliklerde abonelikleri hem de olmalıdır hello mevcut sanal ağlar arasında eşleme sanal ağ oluşturma toohello ilişkilendirilmiş zaman aynı Azure Active Directory Kiracı. Azure Active Directory kiracısı zaten sahip değilseniz, hızlı bir şekilde yapabilecekleriniz [oluşturmak](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Tooconnect sanal gerekiyorsa her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla veya farklı Azure bölgelerinde yok ya da Aboneliklerde mevcut ağları ilişkili toodifferent Azure Active Directory kiracıları, bir Azure kullanabileceğiniz[VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar. 

Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) veya Azure [PowerShell](#powershell) toocreate bir sanal ağ eşlemesi. Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.

## <a name="portal"></a>Eşlemesi - oluşturmak Azure portalı

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum hello portal dışında hello adımları atlayın ve başka bir kullanıcı izinleri toohello sanal ağlar atama hello adımları atlayın hello kullanabilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) UserA olarak. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
2. Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.
3. Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:
    - **Ad**: *myVnetA*
    - **Adres alanı**: *10.0.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.0.0.0/24*
    - **Abonelik**: A. abonelik seçin
    - **Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroupA*
    - **Konum**: *Doğu ABD*
4. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetA*. Tıklatın **myVnetA** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnetA** sanal ağ.
5. Merhaba, **myVnetA** görünür, dikey tıklayın **erişim denetimi (IAM)** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.
6. Merhaba, **myVnetA - erişim denetimi (IAM)** görünür, dikey tıklayın **+ Ekle**.
7. Merhaba, **izinleri ekleyin** görünen seçin dikey **ağ Katılımcısı** hello içinde **rol** kutusu.
8. Merhaba, **seçin** kutusunda, bir UserB seçin veya Kullanıcıb'in e-posta adresi toosearch yazın. Merhaba gösterilen kullanıcıların hello listesidir aynı Azure Active Directory Kiracı hello sanal ağ olarak ayarladığınız için hello eşliği ayarlama.
9. **Kaydet** düğmesine tıklayın.
10. Merhaba, **myVnetA - erişim denetimi (IAM)** dikey penceresinde tıklatın **özellikleri** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri. Kopya hello **kaynak kimliği**, bir sonraki adımda kullanılır. Merhaba kaynak kimliği olan aşağıdaki örneğine benzer toohello: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. UserA olarak hello portal dışında oturum sonra UserB oturum açın.
12. 2-3 girmek veya adım 3'te değerleri aşağıdaki hello seçerek, adımları tamamlayın:

    - **Ad**: *myVnetB*
    - **Adres alanı**: *10.1.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.1.0.0/24*
    - **Abonelik**: Abonelik B. seçin
    - **Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroupB*
    - **Konum**: *Doğu ABD*

13. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetB*. Tıklatın **myVnetB** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnetB** sanal ağ.
14. Merhaba, **myVnetB** görünür, dikey tıklayın **özellikleri** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri. Kopya hello **kaynak kimliği**, bir sonraki adımda kullanılır. Merhaba kaynak kimliği olan aşağıdaki örneğine benzer toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Tıklatın **erişim denetimi (IAM)** hello içinde **myVnetB** dikey ve ardından tam adımlar 5-10 girme myVnetB için **Kullanıcıa** 8. adımda.
16. Dışında hello portalı UserB olarak oturum açın ve UserA oturum açın.
17. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetA*. Tıklatın **myVnetA** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnet** sanal ağ.
18. Tıklatın **myVnetA**.
19. Merhaba, **myVnetA** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.
20. Merhaba, **myVnetA - eşlemeler** görünen dikey tıklayın **+ Ekle**
21. Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:
     - **Ad**: *myVnetAToMyVnetB*
     - **Sanal ağ dağıtım modeli**: seçin **Resource Manager**.
     - **Kaynak Kimliğimi biliyorum**: Bu onay kutusunu işaretleyin.
     - **Kaynak Kimliği**: 14. adımdan hello kaynak Kimliğini girin.
     - **Sanal ağ erişimine izin ver:** emin **etkin** seçilir.
    Diğer bir ayarları, bu öğreticide kullanılır. Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).
22. ' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnetA - eşlemeler** dikey penceresini yeniden. Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir. **Başlatılan** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnetAToMyVnetB** sizin eşlemeyi oluşturuldu. MyVnetA toomyVnetB eşlenen, ancak şimdi myVnetB toomyVnetA eş gerekir. Merhaba eşliği her iki yönde de hello sanal ağlar toocommunicate tooenable kaynaklarında birbirleri ile oluşturulması gerekir.
23. UserA olarak hello portal dışında oturum ve UserB oturum açın.
24. Yeniden myVnetB için 17 21 adımları tamamlayın. Merhaba eşliği 21. adımda ad *myVnetBToMyVnetA*seçin *myVnetA* için **sanal ağ**ve hello 10 adımda hello kimliği girin **kaynak kimliği** kutusu.
25. ' I tıklattıktan sonra birkaç saniye **Tamam** toocreate hello myVnetB için hello eşliği **myVnetBToMyVnetA** , yeni oluşturduğunuz eşliği ile listelendiğini **bağlı** hello içinde **Eşleme durumu** sütun.
26. Dışında hello portalı UserB olarak oturum açın ve UserA oturum açın.
27. Adımları 17-19 yeniden tamamlayın. Merhaba **EŞLİĞİ durumu** hello için **myVnetAToVNetB** eşliği olan şimdi de **bağlı**. Merhaba eşliği başarıyla kuruldu gördükten sonra **bağlı** hello içinde **EŞLİĞİ durum** hello eşlemesindeki her iki sanal ağlar için sütun. Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
29. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.

## <a name="cli"></a>Eşlemesi - oluşturmak Azure CLI

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum Azure dışında hello adımları atlayın ve kullanıcı rol atamalarını oluşturmak hello satırlarını komut kaldırmak hello kullanabilirsiniz. Değiştir UserA@azure.com ve UserB@azure.com UserA ve userb adlı için kullanmakta olduğunuz hello kullanıcı adları kodlarla aşağıdaki hello tümünde.

komut dosyası izleyen hello:

- Hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. çalıştırma toofind hello sürüm `az --version`. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Bir Bash kabuğunda çalışır. Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Merhaba CLI ve bağımlılıklarını yüklemek yerine, hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. Merhaba tıklatın **deneyin** tooyour içinde Azure hesap ile oturum bir bulut Kabuk çağıran aşağıdaki hello komut düğmesi. 

1. CLI oturumu açın ve içinde tooAzure hello kullanarak UserA oturum `azure login` komutu. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
2. Kopyalama komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki Merhaba, yerine `<SubscriptionA-Id>` hello kimliği, SubscriptionA kopyalama hello betik sonra değiştirilmiş., CLI oturum ve tuşuna yapıştırın `Enter`. Aboneliğinizi kimliği bilmiyorsanız, hello 'az hesabı Göster' komutu girin. Merhaba değeri **kimliği** hello çıktı, abonelik kimliği değil.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     Merhaba iznini atama UserB için zorunlu değildir. Kullanıcıların kendi sanal ağlarını için eşleme isteklerini ayrı ayrı Yükselt olsa bile hello eşleşme istekleri sürece eşleme kurulabilir. Merhaba yerel sanal ağ içinde ağ Katılımcısı olarak myVNetB ayrıcalıklı bir kullanıcısı ekleme daha kolay toodo hello kurulumu kolaylaştırır.
3. Azure oturumunu hello kullanarak UserA oturum `az logout` komut sonra tooAzure UserB olarak oturum. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
4. MyVnetB oluşturun. Adım 2 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. Değiştir `<SubscriptionA-Id>` hello kimliği, SubscriptionB ile. 10.0.0.0/16 too10.1.0.0/16, tooB tüm değiştikçe ve tüm Bs tooA değiştirin. Değiştirilen hello betiği kopyalayın, tooyour CLI oturum ve tuşuna yapıştırın `Enter`. 
5. UserB olarak Azure dışında ve tooAzure UserA olarak oturum.
6. MyVnetA toomyVnetB eşliği bir sanal ağ oluşturun. Komut dosyası içeriği tooa metin düzenleyici, Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<SubscriptionB-Id>` hello kimliği, SubscriptionB ile. tooexecute hello komut dosyası, değişiklik hello betiği kopyalayın, CLI oturumunuza yapıştırın ve Enter tuşuna basın.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Merhaba myVnetA eşleme durumunu görüntüleyin.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    Merhaba durumu **başlatılan**. Çok değiştirir**bağlı** myVnetB hello eşleme toomyVnetA oluşturduktan sonra.

8. Azure'dan Kullanıcıa çıkışı ve tooAzure UserB olarak oturum.
9. Merhaba myVnetB toomyVnetA eşlemesi oluşturun. Adım 6 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. Değiştir `<SubscriptionB-Id>` SubscriptionA ve tooB ve tüm Bs tooA olarak tüm değişiklik için hello kimliği. Merhaba değişiklikleri yaptıktan sonra kopyalama hello betik değiştiren, CLI oturum ve tuşuna yapıştırma `Enter`.
10. Merhaba myVnetB eşleme durumunu görüntüleyin. Adım 7 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. TooB hello kaynak grubu ve sanal ağ adları değiştirme, kopyalama hello komut dosyası, tooyour CLI oturumunda değiştiren hello betiğini yapıştırın ve tuşuna basın `Enter`. Merhaba eşleme durumunda **bağlı**. eşleme durumunu myVnetA değişiklikleri çok hello**bağlı** myVnetB toomyVnetA hello eşliği oluşturduktan sonra. Kullanıcıa geri tooAzure ve tam adım 7 tekrar tooverify hello eşleme durumunu myVnetA oturum. 

    > [!NOTE]
    > Merhaba eşliği değil kurulduğunda hello eşleme duruma gelene kadar **bağlı** her iki sanal ağlar için.

11. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
12. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.

Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Eşlemesi - oluşturmak PowerShell

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum Azure dışında hello adımları atlayın ve kullanıcı rol atamalarını oluşturmak hello satırlarını komut kaldırmak hello kullanabilirsiniz. Değiştir UserA@azure.com ve UserB@azure.com UserA ve userb adlı için kullanmakta olduğunuz hello kullanıcı adları kodlarla aşağıdaki hello tümünde.

1. Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumu başlatın.
3. PowerShell'de hello girerek içinde tooAzure UserA oturum `login-azurermaccount` komutu. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
4. A. kopyalama hello betik tooa metnini izleyen bir kaynak grubu ve sanal ağ Düzenleyicisi bilgisayarınıza oluşturun. Değiştir `<SubscriptionA-Id>` hello kimliği, SubscriptionA ile. Merhaba, abonelik kimliği bilmiyorsanız, girin `Get-AzureRmSubscription` komutu tooview onu. Merhaba değeri **kimliği** hello çıkış abonelik kimliğinizi döndürülür tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyası, içinde tooPowerShell yapıştırın ve tuşuna `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    Merhaba iznini atama UserB için zorunlu değildir. Kullanıcıların kendi sanal ağlarını için eşleme isteklerini ayrı ayrı Yükselt olsa bile hello eşleşme istekleri sürece eşleme kurulabilir. Merhaba ayrıcalıklı bir kullanıcısı ekleme diğer sanal ağ hello yerel sanal ağ içinde bir kullanıcı olarak daha kolay toodo hello kurulumu kolaylaştırır.
5. Azure'dan Kullanıcıa çıkışı ve UserB oturum. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
6. Adım 4 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. Değiştir `<SubscriptionA-Id>` abonelik B. değişiklik 10.0.0.0/16 too10.1.0.0/16 için hello kimliği. Tüm tooB ve tüm Bs tooA değiştirin. tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyası, PowerShell içinde yapıştırın ve ardından basın `Enter`.
7. Azure'dan UserB çıkışı ve UserA oturum.
8. Merhaba myVnetA toomyVnetB eşlemesi oluşturun. Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<SubscriptionB-Id>` abonelik B. tooexecute hello betik hello kimliği, kopyalama değiştiren hello komut dosyası, içinde tooPowerShell yapıştırın ve tuşuna basın `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Merhaba myVnetA eşleme durumunu görüntüleyin.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Merhaba durumu **başlatılan**. Çok değiştirir**bağlı** hello eşleme toomyVnetA myVnetB gelen kurulum sonra.

10. Azure'dan Kullanıcıa çıkışı ve UserB oturum.
11. Merhaba myVnetB toomyVnetA eşlemesi oluşturun. Adım 8 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. Değiştir `<SubscriptionB-Id>` tüm abonelik A ve değişiklik hello kimlikli A'ın tooB ve tüm B'nin tooA. tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyası, içinde tooPowerShell yapıştırın ve tuşuna `Enter`.
12. Merhaba myVnetB eşleme durumunu görüntüleyin. Adım 9 tooa metin düzenleyicide, bilgisayarınızdaki Hello komut dosyası içeriğini kopyalayın. Merhaba kaynak grubu ve sanal ağ adları tooB değiştirin. tooexecute hello komut dosyası, PowerShell içinde değiştirilen hello betiğini yapıştırın ve tuşuna basın `Enter`. Merhaba durumu **bağlı**. eşleme durumunu hello **myVnetA** çok değiştirir**bağlı** gelen hello eşliği oluşturduktan sonra **myVnetB** çok**myVnetA**. Kullanıcıa geri tooAzure ve 9. adım tam tekrar tooverify hello eşleme durumunu myVnetA oturum. 

    > [!NOTE]
    > Merhaba eşliği değil kurulduğunda hello eşleme duruma gelene kadar **bağlı** her iki sanal ağlar için.

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
14. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.

## <a name="permissions"></a>İzinleri

bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir. Örneğin, adlı iki sanal ağ eşlemesi **myVnetA** ve **myVnetB**, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:
    
|Sanal ağ|Rol|İzinler|
|---|---|---|
|myVnetA|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).

## <a name="delete"></a>Kaynakları silin
Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz. Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.

### <a name="delete-portal"></a>Azure portalı

1. Toohello Azure portalında UserA oturum açın.
2. Merhaba portal arama kutusuna **myResourceGroupA**. Merhaba arama sonuçlarında tıklatın **myResourceGroupA**.
3. Merhaba üzerinde **myResourceGroupA** dikey penceresinde hello tıklatın **silmek** simgesi.
4. Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroupA**ve ardından **silmek**.
5. UserA olarak hello portal dışında oturum ve UserB oturum açın.
6. MyResourceGroupB için 2-4 arası adımları tamamlayın.

### <a name="delete-cli"></a>Azure CLI

1. TooAzure UserA olarak oturum ve hello aşağıdaki komutu yürütün:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. UserA olarak Azure dışında oturum ve UserB oturum açın.
3. Merhaba aşağıdaki komutu yürütün:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. TooAzure UserA olarak oturum ve hello aşağıdaki komutu yürütün:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. UserA olarak Azure dışında oturum ve UserB oturum açın.
3. Merhaba aşağıdaki komutu yürütün:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Sonraki adımlar

- Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.
- Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).
- Nasıl çok öğrenin[bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.
