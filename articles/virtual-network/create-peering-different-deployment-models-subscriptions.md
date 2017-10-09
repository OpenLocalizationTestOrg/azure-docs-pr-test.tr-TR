---
title: "Azure sanal ağ eşlemesi bir - aaaCreate farklı dağıtım modelleri - farklı Aboneliklerde | Microsoft Docs"
description: "Sanal ağlar arasında eşlemeyi bir sanal ağ toocreate farklı Azure aboneliklerinde mevcut farklı Azure dağıtım modelleri arasında nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Sanal Ağ eşlemesi bir - farklı oluşturmak dağıtım modelleri ve abonelikleri

Bu öğreticide, bir sanal ağ farklı dağıtım modeli oluşturulan sanal ağlar arasında eşleme toocreate öğrenin. Merhaba sanal ağlar farklı Aboneliklerde mevcut. Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ. Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md). 

Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla. Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:

|Azure dağıtım modeli  | Azure aboneliği  |
|--------- |---------|
|[Her iki kaynak yöneticisi](virtual-network-create-peering.md) |Aynı|
|[Her iki kaynak yöneticisi](create-peering-different-subscriptions.md) |Farklı|
|[Bir kaynak yöneticisi, bir Klasik](create-peering-different-deployment-models.md) |Aynı|

Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor. Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi. Farklı Aboneliklerde abonelikleri hem de olmalıdır hello mevcut sanal ağlar arasında eşleme sanal ağ oluşturma toohello ilişkilendirilmiş zaman aynı Azure Active Directory Kiracı. Azure Active Directory kiracısı zaten sahip değilseniz, hızlı bir şekilde yapabilecekleriniz [oluşturmak](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Tooconnect sanal gerekiyorsa her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla veya farklı Azure bölgelerinde yok ya da Aboneliklerde mevcut ağları ilişkili toodifferent Azure Active Directory kiracıları, bir Azure kullanabileceğiniz[VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar. 

> [!WARNING]
> Bir sanal ağ içinde sanal ağlar arasında farklı Aboneliklerde bulunan farklı Azure dağıtım modelleri aracılığıyla oluşturulan eşlemesi oluşturma, şu anda önizlemede değil. Bu senaryoda, oluşturulan sanal ağ eşlemesi bulunabilir olmayabilir hello aynı düzeyde kullanılabilirlik ve güvenilirlik senaryolarda kullanılabilirlik yayın genel eşliği sanal ağ oluşturma olarak. Bu senaryoda, oluşturulan sanal ağ eşlemeleri desteklenmez, yetenekleri kısıtlı ve tüm Azure bölgelerde kullanılabilir durumda olmayabilir. Merhaba Hello en güncel bildirimleri için kullanılabilirlik ve bu özellik durumunu denetleme [Azure sanal ağı güncelleştirir](https://azure.microsoft.com/updates/?product=virtual-network) sayfası.

Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) veya Azure [PowerShell](#powershell) toocreate bir sanal ağ eşlemesi. Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.

## <a name="register"></a>Merhaba Önizleme için kaydolun

tooregister hello Önizleme için hello sanal ağları içeren iki abonelikler için izlemeniz tam hello adımları toopeer istiyor. Merhaba tooregister hello Önizleme için kullanabileceğiniz yalnızca PowerShell aracıdır.

1. Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumu başlatın ve içinde tooAzure hello kullanarak oturum `login-azurermaccount` komutu.
3. Aboneliğiniz hello Önizleme için aşağıdaki komutları hello girerek kaydedin:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Bu makalenin hello Portal, Azure CLI veya PowerShell bölümlerdeki Hello adımları kadar hello tamamlamayın **RegistrationState** komutu aşağıdaki hello girdikten sonra aldığınız çıktı **kayıtlı** Her iki abonelikler için:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Eşlemesi - oluşturmak Azure portalı

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum hello portal dışında hello adımları atlayın ve başka bir kullanıcı izinleri toohello sanal ağlar atama hello adımları atlayın hello kullanabilirsiniz. Aşağıdaki adımları hello hiçbirini tamamlamadan önce hello Önizleme için kaydetmeniz gerekir. tooregister, tam hello adımları hello [kaydetmek için hello Önizleme](#register) bu makalenin. Her iki aboneliğin hello Önizleme için kayıtlı kadar adımları kalan hello ile devam etmeyin.
 
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
8. Merhaba, **seçin** kutusunda, UserB seçin veya Kullanıcıb'in e-posta adresi toosearch yazın. Merhaba gösterilen kullanıcıların hello listesidir aynı Azure Active Directory Kiracı hello sanal ağ olarak ayarladığınız için hello eşliği ayarlama. Merhaba listesinde görüntülendiğinde Kullanıcıb'ı tıklatın.
9. **Kaydet** düğmesine tıklayın.
10. UserA olarak hello portal dışında oturum sonra UserB oturum açın.
11. Tıklatın **+ yeni**, türü *sanal ağ* hello içinde **arama hello Market** kutusuna ve ardından **sanal ağ** hello arama sonuçlarında .
12. Merhaba, **sanal ağ** görünen seçin dikey **Klasik** hello içinde **dağıtım modeli seçin** kutusuna ve ardından **oluşturma**.
13.   Görüntülenen hello oluşturma sanal ağ (Klasik) kutusunda, değerleri aşağıdaki hello girin:

    - **Ad**: *myVnetB*
    - **Adres alanı**: *10.1.0.0/16*
    - **Alt ağ adı**: *varsayılan*
    - **Alt ağ adres aralığı**: *10.1.0.0/24*
    - **Abonelik**: Abonelik B. seçin
    - **Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroupB*
    - **Konum**: *Doğu ABD*

14. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetB*. Tıklatın **myVnetB** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnetB** sanal ağ.
15. Merhaba, **myVnetB** görünür, dikey tıklayın **özellikleri** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri. Kopya hello **kaynak kimliği**, bir sonraki adımda kullanılır. Merhaba kaynak kimliği olan aşağıdaki örneğine benzer toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. 5-9 myVnetB, girmek için adımları **Kullanıcıa** 8. adımda.
17. Dışında hello portalı UserB olarak oturum açın ve UserA oturum açın.
18. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetA*. Tıklatın **myVnetA** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnet** sanal ağ.
19. Tıklatın **myVnetA**.
20. Merhaba, **myVnetA** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.
21. Merhaba, **myVnetA - eşlemeler** görünen dikey tıklayın **+ Ekle**
22. Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:
     - **Ad**: *myVnetAToMyVnetB*
     - **Sanal ağ dağıtım modeli**: seçin **Klasik**.
     - **Kaynak Kimliğimi biliyorum**: Bu onay kutusunu işaretleyin.
     - **Kaynak Kimliği**: 15. adımdan myVnetB hello kaynak Kimliğini girin.
     - **Sanal ağ erişimine izin ver:** emin **etkin** seçilir.
    Diğer bir ayarları, bu öğreticide kullanılır. Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).
23. ' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnetA - eşlemeler** dikey penceresini yeniden. Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir. **Bağlı** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnetAToMyVnetB** sizin eşlemeyi oluşturuldu. Merhaba eşliği şimdi oluşturulur. Gereksinim toopeer hello sanal ağ (Klasik) toohello sanal ağ (Resource Manager) yoktur.

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
25. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.

## <a name="cli"></a>Eşlemesi - oluşturmak Azure CLI

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum Azure dışında hello adımları atlayın ve kullanıcı rol atamalarını oluşturmak hello satırlarını komut kaldırmak hello kullanabilirsiniz. Değiştir UserA@azure.com ve UserB@azure.com UserA ve userb adlı için kullanmakta olduğunuz hello kullanıcı adları kodlarla aşağıdaki hello tümünde. 

Aşağıdaki adımları hello hiçbirini tamamlamadan önce hello Önizleme için kaydetmeniz gerekir. tooregister, tam hello adımları hello [kaydetmek için hello Önizleme](#register) bu makalenin. Her iki aboneliğin hello Önizleme için kayıtlı kadar adımları kalan hello ile devam etmeyin.

1. [Yükleme](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello sanal ağ (Klasik).
2. CLI oturumu açın ve içinde tooAzure hello kullanarak UserB oturum `azure login` komutu.
3. Merhaba girerek Hello CLI Hizmet Yönetimi modunda çalışacak `azure config mode asm` komutu.
4. Toocreate hello sanal ağ (Klasik) komutu aşağıdaki hello girin:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. adımları kalan hello Azure CLI 2.0.4 hello ile bir bash kabuğunda kullanarak doldurulması gerekir ya da daha sonra [yüklü](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), veya hello Azure bulut Kabuğu'nu kullanarak. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. Merhaba tıklatın **deneyin** hello düğmesini komutlar bir bulut tooyour Azure hesabı açtığı Kabuğu'nu açar bu izleyin. Bir Windows istemcisinde CLI betikleri çalıştırma seçenekleri bash için bkz: [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<SubscriptionB-Id>` abonelik kimliğinizi içeren Merhaba, abonelik kimliği bilmiyorsanız, girin `az account show` komutu. Merhaba değeri **kimliği** hello çıktı, abonelik kimliği değil. Değiştiren hello betiği kopyalayın, tooyour CLI 2.0 oturumunda yapıştırın ve tuşuna `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Merhaba sanal ağ (Klasik) 4. adımda oluşturduğunuz zaman hello sanal ağ hello oluşturulan Azure *varsayılan ağ* kaynak grubu.
7. Azure ve oturum açma dışında UserB hello CLI 2.0 UserA oturum açın.
8. Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun. Kopyalama hello aşağıdaki komut dosyası, tooyour CLI oturumunda yapıştırın ve tuşuna `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Merhaba farklı dağıtım modelleri arasında oluşturulan hello iki sanal ağlar arasında eşleme sanal ağ oluşturun. Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın. Değiştir `<SubscriptionB-id>` aboneliğinizle kimliği. Merhaba, abonelik kimliği bilmiyorsanız, girin `az account show` komutu. Merhaba değeri **kimliği** hello çıktı, abonelik kimliği değil. Oluşturulan Azure adlı adım 4'te bir kaynak grubunda oluşturduğunuz hello sanal ağ (Klasik) *varsayılan ağ*. CLI oturumunuzda değiştiren hello betik yapıştırın ve tuşuna `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Merhaba betik yürütüldükten sonra hello sanal ağ (Resource Manager) hello eşlemesi gözden geçirin. Komut dosyası izleyen hello kopyalayın ve ardından CLI oturumunuzda yapıştırın:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Merhaba çıktısını gösterir **bağlı** hello içinde **PeeringState** sütun.

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
12. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.

## <a name="powershell"></a>Eşlemesi - oluşturmak PowerShell

Bu öğretici, her abonelik için farklı hesaplar kullanır. İzinleri tooboth aboneliklere sahip bir hesap kullanıyorsanız, aynı tüm adımlar için hesap, oturum Azure dışında hello adımları atlayın ve kullanıcı rol atamalarını oluşturmak hello satırlarını komut kaldırmak hello kullanabilirsiniz. Değiştir UserA@azure.com ve UserB@azure.com UserA ve userb adlı için kullanmakta olduğunuz hello kullanıcı adları kodlarla aşağıdaki hello tümünde. 

Aşağıdaki adımları hello hiçbirini tamamlamadan önce hello Önizleme için kaydetmeniz gerekir. tooregister, tam hello adımları hello [kaydetmek için hello Önizleme](#register) bu makalenin. Her iki aboneliğin hello Önizleme için kayıtlı kadar adımları kalan hello ile devam etmeyin.

1. Merhaba PowerShell Hello en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) ve [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modüller. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumu başlatın.
3. PowerShell'de, UserB olarak tooUserB'ın Abonelikteki hello girerek oturum `Add-AzureAccount` komutu.
4. bir sanal ağ (Klasik) PowerShell ile toocreate, yeni bir, veya var olan değiştirmeniz gerekir ağ yapılandırma dosyası. Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md). Merhaba dosya hello aşağıdakileri içermelidir **VirtualNetworkSite** öğesi Bu öğreticide kullanılan hello sanal ağ için:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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

5. Kullanıcıb toouse Resource Manager komutları olarak tooUserB'ın Abonelikteki hello girerek oturum `login-azurermaccount` komutu.
6. B. kopyalama hello aşağıdaki komut dosyası tooa metin düzenleyici, bilgisayarınızdaki ve değiştirme Ata Kullanıcıa izinleri toovirtual ağ `<SubscriptionB-id>` abonelik B. hello kimliği Merhaba abonelik kimliği bilmiyorsanız, hello girin `Get-AzureRmSubscription` komutu tooview onu. Merhaba değeri **kimliği** hello çıkış abonelik kimliğinizi döndürülür Oluşturulan Azure adlı adım 4'te bir kaynak grubunda oluşturduğunuz hello sanal ağ (Klasik) *varsayılan ağ*. tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyası, içinde tooPowerShell yapıştırın ve tuşuna `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. UserB olarak Azure dışında ve UserA olarak tooUserA'ın Abonelikteki hello girerek oturum `login-azurermaccount` komutu. Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir. Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.
8. Komut dosyasını tooPowerShell ve tuşuna basarak yapıştırma aşağıdaki hello kopyalayarak Hello sanal ağ (Resource Manager) oluşturma `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Kullanıcıb izinleri toomyVnetA atayın. Kopya hello aşağıdaki komut dosyası tooa metin düzenleyici, bilgisayarınızdaki ve değiştirme `<SubscriptionA-Id>` abonelik A. hello kimliği Merhaba abonelik kimliği bilmiyorsanız, hello girin `Get-AzureRmSubscription` komutu tooview onu. Merhaba değeri **kimliği** hello çıkış abonelik kimliğinizi döndürülür PowerShell'de hello komut dosyasının değiştirilmiş sürümünü hello yapıştırın ve tuşuna basarak `Enter` tooexecute onu.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Kopya hello aşağıdaki komut dosyası tooa metin düzenleyici, bilgisayarınızdaki ve değiştirme `<SubscriptionB-id>` abonelik B. toopeer myVnetA toomyVNetB hello kimliği, kopyalama değiştiren hello komut dosyası, içinde tooPowerShell yapıştırın ve tuşuna basarak `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Aşağıdaki komut, PowerShell ve tuşlarına basarak yapıştırma hello kopyalayarak hello eşleme myVnetA durumunu görüntülemek `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Merhaba durumu **bağlı**. Çok değiştirir**bağlı** hello eşleme toomyVnetA myVnetB gelen kurulum sonra.

    Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur. Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır. Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir. Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.
13. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.

## <a name="permissions"></a>İzinleri

bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir. Örneğin, myVnetA ve myVnetB adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:
    
|Sanal ağ|Dağıtım modeli|Rol|İzinler|
|---|---|---|---|
|myVnetA|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Yok|
|myVnetB|Resource Manager|[Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klasik|[Klasik Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).

## <a name="delete"></a>Kaynakları silin
Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz. Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.

### <a name="delete-portal"></a>Azure portalı

1. Merhaba portal arama kutusuna **myResourceGroupA**. Merhaba arama sonuçlarında tıklatın **myResourceGroupA**.
2. Merhaba üzerinde **myResourceGroupA** dikey penceresinde hello tıklatın **silmek** simgesi.
3. Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroupA**ve ardından **silmek**.
4. Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myVnetB*. Tıklatın **myVnetB** hello arama sonuçlarında görüntülendiğinde. Merhaba bir dikey penceresi görünür **myVnetB** sanal ağ.
5. Merhaba, **myVnetB** dikey penceresinde tıklatın **silmek**.
6. tooconfirm hello silme tıklatın **Evet** hello içinde **Delete sanal ağ** kutusu.

### <a name="delete-cli"></a>Azure CLI

1. Hello kullanarak tooAzure içinde CLI 2.0 toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello ile oturum:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Hello kullanarak tooAzure komutları aşağıdaki hello ile Azure CLI 1.0 toodelete hello sanal ağ (Klasik) oturum:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Merhaba PowerShell komut isteminde toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello girin:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello sanal ağ (Klasik) PowerShell ile varolan bir ağ yapılandırma dosyasını değiştirmeniz gerekir. Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md). Bu öğreticide kullanılan hello sanal ağ için VirtualNetworkSite öğesi aşağıdaki hello kaldırın:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
