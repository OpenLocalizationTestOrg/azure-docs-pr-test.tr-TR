---
title: "Azure Ağ İzleyicisi aaaIntroduction toosecurity Grup görünümünde | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi güvenlik görünüm yetenek genel bir bakış sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Giriş toonetwork güvenlik grubu Azure Ağ İzleyicisi görünümünde

Ağ güvenlik grupları, bir alt ağ düzeyinde veya bir NIC düzeyi ilişkilendirilir. Bir alt düzeyde ilişkili hello alt ağdaki tooall hello VM örnekleri uygulanır. Ağ güvenlik grubu görünümü tüm yapılandırılmış hello Nsg'ler ve hello yapılandırma hakkında bilgi sağlayan bir sanal makine için bir NIC ve alt ağ düzeyinde ilişkili kurallar döndürür. Ayrıca, her bir VM hello NIC hello etkin güvenlik kuralları döndürülür. Ağ güvenlik grubu kullanarak görünüm açık bağlantı noktaları gibi ağ güvenlik açıkları için bir VM değerlendirebilirsiniz. De doğrulamak, ağ güvenlik grubu temel alarak beklendiği gibi çalışıp çalışmadığını bir [hello karşılaştırması yapılandırılmış ve etkin güvenlik kuralları hello](network-watcher-nsg-auditing-powershell.md).

Daha uzun bir kullanım örneği, güvenlik uyumluluğunu ve denetim gerçekleştirilir. Kuruluşunuzdaki güvenlik idare modeli olarak güvenlik kuralları Düzenleyici kümesi tanımlayabilirsiniz. Bir dönemsel uyumluluk denetimi hello VM'ler, ağınızdaki her hello düzenleyici kuralları hello etkili kuralları ile karşılaştırarak programlı bir şekilde uygulanabilir.

Hello portal kuralları etkili, alt ağ, ağ arabirimi ve varsayılan ayrılır. Bu basit bir hello uygulanan kurallar tooa sanal makine görünüme sağlar. Tooeasily karşıdan hello sekmesini olursa olsun tüm hello güvenlik kuralları bir CSV dosyasına karşıdan yükle düğmesi bulunur.

![Güvenlik grubu görünümü][1]

Kuralları seçilebilir ve tooshow hello ağ güvenlik grubu ve kaynak ve hedef öneklerinin yeni bir dikey pencere açılır. Bu dikey pencereden toohello ağ güvenlik grubu kaynak doğrudan gidebilirsiniz.

![ayrıntıya gitme][2]

### <a name="next-steps"></a>Sonraki adımlar

Tooaudit ağınızda güvenlik Grup nasıl öğrenin ayarları şu adresi ziyaret ederek [PowerShell ile denetim ağ güvenlik grubu ayarları](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









