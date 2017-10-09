---
title: Hello Azure portal kullanarak aaaManage Nsg'ler | Microsoft Docs
description: "Bilgi nasıl hello Azure portal kullanarak Nsg'ler varolan toomanage."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a>Nsg'ler Hello portal kullanarak yönetme

> [!div class="op_single_selector"]
> * [Portal](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [Azure CLI](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Bilgi alma
Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.

### <a name="view-existing-nsgs"></a>Varolan Nsg'ler görüntüleyin

tooview tüm Nsg'ler bir abonelikte, aşağıdaki adımları tam hello var:

1. Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.

2. Tıklatın **Gözat >** > **ağ güvenlik grupları**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Merhaba listesinde Nsg'ler hello denetleyin **ağ güvenlik grupları** dikey.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Bir kaynak grubunda görünüm Nsg'ler

tooview hello listesinde Nsg'ler hello **RG NSG** kaynak grubu, şu adımları tam hello:

1. Tıklatın **kaynak grupları >** > **RG NSG** > **...** .

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Hello gösterildiği gibi kaynak Hello listesinde hello NSG simgesini görüntüleme öğeleri arar **kaynakları** dikey penceresinde aşağıdaki.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Bir NSG için tüm kuralları listesinde

adlı bir NSG tooview hello kuralları **NSG ön uç**tam hello adımları izleyin:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.

2. Merhaba, **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Merhaba **gelen güvenlik kuralları** dikey penceresi aşağıda gösterildiği gibi görüntülenir.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. Merhaba, **ayarları** sekmesini tıklatın, **giden güvenlik kurallarında** toosee hello giden kuralları.

    > [!NOTE]
    > tooview varsayılan kuralları tıklatın hello **varsayılan kuralları** hello kuralları görüntüler hello dikey penceresinde hello üstündeki simgesi.
    >

### <a name="view-nsgs-associations"></a>Nsg'ler ilişkilendirmelerini görüntülemek

tooview hangi kaynaklara hello **NSG ön uç** NSG olan aşağıdaki adımları ile tam hello:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.

2. Merhaba, **ayarları** sekmesini tıklatın, **alt ağlar** hangi alt ağlardır tooview toohello NSG ilişkilendirilmiş.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. Merhaba, **ayarları** sekmesini tıklatın, **ağ arabirimleri** tooview ne NIC'ler ilişkili toohello NSG.

## <a name="manage-rules"></a>Kuralları yönetme
NSG varolan kuralları tooan eklemek, mevcut kuralları düzenlemek ve kuralları kaldırın.

### <a name="add-a-rule"></a>Kural ekleme
izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, aşağıdaki adımları tam hello:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.
2. Merhaba, **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.
3. Merhaba, **gelen güvenlik kuralları** dikey penceresinde tıklatın **Ekle**. Ardından hello **gelen Güvenlik Kuralı Ekle** dikey penceresinde, aşağıda gösterildiği gibi hello değerlerini doldurun ve ardından **Tamam**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Birkaç saniye sonra hello yeni hello kuralında fark **gelen güvenlik kuralları** dikey.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Bir kural değiştirme
tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** aşağıdaki adımları yalnızca, tam hello:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.
2. Merhaba, **ayarları** sekmesinde, yukarıda oluşturduğunuz hello kural'ı tıklatın.
3. Merhaba, **izin https** dikey penceresinde, değişiklik hello **kaynak** aşağıda gösterildiği gibi özelliği ve ardından **kaydetmek**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Kural silme

Aşağıdaki adımları toodelete hello kural yukarıda oluşturulan, tam hello:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.
2. Merhaba, **ayarları** sekmesinde, yukarıda oluşturduğunuz hello kural'ı tıklatın.
3. Merhaba, **izin https** dikey penceresinde tıklatın **silmek**ve ardından **Evet**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>İlişkileri yönetme
Bir NSG toosubnets ve NIC ilişkilendirebilirsiniz. Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.

### <a name="associate-an-nsg-tooa-nic"></a>Bir NSG tooa NIC ilişkilendirme
tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, aşağıdaki adımları tam hello:

1. Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.
2. Merhaba, **ayarları** sekmesini tıklatın, **ağ arabirimleri** > **ilişkilendirmek** > **TestNICWeb1**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır

toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** NIC, aşağıdaki adımları tam hello:

1. Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestNICWeb1**.

2. Merhaba, **TestNICWeb1** dikey penceresinde tıklatın **değiştirme güvenlik...**   >  **Hiçbiri**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> NSG varolan bu dikey tooassociate hello NIC tooany de kullanabilirsiniz.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır

toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt ağ, aşağıdaki adımları tam hello:

1. Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.

2. Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **Hiçbiri**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Bir NSG tooa alt ağını ilişkilendirin

tooassociate hello **NSG ön uç** NSG toohello **FronEnd** yeniden alt ağ, aşağıdaki adımları tam hello:

1. Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **NSG ön uç**.
3. Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.

> [!NOTE]
> Ayrıca, bir NSG tooa alt ağ üzerinden thh NSG's ilişkilendirebilirsiniz **ayarları** dikey.
>

## <a name="delete-an-nsg"></a>Bir NSG'yi Sil
Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz. toodelete bir NSG, aşağıdaki adımları tam hello:.

1. Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **NSG ön uç**.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **ağ arabirimleri**.
3. Listelenen NIC'ler varsa, hello NIC tıklayın ve adım 2'de izleyin [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC).
4. 3. adım her NIC için yineleyin
5. Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar**.
6. Listelenen hiçbir alt ağ yoksa, hello alt ağ'ı tıklatın ve 2 ve 3'te adımları izleyerek [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet).
7. Sol toohello kayar **NSG ön uç** dikey penceresinde, ardından **silmek** > **Evet**.

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.
