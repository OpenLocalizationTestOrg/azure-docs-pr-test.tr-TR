---
title: "Bant altyapınızın yerini alması için Azure Yedekleme'yi | Microsoft Docs"
description: "Yedekleme ve geri yükleme verilerini azure'da olanak veren bant benzeri semantiği Azure Backup'nasıl sağladığını öğrenin"
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="d731c-103">Uzun vadeli depolama için Azure bulut banttan taşıma</span><span class="sxs-lookup"><span data-stu-id="d731c-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="d731c-104">Azure yedekleme ve System Center Data Protection Manager müşteriler yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d731c-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="d731c-105">Kuruluşunuzun gereksinimlerine en uygun tablolarındaki verileri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="d731c-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="d731c-106">Uzun süre yedekleme verilerini korur</span><span class="sxs-lookup"><span data-stu-id="d731c-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="d731c-107">(Bant yerine) kendi uzun vadeli bekletme parçası gereken Azure olun.</span><span class="sxs-lookup"><span data-stu-id="d731c-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="d731c-108">Bu makalede, müşteriler yedekleme ve bekletme ilkeleri nasıl etkinleştirebilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d731c-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="d731c-109">Kendi uzun-süreli saklama adres için bantları kullanacak müşterilerin, artık bu özelliğin kullanılabilirliği ile güçlü ve uygun bir alternatif sahip.</span><span class="sxs-lookup"><span data-stu-id="d731c-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="d731c-110">En son sürümünü Azure yedekleme özelliği etkinleştirilmişse (kullanılabilen [burada](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="d731c-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="d731c-111">System Center DPM müşteriler şekilde güncelleştirilmesi gerekir, en az DPM 2012 R2 DPM Azure Backup hizmeti ile kullanmadan önce UR5.</span><span class="sxs-lookup"><span data-stu-id="d731c-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="d731c-112">Yedekleme zamanlaması nedir?</span><span class="sxs-lookup"><span data-stu-id="d731c-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="d731c-113">Yedekleme zamanlaması, yedekleme işlemi sıklığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d731c-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="d731c-114">Örneğin, aşağıdaki ekran ayarlarında yedeklemeleri 6 pm saatinde ve gece alınır gösterir.</span><span class="sxs-lookup"><span data-stu-id="d731c-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Günlük Zamanlama](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="d731c-116">Müşterileri de haftalık bir yedekleme zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d731c-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="d731c-117">Örneğin, aşağıdaki ekran ayarlarında yedeklemeleri her alternatif Pazar & Çarşamba 09:30:00 ve 1: 00'da alınacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d731c-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Haftalık Zamanlama](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="d731c-119">Bekletme İlkesi nedir?</span><span class="sxs-lookup"><span data-stu-id="d731c-119">What is the Retention Policy?</span></span>
<span data-ttu-id="d731c-120">Bekletme İlkesi yedeğin depolanması gereken süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="d731c-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="d731c-121">Müşteriler, yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, yedeklemenin ne zamana göre farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d731c-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="d731c-122">Örneğin, bir işletimsel kurtarma noktası olarak hizmet veren, günlük, geçen yedekleme noktası 90 gün boyunca korunur.</span><span class="sxs-lookup"><span data-stu-id="d731c-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="d731c-123">Denetim amacıyla her üç aylık dönemin sonunda alınan yedekleme noktası uzun bir süre için korunur.</span><span class="sxs-lookup"><span data-stu-id="d731c-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Bekletme İlkesi](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="d731c-125">"Bu ilkede belirtilen bekletme noktalarını" toplam sayısı olan 90 (günlük noktaları) + 40 (her biri 10 Yıl Çeyrek) 130 =.</span><span class="sxs-lookup"><span data-stu-id="d731c-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="d731c-126">Örnek – hem de bir araya getirme</span><span class="sxs-lookup"><span data-stu-id="d731c-126">Example – Putting both together</span></span>
![Örnek ekran](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="d731c-128">**Günlük Bekletme İlkesi**: günlük alınan yedeklemeler yedi gün boyunca saklanır.</span><span class="sxs-lookup"><span data-stu-id="d731c-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="d731c-129">**Haftalık Bekletme İlkesi**: her gün gece ve 6 PM Cumartesi alınan yedeklemeler için dört hafta korunur</span><span class="sxs-lookup"><span data-stu-id="d731c-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="d731c-130">**Aylık Bekletme İlkesi**: Gece ve her ayın son Cumartesi 6 pm alınan yedeklemeler için 12 ay boyunca korunur</span><span class="sxs-lookup"><span data-stu-id="d731c-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="d731c-131">**Yıllık Bekletme İlkesi**: her Mart Son Cumartesi gece alınan yedeklemeler, 10 yılı aşkın korunur</span><span class="sxs-lookup"><span data-stu-id="d731c-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="d731c-132">"Bekletme noktalarını" toplam sayısı (içinden bir müşteri geri yükleyebilir, veri noktaları) önceki diyagramda aşağıdaki gibi hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="d731c-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="d731c-133">iki yedi gün = 14 gün başına kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="d731c-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="d731c-134">iki haftada bir dört hafta = 8 için kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="d731c-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="d731c-135">iki aylık 12 ay = 24 için kurtarma noktalarını</span><span class="sxs-lookup"><span data-stu-id="d731c-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="d731c-136">bir işaret 10 yıl = 10 kurtarma başına yıllık</span><span class="sxs-lookup"><span data-stu-id="d731c-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="d731c-137">Toplam kurtarma noktaları 56 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d731c-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="d731c-138">Azure yedekleme kurtarma noktalarının sayısı üzerinde bir kısıtlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="d731c-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="d731c-139">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d731c-139">Advanced configuration</span></span>
<span data-ttu-id="d731c-140">Tıklayarak **Değiştir** önceki ekranında müşteriler bekletme zamanlamaları belirterek daha fazla esneklik bulunur.</span><span class="sxs-lookup"><span data-stu-id="d731c-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Değiştir](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="d731c-142">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d731c-142">Next Steps</span></span>
<span data-ttu-id="d731c-143">Azure yedekleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="d731c-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="d731c-144">Azure Backup'a giriş</span><span class="sxs-lookup"><span data-stu-id="d731c-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="d731c-145">Azure Backup'ı deneyin</span><span class="sxs-lookup"><span data-stu-id="d731c-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
