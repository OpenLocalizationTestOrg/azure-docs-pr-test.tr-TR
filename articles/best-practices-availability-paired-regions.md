---
title: "İş devamlılığı ve olağanüstü durum kurtarma (BCDR): Azure eşleştirilmiş bölgeleri | Microsoft Docs"
description: "Azure bölgesel eşleştirme, tooensure hakkında uygulamaların veri merkezi hataları sırasında dayanıklı olduğunu öğrenin."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>İş devamlılığı ve olağanüstü durum kurtarma (BCDR): Azure eşleştirilmiş bölgeleri

## <a name="what-are-paired-regions"></a>Hangi bölgeleri eşleştirilmiş?

Merhaba Dünya birden çok coğrafi olarak Azure çalışır. Bir Azure Coğrafya, en az bir Azure bölgesi içeren hello World tanımlı bir alandır. Bir Azure bölgesine bir veya daha fazla veri merkezleri içeren bir coğrafi konum içinde bir alandır.

Her Azure bölgesi hello içinde başka bir bölge ile eşleştirilmiş bir bölgesel çifti birlikte yapmadan aynı Coğrafya. Merhaba, kendi Coğrafya dışında bir bölge ile eşleştirilmiş Brezilya Güney istisnadır.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Şekil 1 – Azure bölgesel çifti diyagramı

| coğrafi konum | Eşleştirilmiş bölgeleri |  |
|:--- |:--- |:--- |
| Asya |Doğu Asya |Güneydoğu Asya |
| Avustralya |Avustralya Doğu |Avustralya Güneydoğu |
| Kanada |Kanada Orta |Doğu Kanada |
| Çin |Çin Kuzey |Çin Doğu|
| Hindistan |Orta Hindistan |Güney Hindistan |
| Japonya |Japonya Doğu |Japonya Batı |
| Kore |Kore Orta |Kore Güney |
| Kuzey Amerika |Orta Kuzey ABD |Orta Güney ABD |
| Kuzey Amerika |Doğu ABD |Batı ABD |
| Kuzey Amerika |Doğu ABD 2 |Orta ABD |
| Kuzey Amerika |Batı ABD 2 |Batı Orta ABD |
| Avrupa |Kuzey Avrupa |Batı Avrupa |
| Japonya |Japonya Doğu |Japonya Batı |
| Brezilya |Brezilya Güney (1) |Orta Güney ABD |
| ABD Devleti |ABD Devleti Iowa |ABD Devleti Virginia |
| ABD Devleti |ABD Devleti Virginia |ABD Devleti Texas |
| ABD Devleti |ABD Devleti Texas |ABD Devleti Arizona |
| ABD Devleti |ABD Devleti Arizona |ABD Devleti Texas |
| BİRLEŞİK KRALLIK |Birleşik Krallık Batı |Birleşik Krallık Güney |
| Almanya |Almanya Orta |Almanya Kuzeydoğu |

Tablo 1 - Azure bölgesel çiftlerini eşleme

> (1) Brezilya Güney benzersiz çünkü kendi Coğrafya dışında bir bölge ile eşlenmiş. Brezilya Güney'nın ikincil bölge Orta Güney ABD, ancak orta Güney ABD'ın ikincil bölge Brezilya Güney değil.


Azure'nın yalıtım ve kullanılabilirlik ilkelerden Bölgesel çiftleri toobenefit arasında iş yükleri çoğaltmak öneririz. Örneğin, planlı Azure sistem güncelleştirmeleri sırayla dağıtılır (Merhaba değil, aynı anda) eşleştirilmiş bölgeler arasında. Bile hello ender olayda hatalı bir güncelleştirme, her iki bölgeleri aynı anda etkilenmez, anlamına gelir. Ayrıca, hello kurtarılamaz geniş bir kesinti içinde her çifti dışında en az bir bölge kurtarılması öncelik.

## <a name="an-example-of-paired-regions"></a>Eşleştirilmiş bölgeler örneği
Şekil 2'de aşağıdaki hello bölgesel çifti olağanüstü durum kurtarma için kullandığı kuramsal bir uygulamayı gösterir. Merhaba yeşil numaraları (Azure, depolama, işlem ve veritabanı) üç Azure Hizmetleri hello çapraz bölge etkinliklerini vurgulayın ve nasıl oldukları tooreplicate bölgeler arasında yapılandırılır. eşleştirilmiş bölgeler arasında dağıtma hello benzersiz avantajlarını hello turuncu numaralarına göre vurgulanır.

