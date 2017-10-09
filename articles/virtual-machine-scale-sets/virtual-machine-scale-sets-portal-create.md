---
title: "Azure portal kullanarak bir sanal makine ölçek kümesi aaaCreate hello | Microsoft Docs"
description: "Azure portalını kullanarak ölçek kümeleri dağıtın."
keywords: "Sanal makine ölçekleme kümeleri"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Nasıl bir sanal makine ölçek kümesi ile toocreate hello Azure portalı
Bu öğretici, ne kadar kolay toocreate bir sanal makine ölçek kümesi yalnızca birkaç dakika içinde hello Azure portal kullanarak olduğunu gösterir. Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Merhaba Marketi'nden Hello VM görüntüsü seçin
Merhaba Portalı'ndan bir ölçeği CentOS, CoreOS, Debian, açık Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server veya Windows Server görüntülerini ile Ayarla kolayca dağıtabilirsiniz.

İlk olarak, toohello gidin [Azure portal](https://portal.azure.com) bir web tarayıcısında. Tıklatın `New`, arama `scale set`seçip hello `Virtual machine scale set` girişi:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Merhaba ölçek kümesi oluşturma
Şimdi hello varsayılan ayarları kullanmak ve hızlı bir şekilde hello ölçek kümesi oluşturun.

* Merhaba üzerinde `Basics` dikey penceresinde hello ölçek kümesi için bir ad girin. Bu adı hello temel haline hello hello yük dengeleyici hello ölçek kümesini önünde FQDN'sini bu nedenle hello adı benzersiz tüm Azure arasında olduğundan emin olun.
* Tercih ettiğiniz seçin, istenen işletim sistemi yazın, istediğiniz kullanıcı adınızı girin ve kimlik doğrulama türünü seçin. Bir parola seçerseniz, en az 12 karakter uzunluğunda ve üç dışında hello dört aşağıdaki karmaşıklık gereksinimlerini karşılayacak olmalıdır: bir küçük harf karakter, bir büyük harf karakter, bir sayı ve bir özel karakter. [Kullanıcı adı ve parola gereksinimleri](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm) hakkında daha fazla bilgi edinin. Seçerseniz `SSH public key`, emin tooonly Yapıştır ortak anahtarınızı, özel anahtarınızı değil:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Tooa tek yerleştirme Grup toolimit hello ölçek kümesi gibi veya birden çok yerleştirme grupları yayılacağı olup olmadığını yaptığınız seçin. Ölçek ayarlar belirli kısıtlamalarla 100'den VM'ler Kapasite (yukarı too1, 000) için hello ölçek toospan yerleştirme grupları olanak sağlar. Daha fazla bilgi için bkz: [bu belgeleri](./virtual-machine-scale-sets-placement-groups.md).
* İstenen kaynak grubu adı ve konum girin ve ardından `OK`.
* Merhaba üzerinde `Virtual machine scale set service settings` dikey: İstenen etki alanı adı etiketi (Merhaba ölçek kümesini önünde hello yük dengeleyici için FQDN hello hello tabanı) girin. Bu etiketi tüm Azure arasında benzersiz olması gerekir.
* İstenen işletim sistemi disk görüntüsü, örnek sayısı ve makine boyutu seçin.
* İstenen disk türünü seçin: yönetilen veya yönetilmeyen. Daha fazla bilgi için bkz: [bu belgeleri](./virtual-machine-scale-sets-managed-disks.md). Toohave hello ölçek kümesini seçerseniz birden çok yerleştirme grupları span, yönetilen disk ölçek kümeleri toospan yerleştirme grupları için gerekli olmadığından bu seçenek kullanılamaz.
* Etkinleştirmek veya otomatik ölçeklendirme devre dışı bırakın ve etkinleştirilirse yapılandırın:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Merhaba üzerinde `Summary` doğrulama işiniz bittiğinde, dikey tıklayın `OK` toostart hello ölçek kümesi dağıtım.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Merhaba ölçek kümesindeki VM tooa Bağlan
Toolimit seçerseniz, Ölçek tooa tek yerleştirme Grup ayarlayın, ardından hello ölçek kümesini NAT kuralları yapılandırılmış toolet toohello ölçeği kolayca Ayarla bağlandığınız dağıtılan (tooconnect toohello sanal makineleri hello ölçeğinde ayarlı değil, büyük olasılıkla toocreate gerekir bir Merhaba jumpbox hello ölçek kümesi aynı sanal ağ). toosee bunları gidin toohello `Inbound NAT Rules` hello yük dengeleyici hello ölçek kümesi için sekmesinde:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Bu NAT kurallarını kullanarak VM hello ölçek kümesi tooeach bağlanabilir. Gelen bağlantı noktasını 50000, NAT kuralı ise örneği için bir Windows ölçek kümesi için RDP aracılığıyla toothat makine üzerindeki bağlantı kurulamadı `<load-balancer-ip-address>:50000`. Linux ölçek kümesi için hello komutunu kullanarak bağlandığınız `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl toodeploy ölçek CLI hello ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-cli-quick-create.md).

Toodeploy ölçek Powershell'den nasıl ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-windows-create.md).

Nasıl toodeploy ölçek Visual Studio'dan ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-vs-create.md).

Merhaba genel belgelerini denetleyin [belgelerine genel bakış sayfasında ölçek kümeleri için](virtual-machine-scale-sets-overview.md).

Genel bilgi için hello denetleyin [ölçek kümeleri için ana giriş sayfasının](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

