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
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="def1a-103">Uzun vadeli depolama alanınızı Azure bulut bant toohello taşıma</span><span class="sxs-lookup"><span data-stu-id="def1a-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="def1a-104">Azure yedekleme ve System Center Data Protection Manager müşteriler yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="def1a-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="def1a-105">En iyi şekilde hello kuruluşunuzun gereksinimlerine uygun tablolarındaki verileri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="def1a-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="def1a-106">Uzun süre Hello yedekleme verilerini korur</span><span class="sxs-lookup"><span data-stu-id="def1a-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="def1a-107">(Bant yerine) kendi uzun vadeli bekletme parçası gereken Azure olun.</span><span class="sxs-lookup"><span data-stu-id="def1a-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="def1a-108">Bu makalede, müşteriler yedekleme ve bekletme ilkeleri nasıl etkinleştirebilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="def1a-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="def1a-109">Bantları tooaddress kullanan müşteriler, artık bu özelliğin hello kullanılabilirliği ile güçlü ve uygun bir alternatif olan kendi uzun-süreli saklama gerekir.</span><span class="sxs-lookup"><span data-stu-id="def1a-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="def1a-110">Merhaba özelliği hello son hello Azure Backup sürümündeki etkinleştirilmişse (kullanılabilen [burada](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="def1a-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="def1a-111">System Center DPM müşteriler için güncelleştirmeniz gerekir, en az DPM 2012 R2 DPM ile kullanmadan önce UR5 hello Azure Backup hizmeti.</span><span class="sxs-lookup"><span data-stu-id="def1a-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="def1a-112">Merhaba yedekleme zamanlaması nedir?</span><span class="sxs-lookup"><span data-stu-id="def1a-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="def1a-113">Merhaba yedekleme zamanlaması hello yedekleme işlemi hello sıklığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="def1a-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="def1a-114">Örneğin, yedeklemeler 6 pm saatinde ve gece alınır ekran aşağıdaki hello hello ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="def1a-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Günlük Zamanlama](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="def1a-116">Müşterileri de haftalık bir yedekleme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="def1a-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="def1a-117">Örneğin, hello ekran aşağıdaki hello ayarlarında yedeklemeleri her alternatif Pazar & Çarşamba 09:30:00 ve 1: 00'da gerçekleştirilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="def1a-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Haftalık Zamanlama](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="def1a-119">Merhaba bekletme ilkesi nedir?</span><span class="sxs-lookup"><span data-stu-id="def1a-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="def1a-120">Merhaba bekletme ilkesi hello yedekleme depolanmalıdır hello süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="def1a-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="def1a-121">Yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, müşteriler hello yedeklemenin ne zaman farklı bekletme ilkeleri göre belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="def1a-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="def1a-122">Örneğin, bir işletimsel kurtarma noktası olarak hizmet veren, günlük, geçen hello yedekleme noktası 90 gün boyunca korunur.</span><span class="sxs-lookup"><span data-stu-id="def1a-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="def1a-123">her üç aylık denetim amacıyla hello sonunda gerçekleştirilecek hello yedekleme noktası uzun bir süre için korunur.</span><span class="sxs-lookup"><span data-stu-id="def1a-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Bekletme İlkesi](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="def1a-125">Merhaba, toplam "Bu ilkede belirtilen bekletme noktalarını" sayısıdır 90 (günlük noktaları) + 40 (her biri 10 Yıl Çeyrek) 130 =.</span><span class="sxs-lookup"><span data-stu-id="def1a-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="def1a-126">Örnek – hem de bir araya getirme</span><span class="sxs-lookup"><span data-stu-id="def1a-126">Example – Putting both together</span></span>
![Örnek ekran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="def1a-128">**Günlük Bekletme İlkesi**: günlük alınan yedeklemeler yedi gün boyunca saklanır.</span><span class="sxs-lookup"><span data-stu-id="def1a-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="def1a-129">**Haftalık Bekletme İlkesi**: her gün gece ve 6 PM Cumartesi alınan yedeklemeler için dört hafta korunur</span><span class="sxs-lookup"><span data-stu-id="def1a-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="def1a-130">**Aylık Bekletme İlkesi**: Gece ve 6 pm her ayın son Cumartesi hello'alınan yedeklemeler için 12 ay boyunca korunur</span><span class="sxs-lookup"><span data-stu-id="def1a-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="def1a-131">**Yıllık Bekletme İlkesi**: hello'te gece her Mart Son Cumartesi alınan yedeklemeler, 10 yılı aşkın korunur</span><span class="sxs-lookup"><span data-stu-id="def1a-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="def1a-132">Merhaba "bekletme noktalarını" toplam sayısı (içinden bir müşteri geri yükleyebilir, veri noktaları) hello önceki diyagramda aşağıdaki gibi hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="def1a-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="def1a-133">iki yedi gün = 14 gün başına kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="def1a-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="def1a-134">iki haftada bir dört hafta = 8 için kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="def1a-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="def1a-135">iki aylık 12 ay = 24 için kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="def1a-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="def1a-136">bir işaret 10 yıl = 10 kurtarma başına yıllık</span><span class="sxs-lookup"><span data-stu-id="def1a-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="def1a-137">Merhaba toplam kurtarma noktaları 56 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="def1a-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="def1a-138">Azure yedekleme kurtarma noktalarının sayısı üzerinde bir kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="def1a-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="def1a-139">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="def1a-139">Advanced configuration</span></span>
<span data-ttu-id="def1a-140">Tıklayarak **Değiştir** ekran önceki hello müşteriler bekletme zamanlamaları belirterek daha fazla esneklik bulunur.</span><span class="sxs-lookup"><span data-stu-id="def1a-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Değiştir](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="def1a-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="def1a-142">Next Steps</span></span>
<span data-ttu-id="def1a-143">Azure yedekleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="def1a-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="def1a-144">Giriş tooAzure yedekleme</span><span class="sxs-lookup"><span data-stu-id="def1a-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="def1a-145">Azure Backup'ı deneyin</span><span class="sxs-lookup"><span data-stu-id="def1a-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
