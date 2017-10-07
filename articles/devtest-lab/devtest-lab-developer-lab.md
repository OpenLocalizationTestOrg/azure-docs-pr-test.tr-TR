---
title: "Geliştiriciler için Azure DevTest Labs aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DevTest Labs Geliştirici senaryoları için."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a>Geliştiriciler için Azure DevTest Labs kullanın
Azure DevTest Labs birçok senaryoları ancak hello birincil senaryoları birini içerir geliştiriciler için DevTest Labs toohost geliştirme makineleri kullanarak kullanılan tooimplement olabilir. Bu senaryoda, DevTest Labs şu avantajları sağlar:

- Geliştiriciler, geliştirme makinelerinin isteğe bağlı olarak hızlı bir şekilde sağlayabilirsiniz.
- Geliştiriciler, geliştirme makinelerinin gerektiğinde kolayca özelleştirebilirsiniz.
- Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:
  - Geliştiriciler, geliştirme için gerekenden daha fazla VMs alınamıyor.
  - Sanal makineleri ne zaman kullanılmıyor kapatılır. 

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

Bu makalede kullanılan toomeet geliştirici gereksinimleri ve bir laboratuvar yukarı tooset izleyebileceğiniz ayrıntılı adımlar hello çeşitli Azure DevTest Labs özellikleri hakkında bilgi edinin.

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a>Azure DevTest Labs Geliştirici ortamlarıyla uygulama
1. **Merhaba Laboratuvar oluşturma** 
   
    Labs hello Azure DevTest Labs'de başlangıç noktası var. Bir laboratuvar oluşturduktan sonra kullanıcılar (geliştiriciler) toohello Laboratuvar, hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama, ayar ilkeleri toocontrol maliyetleri ve daha fazlasını ekleme gibi görevleri gerçekleştirebilirsiniz.  
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de Laboratuvar oluşturma](devtest-lab-create-lab.md) |Azure DevTest Labs'de Laboratuvar bir toocreate hello Azure portalına nasıl öğrenin. |
2. **Sanal makineleri hazır Market görüntülerini ve özel görüntüleri kullanarak dakikalar içinde oluşturma** 
   
    Görüntüler çok geniş bir yelpazedeki hazır görüntülerden hello Azure Marketi seçer ve hello laboratuarda kullanılabilmesini. Merhaba hazır görüntüleri gereksinimlerinizi karşılamıyorsa, Laboratuvar hello Laboratuvar özel görüntü olarak Azure marketi, gereksinim duyduğunuz tüm hello yazılım yükleme ve kaydetme hello VM hazır bir görüntüden kullanarak VM oluşturarak özel bir görüntü oluşturabilirsiniz.

    Özel resimler kullanacaksanız, bir görüntü Fabrika toocreate kullanmayı düşünün ve resimlerinizi dağıtın. Bir görüntü Fabrika düzenli olarak oluşturur ve yapılandırılmış görüntülerinizin otomatik olarak dağıtan bir yapılandırma olarak kodu çözümüdür. Bir VM ile Merhaba oluşturulduktan sonra bu kaydeder hello gereken süre toomanually yapılandırma hello sistem işletim sistemi temel.
  
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure Market görüntülerini yapılandırın](devtest-lab-configure-marketplace-images.md) |Beyaz liste Azure Market görüntülerini hello geliştiriciler için istediğiniz seçimi yalnızca hello görüntüleri için kullanılabilir hale getirme öğrenin.|
   | [Özel bir görüntü oluşturun](devtest-lab-create-template.md) |Böylece geliştiriciler, hızlı bir şekilde hello özel görüntü kullanarak bir VM oluşturabilir, gereken hello yazılımı yüklenerek özel bir görüntü oluşturun.|
   | [Görüntü Fabrika hakkında bilgi edinin](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Açıklayan bir video izlemek nasıl tooset ayarlama ve bir görüntü Fabrika kullanın.|

3. **Geliştirici makinelerinde için yeniden kullanılabilir şablonlar oluşturma** 
   
    Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır. Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz. Her geliştirici hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs formüller toocreate sanal makineleri yönetme](devtest-lab-manage-formulas.md) |Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.|

4. **Yapıları tooenable esnek VM özelleştirme oluşturma**

   Yapıları kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın. Yapıtlar şunlar olabilir:

   - Aracılar, Fiddler ve Visual Studio gibi hello VM - üzerinde tooinstall istediğiniz araçları.
   - Bir depoyu kopyalama gibi hello VM - üzerinde toorun istediğiniz eylemleri.
   - Tootest istediğiniz uygulamalar.

   Birçok zaten kullanılabilir out-of--box ürünleridir. Özel ihtiyaçlarınız için daha fazla özelleştirme isterseniz kendi özel yapılar oluşturabilirsiniz.

   Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs VM için özel yapılar oluşturma](devtest-lab-artifact-author.md) |Merhaba sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.|
   | [Bir Git deposu toostore özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de ekleme](devtest-lab-add-artifact-repo.md) |Bilgi nasıl toostore kendi özel Git depodaki özel yapıtları.|

5. **Denetim maliyetleri**
   
    Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda bir geliştirici tarafından oluşturulan sanal makineleri tooset bir ilke sağlar. 
   
    İş Çizelgesi kümesi Geliştirici ekibiniz varsa ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden bunu kolayca, ayarı otomatik kapatma ve otomatik başlatma ilkeleri hello laboratuarda tarafından gerçekleştirebilirsiniz. 
   
    Uygulama geliştirme tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Laboratuvar ilkelerini tanımlama](devtest-lab-set-lab-policy.md) |Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz. |
   | [Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Geliştirme tamamlandığında, tek bir işlemde tüm hello labs silin.|

1. **Sanal ağ tooa VM ekleme** 
   
    Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur. Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, Vm'leri oluştururken, böylece kullanılabilir VNET tooyour Laboratuvar kullanıcının bu sanal ağ ayarları ekleyebilirsiniz.

    Ayrıca, bir Azure Active Directory etki alanı katılma yapı hello VM oluşturulduğunda, bir VM tooa etki alanına katılacak kullanılabilir yoktur. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md) |Nasıl tooconfigure Azure DevTest Labs kullanarak bir sanal ağ hello Azure portal hakkında bilgi edinin.|

6. **Her geliştirici paylaşımı hello laboratuvarla**
   
    Labs, geliştiricilere paylaşan bir bağlantıyı kullanarak doğrudan erişilebilir. Sahip oldukları sürece bile toohave bir Azure hesabı sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account). Geliştiriciler, diğer geliştiriciler tarafından oluşturulan VM'ler göremezsiniz.  
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de Geliştirici tooa Laboratuvar ekleme](devtest-lab-add-devtest-user.md) |Hello Azure portal tooadd geliştiriciler tooyour Laboratuvar kullanın.|
   | [Bir PowerShell Betiği kullanılarak geliştiriciler toohello Laboratuvar ekleme](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Geliştiriciler tooyour Laboratuvar ekleme PowerShell tooautomate kullanın. |
   | [Bir bağlantı toohello Laboratuvar Al](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Nasıl geliştiriciler Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.|

7. **Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek** 
   
    Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Resource Manager şablonu kullanarak bir laboratuvar oluşturma](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

