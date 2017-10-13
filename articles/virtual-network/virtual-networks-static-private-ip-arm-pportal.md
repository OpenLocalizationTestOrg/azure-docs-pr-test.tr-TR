---
title: "Özel IP adresleri VM'ler - Azure portal için yapılandırma | Microsoft Docs"
description: "Azure Portalı'nı kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
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
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a>Azure Portalı'nı kullanarak bir sanal makine için özel IP adreslerini yapılandırın

> [!div class="op_single_selector"]
> * [Azure portal](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure portal (Klasik)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (Klasik)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI (Klasik)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede Resource Manager dağıtım modeli anlatılmaktadır. Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

Aşağıdaki örnek adımları zaten oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği adımları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a>Özel statik IP adresleri test etmek için bir VM oluşturma
Azure portalı kullanarak bir VM Resource Manager dağıtım modunda oluşturulması sırasında özel bir statik IP adresi ayarlanamıyor. VM önce oluşturmanız gerekir, statik olarak kendi özel IP tehn ayarlayın.

Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet*, aşağıdaki adımları izleyin.

1. Tarayıcıdan http://portal.azure.com adresine gidin ve gerekiyorsa Azure hesabınıza giriş yapın.
2. Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, dikkat **dağıtımmodeliseçin** listesinde zaten gösterir **Resource Manager**ve ardından **oluşturma**, aşağıdaki şekilde görüldüğü gibi.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. İçinde **Temelleri** dikey penceresinde oluşturulacak VM adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası, aşağıdaki şekilde görüldüğü gibi.
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Emin olun **konumu** seçili *Orta ABD*, ardından **Varolanı seç** altında **kaynak grubu**, ardından**Kaynak grubu** yeniden, ardından *TestRG*ve ardından **Tamam**.
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. İçinde **bir boyutu seçin** dikey penceresinde, select **A1 standart**ve ardından **seçin**.
   
    ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. İçinde **ayarları** dikey penceresinde, aşağıdaki özellikleri ayarlanmadığından emin olun değerleriyle ayarlanır ve ardından **Tamam**.
   
    -**Depolama hesabı**: *vnetstorage*
   
   * **Ağ**: *TestVNet*
   * **Alt ağ**: *ön uç*
     
     ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. İçinde **Özet** dikey penceresinde tıklatın **Tamam**. Panonuzda görüntülenen döşemenin aşağıdaki dikkat edin.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a>Bir VM için özel statik IP adresi bilgilerini alma
Yukarıdaki adımları ile oluşturulan sanal makine için statik özel IP adresi bilgilerini görüntülemek için aşağıdaki adımları yürütün.

1. Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri** > **DNS01** > **tüm ayarlar**   >  **Ağ arabirimleri** ve listelenen yalnızca ağ arabirimi'ı tıklatın.
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. İçinde **ağ arabirimi** dikey penceresinde tıklatın **tüm ayarları** > **IP adreslerini** ve fark **atama** ve  **IP adresi** değerleri.
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a>Mevcut bir VM'yi özel bir statik IP adresi ekleme
Yukarıdaki adımları kullanılarak oluşturulan VM için özel bir statik IP adresi eklemek için aşağıdaki adımları izleyin:

1. Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** altında **atama**.
2. Tür *192.168.1.101* için **IP adresi**ve ardından **kaydetmek**.
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> ' I tıklattıktan sonra IF **kaydetmek** atama hala ayarlanır fark **dinamik**, yazdığınız IP adresi zaten kullanımda olduğunu gösterir. Farklı bir IP adresi deneyin.
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a>Özel bir statik IP adresi bir VM'den kaldırma
Özel statik IP adresi yukarıda oluşturduğunuz sanal makineden kaldırmak için aşağıdaki adımı tamamlayın:

Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** altında **atama**ve ardından **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

