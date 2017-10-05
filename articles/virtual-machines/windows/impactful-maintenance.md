---
title: "Azure'da Windows sanal makineleri için etkili bakım | Microsoft Docs"
description: "Windows sanal makineler için etkili Bakım."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 75cd4d567deb98e5d2498dc607b43dae483f1c94
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Sanal makineler için etkili bakım

Burada altyapının için planlı bakım nedeniyle, VM'ler yeniden bazı durumlar vardır. Azure üzerinde barındırılan Vm'leriniz kullanılabilirliğini etkili olmasının, aşağıdaki artık kullanabilmeniz için kullanılabilir:

-   En az 30 gün önce etkisini bildirim gönderilir.

-   Her VM başına bakım pencereleri görünürlük.

-   Esneklik ve denetim tam zaman Vm'leriniz etkilemeye bakım için ayarlama.

Microsoft Azure bakım yinelemelerini zamanlandı. Başlangıç yinelemelerini yeni düzeltmeler ve Özellikler çıkış çalışırken söz konusu riski azaltmak için daha küçük kapsama sahip. Sonraki yinelemelerden birden çok bölgelerden (hiçbir zaman aynı bölge çifti) yayılabilir. Bir VM tek bakım yinelemede dahil edilir. Yineleme durdurulursa, kalan sanal makineleri başka bir, gelecekteki, yineleme dahil edilir.

Planlı bakım yineleme iki aşamaya sahiptir: Pre-emptive bakım penceresi ve zamanlanmış bakım penceresi.

**Pre-emptive bakım penceresi** bakım, sanal makineleri üzerinde başlatmak için esneklik sağlar. Bunu yaparak, ne zaman Vm'leriniz etkilenen, belirleyebilirsiniz güncelleştirme ve Bakım yapılmamaktadır her VM arasındaki süre dizisi. Bakım için planlanan olup olmadığını görmek için her bir VM sorgulamak ve başlatılan bakım isteğiniz sonucunu denetleyin.

**Zamanlanmış bakım penceresi** Azure Vm'leriniz bakım için zamanlanmış olduğunda. Önleyici bakım penceresi izler, bu zaman penceresi sırasında hala sorgu için bakım penceresi, ancak artık bakım düzenlemek kullanabilirsiniz.

## <a name="availability-considerations-during-planned-maintenance"></a>Planlı bakım sırasında kullanılabilirlik konuları 

### <a name="paired-regions"></a>Eşleştirilmiş bölgeleri

