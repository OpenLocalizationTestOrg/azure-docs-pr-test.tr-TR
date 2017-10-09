---
title: Azure DevTest Labs aaaManage temel Laboratuvar ilkeleri | Microsoft Docs
description: "Bilgi nasıl tooset bazı DevTest Labs laboratuvarda için hello temel ilkeleri (ayarlar)"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs laboratuvarda için temel ilkelerini yönetme

Azure DevTest Labs, ortamlarındaki atık ilkeleri (ayarlar) yöneterek her Laboratuvar için en aza indirmek ve toocontrol maliyeti sağlar. Bu makalede, nasıl tooset iki hello en kritik ilkeleri - sınırlama sayısı hello öğrenerek ilkelerini kullanmaya başlama sanal oluşturduğunuz ya da bir tek kullanıcı ve yapılandırılırken otomatik kapatma tarafından talep makineler (VM). tooview nasıl tooset her Laboratuvar ilke hello makalesine bakın [Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Azure DevTest Labs Laboratuvar 's ilkelerinde erişme
Merhaba aşağıdaki adımlar, Azure DevTest Labs laboratuvarda ilkelerini kurma yol:

tooview (ve değişiklik) hello ilkeleri bir laboratuvar için şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.

1. Merhaba istenen Laboratuvar labs Hello listeden seçin.   

1. Seçin **yapılandırma ve ilkeleri**.

    ![İlke ayarları dikey penceresini](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Merhaba **yapılandırma ve ilkeleri** dikey belirleyebileceğiniz ayarlar menüsünü içerir. Bu makalede yalnızca hello ayarlarını kapsar **kullanıcı başına sanal makineler** ve **otomatik kapatma**. toolearn ayarları, kalan hello hakkında bkz [Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetmek](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Kullanıcı başına kümesi sanal makineler
Hello İlkesi **kullanıcı başına sanal makineler** toospecify hello en fazla ayrı bir kullanıcı tarafından oluşturulan VM'ler sağlar. Merhaba Kullanıcı sınırı sağlandığında bir kullanıcı toocreate veya talep VM çalışırsa, bir hata iletisi VM oluşturulan/talep edilemez edilmesine bu hello gösterir. 

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Seçin **Evet** toolimit hello VM'lerin sayısını kullanıcı başına. Kullanıcı başına VM'ler toolimit hello numarasını istemiyorsanız seçin **Hayır**. Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin. 

1. Seçin **Evet** toolimit hello SSD (katı hal disk) kullanabilirsiniz VM sayısı. Toolimit hello SSD kullanabilirsiniz VM'lerin sayısını istemiyorsanız seçin **Hayır**. Seçerseniz **Evet**, SSD kullanılarak oluşturulabilir VM'ler hello sayısını belirten bir değer girin. 

1. **Kaydet**’i seçin.

## <a name="set-auto-shutdown"></a>Set otomatik-kapatma
Merhaba otomatik kapatma ilke bu Laboratuvar ait VM'ler kapatma toospecify hello zaman sağlayarak boşa harcanmasına toominimize Laboratuvar yardımcı olur.

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik kapatma**.
   
    ![Otomatik kapatma](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.

1. Bu ilkeyi etkinleştirirseniz, tüm VM'ler aşağı hello saat (ve saat dilimi) tooshut hello geçerli laboratuvarda belirtin.

1. Belirtin **Evet** veya **Hayır** hello seçeneği toosend için otomatik kapatma süresi bir bildirim 15 dakika önceki toohello belirtildi. Belirtirseniz **Evet**, bir Web kancası URL'si uç nokta tooreceive hello bildirim girin. Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası veya API Azure işlevi oluşturma](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. **Kaydet**’i seçin.

    Etkinleştirildiğinde, varsayılan olarak, bu ilke tooall VM'ler hello geçerli laboratuarda uygulanır. Bu ayar için belirli bir VM'yi tooremove açmak hello VM'in dikey penceresinde ve değişiklik kendi **otomatik kapatma** ayarı 

## <a name="set-auto-start"></a>Otomatik başlangıcı Ayarla
Merhaba VM'ler hello geçerli laboratuarda yeniden başlatıldığında hello otomatik başlatma ilkesi, toospecify sağlar.  

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik başlatma**.
   
    ![Otomatik başlatma](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.

3. Bu ilkeyi etkinleştirirseniz, hello zamanlanmış başlangıç saati, saat dilimi ve hello için hangi hello zaman geçerlidir hello haftanın günleri belirtin. 

4. **Kaydet**’i seçin.

    Etkinleştirildikten sonra bu ilke otomatik olarak uygulanan tooany VM'ler hello geçerli laboratuvarda değil. tooapply bu ayarı tooa belirli VM, açık hello VM'in dikey ve değişiklik kendi **otomatik başlatma** ayarı 

## <a name="next-steps"></a>Sonraki adımlar

- [Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md) -öğrenin nasıl toomodify diğer Laboratuvar ilkeleri 
