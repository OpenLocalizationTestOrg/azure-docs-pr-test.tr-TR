---
title: "VM ve PaaS aaaUse Azure DevTest Labs test ortamları | Microsoft Docs"
description: "Nasıl toouse Azure DevTest Labs VM ve PaaS için test ortamı senaryoları hakkında bilgi edinin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>Sınama ortamlarında kullanım Azure DevTest Labs VM ve PaaS

Azure DevTest Labs tooimplement birçok senaryoları kullanabilirsiniz, ancak Sınayıcılar için DevTest Labs toohost makineleri kullanarak birincil bir senaryo içerir. 

Bu senaryoda, DevTest Labs şu avantajları sağlar:

- Sınayıcılar hızlı bir şekilde yeniden kullanılabilir şablonlar ve yapıları kullanarak Windows ve Linux ortamlar sağlama tarafından hello kendi uygulamasının en son sürümünü test edebilirsiniz.
- Sınayıcılar kendi yükleme birden çok test aracılarını sağlama tarafından testi yukarı ölçeklendirebilirsiniz.
- Yöneticiler, sağlayarak maliyetleri denetleyebilirsiniz:
  - Sınayıcılar ihtiyaç duydukları olandan daha fazla VMs alınamıyor.
  - Sanal makineleri ne zaman kullanılmıyor kapatılır.

![DevTest Labs için eğitim kullanın](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

Bu makalede, çeşitli Azure DevTest Labs kullanılan özellikler toomeet tester gereksinimleri hakkında bilgi edinin ve ayrıntılı adımlar toofollow tooset bir laboratuvar yukarı hello.

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>Azure DevTest Labs içeren test ortamlarında uygulama
1. **Merhaba Laboratuvar oluşturma** 
   
    Labs hello Azure DevTest Labs'de başlangıç noktası var. Bir laboratuvar oluşturduktan sonra kullanıcılar (sınayıcılar) toohello Laboratuvar, hızlı bir şekilde, oluşturabilirsiniz VM görüntülerini tanımlama, ayar ilkeleri toocontrol maliyetleri ve daha fazlasını ekleme gibi görevleri gerçekleştirebilirsiniz.  
   
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
   | [Azure Market görüntülerini yapılandırın](devtest-lab-configure-marketplace-images.md) |Beyaz liste Azure Market görüntülerini hello Sınayıcılar için istediğiniz seçimi yalnızca hello görüntüleri için kullanılabilir hale getirme öğrenin.|
   | [Özel bir görüntü oluşturun](devtest-lab-create-template.md) |Sınayıcılar hızlı bir şekilde hello özel görüntü kullanarak bir VM oluşturmak için gereksinim duyduğunuz hello yazılımı yüklenerek özel bir görüntü oluşturun.|
   | [Görüntü Fabrika hakkında bilgi edinin](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |Açıklayan bir video izlemek nasıl tooset ayarlama ve bir görüntü Fabrika kullanın.|

3. **Test makinelerini için yeniden kullanılabilir şablonlar oluşturma** 
   
    Azure DevTest Labs formülde varsayılan özellik değerleri listesine toocreate VM kullanılır. Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağı seçerek hello laboratuarda bir formül oluşturabilirsiniz. Her tester hello Laboratuvar hello formülde görebilir ve toocreate VM kullanın. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs formüller toocreate sanal makineleri yönetme](devtest-lab-manage-formulas.md) |Görüntü, VM boyutu (CPU ve RAM birleşimi) ve bir sanal ağ seçerek bir formül nasıl oluşturabileceğinizi öğrenin.|

3. **Çoklu VM test ortamları oluşturma** 
   
    Azure Resource Manager şablonları toodefine hello altyapı ve Azure çözümünüzü yapılandırmasını kullanır ve art arda birden çok test tutarlı bir durumda VM'ler dağıtın.

    Azure PaaS kaynaklarına bir ortamda bir Resource Manager şablonunda sağlanabilir ve maliyet izlemesi görünür. Ancak, VM otomatik kapatma tooPaaS kaynakların geçerli değildir.

    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynakları oluşturma](devtest-lab-create-environment-from-arm.md) |Tutarlı bir durumda birden çok VM test ortamınızı nasıl dağıtabileceğiniz hakkında bilgi edinin.|