![Eşleştirilmiş bölge avantajları genel bakış](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Şekil 2 – kuramsal Azure bölgesel çifti

## <a name="cross-region-activities"></a>Çapraz bölge etkinlikleri
Başvurulan tooin Şekil 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **Azure işlem (PaaS)** – başka işlem kaynakları sağlamak önceden tooensure kaynaklar başka bir bölgede bir olağanüstü durum sırasında kullanılabilir. Daha fazla bilgi için bkz: [Azure dayanıklılık teknik kılavuz](resiliency/resiliency-technical-guidance.md).

![Depolama](./media/best-practices-availability-paired-regions/2Green.png) **Azure Storage** -bir Azure depolama hesabı oluşturduğunuzda, coğrafi olarak yedekli depolama (GRS) varsayılan olarak yapılandırılır. GRS ile verileriniz otomatik olarak üç kez hello birincil bölge içinde ve üç kez hello eşleştirilmiş bölgede yinelenir. Daha fazla bilgi için bkz: [Azure depolama artıklığı seçeneği](storage/common/storage-redundancy.md).

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **Azure SQL veritabanlarını** – ile Azure SQL standart coğrafi çoğaltma, zaman uyumsuz çoğaltma işlemleri tooa eşleştirilmiş bölgesinin yapılandırabilirsiniz. Premium, coğrafi çoğaltma, çoğaltma tooany bölge hello world yapılandırabilirsiniz; Ancak, bu kaynakları çoğu olağanüstü durum kurtarma senaryoları için eşlenmiş bir bölgede dağıttığınız öneririz. Daha fazla bilgi için bkz: [Azure SQL Database coğrafi çoğaltma](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager** -Resource Manager kendiliğinden bölgeler arasında Hizmet Yönetim bileşenlerinin mantıksal yalıtım sağlar. Bu mantıksal bir bölgede hatalarıdır olasılığını tooimpact anlamına gelir. başka bir.

## <a name="benefits-of-paired-regions"></a>Eşleştirilmiş bölgeler yararları
Başvurulan tooin Şekil 2.  

![Yalıtım](./media/best-practices-availability-paired-regions/5Orange.png)
**fiziksel yalıtım** – olası, Azure, bu tüm coğrafi bölgelerde pratik veya mümkün olmasa da, en az 300 mil bölgesel çiftindeki veri merkezleri arasında ayrım tercih eder. Fiziksel veri merkezi ayrımı doğal afetler, hukuki unrest, güç kesintileri veya aynı anda hem bölgeler etkilemeden fiziksel ağ kesintileri hello olasılığını azaltır. Yalıtım konu toohello kısıtlamaları hello Coğrafya (Coğrafya boyutu, güç/ağ altyapısı kullanılabilirlik, düzenlemeler, vb.) içinde ' dir.  

![Çoğaltma](./media/best-practices-availability-paired-regions/6Orange.png)
**Platform tarafından sağlanan çoğaltma** -otomatik çoğaltma toohello eşleştirilmiş bölge coğrafi olarak yedekli depolama alanı gibi bazı hizmetler sağlar.

![Kurtarma](./media/best-practices-availability-paired-regions/7Orange.png)
**bölge kurtarma sipariş** – geniş bir kesinti hello olayda her çifti dışında bir bölge kurtarılması öncelik. Eşleştirilmiş bölgeler arasında dağıtılan uygulamalar hello bölgelerinden öncelikli kurtarılan toohave sağlanır. Bir uygulama değil eşleştirilmelidir bölgeler arasında dağıtılırsa, Kurtarma – hello servis talebi hello seçilen bölgeler kurtarılan son iki toobe hello kötü gecikebilir.

![Güncelleştirmeleri](./media/best-practices-availability-paired-regions/8Orange.png)
**sıralı güncelleştirme** – planlanan Azure sistem güncelleştirmelerini yapılır toopaired bölgeler sırayla (Merhaba değil, aynı anda) toominimize kapalı kalma süresi, hataları ve mantıksal hataları hello ender olayda hello etkisi bozuk bir güncelleştirmesi.

![Veri](./media/best-practices-availability-paired-regions/9Orange.png)
**veri residency** – bir bölge içinde hello aynı bulunduğu Coğrafya (Brezilya Güney, hello durumla) çiftini vergi ve yasa zorlama dairesi amaçları için sipariş toomeet veri residency gereksinimlerinde olarak.
