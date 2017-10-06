---
title: "aaaAuto hello Klasik Portalı'nda bir bulut hizmeti ölçeklendirin | Microsoft Docs"
description: "(Klasik) Nasıl toouse hello Klasik portal tooconfigure otomatik ölçek kuralı için bir bulut hizmeti web rolü veya Azure çalışan rolünde öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Tooconfigure otomatik olarak nasıl hello Klasik Portalı'nda bir bulut hizmeti için ölçeklendirme
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-scale-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-scale.md)

Merhaba ölçek sayfasında hello Klasik Azure portalı, web rolü veya çalışan rolü için otomatik ölçeklendirme ayarlarını yapılandırabilirsiniz. Alternatif olarak, el ile yerine otomatik ölçeklendirmeyi kural tabanlı ölçeklendirme yapılandırabilirsiniz.

> [!NOTE]
> Bu makalede bulut hizmeti web ve çalışan rolleri odaklanır. Bir sanal makine (Klasik) doğrudan oluşturduğunuzda, bir bulut hizmetinde barındırılır. Bu bilgilerin bazıları, sanal makinelerin toothese türleri geçerlidir. Sanal makinelerin bir kullanılabilirlik kümesi ölçeklendirme yalnızca bunları açma ve kapatma yapılandırdığınız hello ölçek kurallara göre kapatılıyor. Sanal makineler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Yönet hello sanal makinelerin kullanılabilirliğini](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Uygulamanız için ölçeklendirme yapılandırmadan önce aşağıdaki bilgilerle hello dikkate almanız gerekir:

* Ölçeklendirme Çekirdek kullanımını etkilenir.

    Daha fazla sayıda çekirdek büyük rol örneği kullanın. Aboneliğiniz için çekirdek hello sınırı içinde yalnızca bir uygulama ölçeklendirebilirsiniz. Örneğin, aboneliğiniz 20 olarak belirlenen çekirdek sınırına sahip söyleyin. İki orta ölçekli bulut hizmetleriyle (4 çekirdeğe toplamı) bir uygulama çalıştırırsanız hello kalan 16 çekirdek tarafından aboneliğinizde diğer bulut hizmet dağıtımları yalnızca ölçeklendirebilirsiniz. Boyutları hakkında daha fazla bilgi için bkz: [bulut hizmeti boyutları](cloud-services-sizes-specs.md).

* Bir kuyruk oluşturun ve bir ileti eşiğine dayalı bir uygulama ölçeklendirebilirsiniz önce bir rolü ile ilişkilendir. Daha fazla bilgi için bkz: [nasıl toouse hello kuyruk depolama hizmeti](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Bağlantılı tooyour olan kaynaklar ölçeklendirebilirsiniz bulut hizmeti. Kaynakları bağlama hakkında daha fazla bilgi için bkz: [nasıl yapılır: bir kaynak tooa bulut hizmeti bağlantı](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* Uygulamanızın tooenable yüksek kullanılabilirlik, iki veya daha fazla rol örneği ile dağıtılır emin olmalısınız. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Zamanlama ölçeklendirme
Varsayılan olarak, tüm rolleri belirli bir zamanlama izlemeyin. Bu nedenle, değiştirilen tüm ayarlar tooall kez ve hello yıl boyunca her gün uygulanır. İsterseniz, el ile veya otomatik modları aşağıdaki hello biri için ölçeklendirme ayarlayabilirsiniz:

* Haftanın günü
* Hafta sonları
* Hafta gece
* Hafta mornings
* Belirli tarihleri
* Belirli bir tarih aralığı

Merhaba zamanlama ayarı hello yapılandırılmış [Klasik Azure portalı](https://manage.windowsazure.com/) hello üzerinde  
**Bulut Hizmetleri** > **\[bulut hizmetiniz\]** > **ölçek**  >   **\[Üretim ve hazırlama\]**  sayfası.

Merhaba tıklatın **zamanlama süreleri ayarlamanız** düğmesini toochange istediğiniz her rol için.

![Bulut hizmeti bir zamanlamaya göre otomatik ölçeklendirme][scale_schedules]

## <a name="manual-scale"></a>El ile ölçek
Merhaba üzerinde **ölçek** sayfasında, el ile artırabilir veya örnekleri bir bulut hizmetinde çalışan sayısı hello azaltın. Bir zamanlama oluşturmadıysanız, bu ayar her oluşturduğunuz zamanlamayı veya tooall zaman için yapılandırılır.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
   
   > [!TIP]
   > Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.

2. Tıklatın **ölçek**.
3. Ölçeklendirme seçenekleri için toochange istediğiniz hello zamanlamayı seçin. *Hayır programlanan zamanlarda* tanımlı bir zamanlama varsa hello varsayılandır.
4. Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **NONE**. Bu ayar, tüm rolleri hello varsayılandır.
5. Merhaba bulut hizmetindeki her rol örnekleri toouse hello sayısını değiştirmek için kaydırıcıyı sahiptir.
   
    ![Bir bulut hizmet rolü elle ölçeklendirme][manual_scale]
   
    Daha fazla örnekleri gerekiyorsa, toochange hello gerekebilir [bulut hizmeti sanal makine boyutu](cloud-services-sizes-specs.md).
6. **Kaydet** düğmesine tıklayın.  
   Rol örnekleri eklenir veya seçimlerinizi tabanlı kaldırılır.

> [!TIP]
> Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.

## <a name="automatic-scale---cpu"></a>Otomatik ölçek - CPU
Merhaba ortalama CPU kullanım yüzdesini üstünde veya altında belirtilen eşikler kalırsa Bu mod ölçeklendirir. Rol örnekleri oluşturulur veya böyle bir durumda silindi.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
   
   > [!TIP]
   > Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.

2. Tıklatın **ölçek**.
3. Ölçeklendirme seçenekleri için toochange istediğiniz hello zamanlamayı seçin. *Hayır programlanan zamanlarda* tanımlı bir zamanlama varsa hello varsayılandır.
4. Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **CPU**.
5. Artık rol örnekleri, hello hedef CPU kullanımı (ölçek büyütme bir tootrigger) ve kaç tane tooscale yukarı ve aşağı tarafından örnekleri minimum ve maksimum aralığını yapılandırabilirsiniz.

![Bir bulut hizmet rolü tarafından cpu yükünü ölçeklendirme][cpu_scale]

> [!TIP]
> Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.

## <a name="automatic-scale---queue"></a>Otomatik ölçek - sırası
Sıradaki iletileri Hello sayısı üzerinde veya belirtilen eşiğin altında kalırsa bu modu otomatik olarak ölçeklendirir. Rol örnekleri oluşturulur veya böyle bir durumda silindi.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
   
   > [!TIP]
   > Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.

2. Tıklatın **ölçek**.
3. Hello bulur **ölçek ölçüm tarafından** bölümünde ve seçin **SIRA**.
4. Artık rol örnekleri, hello kuyruk ve her bir örneği ve tarafından kaç örnekleri tooscale yukarı ve aşağı için kuyruk iletileri tooprocess sayısı minimum ve maksimum aralığını yapılandırabilirsiniz.

![İleti sırası tarafından bir bulut hizmet rolü ölçeklendirme][queue_scale]

> [!TIP]
> Her gördüğünüz ![][tip_icon] fare tooit taşıyın ve hangi belirli bir ayarı yaptığı hakkında Yardım alabilirsiniz.

## <a name="scale-linked-resources"></a>Bağlı kaynaklar ölçeklendirme
Genellikle bir rolü ölçeklendirdiğinizde Merhaba uygulaması da kullanarak faydalı tooscale hello veritabanı yok. Merhaba veritabanı toohello bulut hizmeti bağlantı varsa, hello uygun bağlantıyı tıklatarak o kaynağın ayarlarını ölçeklendirme hello erişebilir.

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**ve ardından hello bulut hizmeti tooopen hello Panosu hello adına tıklayın.
   
   > [!TIP]
   > Bulut hizmetinizi görmüyorsanız, gelen toochange gerekebilir **üretim** çok**hazırlama** veya tam tersi.

2. Tıklatın **ölçek**.
3. Hello bulur **bağlı kaynakları** 'ye tıklayın **bu veritabanı için ölçek yönetmek**.
   
   > [!NOTE]
   > Görmüyorsanız, bir **bağlı kaynakları** bölümünde, büyük olasılıkla herhangi bağlı kaynaklar yok.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