4. **Yapıları tooenable esnek VM özelleştirme oluşturma**

   Yapıları kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın. Yapıtlar şunlar olabilir:

   - Aracılar, Fiddler ve Visual Studio gibi hello VM - üzerinde tooinstall istediğiniz araçları.
   - Bir depoyu kopyalama gibi hello VM - üzerinde toorun istediğiniz eylemleri.
   - Tootest istediğiniz uygulamalar.

   Birçok zaten kullanılabilir out-of--box ürünleridir. Ancak, özel gereksinimlerinizi karşılamak için daha fazla özelleştirme istiyorsanız, özel yapıtları oluşturabilirsiniz.

   Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [DevTest Labs VM için özel yapılar oluşturma](devtest-lab-artifact-author.md) |Merhaba sanal makineler için kendi özel yapılar laboratuvarınızda oluşturun.|
   | [Bir Git deposu toostore özel yapılar ve kullanmak için Azure Resource Manager şablonları Azure DevTest Labs'de ekleme](devtest-lab-add-artifact-repo.md) |Bilgi nasıl toostore kendi özel Git depodaki özel yapıtları.|

5. **Denetim maliyetleri**
   
    Azure DevTest Labs hello Laboratuvar toospecify hello en fazla sayıda hello laboratuarda tester tarafından oluşturulan sanal makineleri tooset bir ilke sağlar. 
   
    İş Çizelgesi kümesi test ekibiniz varsa ve toostop tüm hello VM'ler hello günün belirli bir zamanda istediğiniz ve ardından bunları günü izleyen hello otomatik olarak yeniden bunu kolayca, ayarı otomatik kapatma ve otomatik başlatma ilkeleri hello laboratuarda tarafından gerçekleştirebilirsiniz. 
   
    Uygulama geliştirme tamamlandığında, son olarak, tüm hello sanal makineleri aynı anda tek bir PowerShell Betiği çalıştırarak silebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Laboratuvar ilkelerini tanımlama](devtest-lab-set-lab-policy.md) |Maliyetleri hello laboratuvarda ilkeleri ayarlayarak denetleyebilirsiniz. |
   | [Tüm hello Laboratuvar bir PowerShell komut dosyası kullanarak sanal makineleri silin](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Test tamamlandığında tek bir işlemde tüm hello labs silin.|

1. **Sanal ağ tooa Laboratuvar ekleme** 
   
    Her bir laboratuvar oluşturulduğunda DevTest Labs yeni bir sanal ağ (VNET) oluşturur. Kendi VNET-Örneğin, ExpressRoute veya siteden siteye VPN kullanarak – yapılandırdıysanız, Vm'leri oluştururken, böylece kullanılabilir VNET tooyour Laboratuvar kullanıcının bu sanal ağ ayarları ekleyebilirsiniz.

    Ayrıca, hello VM oluşturulduğunda, bir VM tooa etki alanına katılan bir Azure Active Directory etki alanı katılma yapıya kullanılabilir yoktur. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md) |Nasıl tooconfigure Azure DevTest Labs kullanarak bir sanal ağ hello Azure portal hakkında bilgi edinin.|

6. **Merhaba Laboratuvar her tester ile paylaşma**
   
    Labs, denetleyicilerle paylaşmanızı bir bağlantıyı kullanarak doğrudan erişilebilir. Sahip oldukları sürece bile toohave bir Azure hesabı sahip olmayan bir [Microsoft hesabı](devtest-lab-faq.md#what-is-a-microsoft-account). Sınayıcılar diğer test eden tarafından oluşturulan VM'ler göremezsiniz.  
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Azure DevTest Labs'de tester tooa Laboratuvar ekleme](devtest-lab-add-devtest-user.md) |Hello Azure portal tooadd sınayıcılar tooyour Laboratuvar kullanın.|
   | [Bir PowerShell Betiği kullanılarak sınayıcılar toohello Laboratuvar ekleme](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |Sınayıcılar tooyour Laboratuvar ekleme PowerShell tooautomate kullanın. |
   | [Bir bağlantı toohello Laboratuvar Al](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |Nasıl sınayıcılar Laboratuvar köprü üzerinden doğrudan erişebileceğiniz öğrenin.|

7. **Daha fazla takımlar için laboratuvar oluşturmayı otomatikleştirmek** 
   
    Laboratuvar oluşturma, Resource Manager şablonu oluşturma ve toocreate aynı labs tekrar tekrar kullanarak özel ayarları da dahil olmak üzere otomatik hale getirebilirsiniz. 
   
    Aşağıdaki tablonun hello hello bağlantıları tıklayarak daha fazla bilgi edinin:
   
   | Görev | Öğrenecekleriniz |
   | --- | --- |
   | [Resource Manager şablonu kullanarak bir laboratuvar oluşturma](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |Labs Resource Manager şablonları kullanarak Azure DevTest Labs içinde oluşturun. |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

