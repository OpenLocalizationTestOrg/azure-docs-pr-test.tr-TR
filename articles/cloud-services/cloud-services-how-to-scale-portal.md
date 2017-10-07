---
title: "aaaAuto hello Portalı'nda bir bulut hizmeti ölçeklendirin | Microsoft Docs"
description: "Nasıl toouse hello portal tooconfigure otomatik ölçek kuralı için bir bulut hizmeti web rolü veya Azure çalışan rolünde öğrenin."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Tooconfigure otomatik olarak nasıl hello portalında bulut hizmeti için ölçeklendirme
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-scale-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-scale.md)

Koşullar bir ölçekte veya işlemi uzaklaştırma tetikleyen bir bulut hizmeti çalışan rolü için ayarlayabilirsiniz. Merhaba rol Hello koşullarını hello CPU, disk veya ağ yükü hello rolünün temel alabilir. Ayrıca, aboneliğinizle ilişkilendirilmiş diğer bazı Azure kaynak ileti sırası veya hello ölçüsü dayalı bir koşul ayarlayabilirsiniz.

> [!NOTE]
> Bu makalede bulut hizmeti web ve çalışan rolleri odaklanır. Bir sanal makine (Klasik) doğrudan oluşturduğunuzda, bir bulut hizmetinde barındırılır. Standart bir sanal makine ile ilişkilendirerek ölçeklenebilen bir [kullanılabilirlik kümesi](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) ve bunları el ile açın veya kapatın.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Uygulamanız için ölçeklendirme yapılandırmadan önce aşağıdaki bilgilerle hello dikkate almanız gerekir:

* Ölçeklendirme Çekirdek kullanımını etkilenir.

    Daha fazla sayıda çekirdek büyük rol örneği kullanın. Aboneliğiniz için çekirdek hello sınırı içinde yalnızca bir uygulama ölçeklendirebilirsiniz. Örneğin, aboneliğiniz 20 olarak belirlenen çekirdek sınırına sahip söyleyin. İki orta ölçekli bulut hizmetleriyle (4 çekirdeğe toplamı) bir uygulama çalıştırırsanız hello kalan 16 çekirdek tarafından aboneliğinizde diğer bulut hizmet dağıtımları yalnızca ölçeklendirebilirsiniz. Boyutları hakkında daha fazla bilgi için bkz: [bulut hizmeti boyutları](cloud-services-sizes-specs.md).

* Ölçeklendirmek bir kuyruk iletisi eşiğine dayalı. Hakkında daha fazla bilgi için bkz: toouse sıraları [nasıl toouse hello kuyruk depolama hizmeti](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Ayrıca, aboneliğinizle ilişkilendirilmiş diğer kaynakları ölçeklendirebilirsiniz.

* Uygulamanızın tooenable yüksek kullanılabilirlik, iki veya daha fazla rol örneği ile dağıtılır emin olmalısınız. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Ölçek bulunduğu
Bulut hizmeti seçtikten sonra hello bulut hizmeti dikey görünür olması gerekir.

1. Merhaba üzerinde hello bulut hizmeti dikey **roller ve örnekler** kutucuğu, hello bulut hizmeti seçin hello adı.   
   **Önemli**: hizmet rolü, hello rolü rol örneği hello değil emin tooclick hello bulut olun.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Select hello **ölçek** döşeme.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Otomatik ölçeklendirme
Bir rol için ölçek ayarları ya da iki modlarıyla yapılandırabilirsiniz **el ile** veya **otomatik**. Beklediğiniz gibi el ile hello mutlak örneklerinin sayısını ayarlayın. Otomatik ancak nasıl ve nasıl tarafından çok yöneten kuralları ölçeklendirmeniz gerekir tooset sağlar.

Set hello **göre Ölçeklendirmeniz** çok seçenek**zamanlama ve performans kuralları**.

![Bulut Hizmetleri ölçek ayarları profili ve kural](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Varolan bir profili.
2. Merhaba üst profil için bir kural ekleyin.
3. Başka bir profili ekleyin.

Seçin **profili eklemek**. Hello profil belirler hangi modu için hello ölçek toouse istediğiniz: **her zaman**, **yineleme**, **sabit tarihi**.

Hello profili ve kuralları yapılandırdıktan sonra hello seçin **kaydetmek** hello üst simgesine tıklayın.

#### <a name="profile"></a>Profil
Hello profil minimum ayarlar hello için en fazla örnek ölçeklendirme ve ayrıca bu ölçek aralığı etkin olduğunda.

* **Her zaman**

    Her zaman bu aralıktaki kullanılabilir örneklerinin tutun.  

    ![Her zaman ölçeklendirme bulut hizmeti](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Yineleme**

    Merhaba hafta tooscale gün kümesi seçin.

    ![Bulut hizmeti ölçekli bir yineleme zamanlaması](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Sabit tarih**

    Bir sabit tarih aralığı tooscale hello rolü.

    ![Bulut hizmeti ölçekli sabit tarih](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Hello profil yapılandırdıktan sonra hello seçin **Tamam** hello profili dikey penceresi hello sonundaki düğmesi.

#### <a name="rule"></a>Kural
Kuralları tooa profile eklenir ve hello ölçek tetikleyen bir koşul temsil eder.

Merhaba kural tetikleyici hello bulut hizmeti (CPU kullanımı, disk etkinliği veya ağ etkinliği) ölçüsü üzerinde temel toowhich koşullu bir değer ekleyebilirsiniz. Ayrıca, aboneliğinizle ilişkilendirilmiş diğer bazı Azure kaynak ileti sırası veya hello ölçüsü göre hello tetikleyici olabilir.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Hello kuralını yapılandırdıktan sonra hello seçin **Tamam** hello kural dikey penceresinde hello sonundaki düğmesi.

## <a name="back-toomanual-scale"></a>Geri toomanual ölçek
Toohello gidin [ölçek ayarı](#where-scale-is-located) ve kümesi hello **göre Ölçeklendirmeniz** çok seçenek**el ile girdiğim bir örnek sayısı**.

![Bulut Hizmetleri ölçek ayarları profili ve kural](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Bu ayar otomatik ölçeklendirme hello rolden kaldırır ve ardından hello örnek sayısı doğrudan ayarlayabilirsiniz.

1. Merhaba Ölçek (el ile veya otomatik) seçeneği.
2. Bir rol örneği kaydırıcı tooset hello örnekleri tooscale için.
3. Merhaba rol tooscale örnekleri.

Merhaba ölçek ayarlarını yapılandırdıktan sonra hello seçin **kaydetmek** hello üst simgesine tıklayın.
