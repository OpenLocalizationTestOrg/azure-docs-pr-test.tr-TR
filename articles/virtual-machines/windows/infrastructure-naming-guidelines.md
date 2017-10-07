---
title: "adlandırma yönergeleri - Windows aaaAzure altyapı | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde adlandırma hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a>Adlandırma yönergeleri Windows VM'ler için azure altyapı

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede, tüm, çeşitli Azure kaynaklarını toobuild mantıksal ve kolayca tanımlanabilen bir adlandırma kurallarına tooapproach kaynakları ortamınızda çoğaltmanın nasıl ayarlanacağını anlamaya odaklanır.

## <a name="implementation-guidelines-for-naming-conventions"></a>Uygulama yönergeleri için adlandırma kuralları
Kararları:

* Azure kaynakları için adlandırma kuralları nelerdir?

Görevler:

* Merhaba affixes toouse, kaynakları toomaintain tutarlılık arasında tanımlayın.
* Depolama hesabı adları verilen bunları gereksinimini toobe genel benzersiz hello tanımlayın.
* Belge hello adlandırma kuralı toobe kullanılan ve tooall tarafların dahil edilen tooensure tutarlılık dağıtımlar arasında dağıtabilirsiniz.

## <a name="naming-conventions"></a>Adlandırma kuralları
Herhangi bir şey Azure'da oluşturmadan önce iyi bir adlandırma kuralı yerinde olmalıdır. Bir adlandırma kuralı tüm hello kaynakları kaynaklarla yönetmeyle ilgili alt hello yönetici yükünü yardımcı olan bir tahmin edilebilir ad sahip olmasını sağlar.

Adlandırma kuralları belirli Azure aboneliği veya hesabı veya tüm kuruluşunuz için tanımlanan belirli bir dizi toofollow seçebilirsiniz. Bu bir takım Azure üzerinde bir proje üzerinde toowork gerektiğinde Azure kaynakları ile çalışırken, kuruluşların tooestablish örtük kuralları içinde kişiler için kolay olsa da, bu model iyi ölçeklenmez.

Adlandırma kuralları Önden kümesinde kabul etmiş olursunuz. Bu kurallar kümesine arasında Kes adlandırma kuralları ile ilgili bazı noktalar vardır.

## <a name="affixes"></a>Affixes
Toodefine bir adlandırma kuralı Ara gibi hello eklemesi adresindeki olup bir karar gelir:

* Merhaba adı (önek) Hello başlangıcı
* Merhaba adının sonuna kadar hello (sonek)

Örneğin, hello kullanarak bir kaynak grubu için iki olası adları şunlardır `rg` eklemesi:

* Rg WebApp (önek)
* WebApp Rg (sonek)

Affixes hello belirli kaynakları tanımlayan toodifferent yönlerini başvurabilir. Merhaba aşağıdaki tabloda genelde kullanılan bazı örnekler gösterilmektedir.

| En boy | Örnekler | Notlar |
|:--- |:--- |:--- |
| Ortam |geliştirme, stg, üretim |Merhaba amacı ve her ortam adı bağlı olarak. |
| Konum |usw (Batı ABD) kullanın (Doğu ABD 2) |Merhaba hello datacenter veya hello bölge hello kuruluşun bölgesi bağlı olarak. |
| Azure bileşeni, hizmet veya ürünün |Kaynak grubu, sanal ağ için sanal ağ için rg |Kaynak için hangi hello sağlar hello ürün bağlı olarak destekler. |
| Rol |SQL, ya, sp, IIS |Merhaba sanal makinenin Hello rolüne bağlı olarak. |
| Örnek |01, 02, 03, vs. |Birden fazla örneğine sahip kaynaklar. Örneğin, web sunucuları bir bulut hizmetinde yük dengeli. |

Adlandırma kuralları oluşturulurken, bunlar açıkça hangi durumunda olduğundan emin olun kaynağının ve hangi konumda (önek vs sonek) her tür için toouse affixes.

## <a name="dates"></a>tarihleri
Genellikle, bir kaynağın hello adından oluşturma önemli toodetermine hello tarihi olur. Merhaba YYYYAAGG tarih biçimi öneririz. Bu biçim yalnızca hello tam tarih kaydedilir ancak aynı zamanda adları farklı yalnızca başlangıç tarihi bu iki kaynak hello sıralanmış alfabetik ve kronolojik sağlar aynı anda.

## <a name="naming-resources"></a>Adlandırma kaynakları
Merhaba Adlandırma kuralında her kaynak türünü tanımlayın, nasıl tooassign tooeach kaynak, adları tanımlayan kurallar olmalıdır oluşturulur. Bu kurallar tooall türdeki kaynağı örneğin uygulamanız gerekir:

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

başvurduğu yeterli bilgi toodetermine toowhich kaynak adı hello tooensure sağlar, açıklayıcı adlar kullanmanız gerekir.

## <a name="computer-names"></a>Bilgisayar adları
Bir sanal makine (VM) oluşturduğunuzda, Microsoft Azure hello kaynak adı için kullanılan bir VM adı, too15 karakter gerektirir. Azure kullanır hello VM yüklü hello işletim sistemi için aynı adı hello. Ancak, bu adları değil her zaman olması hello aynı.

Bir VM zaten bir işletim sistemini içeren bir .vhd görüntü dosyasından oluşturulan durumunda, azure'da hello VM adı VM'nin işletim sisteminin bilgisayar adı hello farklı olabilir. Bu durum, bu nedenle değil öneririz zorluk tooVM yönetim derecesini ekleyebilirsiniz. Hello Azure VM kaynak hello aynı toohello işletim sistemi, VM atamak hello bilgisayar adı atayın.

Bu hello Azure VM adı olduğu hello işletim sisteminin bilgisayar adı altındaki hello aynı öneririz.

## <a name="storage-account-names"></a>Depolama hesabı adları
Bu bölümde çok uygulanmaz[Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)ayrı bir depolama hesabı oluşturma gibi. Yönetilmeyen diskler için depolama hesapları adlarını yöneten özel kurallar vardır. Yalnızca küçük harfler ve sayılar da kullanabilirsiniz. Daha fazla bilgi için bkz: [depolama hesabı oluşturma](../../storage/storage-create-storage-account.md#create-a-storage-account). Ayrıca, core.windows.net, birlikte hello depolama hesabı adı genel olarak geçerli, benzersiz bir DNS adı olmalıdır. Merhaba depolama hesabı mystorageaccount çağrılırsa, örneğin, hello aşağıdaki ortaya çıkan DNS adları benzersiz olmalıdır:

* mystorageaccount.BLOB.Core.Windows.NET
* mystorageaccount.Table.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

