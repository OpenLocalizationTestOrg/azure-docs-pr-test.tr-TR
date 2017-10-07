---
title: Azure DevTest Labs laboratuvarda aaaCreate | Microsoft Docs
description: "Sanal makineler için Azure DevTest Labs'de bir laboratuvar oluşturma"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs'de laboratuvar oluşturma
Sınırları ve kotalar belirterek daha iyi olanak sağlayan sanal makineler (VM'ler), bu kaynakları yönetmek gibi Azure DevTest Labs laboratuvarda kaynakları, bir grup kapsayan hello altyapısıdır. Bu makalede hello Azure portal kullanarak bir laboratuvar oluşturma hello işleminde size kılavuzluk eder.

## <a name="prerequisites"></a>Ön koşullar
toocreate bir laboratuvar, şunlar gerekir:

* Azure aboneliği. Azure satın alma seçenekleri hakkında toolearn bkz [nasıl toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) veya [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/). Merhaba abonelik toocreate hello Laboratuvar hello sahibi olmanız gerekir.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Adımları toocreate Azure DevTest Labs laboratuvarda
Aşağıdaki adımları hello nasıl toouse hello Azure portal toocreate Azure DevTest Labs laboratuvarda gösterilmektedir. 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Merhaba ana menüden hello sol tarafında seçin **daha Hizmetleri** (sonundaki hello hello listesi).

    ![Diğer hizmetler menü seçeneği](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Kullanılabilir hizmetler hello listesinden **DevTest Labs**.
1. Merhaba üzerinde **DevTest Labs** dikey penceresinde, select **Ekle**.
   
    ![Laboratuvar ekleme](./media/devtest-lab-create-lab/add-lab-button.png)

1. Merhaba üzerinde **DevTest Lab Oluştur** dikey penceresinde:
   
    1. Girin bir **Laboratuvar adı** hello yeni Laboratuvar için.
    2. Select hello **abonelik** tooassociate hello Laboratuvar ile.
    3. Seçin bir **konumu** hangi toostore hello laboratuarda.
    4. Seçin **otomatik kapatma** toospecify tooenable - isterseniz ve hello parametrelerini - tanımlayın hello otomatik tüm hello Laboratuvar'ın Vm'leri kapatılıyor. Merhaba otomatik kapatma özelliği yapabildiği belirtebilirsiniz VM hello istediğinizde çoğunlukla bir maliyet tasarrufu özelliğidir tooautomatically kapatıldı. Merhaba makalede açıklanan başlangıç adımları izleyerek hello Laboratuvar oluşturduktan sonra otomatik kapatma ayarları değiştirebilirsiniz [Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetmek](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Seçin **PIN tooDashboard** hello Laboratuvar tooappear hello portal panosunda, bir kısayol istiyorsanız.
    6. Seçin **Otomasyon seçenekleri** tooget Azure Resource Manager şablonları yapılandırma Otomasyon için. 
    7. **Oluştur**’u seçin. Seçtikten sonra **oluşturma**, hello **DevTest Labs** dikey penceresinde görüntüler. Merhaba izleyerek hello Laboratuvar oluşturma işlemi hello durumunu izleyebilirsiniz **bildirimleri** alanı. Tamamlandığında, yenileme hello sayfa toosee hello Laboratuvar hello labs listesinde yeni oluşturulan.  
    
    ![Laboratuvar dikey penceresi oluşturma](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
Laboratuvarınızı oluşturduktan sonra bazı sonraki adımları tooconsider şunlardır:

* [Güvenli erişim tooa Laboratuvar](devtest-lab-add-devtest-user.md).
* [Laboratuvar ilkeleri belirleme](devtest-lab-set-lab-policy.md).
* [Laboratuvar şablonu oluşturma](devtest-lab-create-template.md).
* [VM'leriniz için özel yapılar oluşturma](devtest-lab-artifact-author.md).
* [Yapıları tooa Laboratuvar'yle bir VM'yi eklemek](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

