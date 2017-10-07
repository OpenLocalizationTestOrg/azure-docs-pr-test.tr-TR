---
title: "bir Azure sanal ağ (Klasik) bir benzeşim grubu tooa bölgesinden aaaMigrate | Microsoft Docs"
description: "Nasıl toomigrate sanal ağ (Klasik) üzerinden benzeşim grubunda tooa bölge öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Bir benzeşim grubu tooa bölgesindeki bir sanal ağ (Klasik) geçirme

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager dağıtım modeli kullanmanızı önerir.

Benzeşim grupları, kaynaklar aynı benzeşim grubu fiziksel olarak, bu kaynakları toocommunicate daha hızlı etkinleştirme birbirine yakın sunucuları tarafından barındırılan hello içinde oluşturduğunuzdan emin olun. Geçmiş Hello benzeşim grupları sanal ağları (Klasik) oluşturmak için bir gereksinim yoktu. O anda sanal ağları (Klasik) yönetilen hello Ağ Yöneticisi hizmeti yalnızca fiziksel sunucularda veya ölçek birimi kümesinde işe yarayabilir. Mimari geliştirmeleri ağ yönetimi tooa bölge hello kapsamını artırmıştır.

Bu mimari geliştirmeler sonucunda benzeşim grupları artık önerilen veya sanal ağları (Klasik) için gerekli. benzeşim grupları Hello kullanımını sanal ağları (Klasik) bölgeleri değiştirilir. (Klasik) bölgeleri ile ilişkilendirilmiş sanal ağları bölgesel sanal ağ adı verilir.

Benzeşim grupları genel kullanmamanızı öneririz. Merhaba sanal ağ gereksinimi yanı sıra benzeşim grupları da önemli toouse işlem (Klasik) ve depolama (Klasik) gibi tooensure kaynaklar, diğer yerleştirildi. Ancak, hello geçerli Azure ağ mimarisiyle bu yerleştirme gereksinimleri artık gerekli değildir.

> [!IMPORTANT]
> Hala teknik olarak mümkün toocreate bir benzeşim grubu ile ilişkili bir sanal ağ olmasına karşın, yoktur ilgi çekici herhangi bir nedenle toodo şekilde. Ağ güvenlik grupları gibi birçok sanal ağ özellikleri bölgesel bir sanal ağ kullanırken yalnızca kullanılabilir ve benzeşim gruplarıyla ilişkili sanal ağlar için kullanılamıyor.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Merhaba ağ yapılandırma dosyasını düzenleyin

1. Merhaba ağ yapılandırma dosyasını dışarı aktarın. nasıl tooexport bir ağ yapılandırması PowerShell kullanarak dosya veya Azure komut satırı arabirimi (CLI) 1.0, hello toolearn bkz [bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md#export).
2. Merhaba ağ yapılandırma dosyasını düzenlemenize değiştirme **AffinityGroup** ile **konumu**. Bir Azure belirttiğiniz [bölge](https://azure.microsoft.com/regions) için **konumu**.
   
   > [!NOTE]
   > Merhaba **konumu** , sanal ağ (Klasik) ile ilişkili hello benzeşim grubu için belirtilen hello bölgedir. Örneğin, sanal ağ (Klasik) geçirdiğinizde, Batı ABD içinde bulunan bir benzeşim grubu ile ilişkili ise, **konumu** tooWest ABD işaret etmelidir. 
   > 
   > 
   
    Ağ yapılandırma dosyanızda izleyerek, hello değerleri kendi değerlerinizle değiştirerek hello düzenleyin: 
   
    **Eski değer:** \<VirtualNetworkSitename "VNetUSWest" AffinityGroup = "VNetDemoAG" =\> 
   
    **Yeni değer:** \<VirtualNetworkSitename = "VNetUSWest" Konum "Batı ABD" =\>
3. Değişikliklerinizi kaydetmek ve [alma](virtual-networks-using-network-configuration-file.md#import) ağ yapılandırması tooAzure hello.

> [!NOTE]
> Bu geçiş kapalı kalma süresi tooyour Hizmetleri neden olmaz.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Bir benzeşim grubunda bir VM'ye (Klasik) varsa, hangi toodo
(Klasik), şu anda bir benzeşim grubunda yer alan VM'ler hello benzeşim grubundan kaldırılmış toobe gerekmez. Bir VM dağıtıldığında, dağıtılan tooa tek ölçek birimi değil. Benzeşim grupları, kullanılabilir VM boyutları için yeni bir VM dağıtımı hello kümesi kısıtlayabilir ancak dağıtılan var olan VM zaten kısıtlı toohello kümesi VM boyutları hello ölçek birimi hangi hello VM dağıtılırken kullanılabilir. Tooa ölçek birimi hello VM zaten dağıtılmış olduğundan, bir VM bir benzeşim grubundan kaldırma hello VM üzerinde etkisi yoktur.
