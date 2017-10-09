---
title: "aaaConfigure özel IP adresleri VM'ler (Klasik) - Azure portalı | Microsoft Docs"
description: "Tooconfigure özel IP adresleri kullanarak sanal makineleri (Klasik) için Azure portalını nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Hello Azure portal kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [hello Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Merhaba örnek adımları zaten oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği toorun hello adımları istiyorsanız, ilk derleme açıklandığı hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken
toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:

1. Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.
2. Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, o hello fark **dağıtımmodeliseçin** listesinde zaten gösterir **Klasik**ve ardından **oluşturma**.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. Merhaba, **VM Oluştur** dikey penceresinde hello VM toobe oluşturulan hello adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası hello.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Tıklatın **isteğe bağlı yapılandırma** > **ağ** > **sanal ağ**ve ardından **TestVNet**. Varsa **TestVNet** kullanılamıyor hello kullandığınızdan emin olun *Orta ABD* konumu ve bu makalenin hello başında açıklanan hello test ortamı oluşturdunuz.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. Merhaba, **ağ** dikey penceresinde seçili yapma emin hello alt ağıdır *ön uç*, ardından **IP adreslerini**altında **IP adresi ataması** tıklatın **statik**ve ardından girin *192.168.1.101* için **IP adresi** aşağıda görüldüğü gibi.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. ' I tıklatın **Tamam** hello içinde **IP adresleri** dikey penceresinde'ye tıklayın **Tamam** hello içinde **ağ** dikey penceresinde ve tıklatın **Tamam**hello içinde **isteğe bağlı yapılandırma** dikey.
7. Merhaba, **VM Oluştur** dikey penceresinde tıklatın **oluşturma**. Panonuzda görüntülenen bildirim hello döşeme aşağıdaki.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi
VM yukarıdaki hello adımları ile oluşturulan tooview hello statik özel IP adresi bilgileri hello hello adımları yürütün.

1. Hello Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri (Klasik)** > **DNS01**  >   **Tüm ayarları** > **IP adreslerini** ve IP adresi ve IP adresi ataması aşağıda görüldüğü gibi hello dikkat edin.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Nasıl tooremove bir statik özel IP adresi bir sanal makineden
tooremove hello statik özel IP adresinden yukarıda, VM oluşturduğunuz hello hello adımları izleyin.

1. Hello gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** toohello sağ **IP adresi ataması**, ardından **kaydetmek**ve ardından tıklatın **Evet**.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Nasıl tooadd statik özel IP adresi VM varolan tooan
tooadd bir statik özel IP adresi toohello hello yukarıdaki adımları kullanarak oluşturulan VM hello adımları izleyin:

1. Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** sağında toohello **IP adresi ataması**.
2. Tür *192.168.1.101* için **IP adresi**, ardından **kaydetmek**ve ardından **Evet**.

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

