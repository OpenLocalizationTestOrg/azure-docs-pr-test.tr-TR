---
title: "aaaConfigure özel IP adresleri VM'ler - Azure portalı | Microsoft Docs"
description: "Tooconfigure özel IP adresleri kullanarak sanal makineleri için Azure portalını nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir sanal makine için özel IP adreslerini yapılandırın

> [!div class="op_single_selector"]
> * [Azure portal](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure portal (Klasik)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (Klasik)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI (Klasik)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Merhaba örnek adımları zaten oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği toorun hello adımları istiyorsanız, ilk derleme açıklandığı hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Nasıl toocreate statik özel IP test etmek için bir VM adresleri
Hello Azure portal kullanarak bir VM hello Resource Manager dağıtım modunda hello oluşturulması sırasında özel bir statik IP adresi ayarlanamıyor. Merhaba VM önce oluşturmanız gerekir, kendi özel IP toobe tehn statik olarak ayarlayın.

toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet*, hello adımları izleyin.

1. Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.
2. Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, o hello fark **dağıtımmodeliseçin** listesinde zaten gösterir **Resource Manager**ve ardından **oluşturma**hello aşağıdaki çizimde görüldüğü gibi.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. Merhaba, **Temelleri** dikey penceresinde hello VM toobe oluşturulan hello adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası, hello aşağıdaki çizimde görüldüğü gibi hello.
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Hello emin olun **konumu** seçili *Orta ABD*, ardından **Varolanı seç** altında **kaynak grubu**, ardından**Kaynak grubu** yeniden, ardından *TestRG*ve ardından **Tamam**.
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. Merhaba, **bir boyutu seçin** dikey penceresinde, select **A1 standart**ve ardından **seçin**.
   
    ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. İçinde **ayarları** dikey penceresinde, aşağıdaki özelliklere yapma emin hello ayarlanır aşağıdaki hello değerleri ile ayarlanır ve ardından **Tamam**.
   
    -**Depolama hesabı**: *vnetstorage*
   
   * **Ağ**: *TestVNet*
   * **Alt ağ**: *ön uç*
     
     ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. Merhaba, **Özet** dikey penceresinde tıklatın **Tamam**. Panonuzda görüntülenen bildirim hello döşeme aşağıdaki.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi
VM yukarıdaki hello adımları ile oluşturulan tooview hello statik özel IP adresi bilgileri hello hello adımları yürütün.

1. Hello Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri** > **DNS01** > **tüm ayarları** > **ağ arabirimleri** ve listelenen hello yalnızca ağ arabirimi'ı tıklatın.
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. Merhaba, **ağ arabirimi** dikey penceresinde tıklatın **tüm ayarları** > **IP adreslerini** ve bildirim hello **atama** ve **IP adresi** değerleri.
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Nasıl tooadd statik özel IP adresi VM varolan tooan
tooadd bir statik özel IP adresi toohello hello yukarıdaki adımları kullanarak oluşturulan VM hello adımları izleyin:

1. Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** altında **atama**.
2. Tür *192.168.1.101* için **IP adresi**ve ardından **kaydetmek**.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> ' I tıklattıktan sonra IF **kaydetmek** hello atama hala çok ayarlandığına dikkat edin**dinamik**, yazdığınız başlangıç IP adresi zaten kullanımda olduğunu gösterir. Farklı bir IP adresi deneyin.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Nasıl tooremove bir statik özel IP adresi bir sanal makineden
tooremove hello statik özel IP adresinden yukarıda, VM oluşturduğunuz hello adım aşağıdaki hello tamamlayın:

Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** altında **atama**ve ardından **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

