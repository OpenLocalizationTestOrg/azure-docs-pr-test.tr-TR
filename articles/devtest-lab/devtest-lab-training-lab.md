---
title: "Eğitim için Azure DevTest Labs aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DevTest Labs eğitim senaryoları için."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>Azure DevTest Labs için eğitim kullanın
Azure DevTest Labs kullanılan tooimplement toplama toodev ve test birçok anahtar senaryolarda olabilir. Bu senaryolarda bir laboratuvar eğitim için yukarı tooset biridir. Azure DevTest Labs toocreate özel şablonlar sağlayabileceğiniz bir laboratuvar verir her Yardımcısı toocreate aynı ve yalıtılmış ortamlar için eğitim kullanabilirsiniz. Yalnızca bunları ihtiyaç duydukları ve sanal makineleri için hello eğitim gerekli gibi-yeterli kaynak - içeren kullandığınızda eğitim ortamları kullanılabilir tooeach Yardımcısı olduğunu ilkeleri tooensure uygulayabilirsiniz. Son olarak, tek bir tıklatmayla erişebilirsiniz trainees ile kolayca hello Laboratuvar paylaşabilirsiniz.

![DevTest Labs için eğitim kullanın](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure DevTest Labs herhangi bir sanal ortam gerekli tooconduct Eğitim gereksinimleri aşağıdaki hello uyuyor: 

* Trainees diğer trainees tarafından oluşturulan VM'ler göremiyorum
* Her eğitim makine özdeş olmalıdır
* Trainees eğitim ortamlarının hızlı bir şekilde sağlayabilirsiniz
* Bunları kullanmıyorsanız, bunlar hello eğitim ve ayrıca kapatma VM'ler için gerekenden daha fazla VMs trainees alınamıyor sağlayarak maliyet denetimi
* Merhaba eğitim Laboratuvar her Yardımcısı ile kolayca paylaşın
* Merhaba eğitim Laboratuvar yeniden yeniden

Bu makalede, Eğitim gereksinimleri ve eğitim için bir laboratuvar yukarı tooset izleyebileceğiniz ayrıntılı adımlar toomeet hello daha önce açıklanan kullanılabilen çeşitli Azure DevTest Labs özelliklerini öğrenin.  

## <a name="implementing-training-with-azure-devtest-labs"></a>Azure DevTest Labs eğitime uygulama
1. **Merhaba Laboratuvar oluşturma** 
   
    Labs hello Azure DevTest Labs'de başlangıç noktası var. Bir laboratuvar oluşturduktan sonra görevleri hızla oluşturabilirsiniz VM görüntüleri gibi kullanıcıların (trainees) toohello Laboratuvar, kümesi ilkeleri toocontrol maliyetleri ekledikçe tanımlayın ve daha fazlasını gerçekleştirebilirsiniz.   
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de Laboratuvar oluşturma](devtest-lab-create-lab.md) |Azure DevTest Labs'de Laboratuvar bir toocreate hello Azure portalına nasıl öğrenin. |
2. **Eğitim VM'ler hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma** 
   
    Görüntüler çok geniş bir yelpazedeki hazır görüntülerden hello Azure Marketi seçer ve hello laboratuarda hello trainees için kullanılabilir duruma getirmek. Merhaba hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar Azure hello Laboratuvar özel görüntü olarak hello VM kaydetme ve hello eğitim için gereken tüm hello yazılım yükleme Marketi'nden hazır bir görüntü kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure Market görüntülerini yapılandırın](devtest-lab-configure-marketplace-images.md) |Beyaz liste Azure Market görüntülerini öğrenin; Seçimi yalnızca hello görüntüler için kullanılabilir hale getirme için hello eğitim istiyor. |
   | [Özel bir görüntü oluşturun](devtest-lab-create-template.md) |Özel bir görüntü trainees hızlı bir şekilde hello özel görüntü kullanarak bir VM'i oluşturabilmeniz için hello eğitim ihtiyacınız hello yazılım yüklenerek oluşturun. |
3. **Eğitim makineler için yeniden kullanılabilir şablonlar oluşturma** 
   
    Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır. Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz. Her Yardımcısı hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs formüller toocreate sanal makineleri yönetme](devtest-lab-manage-formulas.md) |Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin. |
4. **Denetim maliyetleri**
   
    Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda Yardımcısı tarafından oluşturulan sanal makineleri tooset bir ilke sağlar. 
   
    Birden çok gün eğitim gerçekleştirme ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden, kolayca otomatik kapatma ayarı tarafından gerçekleştirmek ve otomatik başlatma hello Laboratuvar ilkeleri. 
   
    Eğitim tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Laboratuvar ilkelerini tanımlama](devtest-lab-set-lab-policy.md) |Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz. |
   | [Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Merhaba eğitim tamamlandığında, tek bir işlemde tüm hello labs silin. |
5. **Paylaşım hello laboratuvarla her Yardımcısı**
   
    Labs, trainees ile paylaştığınız bir bağlantıyı kullanarak doğrudan erişilebilir. Sahip oldukları sürece, trainees bile toohave bir Azure hesabınız yoksa bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account). Trainees diğer trainees tarafından oluşturulan VM'ler göremezsiniz.  
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de Yardımcısı tooa Laboratuvar ekleme](devtest-lab-add-devtest-user.md) |Hello Azure portal tooadd trainees tooyour eğitim Laboratuvar kullanın. |
   | [Bir PowerShell Betiği kullanılarak trainees toohello Laboratuvar ekleme](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |PowerShell tooautomate trainees tooyour eğitim Laboratuvar ekleme kullanın. |
   | [Bir bağlantı toohello Laboratuvar Al](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Nasıl bir laboratuvar doğrudan bir köprü erişilebilen öğrenin. |
6. **Merhaba Laboratuvar yeniden yeniden** 
   
    Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Resource Manager şablonu kullanarak bir laboratuvar oluşturma](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

