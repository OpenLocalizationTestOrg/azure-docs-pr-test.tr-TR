---
title: "Azure DevTest Labs aaaConfigure Azure Market görüntü ayarlarında | Microsoft Docs"
description: "Hangi Azure Marketi görüntüleri bir VM Azure DevTest Labs'de oluşturulurken kullanılan yapılandırma"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>Azure DevTest Labs'de Azure Market görüntü ayarlarını yapılandırma
DevTest Labs Laboratuvar içinde kullanılan Azure Market görüntülerini toobe nasıl yapılandırdığınıza bağlı olarak Azure Market görüntüsünü temel oluşturma Vm'leri destekler. Bu makale size nasıl gösterir, varsa, Azure Market görüntülerini olabilecek toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır. Bu, ekibinizin yalnızca ihtiyaç duydukları erişim toohello Market görüntülerini sahip olmasını sağlar. 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>Bir VM oluşturulurken hangi Azure Market görüntülerini verileceğini seçin
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin. 
4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma ve ilkeleri**.
5. Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** altında dikey **sanal makine tabanları**seçin **Market görüntülerini**.
6. Tam Azure Market görüntülerini toobe yeni bir VM temeli olarak kullanmak için kullanılabilir tüm hello isteyip istemediğinizi belirtin. Seçerseniz **Evet**, ardından tüm hello Azure Market görüntülerini tüm hello ölçütleri karşılayan verilir hello laboratuar ortamında:
   
   * Merhaba görüntüsünü oluşturur tek bir VM'ye **ve**
   * Merhaba görüntüsünü kullanan Azure Resource Manager tooprovision VM'ler **ve**
   * Hello görüntü ek lisans planı satın almayı gerektirmez
     
    İzin verilen hiçbir görüntüleri toobe istediğiniz veya hangi görüntüleri seçin, kullanılabilir toospecify isterseniz **Hayır**.
     
     ![Seçenek tooallow tüm Market görüntülerini toobe temel görüntü olarak VM'ler için kullanılır](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. Seçerseniz **Hayır** toohello önceki adım, hello **izin verilen görüntüleri/seçmek tüm** onay kutusunu etkindir. 
   Merhaba arama kutusu tooquickly seçin birlikte bu seçeneği kullanın veya hello listesinde görüntülenen tüm hello öğelerin seçimini kaldırın.
   * Tooallow VM oluşturmak için ayrı ayrı her görüntünün karşılık gelen onay kutusunu işaretleyerek istediğiniz hello Azure Market görüntülerini seçin.
   * Merhaba laboratuar ortamında kullanılan tüm Azure Marketi görüntüleri toobe tooallow istemiyorsanız, hiçbir şey hello listeden seçin.
   
    ![Hangi Azure Market görüntülerini VM'ler için temel görüntü olarak kullanılabilir belirtebilirsiniz](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bir VM oluşturulurken Azure Market görüntülerini nasıl verildiğini yapılandırdıktan sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).

