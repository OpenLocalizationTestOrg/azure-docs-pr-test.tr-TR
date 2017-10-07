---
title: "azure'da Windows sanal makineleri için aaaImpactful bakım | Microsoft Docs"
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
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Sanal makineler için etkili bakım

Burada Vm'leriniz altyapısını temel tooplanned bakım toohello yeniden başlatılır bazı durumlar vardır. Azure üzerinde barındırılan Vm'leriniz etkili toothe kullanılabilirliğini olmasının, hello aşağıdaki, toouse artık kullanılabilir:

-   En az 30 gün önce hello etkisi bildirim gönderilir.

-   Her VM başına görünürlük toohello bakım pencereleri.

-   Esneklik ve denetim hello tam zaman Vm'leriniz etkilemeye bakım için ayarlama.

Microsoft Azure bakım yinelemelerini zamanlandı. Başlangıç yinelemelerini yeni düzeltmeler ve Özellikler çıkış çalışırken söz konusu sipariş tooreduce hello riski küçük kapsamda sahip. Sonraki yinelemelerden birden çok bölgeye span (Merhaba hiçbir zaman gelen aynı bölge çifti). Bir VM tek bakım yinelemede dahil edilir. Yineleme durdurulursa, kalan sanal makineleri başka bir, gelecekteki, yineleme dahil edilir.

Merhaba planlı bakım yineleme iki aşamaya sahiptir: Pre-emptive bakım penceresi ve zamanlanmış bakım penceresi.

Merhaba **Pre-emptive bakım penceresi** hello esneklik tooinitiate hello bakım, sanal makineleri üzerinde sağlar. Bunu yaparak, ne zaman Vm'leriniz etkilenen belirlemek, dizi hello güncelleştirme ve Bakım yapılmamaktadır her VM arasındaki hello süre hello. Her VM toosee bakım için planlanan olup olmadığını sorgular ve başlatılan bakım isteğiniz hello sonucunu denetleyin.

Merhaba **zamanlanmış bakım penceresi** Azure Vm'leriniz hello bakım için zamanlanmış olduğunda. Önleyici bakım penceresi izler, bu zaman penceresi sırasında hala hello bakım penceresi için sorgu, ancak artık mümkün tooorchestrate hello bakım olabilir.

## <a name="availability-considerations-during-planned-maintenance"></a>Planlı bakım sırasında kullanılabilirlik konuları 

### <a name="paired-regions"></a>Eşleştirilmiş bölgeleri

