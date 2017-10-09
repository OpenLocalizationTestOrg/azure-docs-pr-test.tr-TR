---
title: "bir Azure sanal ağı birden fazla alt ağı aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate birden fazla alt ağı azure'da bir sanal ağ."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Birden çok alt ağı ile bir sanal ağ oluşturma

Bu öğreticide, nasıl toocreate olan temel bir Azure sanal ağında ayrı ortak ve özel alt ağlar hakkında bilgi edinin. Bir alt ağda sanal makineler, uygulama hizmeti ortamları, sanal makine ölçek kümeleri, Azure Hdınsight ve bulut Hizmetleri gibi Azure kaynaklarını oluşturabilirsiniz. Sanal ağlar kaynaklarında birbirleriyle ve diğer ağ bağlantılı tooa sanal ağınızdaki kaynaklara ile iletişim kurabilir.

Merhaba aşağıdaki bölümleri içerir toocreate bir sanal ağ hello kullanarak izleyebileceğiniz olduğunu adımlar [Azure portal](#portal), Azure komut satırı arabirimi hello ([Azure CLI](#azure-cli)), [Azure PowerShell ](#powershell)ve bir [Azure Resource Manager şablonu](#resource-manager-template). Merhaba, hangi aracının toocreate hello sanal ağı kullanmayı hello aynı, bakılmaksızın sonucudur. Bir aracı bağlantı toogo toothat bölümüne hello öğreticinin tıklatın. Tüm hakkında daha fazla bilgi [sanal ağ](virtual-network-manage-network.md) ve [alt](virtual-network-manage-subnet.md) ayarlar.

Bu makalede adımları toocreate hello dağıtım modeli yeni sanal ağları oluştururken kullanmanızı öneririz hello Resource Manager dağıtım modeli üzerinden sanal bir ağ sağlar. Bir sanal ağ (Klasik) toocreate gerekirse bkz [bir sanal ağ (Klasik) oluşturmak](create-virtual-network-classic.md). Azure'nın dağıtım modeliyle bilmiyorsanız bkz [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Azure portalı

1. Bir Internet tarayıcısında toohello Git [Azure portal](https://portal.azure.com). Kullanarak oturum açın, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Merhaba Portalı'nda tıklatın **+ yeni** > **ağ** > **sanal ağ**.
3. Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:

    |Ayar|Değer|
    |---|---|
    |Ad|myVnet|
    |Adres alanı|10.0.0.0/16|
    |Alt ağ adı|Genel|
    |Alt ağ adres aralığı|10.0.0.0/24|
    |Kaynak grubu|Bırakın **Yeni Oluştur** seçili yazıp enter **myResourceGroup**.|
    |Abonelik ve konum|Abonelik ve konum seçin.

    Yeni tooAzure değilseniz, hakkında daha fazla bilgi [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (tooas ya da *bölgeleri*).
4. Bir sanal ağ oluşturduğunuzda, hello Portalı'nda, yalnızca bir alt ağ oluşturabilirsiniz. Merhaba sanal ağ oluşturduktan sonra Bu öğreticide, ikinci bir alt ağ oluşturun. Daha sonra Internet'ten erişilebilen kaynaklara hello oluşturacağınız **ortak** alt ağ. Merhaba hello Internet üzerinden erişilebilir olmayan kaynakları de oluşturabilir **özel** alt ağ. toocreate hello ikinci alt, hello **arama kaynakları** kutusuna hello hello sayfanın başında **myVnet**. Merhaba arama sonuçlarında tıklatın **myVnet**. Aynı ada aboneliğinizde Merhaba, her sanal ağ altında listelenen hello kaynak gruplarını denetle birden çok sanal ağ ile varsa. Merhaba tıklatın olun **myVnet** arama hello kaynak Grubu'na sonucu **myResourceGroup**.
5. Merhaba üzerinde **myVnet** dikey altında **ayarları**, tıklatın **alt ağlar**.
6. Merhaba üzerinde **myVnet - alt ağlar** dikey penceresinde tıklatın **+ alt**.
7. Merhaba üzerinde **alt ağ Ekle** dikey penceresinde için **adı**, girin **özel**. İçin **adres aralığı**, girin **10.0.1.0/24**.  **Tamam** düğmesine tıklayın.
8. Merhaba üzerinde **myVnet - alt ağlar** dikey penceresinde, gözden geçirme hello alt ağlar. Merhaba görebilirsiniz **ortak** ve **özel** oluşturduğunuz alt ağlar.
9. **İsteğe bağlı:** tam hello Bu öğreticide oluşturduğunuz toodelete hello kaynakları adımları [silmek kaynakları](#delete-portal) bu makalede.

## <a name="azure-cli"></a>Azure CLI

Windows, Linux veya macOS hello komutları çalıştırmak isteyip azure CLI aynı hello komutlardır. Ancak, işletim sistemi Kabukları arasında komut dosyası farklar vardır. Aşağıdaki adımları hello Hello kodda bir Bash kabuğunda yürütür. 

1. [Hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Merhaba bulut Kabuk Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuk hello bulut Kabuğu'nu tıklatın (**> _**) düğmesini hello hello üstündeki [portal](https://portal.azure.com) veya hello tıklatmanız *deneyin* izleyin hello adımları düğmesini. 
2. Merhaba ile tooAzure Hello CLI yerel olarak çalışıyorsa, oturumu `az login` komutu. Merhaba bulut Kabuk kullanıyorsanız, zaten oturum açtınız.
3. Gözden geçirme hello komut dosyası ve kendi yorumları aşağıdaki. Tarayıcınızda hello betiği kopyalayın ve CLI oturumunuza yapıştırın:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Merhaba betik tamamlandığında çalışan, hello alt ağlar hello sanal ağ için gözden geçirin. Merhaba aşağıdaki komutu kopyalayın ve CLI oturumunuza yapıştırın:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.

## <a name="powershell"></a>PowerShell

1. Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Bir PowerShell oturumunda ile tooAzure oturumu, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) hello kullanarak `login-azurermaccount` komutu.

3. Gözden geçirme hello komut dosyası ve kendi yorumları aşağıdaki. Tarayıcınızda hello betiği kopyalayın ve PowerShell oturumunuza yapıştırın:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. tooreview hello alt hello sanal ağ için komutu aşağıdaki hello kopyalayın ve PowerShell oturumunuza yapıştırın:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.

## <a name="resource-manager-template"></a>Resource Manager şablonu

Bir Azure Resource Manager şablonu kullanarak bir sanal ağ dağıtabilirsiniz. Şablonlar hakkında daha fazla toolearn bkz [Resource Manager nedir](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). tooaccess hello şablonu ve kendi parametreleriyle ilgili toolearn bkz hello [iki alt ağa sahip bir sanal ağ oluşturma](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) şablonu. Hello kullanarak hello şablonu dağıtabilirsiniz [portal](#template-portal), [Azure CLI](#template-cli), veya [PowerShell](#template-powershell).

**İsteğe bağlı:** Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımlar tüm alt bölümlerde [silmek kaynakları](#delete) bu makalede.

### <a name="template-portal"></a>Azure portalı

1. Merhaba, tarayıcınızı açmak [şablon sayfasına](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Merhaba tıklatın **tooAzure dağıtmak** düğmesi. TooAzure zaten oturum açtınız, görüntülenen hello Azure portalı oturum açma ekranında oturum açın.
3. Kullanarak toohello Portalı'nda oturum, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Merhaba parametreleri için değerleri aşağıdaki hello girin:

    |Parametre|Değer|
    |---|---|
    |Abonelik|Aboneliğinizi seçin|
    |Kaynak grubu|myResourceGroup|
    |Konum|Konum seçin|
    |Vnet adı|myVnet|
    |Vnet adres ön eki|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Genel|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Özel|

5. Toohello hüküm ve koşulları kabul edin ve ardından **satın alma** toodeploy hello sanal ağ.

### <a name="template-cli"></a>Azure CLI

1. [Hello Azure CLI yükleyip](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Merhaba en son sürümünü hello Azure CLI yüklenmiş olduğundan emin olun. CLI komutları için tooget Yardım yazın `az <command> --help`. Yükleme hello CLI ve ön koşullar yerine hello Azure bulut Kabuk kullanabilirsiniz. Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir. Merhaba bulut Kabuk Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir. toouse hello bulut Kabuk hello bulut Kabuğu'nu tıklatın **> _** düğmesi hello hello üstündeki [portal](https://portal.azure.com), veya hello tıklatmanız **deneyin** izleyin hello adımları düğmesini. 
2. Merhaba ile tooAzure Hello CLI yerel olarak çalışıyorsa, oturumu `az login` komutu. Merhaba bulut Kabuk kullanıyorsanız, zaten oturum açtınız.
3. toocreate hello sanal ağ için bir kaynak grubu, kopyalama hello aşağıdaki komut ve CLI oturumunuza yapıştırın:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Merhaba şablon parametreleri seçenekleri aşağıdaki hello birini kullanarak dağıtabilirsiniz:
    - **Varsayılan parametre değerlerini**. Merhaba aşağıdaki komutu girin:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Özel parametre değerlerini**. Karşıdan yükle ve hello şablonunun dağıtmadan önce hello şablonu değiştirin. Ayrıca hello komut satırında parametreleri kullanarak hello şablonu dağıtma, veya ayrı parametreleri dosyasıyla hello şablonunu dağıtın. toodownload hello şablonu ve parametre dosyalarını hello tıklatın **Github'da Gözat** hello düğmesinde [iki alt ağa sahip bir sanal ağ oluşturma](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) şablon sayfası. Merhaba, Github'da tıklatın **azuredeploy.parameters.json** veya **azuredeploy.json** dosya. Ardından, hello **Raw** toodisplay hello dosya düğmesi. Tarayıcınızda, hello hello dosyasının içeriğini kopyalayın. Merhaba içeriği tooa dosyayı bilgisayarınıza kaydedin. Merhaba şablonunda hello parametre değerlerini değiştirmek veya ayrı parametreleri dosyasıyla hello şablonu dağıtabilirsiniz.  

    Bu yöntemleri kullanarak toodeploy şablonları nasıl türü hakkında daha fazla bilgi toolearn `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Toosign ile bir PowerShell oturumunda, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), girin `login-azurermaccount`.
3. toocreate hello sanal ağ için bir kaynak grubu hello aşağıdaki komutu girin:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Merhaba şablon parametreleri seçenekleri aşağıdaki hello birini kullanarak dağıtabilirsiniz:
    - **Varsayılan parametre değerlerini**. Merhaba aşağıdaki komutu girin:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Özel parametre değerlerini**. Karşıdan yükle ve dağıtmadan önce hello şablonu değiştirin. Ayrıca hello komut satırında parametreleri kullanarak hello şablonu dağıtma, veya ayrı parametreleri dosyasıyla hello şablonunu dağıtın. toodownload hello şablonu ve parametre dosyalarını hello tıklatın **Github'da Gözat** hello düğmesinde [iki alt ağa sahip bir sanal ağ oluşturma](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) şablon sayfası. Merhaba, Github'da tıklatın **azuredeploy.parameters.json** veya **azuredeploy.json** dosya. Ardından, hello **Raw** toodisplay hello dosya düğmesi. Tarayıcınızda, hello hello dosyasının içeriğini kopyalayın. Merhaba içeriği tooa dosyayı bilgisayarınıza kaydedin. Merhaba şablonunda hello parametre değerlerini değiştirmek veya ayrı parametreleri dosyasıyla hello şablonu dağıtabilirsiniz.  

    Bu yöntemleri kullanarak toodeploy şablonları nasıl türü hakkında daha fazla bilgi toolearn `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Kaynakları silin

Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi yok, oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz. Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.

### <a name="delete-portal"></a>Azure portalı

1. Merhaba portal arama kutusuna **myResourceGroup**. Merhaba arama sonuçlarında tıklatın **myResourceGroup**.
2. Merhaba üzerinde **myResourceGroup** dikey penceresinde hello tıklatın **silmek** simgesi.
3. Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.

### <a name="delete-cli"></a>Azure CLI

CLI oturumunda hello aşağıdaki komutu girin:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Bir PowerShell oturumunda hello aşağıdaki komutu girin:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Sonraki adımlar

- tüm sanal ağ ve alt ağ ayarları hakkında toolearn bkz [sanal ağlarını yönetmeleri](virtual-network-manage-network.md#view-vnet) ve [sanal ağ alt ağlarını yönetin](virtual-network-manage-subnet.md#create-subnet). Sanal ağlar ve alt ağlar, bir üretim ortamında toomeet farklı gereksinimleri kullanmaya yönelik çeşitli seçenekleriniz vardır.
- gelen ve giden toofilter alt ağ trafiği, oluşturma ve uygulama [ağ güvenlik grubu](virtual-networks-nsg.md) toosubnets.
- Oluşturma bir [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine ve tooan varolan sanal ağa bağlayın.
- tooconnect iki sanal ağlar olarak Merhaba aynı Azure konumunda, oluşturma bir [sanal ağ eşlemesi](virtual-network-peering-overview.md) hello sanal ağlar arasında.
- Kullanarak Hello sanal ağ tooan şirket ağına bağlanan bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hattı.