Her Azure bölgesi birlikte bölgesel çifti yapmadan aynı coğrafi konum içinde başka bir bölge ile eşleştirilmiş. Bakım yürütürken, Azure yalnızca tek bir bölgedeki sanal makine örnekleri kendi çiftinin güncelleştirin. Örneğin, Orta Kuzey ABD’de Sanal Makineler güncelleştirilirken Azure aynı anda Orta Güney ABD’deki bir Sanal Makineyi güncelleştirmez. Bu, ayrı bir şekilde zamanlanır, böylelikle bölgeler arasında yük devretme veya yük dengeleme sağlanır. Ancak, Kuzey Avrupa gibi diğer bölgelerde, Doğu ABD ile aynı zamanda bakım yapılabilir.
Daha fazla bilgi edinin [Azure bölgesi çiftleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Tek örnek VM'ler vs. Kullanılabilirlik kümesi veya VM ölçek kümesi

Azure'da sanal makineleri kullanarak bir iş yükü dağıtırken, kullanılabilirlik, uygulamanız için yüksek kullanılabilirlik sağlamak amacıyla kümesi içindeki sanal makineleri oluşturabilirsiniz. Bu yapılandırma bir kesinti veya bakım olayları sırasında en az bir sanal makinenin kullanılabilir olmasını sağlar.

Bir kullanılabilirlik kümesi içinde tek tek sanal makineleri en fazla 20 güncelleştirme etki alanları arasında yayılır. Planlı bakım sırasında herhangi bir anda yalnızca bir tek güncelleştirme etki alanı etkilenmez. Güncelleme etki alanına etkilenip sırasını sırayla planlı bakım sırasında devam değil. Tek örnek VM'ler (kullanılabilirlik kümesinin parçası olmayan) tahmin etmek veya ve kaç tane sanal makineleri birlikte etkilenen belirlenmesi için bir yolu yoktur.

Sanal makine ölçek kümeleri dağıtmak ve aynı sanal makineleri bir küme tek bir kaynak olarak yönetmenize olanak sağlayan bir Azure işlem kaynaktır.
Bir kullanılabilirlik benzer garanti güncelleştirme etki alanları formunda ölçek kümesi sağlar. 

Sanal makinelerinizin yüksek kullanılabilirlik için yapılandırma hakkında daha fazla bilgi için bkz: [ *Windows sanal makinelerin kullanılabilirliğini yönetme*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Zamanlanmış olaylar

Azure meta veri hizmeti, Azure üzerinde barındırılan sanal makineniz hakkında bilgi bulmak sağlar. Olaylar, ilgili gelişmeler yüzeyleri bilgileri gösterilen kategorilerden birini zamanlanmış (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi.

Zamanlanmış olaylar hakkında daha fazla bilgi için başvurmak [Azure meta veri hizmeti - zamanlanmış olaylar](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Bakım bulma ve bildirimler

Bakım zamanlaması tek tek sanal makineleri düzeyinde müşterilere görünür olur. Azure portal, API, PowerShell veya CLI sorguya önleyici ve zamanlanmış bakım pencereleri kullanabilirsiniz. Ayrıca, bir bildirim (e-posta) durumda almayı işlemi sırasında bir (veya daha fazla), VM'lerin etkilenen burada.

Önleyici Bakım ve zamanlanmış bakım aşamaları içeren bir bildirim başlayın. Azure abonelik başına tek bir bildirim almak bekler. Bildirim abonelik yönetici ve ortak yönetici için varsayılan olarak gönderilir. İzleyici bakım bildirim için de yapılandırabilirsiniz.

### <a name="view-the-maintenance-window-in-the-portal"></a>Bakım penceresi portalında görüntüleyin 

Azure Portalı'nı kullanın ve bakım için zamanlanmış VM'ler arayın.

1.  Azure Portal’da oturum açın.

2.  Açarak **sanal makineleri** dikey.

3.  Tıklatın **sütunları** aralarından seçim yapabileceğiniz kullanılabilir sütunlar listesi açmak için düğmesi

4.  Seçin ve ekleyin **bakım penceresi** sütun. Bakım için zamanlanmış VM'ler ortaya bakım pencereleri sahip. Bakım tamamlandı veya için iptal edildiğinde, bakım penceresi artık olması sunulur.

### <a name="query-maintenance-details-using-the-azure-api"></a>Azure API'sini kullanarak sorgu Bakım Ayrıntıları

Kullanım [VM bilgi API almak](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) ve tekil bir VM Bakım Ayrıntıları bulmak örneği görünümüne bakın. Yanıt aşağıdaki öğeleri içerir:

  - isCustomerInitiatedMaintenanceAllowed: VM'de önleyici dağıtın başlatmak olup olmadığını gösterir.

  - preMaintenanceWindowStartTime: önleyici bakım penceresi başlangıç zamanı.

  - preMaintenanceWindowEndTime: önleyici bakım penceresi bitiş zamanı. Bu tarihten sonra artık bu VM'de bakım başlatamaz olacaktır.
    
  - maintenanceWindowStartTime: VM etkilendi zamanlanmış bakım penceresinin başlangıç zamanı.

  - maintenanceWindowEndTime: zamanlanmış bakım penceresi bitiş zamanı.
  
  - lastOperationResultCode:, son bakım dağıtın işleminin sonucu.
 
  - lastOperationMessage: Son bakım dağıtın işleminin sonucunu açıklayan ileti.

## <a name="pre-emptive-redeploy"></a>Önleyici dağıtın

Önleyici dağıtın eylem bakım Azure Vm'leriniz için ne zaman uygulandığı zaman denetleme esnekliği sağlar. Planlı bakım burada her Vm'leriniz için tam zamanında başlatılması karar verebilirsiniz bir önleyici bakım penceresi ile başlar. Böyle bir işlevsellik yararlı olduğu kullanım örnekleri şunlardır:

-   Bakım son müşteriyle koordine olmanız gerekir.

-   Azure tarafından sunulan değerinin zamanlanan bakım penceresinden yeterli değil.
    Haftanın En meşgul zamanında olmasını penceresi olur veya çok uzun olabilir.

-   Çok örnekli veya çok katmanlı uygulamalar için iki VM veya belirli bir dizi takip etmek arasındaki yeterli süre gerekir.

Bir VM üzerinde önleyici dağıtın için çağırdığınızda, VM zaten güncelleştirilmiş bir düğüme taşınır ve tüm yapılandırma seçenekleri ve ilişkili kaynakları geri korur, çalıştırır. Bunun yapılması, geçici disk kaybolur ve dinamik IP adresleri ile ilişkili sanal ağ arabirimi güncelleştirilir.

Önleyici dağıtın kez VM başına etkinleştirilir. İşlemi sırasında bir hata varsa, işlemi iptal edildi, VM etkilenmez ve planlı bakım yinelemeden diğerine dışlandı. Daha sonra yeni bir zamanlama ile temas ve olması zamanlamak ve Vm'lerinizi üzerindeki etkiyi sırası için yeni bir fırsat sunulan.