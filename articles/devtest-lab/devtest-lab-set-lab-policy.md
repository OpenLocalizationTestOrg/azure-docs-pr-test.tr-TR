---
title: Azure DevTest Labs aaaManage Laboratuvar ilkeleri | Microsoft Docs
description: "Bilgi toodefine Laboratuvar ilkeleri gibi VM boyutları nasıl kullanıcı başına en fazla VM'ler ve kapatma Otomasyon."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetme

Azure DevTest Labs maliyet denetlemek ve atık, ortamlarındaki ilkeleri (ayarlar) yöneterek her Laboratuvar için en aza indirmenize olanak sağlar. Bu makalede, adım adım ayrıntılı olarak açıklanmaktadır nasıl tooset her ilke.  

## <a name="set-allowed-virtual-machine-sizes"></a>Sanal makine boyutlarını izin kümesi
Hello İlkesi ayarı hello için VM boyutları yardımcı toominimize Laboratuvar hangi VM boyutları hello laboratuvarda izin verilen toospecify etkinleştirerek boşa harcanmasına izin. Bu ilke etkinleştirilirse, yalnızca VM boyutları bu listeden kullanılan toocreate VM'ler olabilir.

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **sanal makine boyutları izin**.
   
    ![İzin verilen sanal makine boyutları](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.

1. Bu ilkeyi etkinleştirirseniz, laboratuvarınızda oluşturulabilmesi için bir veya daha fazla VM boyutları seçin.

1. **Kaydet**’i seçin.

## <a name="set-virtual-machines-per-user"></a>Kullanıcı başına kümesi sanal makineler
Hello İlkesi **kullanıcı başına sanal makineler** toospecify hello en fazla ayrı bir kullanıcı tarafından oluşturulan VM'ler sağlar. Merhaba Kullanıcı sınırı sağlandığında bir kullanıcı toocreate veya talep VM çalışırsa, bir hata iletisi VM oluşturulan/talep edilemez edilmesine bu hello gösterir. 

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Seçin **Evet** toolimit hello VM'lerin sayısını kullanıcı başına. Kullanıcı başına VM'ler toolimit hello numarasını istemiyorsanız seçin **Hayır**. Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin. 

1. Seçin **Evet** toolimit hello SSD (katı hal disk) kullanabilirsiniz VM sayısı. Toolimit hello SSD kullanabilirsiniz VM'lerin sayısını istemiyorsanız seçin **Hayır**. Seçerseniz **Evet**, SSD kullanılarak oluşturulabilir VM'ler hello sayısını belirten bir değer girin. 

1. **Kaydet**’i seçin.

## <a name="set-virtual-machines-per-lab"></a>Laboratuvar başına kümesi sanal makineler
Hello İlkesi **Laboratuvar başına sanal makine** hello geçerli Laboratuvar için toospecify hello maksimum oluşturulabilecek VM'lerin sayısını sağlar. Bir kullanıcı Hello Laboratuvar sınırı sağlandığında toocreate VM çalışırsa, bir hata iletisi VM oluşturulamıyor, hello gösterir. 

1. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **Laboratuvar başına sanal makine**.
   
    ![Laboratuvar başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Seçin **Evet** toolimit hello VM'lerin sayısını Laboratuvar başına. Toolimit hello VM'lerin sayısını Laboratuvar başına istemiyorsanız seçin **Hayır**. Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin. 

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

## <a name="set-expiration-date"></a>Sona erme tarihi ayarlama
Bir süre sonu ayarlayabilirsiniz ne zaman tarih, [hello VM oluşturma](devtest-lab-add-vm.md). İçinde **Gelişmiş ayarları**, üzerinde VM hello tarih otomatik olarak silinmesini hello Takvim simgesi toospecify seçin.  Varsayılan olarak, hello VM asla sona erecek.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
Uygulanan ve yapılandırdığınız tanımlanan sonra laboratuvarınız için çeşitli VM ilke ayarları Merhaba, İşte bazı şeyleri tootry sonraki:

* [Paylaşılan IP adreslerini anlamak](devtest-lab-shared-ip.md) -paylaşılan IP açıklar adresleri DevTest Labs toominimize hello sayısında ortak IP adresleri gerekli tooconnect tooyour Laboratuvar VM'ler kullanılır.
* [Maliyet yönetimini yapılandırma](devtest-lab-configure-cost-management.md) -gösterilmektedir nasıl toouse hello **aylık tahmini maliyet eğilimi** grafiği  
  tooview, geçerli ayın tahmini maliyet-to-date ve öngörülen hello ayın son maliyet hello.
* [Özel görüntü oluşturma](devtest-lab-create-template.md) - bir VM oluşturduğunuzda, özel bir görüntü veya bir Market görüntüsü olabilecek bir taban belirtin. Bu makalede nasıl toocreate özel bir görüntü bir VHD dosyasından gösterilmektedir.
* [Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) - VMs Azure Market görüntülerini temel oluşturmayı Azure DevTest Labs destekler. Bu makalede gösterilmektedir nasıl olabilen, varsa, Azure Market görüntülerini toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır.
* [Bir laboratuar ortamında bir VM oluşturma](devtest-lab-add-vm-with-artifacts.md) -gösterilmektedir nasıl toocreate temel görüntü bir VM'den (ya da özel veya Market) ve nasıl toowork yapıtlarla birlikte, VM.

