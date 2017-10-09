---
title: "aaaCreate ağ güvenlik grupları - Azure portalı | Microsoft Docs"
description: "Bilgi nasıl toocreate ve ağ güvenlik grupları hello Azure portal kullanarak dağıtın."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>Ağ güvenlik grupları hello Azure portal kullanarak oluşturma

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [hello Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Merhaba örnek PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz senaryosunda hello yukarıdaki temel. Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda. Merhaba adımlar kullanım **RG NSG** hello hello kaynak grubu hello şablonunun adını dağıtılmış olan gibi.

## <a name="create-hello-nsg-frontend-nsg"></a>Merhaba NSG ön uç NSG oluşturma
toocreate hello **NSG ön uç** NSG hello senaryoda yukarıdaki gösterildiği gibi hello adımları izleyin.

1. Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.
2. Tıklatın **Gözat >** > **ağ güvenlik grupları**.
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. Merhaba, **ağ güvenlik grupları** dikey penceresinde tıklatın **Ekle**.
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. Merhaba, **oluşturma ağ güvenlik grubu** dikey penceresinde adlı bir NSG oluşturma *NSG ön uç* hello içinde *RG NSG* kaynak grubu ve ardından **oluşturma**.
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Mevcut bir NSG’de kurallar oluşturma
Varolan bir NSG hello Azure Portalı'ndan toocreate kurallarında hello adımları izleyin.

1. Tıklatın **Gözat >** > **ağ güvenlik grupları**.
2. Nsg'ler Hello listesinde tıklayın **NSG ön uç** > **gelen güvenlik kuralları**
   
    ![Azure portal - NSG ön uç](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Merhaba listesinde **gelen güvenlik kuralları**, tıklatın **Ekle**.
   
    ![Azure portal - Kuralı Ekle](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. Merhaba, **gelen Güvenlik Kuralı Ekle** dikey penceresinde adlı bir kural oluşturmak *web kuralı* önceliğini ile *200* aracılığıyla erişime izin verme *TCP* tooport *80* tooany VM herhangi kaynağı ve ardından **Tamam**. Bu ayarların çoğu varsayılan değerleri zaten olduğuna dikkat edin.
   
    ![Azure portal - kural ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Birkaç saniye sonra hello yeni hello NSG kuralında görürsünüz.
   
    ![Azure portalı - yeni kural](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Arasındaki adımları yineleyin too6 toocreate adlı bir gelen kuralı *rdp kural* önceliği *250* aracılığıyla erişime izin verme *TCP* tooport *3389* tooany herhangi bir kaynaktan VM.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Merhaba NSG toohello ön uç alt ağını ilişkilendirin
1. Tıklatın **Gözat >** > **kaynak grupları** > **RG NSG**.
2. Merhaba, **RG NSG** dikey penceresinde tıklatın **...**   >  **TestVNet**.
   
    ![Azure portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **NSG ön uç**.
   
    ![Azure portal - alt ağ ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.
   
    ![Azure portal - alt ağ ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Merhaba NSG arka uç NSG oluşturma
toocreate hello **NSG arka uç** NSG ve toohello ilişkilendirmek **arka uç** alt ağ, aşağıdaki hello adımları izleyin.

1. Yineleme başlangıç adımları [oluşturma hello NSG ön uç NSG](#Create-the-NSG-FrontEnd-NSG) toocreate adlı bir NSG *NSG arka uç*
2. Yineleme başlangıç adımları [içinde varolan bir NSG kuralları oluşturma](#Create-rules-in-an-existing-NSG) toocreate hello **gelen** hello tabloda kurallarında.
   
   | Gelen kuralı | Giden kuralı |
   | --- | --- |
   | ![Azure portal - gelen kuralı](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - giden kuralı](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Yineleme başlangıç adımları [hello NSG toohello ön uç alt ağını ilişkilendirin](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG arka uç** NSG toohello **arka uç** alt ağ.

## <a name="next-steps"></a>Sonraki Adımlar
* Nasıl çok öğrenin[varolan Nsg'ler yönetme](virtual-network-manage-nsg-arm-portal.md)
* [Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.

