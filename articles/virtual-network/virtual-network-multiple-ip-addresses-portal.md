---
title: "Azure sanal makineleri - Portal için aaaMultiple IP adreslerini | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin tooa kullanarak sanal makine hello Azure portalı | Resource Manager."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Birden çok IP adresleri toovirtual makine Hello Azure portal kullanarak atayın

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Bu makalede nasıl toocreate hello Azure Resource Manager dağıtım modeli kullanılarak aracılığıyla sanal makine (VM) hello Azure portal açıklanmaktadır. Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz. Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma

Birden çok IP adresi ya da özel bir statik IP adresi bir VM'yi toocreate istiyorsanız, PowerShell veya hello Azure CLI kullanarak oluşturmanız gerekir. Merhaba PowerShell veya CLI Seçenekleri Bu makale toolearn hello üstündeki nasıl tıklayın. Tek bir dinamik özel IP adresi ve (isteğe bağlı) hello hello adımları izleyerek hello portal kullanarak tek bir ortak IP adresi ile bir VM oluşturma [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md) veya [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-portal.md) makaleler. Merhaba VM oluşturduktan sonra başlangıç IP adresi türü dinamik toostatic değiştirin ve hello içindeki adımları izleyerek hello portal'ı kullanarak ek IP adreslerini ekleyin [eklemek IP adresleri tooa VM](#add) bu makalenin.

## <a name="add"></a>IP adreslerini tooa VM ekleme

Özel ve genel IP adresleri tooa NIC izleyin hello adımları tamamlayarak ekleyebilirsiniz. Merhaba hello bölümleri aşağıdaki örneklerde, zaten bir VM hello açıklanan hello üç IP yapılandırmasına sahip olduğunu varsayın [senaryo](#Scenario) Bu makale, ancak gerekli değildir, yapın.

### <a name="coreadd"></a>Çekirdek adımları

1. Toohello https://portal.azure.com ve oturum Azure portalında, gerekirse göz atın.
2. Merhaba Portalı'nda tıklatın **daha fazla hizmet** > türü *sanal makineleri* hello filtre kutusuna ve ardından **sanal makineleri**.
3. Merhaba, **sanal makineleri** dikey penceresinde, VM, istediğiniz tooadd IP adreslerinin hello'ı tıklatın. Tıklatın **ağ arabirimleri** görünür hello sanal makine dikey ve ardından hello ağ arabirimi, istediğiniz tooadd hello IP adresleri için. Merhaba örnekte hello gösterilen resim, aşağıdaki hello adlı NIC *myNIC* hello adlı VM gelen *myVM* seçilir:

    ![Ağ arabirimi](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Görüntülenen hello dikey penceresinde hello Seçtiğiniz NIC için tıklayın **IP yapılandırmaları**.

Tam hello izleyin hello bölümlerden biri adımlar, başlangıç IP adresi türüne göre tooadd istersiniz.

### <a name="add-a-private-ip-address"></a>**Özel bir IP adresi Ekle**

Aşağıdaki adımları tooadd yeni bir özel IP adresi hello tamamlayın:

1. Tam hello adımları hello [çekirdek adımları](#coreadd) bu makalenin.
2. **Ekle**'ye tıklayın. Merhaba, **eklemek IP yapılandırması** görünür, dikey penceresi oluşturma adlı IP yapılandırması *IPConfig 4* ile *10.0.0.7* olarak bir *statik* Özel IP adresi ve ardından **Tamam**.

    > [!NOTE]
    > Statik bir IP adresi eklerken, NIC bağlı hello alt hello üzerinde kullanılmayan, geçerli bir adresi belirtmeniz gerekir. Seçtiğiniz hello adresi kullanılabilir değilse, hello portal hello IP adresi için bir X işareti gösterilir ve farklı bir tooselect gerekir.

3. Tamam'ı tıklattığınızda hello dikey penceresi kapanır ve hello listelenen yeni IP yapılandırması görürsünüz. Tıklatın **Tamam** tooclose hello **eklemek IP yapılandırması** dikey.
4. Tıklayabilirsiniz **Ekle** tooadd ek IP yapılandırmaları veya kapat tüm dikey pencereleri toofinish ekleme IP adreslerini açın.
5. Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.

### <a name="add-a-public-ip-address"></a>Bir ortak IP adresi Ekle

Bir ortak IP adresi, bir ortak IP adresi kaynak tooeither yeni bir IP yapılandırması veya var olan IP yapılandırmasını ilişkilendirerek eklenir.

> [!NOTE]
> Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.
> 

### <a name="create-public-ip"></a>Bir ortak IP adresi kaynağı oluşturun

Bir ortak IP adresi, bir ortak IP adresi kaynağı için bir ayardır. İstediğiniz şu anda ilişkili tooan IP yapılandırması değil genel bir IP adresi kaynağı varsa tooassociate tooan IP yapılandırması, hello aşağıdaki adımları atlayın ve gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımları tamamlayın. Kullanılabilir bir ortak IP adresi kaynak yoksa, aşağıdaki adımları toocreate bir hello tamamlayın:

1. Toohello https://portal.azure.com ve oturum Azure portalında, gerekirse göz atın.
3. Merhaba Portalı'nda tıklatın **yeni** > **ağ** > **genel IP adresi**.
4. Merhaba, **ortak IP adresi oluştur** görünür, dikey girin bir **adı**seçin bir **IP adresi ataması** türü, bir **abonelik**, **Kaynak grubu**ve bir **konumu**, ardından **oluşturma**hello resim aşağıdaki gösterildiği gibi:

    ![Bir ortak IP adresi kaynağı oluşturun](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Tam hello tooassociate hello ortak IP adresi kaynak tooan IP yapılandırması izleyin hello bölümlerden biri adımları.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Merhaba ortak IP adresi kaynak tooa yeni IP yapılandırmasını ilişkilendirin

1. Tam hello adımları hello [çekirdek adımları](#coreadd) bu makalenin.
2. **Ekle**'ye tıklayın. Merhaba, **eklemek IP yapılandırması** görünür, dikey penceresi oluşturma adlı IP yapılandırması *IPConfig 4*. Merhaba etkinleştirmek **genel IP adresi** ve var olan, kullanılabilir ortak IP adresi kaynağı hello seçin **genel IP adresi seçin** görünür dikey.

    Merhaba ortak IP adresi kaynağı seçtikten sonra tıklatın **Tamam** ve hello dikey kapatılacak. Var olan bir ortak IP adresi yoksa, bir hello hello adımları tamamlayarak oluşturabilirsiniz [ortak IP adresi kaynak oluşturma](#create-public-ip) bu makalenin. 

3. Gözden geçirme hello yeni IP yapılandırması. Özel bir IP adresi açıkça atanan değildi olsa bile, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiğinden bir otomatik olarak toohello IP yapılandırması atandı.
4. Tıklayabilirsiniz **Ekle** tooadd ek IP yapılandırmaları veya kapat tüm dikey pencereleri toofinish ekleme IP adreslerini açın.
5. İşletim sisteminizin hello hello adımları tamamlayarak Hello özel IP adresi toohello VM işletim sistemi Ekle [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresi toohello işletim sistemi eklemeyin.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Merhaba ortak IP adresi kaynak tooan mevcut IP yapılandırmasını ilişkilendirin

1. Tam hello adımları hello [çekirdek adımları](#coreadd) bu makalenin.
2. Tooadd hello ortak IP adresi kaynağı için istediğiniz hello IP Yapılandırması'nı tıklatın.
3. Görüntülenen hello IPConfig dikey penceresinde tıklayın **IP adresi**.
4. Merhaba, **genel IP adresi seçin** görünür, dikey penceresinde bir ortak IP adresi seçin.
5. Tıklatın **kaydetmek** ve hello dikey pencereler kapatılacak. Var olan bir ortak IP adresi yoksa, bir hello hello adımları tamamlayarak oluşturabilirsiniz [ortak IP adresi kaynak oluşturma](#create-public-ip) bu makalenin.
3. Gözden geçirme hello yeni IP yapılandırması.
4. Tıklayabilirsiniz **Ekle** tooadd ek IP yapılandırmaları veya kapat tüm dikey pencereleri toofinish ekleme IP adreslerini açın. Merhaba ortak IP adresi toohello işletim sistemi eklemeyin.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
