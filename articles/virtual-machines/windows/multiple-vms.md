---
title: "aaaCreate birden çok sanal makine | Microsoft Docs"
description: "Windows üzerinde birden çok sanal makine oluşturmak için Seçenekler"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Birden çok Azure sanal makinesi oluşturma
Burada toocreate çok sayıda benzer sanal makineler (VM'ler) gereken birçok senaryo vardır. Bazı örnekler, yüksek performanslı bilgi işlem (HPC), büyük ölçekli veri analizi, ölçeklenebilir ve genellikle durum bilgisiz orta katman veya arka uç sunucuları (örneğin, Web sunucuları) ve dağıtılmış veritabanlarını içerir.

Bu makalede Azure birden çok VM hello kullanılabilir seçenekler toocreate anlatılmaktadır. Bu seçenekler hello basit durumlar VM'ler bir dizi el ile oluşturduğunuz gidin. iyi VM'ler sayıda birden çok toocreate gerekiyorsa toocreate birçok VM, genellikle kullandığınız hello işlemleri ölçeklendirmeyin.

Birçok benzer VM olduğu toouse hello Azure Resource Manager yapı, tek yönlü toocreate *kaynak döngüler*.

## <a name="resource-loops"></a>Kaynak döngüler
Kaynak döngüler bir söz dizimi toplu Azure Resource Manager şablonlarındaki ' dir. Kaynak döngüler bir döngüde benzer şekilde yapılandırılmış kaynak kümesi oluşturabilirsiniz. Birden çok depolama hesapları, ağ arabirimlerine veya sanal makineleri kaynak döngüler toocreate kullanabilirsiniz. Kaynak döngüleri hakkında daha fazla bilgi için çok başvuran[kaynak döngüler kullanarak kullanılabilirlik kümeleri oluşturma Vm'lerde](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Ölçek zorlukları
Kaynak döngüler ölçekte bir bulut altyapısı çıkışı daha kolay toobuild kolaylaştırır ve daha kısa şablonları oluşturmak, ancak bazı zorluklar kalır. Örneğin, bir kaynak döngü toocreate 100 sanal makineler kullanırsanız, karşılık gelen sanal makineleri ve depolama hesapları ile toocorrelate ağ arabirim denetleyicilerini (NIC'ler) gerekir. VM Hello sayısı büyük olasılıkla toobe hello depolama hesapları sayısından farklı olduğundan, farklı kaynak döngü boyutlarıyla toodeal çok sahip olacaksınız. Bunlar solvable sorunları olan, ancak ölçekli hello karmaşıklığını önemli ölçüde artırır.

Özellikler esnek ölçeklendirir bir altyapı gerektiğinde başka bir sınama oluşur. Örneğin, otomatik olarak artırır veya hello sayısında VM'ler yanıt tooworkload azaltır bir otomatik ölçeklendirme altyapısı isteyebilirsiniz. Sanal makineleri bir tümleşik mekanizması toovary sayısı (genişleme ve ölçek) sağlamaz. İçinde sanal makineleri kaldırarak ölçekleme, VM'ler güncelleştirme ve hata etki alanları arasında dengeli sağlayarak zor tooguarantee yüksek kullanılabilirlik olur.

Son olarak, bir kaynak döngü kullandığınızda, birden çok çağrıları toocreate kaynaklara toohello temel alınan doku bakın. Birden fazla çağrı benzer kaynaklarını oluşturduğunuzda, Azure örtük fırsat tooimprove bu tasarım bağlı olan ve dağıtım güvenilirliği ve performansı en iyi duruma getirme. Bu yerdir *sanal makine ölçek kümeleri* geldikçe.

## <a name="virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri
Sanal makine ölçek kümeleri bir Azure işlem kaynak toodeploy olan ve aynı sanal makineleri bir dizi yönetin. Yapılandırılan tüm sanal makineleri ile aynı Merhaba, VM ölçek kümesi içinde kolay tooscale ve ölçek genişletme. Yalnızca hello hello kümesindeki VM'lerin sayısını değiştirin. VM ölçek kümeleri tooautoscale hello iş yükü hello taleplerine göre de yapılandırabilirsiniz.

Tooscale işlem kaynakları oturumunuzu kapatıp, Ölçek gereken uygulamalar için işlemleri örtük olarak arıza ve güncelleştirme etki alanları arasında dengeli.

NIC ve sanal makineleri gibi birden fazla kaynak bağıntı yerine bir VM ölçek kümesi ağ, depolama, sanal makine ve merkezi olarak yapılandırmanız uzantı özellikleri vardır.

Bir giriş tooVM ölçek ayarlar için toohello başvuran [sanal makine ölçek ayarlar ürün sayfası](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Daha ayrıntılı bilgi için toohello Git [sanal makine ölçek ayarlar belgelerine](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

