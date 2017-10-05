---
title: "Tehdit algılama - Azure SQL veritabanı | Microsoft Docs"
description: "Tehdit algılama veritabanına olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini algılar."
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="20b33-103">SQL veritabanı tehdit algılama</span><span class="sxs-lookup"><span data-stu-id="20b33-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="20b33-104">SQL tehdit algılama erişmek veya veritabanlarını yararlanmak için alışılmadık ve zararlı denemeleri gösteren anormal etkinlikler algılar.</span><span class="sxs-lookup"><span data-stu-id="20b33-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="20b33-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="20b33-105">Overview</span></span>

<span data-ttu-id="20b33-106">SQL tehdit algılama, müşterilerin algılamak ve anormal etkinlikler güvenlik uyarıları sağlayarak göründüklerinde olası risklere yanıt sağlayan bir güvenlik yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="20b33-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="20b33-107">Kullanıcılar, şüpheli veritabanı etkinliklerini, olası güvenlik açıkları ve SQL ekleme saldırıları yanı sıra anormal veritabanı erişimi desenleri bağlı bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="20b33-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="20b33-108">SQL tehdit algılama uyarıları şüpheli etkinlik ayrıntılarını sağlayın ve eylem araştırmak ve tehdidi azaltmak nasıl öneririz.</span><span class="sxs-lookup"><span data-stu-id="20b33-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="20b33-109">Kullanıcıları kullanarak şüpheli olayları Araştır [SQL veritabanı denetimi](sql-database-auditing.md) bunlar erişim, ihlal ya da veritabanındaki verileri yararlanma girişimi sonucu olmadığını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="20b33-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="20b33-110">Tehdit algılama, veritabanına Uzman güvenlik olması veya sistemleri izleme Gelişmiş Güvenlik yönetmek zorunda kalmadan adresi olası tehditlere kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="20b33-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="20b33-111">Örneğin, SQL ekleme veri güdümlü uygulamaları saldırmak için kullanılıyorsa Internet üzerinde ortak Web uygulaması güvenlik sorunlarını biridir.</span><span class="sxs-lookup"><span data-stu-id="20b33-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="20b33-112">Saldırganlar uygulama giriş alanları, kötü amaçlı SQL deyimleri eklemesine uygulama güvenlik açıkları ihlal veya veritabanındaki verileri değiştirme yararlanın.</span><span class="sxs-lookup"><span data-stu-id="20b33-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="20b33-113">SQL tehdit algılama uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/), ve her korumalı SQL veritabanı sunucusu, Azure Güvenlik Merkezi standart katmanını, $15/düğümü/SQL her korumalı burada ay, aynı fiyatla Fatura edilecek Veritabanı sunucusu, bir düğüm olarak sayılır.</span><span class="sxs-lookup"><span data-stu-id="20b33-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="20b33-114">Sizi bu hizmeti 60 gün süresince ücretsiz denemeye davet ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="20b33-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="20b33-115">Tehdit algılama Azure portalında veritabanınız için ayarlama</span><span class="sxs-lookup"><span data-stu-id="20b33-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="20b33-116">Azure portalında başlatma [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20b33-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="20b33-117">İzlemek istediğiniz SQL veritabanı yapılandırma dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="20b33-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="20b33-118">Ayarlar dikey penceresinde seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="20b33-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="20b33-119">![Gezinti Bölmesi][1]</span><span class="sxs-lookup"><span data-stu-id="20b33-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="20b33-120">İçinde **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** tehdit algılama ayarlarını görüntüler denetim.</span><span class="sxs-lookup"><span data-stu-id="20b33-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="20b33-122">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="20b33-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="20b33-123">Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20b33-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="20b33-124">Tıklatın **kaydetmek** içinde **denetim ve tehdit algılama** yeni veya güncelleştirilmiş denetim ve tehdit algılama ayarlarını kaydetmek için dikey.</span><span class="sxs-lookup"><span data-stu-id="20b33-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![Gezinti Bölmesi][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="20b33-126">PowerShell kullanarak tehdit saptamayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="20b33-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="20b33-127">Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="20b33-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="20b33-128">Şüpheli bir olay algılandığında anormal veritabanı etkinliklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="20b33-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="20b33-129">Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="20b33-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="20b33-130">E-posta anormal etkinlikler, veritabanı adı, sunucu adını, uygulama adı ve olay süresi yapısını dahil olmak üzere şüpheli güvenlik olayı üzerinde bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="20b33-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="20b33-131">Ayrıca, e-posta olası nedenler bilgileri sağlarız ve önerilen eylemleri araştırmak ve veritabanına olası tehdidi azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="20b33-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![Gezinti Bölmesi][4]
2. <span data-ttu-id="20b33-133">E-posta uyarısı SQL denetim günlüğü doğrudan bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="20b33-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="20b33-134">Bu bağlantıyı tıklatmak, Azure Portalı'nı başlatır ve şüpheli olay sırada çevresinde SQL denetim kayıtlarının açar.</span><span class="sxs-lookup"><span data-stu-id="20b33-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="20b33-135">Bir denetim kaydı yürütüldü SQL deyimlerini bulmayı kolaylaştıracak şüpheli veritabanı etkinliklerini daha fazla ayrıntı görüntülemek için tıklatın (kimin, ne yaptığını ve ne zaman) ve olay yasal veya kötü amaçlı olup olmadığını belirleme (örn. uygulama Güvenlik Açığı SQL Yerleştirmeye yararlanan, birisi ihlal hassas verileri, vb.).</span><span class="sxs-lookup"><span data-stu-id="20b33-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="20b33-136">
   ![Gezinti Bölmesi][5]</span><span class="sxs-lookup"><span data-stu-id="20b33-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="20b33-137">Tehdit algılama uyarıları veritabanınızı Azure portalında keşfedin</span><span class="sxs-lookup"><span data-stu-id="20b33-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="20b33-138">SQL veritabanı tehdit algılama, uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="20b33-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="20b33-139">Azure portalında veritabanı dikey canlı bir SQL güvenlik kutucuğu etkin tehditleri durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="20b33-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![Gezinti Bölmesi][6]
   
1. <span data-ttu-id="20b33-141">SQL tıklayarak güvenlik kutucuğu, Azure Güvenlik Merkezi uyarıları dikey penceresini başlatır ve veritabanı üzerinde algılanan etkin SQL tehditleri genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="20b33-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![Gezinti Bölmesi][7]

2. <span data-ttu-id="20b33-143">Belirli bir uyarıya tıklayarak, ek ayrıntıları ve bu tehdit araştırma ve gelecekte tehditlere düzeltme eylemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="20b33-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Gezinti Bölmesi][8]


## <a name="next-steps"></a><span data-ttu-id="20b33-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20b33-145">Next steps</span></span>

* <span data-ttu-id="20b33-146">Tehdit algılama hakkında daha fazla bilgi edinmek için bkz [Azure blogu](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="20b33-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="20b33-147">Daha fazla bilgi edinmek [Azure SQL veritabanı denetimi](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="20b33-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="20b33-148">Daha fazla bilgi edinmek [Azure Güvenlik Merkezi](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="20b33-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="20b33-149">Fiyatlandırma hakkında daha fazla ayrıntı için lütfen bkz. [SQL Database fiyatlandırması sayfası](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="20b33-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="20b33-150">PowerShell komut dosyası örneği için bkz: [PowerShell kullanarak denetim ve tehdit algılama yapılandırın](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="20b33-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


