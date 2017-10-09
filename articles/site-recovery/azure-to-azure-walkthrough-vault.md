---
title: "Azure Site Recovery ile bölgeler arasında Azure VM repliction için bir kasa yukarı aaaSet | Microsoft Docs"
description: "Azure Site Kurtarma'yı kullanarak Azure bölgeler arasında Azure çoğaltma için bir kasa yukarı tooset gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>4. adım: Azure tooAzure çoğaltma için bir kasa ayarlayın

Sonra [ağlarını planlama](azure-to-azure-walkthrough-network.md), hello kullanarak tooanother Azure bölgesi çoğaltma Bu makale tooset Azure sanal makineleri (VM'ler) için bir kasa yukarı kullanmak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

- Merhaba makale bitirdikten sonra ayarlanmış bir kurtarma Hizmetleri kasası olmalıdır.
- Bu makalenin hello altındaki tüm yorumlar gönderin ya da hello sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Azure VM çoğaltma şu anda önizlemede değil.




## <a name="create-a-vault"></a>Bir kasa oluşturun

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Merhaba kurtarma Hizmetleri kasası, VM'ler tooreplicate istediğiniz hello konumda oluşturmanızı öneririz. Hedef konumunuz olan hello Orta BİZE, örneğin, hello kasasına oluşturun **Orta ABD**.


## <a name="next-steps"></a>Sonraki adımlar

Çok Git[5. adım: çoğaltmasını etkinleştir](azure-to-azure-walkthrough-enable-replication.md)
