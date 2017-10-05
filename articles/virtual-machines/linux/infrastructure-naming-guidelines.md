---
title: "Adlandırma yönergeleri - Linux azure altyapı | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde adlandırma anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1b086f0972c02d569a7219820a3d596960b6014b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Azure altyapı Linux VM'ler için adlandırma yönergeleri 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede, ortamınızda çoğaltmanın mantıksal ve kolayca tanımlanabilen bir kaynak kümesi oluşturmak tüm çeşitli Azure kaynaklarınızı için adlandırma kurallarını yaklaşımlardan nasıl anlamaya odaklanır.

## <a name="implementation-guidelines-for-naming-conventions"></a>Uygulama yönergeleri için adlandırma kuralları
Kararları:

* Azure kaynakları için adlandırma kuralları nelerdir?

Görevler:

* Kaynaklarınız arasında tutarlılık sağlamak için kullanılacak affixes tanımlayın.
* Depolama hesabı adları bunları genel olarak benzersiz olması gereksinimini verilen tanımlayın.
* Kullanılması ve dağıtımlar arasında tutarlılık sağlamak için ilgili tüm taraflara dağıtmak için adlandırma kuralı belge.

## <a name="naming-conventions"></a>Adlandırma kuralları
Herhangi bir şey Azure'da oluşturmadan önce iyi bir adlandırma kuralı yerinde olmalıdır. Bir adlandırma kuralı tüm kaynakları yardımcı olan bu kaynakları yönetmeyle ilgili yönetim yükünü azaltmak tahmin edilebilir bir ad sağlar.

Adlandırma kuralları belirli Azure aboneliği veya hesabı veya tüm kuruluşunuz için tanımlanan belirli bir kümesini izlemek seçebilirsiniz. Azure kaynakları ile çalışırken örtük kuralları oluşturmak kuruluş içinde kişiler için kolay olsa da, birlikte Azure'da çalışan takımlar için ölçeklendirebilirsiniz olmanız gerekir.

Adlandırma kuralları Önden kümesinde kabul etmiş olursunuz. Kuralları ayarlar için arasında Kes adlandırma kuralları ile ilgili bazı noktalar vardır.

## <a name="affixes"></a>Affixes
Bir adlandırma kuralını tanımlamak için konum olarak bir eklemesi adresindeki olup bir karardır:

* (Önek) adı başlangıcı
* Adının sonuna (sonek)

Örneğin, bir kaynak grubu kullanmak için iki olası adları şunlardır `rg` eklemesi:

* Rg WebApp (önek)
* WebApp Rg (sonek)

Affixes belirli kaynakları tanımlayan farklı yönleri başvurabilir. Aşağıdaki tabloda, genelde kullanılan bazı örnekler gösterilmektedir.

| En boy | Örnekler | Notlar |
|:--- |:--- |:--- |
| Ortam |geliştirme, stg, üretim |Amaç ve her ortam adı bağlı olarak. |
| Konum |usw (Batı ABD) kullanın (Doğu ABD 2) |Veri merkezi veya kuruluşun bölgesinin bölge bağlı olarak. |
| Azure bileşeni, hizmet veya ürünün |Kaynak grubu, sanal ağ için sanal ağ için rg |Kaynak sağlayan ürün bağlı olarak destekler. |
| Rol |DB, uygulama, web |Sanal makine rolüne bağlı olarak. |
| Örnek |01, 02, 03, vs. |Birden fazla örneğine sahip kaynaklar. Örneğin, web sunucuları bir bulut hizmetinde yük dengeli. |

Adlandırma kuralları oluşturulurken, bunlar açık bir şekilde her tür kaynağının ve hangi konumda (önek vs sonek) kullanılmak üzere hangi affixes durum emin olun.

## <a name="dates"></a>tarihleri
Genellikle, bir kaynak adı oluşturulma tarihi belirlemek önemlidir. YYYYAAGG tarih biçimi öneririz. Bu biçim, yalnızca tam sağlar tarih kaydedilir, ancak ayrıca adları farklı tarih yalnızca bu iki kaynak alfabetik olarak ve tarih sırasına göre sıralanır.

## <a name="naming-resources"></a>Adlandırma kaynakları
Her tür tanımlama adlandırma kuralı kaynak, hangi oluşturulan her bir kaynağın adları atama tanımlayan kurallar olmalıdır. Bu kurallar, kaynaklar, tüm türleri için örneğin uygulamanız gerekir:

* Abonelikler
* Hesaplar
* Depolama hesapları
* Sanal ağlar
* Alt ağlar
* Kullanılabilirlik kümeleri
* Kaynak grupları
* Sanal makineler
* Uç Noktalar
* Ağ güvenlik grupları
* Roller

Adı emin olmak için hangi kaynağa başvuruyor, açıklayıcı adlar kullanmanız gerektiğini belirlemek için yeterli bilgi sağlar.

## <a name="computer-names"></a>Bilgisayar adları
Bir sanal makine (VM) oluşturduğunuzda, Azure kaynak adı için kullanılan bir VM adı en fazla 64 karakter gerektirir. Azure VM'de yüklü işletim sistemi için aynı adı kullanır. Ancak, bu adlar her zaman aynı olmayabilir.

Bir VM .vhd görüntü dosyasından bir işletim sistemini zaten içeriyor oluşturduysanız, Azure VM adı VM'ın işletim sistemi bilgisayar adından farklı olabilir. Bu durum, bu nedenle değil öneririz VM yönetimi için Zorluk derecesini ekleyebilirsiniz. Azure VM kaynak aynı adı taşıyan o VM için işletim sistemini atadığınız bilgisayar atayın.

Azure VM adını temel işletim sisteminin bilgisayar adı ile aynı olduğunu öneririz.

## <a name="storage-account-names"></a>Depolama hesabı adları
Bu bölümde uygulanmaz [Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)ayrı bir depolama hesabı oluşturma gibi. Yönetilmeyen diskler için depolama hesapları adlarını yöneten özel kurallar vardır. Yalnızca küçük harfler ve sayılar da kullanabilirsiniz. Daha fazla bilgi için bkz: [depolama hesabı oluşturma](../../storage/storage-create-storage-account.md#create-a-storage-account). Ayrıca, depolama hesabı adıyla core.windows.net, genel olarak geçerli, benzersiz bir DNS adı olmalıdır. Örneğin, depolama hesabı mystorageaccount çağrılırsa, aşağıdaki ortaya çıkan DNS adları benzersiz olmalıdır:

* mystorageaccount.BLOB.Core.Windows.NET
* mystorageaccount.Table.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

