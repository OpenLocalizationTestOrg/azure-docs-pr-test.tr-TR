---
title: Windows sanal makinelerde SAP aaaUsing | Microsoft Docs
description: "Microsoft Azure Windows sanal makinelerle (VM'ler) SAP kullanma hakkında Temizle"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Azure'da Windows sanal makinelerde SAP kullanma
Bulut bilgi işlem, daha da fazla önem hello BT endüstri içinde toolarge ve çokuluslu şirketler yukarı küçük şirketlerden elde yaygın olarak kullanılan bir terimdir. Microsoft Azure hello paylaşılabilen çok sayıda yeni olanakları sunan Microsoft bulut hizmetleri platformu ' dir. Değil sınırlı tootechnical veya bütçeleme kısıtlamaları; bu nedenle şimdi müşteriler mümkün toorapidly sağlama ve devre dışı bırakma sağlama bulut-Hizmetleri uygulamalardır. Donanım altyapısını zamandan ve yatırım yapmak yerine, şirketler Merhaba uygulaması, iş süreçlerini ve onun avantajlarını müşteriler ve kullanıcılar için odaklanabilirsiniz.

Microsoft Azure sanal makinelerle Microsoft olarak hizmet (Iaas) platform kapsamlı bir altyapı sunar. SAP NetWeaver tabanlı uygulamalar, Azure Sanal Makinelerinde (IaaS) desteklenmektedir. Merhaba teknik incelemeler aşağıdaki nasıl tooplan ve uygulama SAP NetWeaver tabanlı uygulamaları azure'da Windows sanal makinelerde açıklanmaktadır. SAP NetWeaver tabanlı uygulamalar üzerinde uygulayabilirsiniz [Linux sanal makineleri](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver azure'da - HA
Başlık: aaaSAP NetWeaver azure'da - kümeleme SAP ASCS/SCS SIOS DataKeeper ile azure'da Windows Server Yük devretme kullanarak örnekleri

Özet: ' Bu belgede açıklanan nasıl toouse SIOS DataKeeper tooset Azure üzerinde yüksek oranda kullanılabilir bir SAP ASCS/SCS yapılandırması. SAP hatası bileşenleriyle SAP ASCS/SCS veya kuyruğa Çoğaltma Hizmetleri gibi paylaşılan diskleri gerektiren Windows Server Yük devretme yapılandırmaları kendi tek noktası korur. Bu SAP bileşenleri SAP sistem hello işlevleri için gereklidir. Bu nedenle toobe koyun yüksek kullanılabilirlik işlevselliği gereksinimlerini toomake bu bileşenlerin tam ve Hyper-V ortamları için Windows Küme yapılandırmaları ile bitti olarak bir sunucu veya bir VM başarısızlığını karşılayabilir emin yerleştirin. Ağustos 2015'ten itibaren kendisini Azure'da hello Windows için gerekli olacak paylaşılan diskleri yüksek oranda kullanılabilir yapılandırmaları Bu kritik SAP bileşenler için gerekli temel sağlayamaz. Ancak hello ürün DataKeeper SIOS tarafından hello yardımıyla, SAP ASCS/SCS için gerektiği gibi Windows Server Yük devretme yapılandırmaları hello Azure Iaas platformu üzerinde oluşturulabilir. Bu yazı, nasıl bir Windows Server Yük devretme yapılandırması paylaşılan disk ile SIOS Datakeeper Azure tarafından sağlanan tooinstall adım adım bir yaklaşım açıklar. Merhaba kağıt hello yüksek kullanılabilirlik yapılandırması bir en iyi şekilde çalışması yapan hello Azure, Windows ve SAP tarafında yapılandırmaları Ayrıntılar açıklanmaktadır. Merhaba kağıt hazırlandı hello SAP yükleme belgelerini ve yüklemeleri ve SAP yazılımı dağıtımları için hello birincil kaynakları temsil eden SAP Notlar platformları verilir.

Güncelleştirilmiş: Ağustos 2015

[Bu kılavuzu hemen indirin](http://go.microsoft.com/fwlink/?LinkId=613056)

