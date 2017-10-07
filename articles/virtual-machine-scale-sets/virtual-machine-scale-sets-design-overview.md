---
title: "aaaDesign Azure sanal makine ölçek kümeleri dikkate alınacak noktalar | Microsoft Docs"
description: "Azure sanal makine ölçek kümeleri için tasarım konuları hakkında bilgi edinin"
keywords: "Linux sanal makine, sanal makine ölçek ayarlar"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Ölçek kümeleri için tasarım konuları
Bu konuda, sanal makine ölçek kümeleri için tasarım konuları açıklanmaktadır. Sanal makine ölçek kümeleri nelerdir hakkında daha fazla bilgi için çok başvurun[sanal makine ölçek kümesi'ne genel bakış](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Ne zaman toouse ölçek yerine sanal makineleri ayarlar?
Genellikle, Ölçek kümeleri makineler kümesi benzer yapılandırmaya sahip olduğu yüksek oranda kullanılabilir altyapısını dağıtmak için kullanışlıdır. Diğer özellikler yalnızca Vm'lerde kullanılabilir, ancak bununla birlikte, bazı özellikler yalnızca ölçek kümeleri içinde kullanılabilir. İçinde ne zaman konusunda bilinçli bir karar toomake sipariş toouse her bir teknolojinin biz öncelikle ölçek kümeleri ancak değil VM'ler kullanılabilir yaygın olarak kullanılan hello özelliklerden bazıları göz atın:

### <a name="scale-set-specific-features"></a>Ölçek kümesi özgü özellikleri

- Merhaba ölçek kümesi yapılandırması belirttiğinizde, daha fazla sanal makineleri paralel hello "kapasite" özelliği toodeploy yalnızca güncelleştirebilirsiniz. Bu paralel birçok ayrı VM dağıtma bir komut dosyası tooorchestrate yazmaktan çok daha kolaydır.
- Yapabilecekleriniz [kullanım Azure otomatik ölçeklendirme tooautomatically ölçek kümesini ölçeklendirin](./virtual-machine-scale-sets-autoscale-overview.md) ancak bireysel VM'ler.
- Yapabilecekleriniz [yeniden görüntü oluşturma ölçek kümesi VM](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) ancak [bireysel VM'ler](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Yapabilecekleriniz [overprovision](./virtual-machine-scale-sets-design-overview.md) ölçek kümesi VM'ler daha fazla güvenilirlik ve daha hızlı dağıtım zamanları için. Bu özel kod toodo yazma sürece bu tek tek sanal makineleri ile yapamazsınız.
- Belirleyebileceğiniz bir [yükseltme İlkesi](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake, kolay tooroll, Ölçek kümesindeki sanal makineleri arasında yükseltme. Tek tek sanal makineleri ile güncelleştirmelerinin kendiniz yönetirler gerekir.

### <a name="vm-specific-features"></a>VM özgü özellikleri

Üzerindeki diğer yandan Merhaba, bazı özellikler yalnızca Vm'lerde kullanılabilir (en az hello anda için):

- Veri diskleri toospecific ekleyebilirsiniz. ölçek kümesindeki tüm VM'ler için tek tek sanal makineleri, ancak eklenen veri disklerini yapılandırılır.
- Boş veri diskleri tooindividual VM'ler ancak ölçek kümesindeki sanal makineleri ekleyebilirsiniz.
- Sizin anlık görüntü tekil bir VM ancak VM ölçek kümesindeki değil.
- Tek bir VM'den ancak VM ölçek kümesindeki bir görüntüsünü yakalayabilirsiniz.
- Yerel diskler toomanaged disklerden tekil bir VM geçirebilirsiniz ancak bu VM'ler için bir ölçek kümesinde işlemi yapamazsınız.
- IPv6 ortak IP adresleri tooindividual VM NIC'ler atayabilirsiniz ancak VM'ler için bir ölçek kümesinde bunu yapamazsınız. IPv6 genel IP adresleri ya da tek tek sanal makineleri önünde tooload dengeleyicileri atayabilir veya VM ölçek kümesi unutmayın.

## <a name="storage"></a>Depolama

### <a name="scale-sets-with-azure-managed-disks"></a>Azure yönetilen diskleri ölçek kümeleri
Ölçek kümeleri ile oluşturulabilir [Azure yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) geleneksel Azure depolama hesapları yerine. Yönetilen diskleri hello aşağıdaki avantajları sağlar:
- Toopre yok-VMs hello ölçeği ayarlamak için Azure depolama hesapları kümesi oluşturun.
- Tanımlayabileceğiniz [veri diskleri ekli](virtual-machine-scale-sets-attached-disks.md) , Ölçek hello VM'ler için ayarlayın.
- Ölçek kümeleri çok yapılandırılabilir[destek too1, 000 VM'ler kümesinde yukarı](virtual-machine-scale-sets-placement-groups.md). 

Var olan bir şablonu varsa, şunları da yapabilirsiniz. [hello şablonu toouse yönetilen diskleri güncelleştirme](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Kullanıcı tarafından yönetilen depolama
Kullanıcı tarafından oluşturulan depolama hesapları toostore hello OS diskleri hello VM'lerin hello kümesindeki yönetilen Azure disklerle tanımlanmamış bir ölçek kümesini kullanır. Depolama hesabı başına veya daha az 20 VM'ler oranını tooachieve en fazla IO ve ayrıca faydalanan önerilir _işleminin_ (aşağıya bakın). Merhaba başlangıç karakterleri hello depolama hesabı adları arasında hello alfabe yayılan önerilir. Yardımcı yük farklı iç sistemlerden yayılan şekilde yapılıyor. 


## <a name="overprovisioning"></a>İşleminin
Ölçek şu anda çok "işleminin" VMs varsayılan ayarlar. Açık işleminin ile hello ölçek gerçekte dönüş için sorulan olandan daha fazla Vm'leri yedekleme ayarlayın, sonra hello istenen VM'ler sayısı sonra ek VM'ler başarıyla hazırlandı hello siler. İşleminin sağlama başarı oranları artırır ve dağıtım süresini azaltır. Merhaba fazladan VM'ler ve bunlar, kota sınırları doğru sayılmaz için faturalandırılır değil.

İşleminin sağlama başarı oranları artırmak olsa da, bu uygulama için kafa karıştırıcı davranışı, neden olabilir değil tasarlanmış toohandle görünmesini ve ardından kayboluyor ek VM'ler olduğu. Kapalı, tooturn işleminin emin olun şablonunuzu dizesinde aşağıdaki hello: `"overprovision": "false"`. Daha fazla ayrıntı hello bulunabilir [ölçek kümesi REST API belgeleri](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Kullanıcı tarafından yönetilen depolama ölçek kümesini kullanıyorsa ve işleminin devre dışı bırakma, depolama hesabı başına 20'den fazla VMs olabilir, ancak toogo 40 g/ç performansı artırmak için yukarıdaki önerilmez. 

## <a name="limits"></a>Sınırlar
Ölçek kümesini bir Market görüntüsü (platform görüntüsü olarak da bilinir) oluşturulmuş ve Azure yönetilen diskleri kapasitesine too1, 000 VM'ler yukarı destekler toouse yapılandırılmış. 100'den fazla VM ölçek kümesi toosupport yapılandırırsanız, tüm senaryoları iş hello aynı (örnek Yük Dengeleme için). Daha fazla bilgi için bkz: [büyük sanal makine ölçek kümeleri ile çalışma](virtual-machine-scale-sets-placement-groups.md). 

Şu anda sınırlı too100 VM'ler ölçeği kullanıcı tarafından yönetilen depolama hesapları ile yapılandırılan Ayarla olmasına (ve 5 depolama hesapları için bu ölçek önerilir).

Özel görüntü (biri tarafından oluşturulan) üzerinde oluşturulan bir ölçek kümesini Azure yönetilen disklerle yapılandırıldığında too100 Vm'leri yedekleme kapasitesine sahip olabilir. Merhaba ölçek kümesini kullanıcı tarafından yönetilen depolama hesapları ile yapılandırılmışsa, bir depolama hesabı içindeki tüm işletim sistemi diski VHD'leri oluşturmanız gerekir. Sonuç olarak, özel bir görüntüde yerleşik ölçek kümesindeki VM'lerin sayısını hello maksimum önerilen ve kullanıcı tarafından yönetilen depolama 20'dir. İşleminin devre dışı bıraktığınızda too40 gidebilirsiniz.

Daha fazla VM'ler için bu sınırları izin verdiğinden, gösterildiği gibi birden fazla ölçek ayarlar toodeploy gerek [bu şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

