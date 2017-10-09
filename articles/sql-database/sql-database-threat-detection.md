---
title: "aaaThreat algılama - Azure SQL veritabanı | Microsoft Docs"
description: "Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="3ca78-103">SQL veritabanı tehdit algılama</span><span class="sxs-lookup"><span data-stu-id="3ca78-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="3ca78-104">SQL tehdit algılama olağan dışı ve zararlı denemeleri tooaccess veya yararlanma veritabanı gösteren anormal etkinlikler algılar.</span><span class="sxs-lookup"><span data-stu-id="3ca78-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="3ca78-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3ca78-105">Overview</span></span>

<span data-ttu-id="3ca78-106">SQL tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ca78-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="3ca78-107">Kullanıcılar, şüpheli veritabanı etkinliklerini, olası güvenlik açıkları ve SQL ekleme saldırıları yanı sıra anormal veritabanı erişimi desenleri bağlı bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3ca78-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="3ca78-108">SQL tehdit algılama uyarıları şüpheli etkinlik ayrıntılarını sağlayın ve eylem nasıl önerilir tooinvestigate ve hello tehdidi azaltmak.</span><span class="sxs-lookup"><span data-stu-id="3ca78-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="3ca78-109">Kullanıcıları kullanarak hello şüpheli olayları Araştır [SQL veritabanı denetimi](sql-database-auditing.md) bir girişim tooaccess sağlamazsa toodetermine ihlal etme veya hello veritabanındaki verileri yararlanma.</span><span class="sxs-lookup"><span data-stu-id="3ca78-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="3ca78-110">Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan kolaylaştırır veya sistemleri izleme Gelişmiş Güvenlik yönetin.</span><span class="sxs-lookup"><span data-stu-id="3ca78-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="3ca78-111">Örneğin, SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir.</span><span class="sxs-lookup"><span data-stu-id="3ca78-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="3ca78-112">Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini uygulama giriş alanlarına ihlal veya hello veritabanındaki verileri değiştirme yararlanın.</span><span class="sxs-lookup"><span data-stu-id="3ca78-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="3ca78-113">SQL tehdit algılama uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/), ve her korumalı SQL veritabanı sunucusu aynı fiyat hello $15/düğümü/SQL her korumalı burada ay, adresindeki Azure Güvenlik Merkezi standart katmanı olarak Fatura edilecek Veritabanı sunucusu, bir düğüm olarak sayılır.</span><span class="sxs-lookup"><span data-stu-id="3ca78-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="3ca78-114">Tootry davet ediyoruz için 60 gün onu boş.</span><span class="sxs-lookup"><span data-stu-id="3ca78-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="3ca78-115">Tehdit algılama'hello Azure portal veritabanınızda için ayarlama</span><span class="sxs-lookup"><span data-stu-id="3ca78-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="3ca78-116">Hello Azure başlatma sırasında portal [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ca78-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3ca78-117">Merhaba SQL toomonitor istediğiniz veritabanını toohello yapılandırma dikey gidin.</span><span class="sxs-lookup"><span data-stu-id="3ca78-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="3ca78-118">Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="3ca78-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="3ca78-119">![Gezinti Bölmesi][1]</span><span class="sxs-lookup"><span data-stu-id="3ca78-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="3ca78-120">Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** hello tehdit algılama ayarlarını görüntüler denetim.</span><span class="sxs-lookup"><span data-stu-id="3ca78-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="3ca78-122">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="3ca78-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="3ca78-123">Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları Hello listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3ca78-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="3ca78-124">Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3ca78-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Gezinti Bölmesi][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="3ca78-126">PowerShell kullanarak tehdit saptamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="3ca78-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="3ca78-127">Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3ca78-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="3ca78-128">Şüpheli bir olay algılandığında anormal veritabanı etkinliklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="3ca78-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="3ca78-129">Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3ca78-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="3ca78-130">Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını, uygulama adı ve hello olay süresi dahil olmak üzere bilgileri sağlarız.</span><span class="sxs-lookup"><span data-stu-id="3ca78-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="3ca78-131">Ayrıca, hello e-posta olası nedenler bilgileri sağlarız ve önerilen eylemler tooinvestigate ve hello olası tehdit toohello veritabanı azaltmak.</span><span class="sxs-lookup"><span data-stu-id="3ca78-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Gezinti Bölmesi][4]
2. <span data-ttu-id="3ca78-133">Merhaba e-posta uyarısı doğrudan bağlantı toohello SQL denetim günlüğü içerir.</span><span class="sxs-lookup"><span data-stu-id="3ca78-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="3ca78-134">Bu bağlantı başlatır hello Azure portal ve açılır hello SQL denetim kayıtlarının hello şüpheli olay hello sırada etrafında'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3ca78-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="3ca78-135">Bir denetim kaydı tooview hello şüpheli veritabanı etkinliklerini, yürütüldüğü daha kolay toofind hello SQL deyimlerini yapma hakkında daha fazla ayrıntı tıklayın (kimin, ne yaptığını ve ne zaman) ve hello olay yasal veya kötü amaçlı olup olmadığını belirlemek (örn. uygulama Güvenlik Açığı tooSQL ekleme yararlanan, birisi ihlal hassas verileri, vb.).</span><span class="sxs-lookup"><span data-stu-id="3ca78-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="3ca78-136">
   ![Gezinti Bölmesi][5]</span><span class="sxs-lookup"><span data-stu-id="3ca78-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="3ca78-137">Tehdit algılama uyarıları hello Azure portal veritabanınızda keşfedin</span><span class="sxs-lookup"><span data-stu-id="3ca78-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="3ca78-138">SQL veritabanı tehdit algılama, uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="3ca78-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="3ca78-139">Merhaba veritabanı dikey penceresinde hello Azure portal parçaları hello etkin tehditleri durumunu içinde dinamik bir SQL güvenlik kutucuğu.</span><span class="sxs-lookup"><span data-stu-id="3ca78-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Gezinti Bölmesi][6]
   
1. <span data-ttu-id="3ca78-141">Merhaba SQL güvenlik kutucuğa tıklandığında hello Azure Güvenlik Merkezi uyarıları dikey penceresini başlatır ve hello veritabanında algılanan etkin SQL tehditleri genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ca78-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Gezinti Bölmesi][7]

2. <span data-ttu-id="3ca78-143">Belirli bir uyarıya tıklayarak, ek ayrıntıları ve bu tehdit araştırma ve gelecekte tehditlere düzeltme eylemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ca78-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Gezinti Bölmesi][8]


## <a name="next-steps"></a><span data-ttu-id="3ca78-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ca78-145">Next steps</span></span>

* <span data-ttu-id="3ca78-146">Tehdit algılama hakkında daha fazla bilgi için başlangıç adresini ziyaret [Azure blogu](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="3ca78-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="3ca78-147">Daha fazla bilgi edinmek [Azure SQL veritabanı denetimi](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="3ca78-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="3ca78-148">Daha fazla bilgi edinmek [Azure Güvenlik Merkezi](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="3ca78-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="3ca78-149">Fiyatlandırma hakkında daha fazla ayrıntı için lütfen bkz hello [SQL Database fiyatlandırması sayfası](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="3ca78-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="3ca78-150">PowerShell komut dosyası örneği için bkz: [PowerShell kullanarak denetim ve tehdit algılama yapılandırın](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3ca78-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


