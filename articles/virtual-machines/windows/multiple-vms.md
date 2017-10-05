---
title: "Birden çok sanal makine oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 5e96805f8880a30a5fc8779d8f07addb6d068c09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Birden çok Azure sanal makinesi oluşturma
Burada, çok sayıda benzer sanal makineler (VM'ler) oluşturmak için gereken birçok senaryo vardır. Bazı örnekler, yüksek performanslı bilgi işlem (HPC), büyük ölçekli veri analizi, ölçeklenebilir ve genellikle durum bilgisiz orta katman veya arka uç sunucuları (örneğin, Web sunucuları) ve dağıtılmış veritabanlarını içerir.

Bu makalede Azure içinde birden çok VM oluşturmak için kullanılabilir seçenekleri açıklanmaktadır. Bu seçenekler VM'ler bir dizi el ile oluşturduğunuz basit durumlar gidin. Birçok VM oluşturmak için de en fazla sayıda sanal makineleri oluşturmanız gerekiyorsa, genellikle kullandığınız işlemleri ölçeklendirmeyin.

Birçok benzer VM oluşturmanın yollarından biri, Azure Resource Manager yapı kullanmaktır *kaynak döngüler*.

## <a name="resource-loops"></a>Kaynak döngüler
Kaynak döngüler bir söz dizimi toplu Azure Resource Manager şablonlarındaki ' dir. Kaynak döngüler bir döngüde benzer şekilde yapılandırılmış kaynak kümesi oluşturabilirsiniz. Kaynak döngüler, birden çok depolama hesapları, ağ arabirimlerine veya sanal makineler oluşturmak için kullanabilirsiniz. Kaynak döngüleri hakkında daha fazla bilgi için başvurmak [kaynak döngüler kullanarak kullanılabilirlik kümeleri oluşturma Vm'lerde](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Ölçek zorlukları
Bir bulut altyapısı ölçekte çıkışı oluşturmak ve daha kısa şablonları oluşturmak kolaylaştırmak kaynak döngüler rağmen bazı zorluklar kalır. Örneğin, 100 sanal makine oluşturmak için bir kaynak döngü kullanırsanız, ağ arabirim denetleyicilerini (NIC'ler) karşılık gelen sanal makineleri ve depolama hesapları ile ilişkilendirilmesi gerekir. VM sayısını büyük olasılıkla depolama hesapları sayısından farklı olduğundan, farklı kaynak döngü boyutlarıyla çok mücadele etmek zorunda kalırsınız. Bunlar solvable sorunları olan, ancak ölçekli karmaşıklığını önemli ölçüde artırır.

Özellikler esnek ölçeklendirir bir altyapı gerektiğinde başka bir sınama oluşur. Örneğin, otomatik olarak artırır veya yanıt iş yükü olarak VM sayısını azaltır bir otomatik ölçeklendirme altyapısı isteyebilirsiniz. Sanal makineleri sayısı (genişleme ve ölçek) değiştirmek için tümleşik bir mekanizması sunmaz. İçinde sanal makineleri kaldırarak ölçekleme, VM'ler güncelleştirme ve hata etki alanları arasında dengeli sağlayarak yüksek oranda kullanılabilirlik garanti etmek zordur.

Son olarak, bir kaynak döngü kullandığınızda, temel alınan doku kaynakları oluşturmak için birden fazla çağrı gidin. Birden fazla çağrı benzer kaynaklarını oluşturduğunuzda, Azure üzerinde bu tasarım geliştirmek ve dağıtım güvenilirliğini ve performansını iyileştirmek için örtük bir fırsat sahiptir. Bu yerdir *sanal makine ölçek kümeleri* geldikçe.

## <a name="virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri
Sanal makine ölçek kümeleri dağıtmak ve aynı VM'ler kümesini yönetmek için bir Azure işlem kaynaktır. Tüm VM'ler ile aynı, VM ölçek kümeleri içinde ölçeklendirmek ve ölçeğini kolayca yapılandırılmış. Yalnızca kümesindeki VM'lerin sayısını değiştirin. İş yükü taleplerine göre otomatik ölçeklendirme VM ölçek kümesi de yapılandırabilirsiniz.

İşlem kaynakları ve ölçeklendirmek için gereken uygulamalar için ölçek işlemleri örtük olarak arıza ve güncelleştirme etki alanları arasında dengeli.

NIC ve sanal makineleri gibi birden fazla kaynak bağıntı yerine bir VM ölçek kümesi ağ, depolama, sanal makine ve merkezi olarak yapılandırmanız uzantı özellikleri vardır.

VM ölçek kümesi için giriş için başvurmak [sanal makine ölçek ayarlar ürün sayfası](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Daha ayrıntılı bilgi için şuraya gidin [sanal makine ölçek ayarlar belgelerine](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

