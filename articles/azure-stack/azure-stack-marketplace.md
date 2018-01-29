---
title: "Özel Market öğesi Azure yığın (bulut işleci) yayımlama | Microsoft Docs"
description: "Bir Azure yığın operatör olarak Azure yığınında özel Market öğesi yayımlama hakkında bilgi edinin."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 7b5f976eb2d51eb86761a2bd0be6adb45ca87681
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="the-azure-stack-marketplace-overview"></a>Azure yığın Market genel bakış

*Uygulandığı öğe: Azure yığın tümleşik sistemleri ve Azure yığın Geliştirme Seti*

Market, hizmetleri, uygulamaları ve ağlar, sanal makineler, depolama ve benzerleri gibi Azure yığını için özelleştirilmiş kaynakları koleksiyonudur. Kullanıcılar yeni uygulamalar yeni kaynaklar oluşturma ve dağıtma için buraya gelin. Bunu, kullanıcıların göz atın ve bunlar kullanmak istediğiniz öğeleri seçin bir alışveriş katalog olarak düşünün. Market öğesi kullanmak için kullanıcılar öğesine erişimi veren bir teklif için abone olmalısınız.

Bir Azure yığın operatör olarak eklemek için öğeleri karar verin (Marketinde yayımlama). Veritabanları, uygulama hizmetleri ve benzeri gibi yayımlayabilirsiniz. Bu, tüm kullanıcılar için görünür sağlar. Oluşturduğunuz özel öğeler yayımlayabilirsiniz. Bir büyümesini öğeleri de yayımlayabilirsiniz [Azure Market öğelerinin listesini](azure-stack-marketplace-azure-items.md). Kullanıcılar Markete bir öğe yayımladığınızda, beş dakika içinde görebilir.

Market'ı açmak için **yeni**.

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a>Market öğesi
Bir Azure yığın Market hizmeti, uygulama veya kullanıcılarınızın indirin ve kullanın kaynak öğedir. Tüm Azure yığın Market öğesi, tüm kullanıcılar tarafından görülebilir.

Her bir Market öğe vardır:

* Kaynak sağlama için bir Azure Resource Manager şablonu
* Dizeleri, simgeler ve diğer pazarlama malzemeleri gibi meta veriler
* Portalda öğeyi görüntülemek için bilgi biçimlendirme

Market'te yayımlanan her öğenin Azure galeri paketi (azpkg) adlı bir biçim kullanır. Dağıtım veya çalışma zamanı kaynakları (örneğin, kod, ZIP dosyalarıyla yazılım ya da sanal makine görüntülerini) Azure yığınına Market öğesi bir parçası değil ayrı olarak ekleyin. 

## <a name="next-steps"></a>Sonraki adımlar
[Oluşturma ve bir Market öğesi yayımlama](azure-stack-create-and-publish-marketplace-item.md)

