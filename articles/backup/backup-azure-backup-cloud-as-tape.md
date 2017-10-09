---
title: "aaaUse Azure Backup tooreplace bant altyapınızın | Microsoft Docs"
description: "Azure Backup sağlayan bant benzeri semantiği toobackup nasıl sağladığını öğrenin ve Azure veri geri yükleme"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Uzun vadeli depolama alanınızı Azure bulut bant toohello taşıma
Azure yedekleme ve System Center Data Protection Manager müşteriler yapabilirsiniz:

* En iyi şekilde hello kuruluşunuzun gereksinimlerine uygun tablolarındaki verileri yedekleyin.
* Uzun süre Hello yedekleme verilerini korur
* (Bant yerine) kendi uzun vadeli bekletme parçası gereken Azure olun.

Bu makalede, müşteriler yedekleme ve bekletme ilkeleri nasıl etkinleştirebilirsiniz açıklanmaktadır. Bantları tooaddress kullanan müşteriler, artık bu özelliğin hello kullanılabilirliği ile güçlü ve uygun bir alternatif olan kendi uzun-süreli saklama gerekir. Merhaba özelliği hello son hello Azure Backup sürümündeki etkinleştirilmişse (kullanılabilen [burada](http://aka.ms/azurebackup_agent)). System Center DPM müşteriler için güncelleştirmeniz gerekir, en az DPM 2012 R2 DPM ile kullanmadan önce UR5 hello Azure Backup hizmeti.

## <a name="what-is-hello-backup-schedule"></a>Merhaba yedekleme zamanlaması nedir?
Merhaba yedekleme zamanlaması hello yedekleme işlemi hello sıklığını belirtir. Örneğin, yedeklemeler 6 pm saatinde ve gece alınır ekran aşağıdaki hello hello ayarlarını belirtin.

![Günlük Zamanlama](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Müşterileri de haftalık bir yedekleme zamanlayabilirsiniz. Örneğin, hello ekran aşağıdaki hello ayarlarında yedeklemeleri her alternatif Pazar & Çarşamba 09:30:00 ve 1: 00'da gerçekleştirilen gösterir.

![Haftalık Zamanlama](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Merhaba bekletme ilkesi nedir?
Merhaba bekletme ilkesi hello yedekleme depolanmalıdır hello süresini belirtir. Yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, müşteriler hello yedeklemenin ne zaman farklı bekletme ilkeleri göre belirtebilirsiniz. Örneğin, bir işletimsel kurtarma noktası olarak hizmet veren, günlük, geçen hello yedekleme noktası 90 gün boyunca korunur. her üç aylık denetim amacıyla hello sonunda gerçekleştirilecek hello yedekleme noktası uzun bir süre için korunur.

![Bekletme İlkesi](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Merhaba, toplam "Bu ilkede belirtilen bekletme noktalarını" sayısıdır 90 (günlük noktaları) + 40 (her biri 10 Yıl Çeyrek) 130 =.

## <a name="example--putting-both-together"></a>Örnek – hem de bir araya getirme
![Örnek ekran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Günlük Bekletme İlkesi**: günlük alınan yedeklemeler yedi gün boyunca saklanır.
2. **Haftalık Bekletme İlkesi**: her gün gece ve 6 PM Cumartesi alınan yedeklemeler için dört hafta korunur
3. **Aylık Bekletme İlkesi**: Gece ve 6 pm her ayın son Cumartesi hello'alınan yedeklemeler için 12 ay boyunca korunur
4. **Yıllık Bekletme İlkesi**: hello'te gece her Mart Son Cumartesi alınan yedeklemeler, 10 yılı aşkın korunur

Merhaba "bekletme noktalarını" toplam sayısı (içinden bir müşteri geri yükleyebilir, veri noktaları) hello önceki diyagramda aşağıdaki gibi hesaplanır:

* iki yedi gün = 14 gün başına kurtarma noktalarını
* iki haftada bir dört hafta = 8 için kurtarma noktalarını
* iki aylık 12 ay = 24 için kurtarma noktalarını
* bir işaret 10 yıl = 10 kurtarma başına yıllık

Merhaba toplam kurtarma noktaları 56 sayısıdır.

> [!NOTE]
> Azure yedekleme kurtarma noktalarının sayısı üzerinde bir kısıtlama yoktur.
>
>

## <a name="advanced-configuration"></a>Gelişmiş yapılandırma
Tıklayarak **Değiştir** ekran önceki hello müşteriler bekletme zamanlamaları belirterek daha fazla esneklik bulunur.

![Değiştir](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Sonraki Adımlar
Azure yedekleme hakkında daha fazla bilgi için bkz:

* [Giriş tooAzure yedekleme](backup-introduction-to-azure-backup.md)
* [Azure Backup'ı deneyin](backup-try-azure-backup-in-10-mins.md)