Her Azure bölgesi hello içinde başka bir bölge ile eşleştirilmiş bir bölgesel çifti birlikte yapmadan aynı Coğrafya. Bakım yürütürken, Azure yalnızca hello sanal makine örneklerini tek bir bölgedeki çiftini güncelleştirin. Örneğin, hello Kuzey Orta ABD sanal makinelerinizde güncelleştirirken Azure tüm sanal makineler Orta Güney ABD hello güncelleştirmez aynı anda. Bu, ayrı bir şekilde zamanlanır, böylelikle bölgeler arasında yük devretme veya yük dengeleme sağlanır. Kuzey Avrupa bakım altında gibi ancak, diğer bölgeleriyle aynı hello Doğu ABD olarak zaman.
Daha fazla bilgi edinin [Azure bölgesi çiftleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Tek örnek VM'ler vs. Kullanılabilirlik kümesi veya VM ölçek kümesi

Azure'da sanal makineleri kullanarak bir iş yükü dağıtırken hello VM'ler kullanılabilirlik sipariş tooprovide yüksek kullanılabilirlik tooyour uygulamada kümesi içinde oluşturabilirsiniz. Bu yapılandırma bir kesinti veya bakım olayları sırasında en az bir sanal makinenin kullanılabilir olmasını sağlar.

Bir kullanılabilirlik kümesi içinde tek tek sanal makineleri too20 güncelleştirme etki alanları arasında yayılır. Planlı bakım sırasında herhangi bir anda yalnızca bir tek güncelleştirme etki alanı etkilenmez. güncelleme etki alanına etkilenip Hello sırasını sırayla planlı bakım sırasında devam değil. Sanal makineleri (değil kullanılabilirlik kümesinin bir parçası) için tek örnek, hiçbir şekilde toopredict veya hangi ve kaç tane sanal makineleri birlikte etkilenen belirler.

Sanal makine ölçek kümesi sağlayan bir Azure işlem toodeploy kaynaktır ve aynı sanal makineleri bir küme tek bir kaynak olarak yönetebilirsiniz.
Merhaba ölçek kümesini benzer garanti güncelleştirme etki alanları formunda tooan kullanılabilirlik sağlar. 

Sanal makinelerinizin yüksek kullanılabilirlik için yapılandırma hakkında daha fazla bilgi için bkz: [ *Merhaba, Windows sanal makinelerin kullanılabilirliğini yönetme*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Zamanlanmış olaylar

Azure meta veri hizmeti, Azure üzerinde barındırılan sanal makineniz toodiscover bilgilerini sağlar. Olaylar, kullanıma sunulan hello kategoriden, ilgili gelişmeler yüzeyleri bilgileri zamanlanmış (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi.

Zamanlanmış olaylar hakkında daha fazla bilgi için çok başvuran[Azure meta veri hizmeti - zamanlanmış olaylar](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Bakım bulma ve bildirimler

Bakım zamanlaması görünür toocustomers tek tek sanal makineleri hello düzeyinde değildir. Azure kullanabilirsiniz portal, API, PowerShell veya CLI tooquery önleyici ve zamanlanmış bakım pencereleri için. Ayrıca, bir bildirim (e-posta) hello durumda almayı hello işlemi sırasında bir (veya daha fazla), VM'lerin etkilenen burada.

Önleyici Bakım ve zamanlanmış bakım aşamaları içeren bir bildirim başlayın. Tooreceive Azure abonelik başına tek bir bildirim bekler. Merhaba bildirim toohello aboneliğinin Yöneticisi ve ortak yönetici varsayılan olarak gönderilir. Merhaba İzleyici bakım bildirim için de yapılandırabilirsiniz.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Merhaba bakım penceresi hello portalında görüntüleyin 

Hello Azure portal kullanın ve bakım için zamanlanmış VM'ler için bakın.

1.  Toohello Azure portalında oturum açın.

2.  Açarak hello **sanal makineleri** dikey.

3.  Merhaba tıklatın **sütunları** düğmesini tooopen hello kullanılabilir sütunlar toochoose listesi

4.  Seçin ve hello ekleyin **bakım penceresi** sütun. Bakım için zamanlanmış VM'ler ortaya hello bakım pencereleri sahip. Bakım tamamlandı veya için iptal edildiğinde, bakım penceresi artık olması sunulur.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Hello Azure API'sini kullanarak sorgu Bakım Ayrıntıları

Kullanım hello [VM bilgi API almak](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) ve hello örneği toodiscover hello bakım ilgili ayrıntıları görüntüle tekil bir VM arayın. Merhaba yanıt hello aşağıdaki öğeleri içerir:

  - isCustomerInitiatedMaintenanceAllowed: hello VM üzerinde önleyici dağıtın başlatmak olup olmadığını gösterir.

  - preMaintenanceWindowStartTime: Merhaba hello önleyici bakım penceresinin başlangıç zamanı.

  - preMaintenanceWindowEndTime: Merhaba hello önleyici bakım penceresi bitiş zamanı. Bu tarihten sonra artık bu VM'de mümkün tooinitiate bakım olacaktır.
    
  - maintenanceWindowStartTime: hello başlangıç zamanı hello zamanlanmış bakım penceresinin VM etkilendi olduğunda.

  - maintenanceWindowEndTime: Merhaba hello zamanlanmış bakım penceresinin bitiş saati.
  
  - lastOperationResultCode: Merhaba, son bakım dağıtın işleminin sonucu.
 
  - lastOperationMessage: Son bakım dağıtın işleminizi açıklayan hello sonucu iletisi.

## <a name="pre-emptive-redeploy"></a>Önleyici dağıtın

Önleyici dağıtın eylemin hello esneklik toocontrol hello zaman bakım uygulanan tooyour VM'ler için Azure'da olduğunda sağlar. Planlı bakım, burada her yeniden, VM'ler toobe hello tam zamanında karar verebilirsiniz bir önleyici bakım penceresi ile başlar. Böyle bir işlevsellik yararlı olduğu kullanım örnekleri şunlardır:

-   Bakım gerek toobe hello son müşteriyle düzenlenir.

-   Azure tarafından sunulan hello zamanlanan bakım penceresinden yeterli değil.
    Merhaba penceresinde hello yoğun saatinde haftanın zamanında toobe olur veya çok uzun olabilir.

-   Çok örnekli veya çok katmanlı uygulamalar için iki VM veya belirli bir dizi toofollow arasında yeterli zaman gerekir.

Bir VM üzerinde önleyici dağıtın için çağırdığınızda, hello VM tooan düğüm zaten güncelleştirildi ve sonra bunu yeniden tüm yapılandırma seçenekleri ve ilişkili kaynakları koruma çalıştırır taşır. Bunun yapılması, hello geçici disk kaybolur ve dinamik IP adresleri ile ilişkili sanal ağ arabirimi güncelleştirilir.

Önleyici dağıtın kez VM başına etkinleştirilir. Merhaba işlemi sırasında bir hata varsa, hello işlemi iptal edildi, VM etkilenmez hello ve hello planlı bakım yinelemeden diğerine dışlandı. Daha sonra yeni bir zamanlama ile temas ve olması Vm'leriniz yeni bir fırsat tooschedule ve sıra hello etkisi sunulan.