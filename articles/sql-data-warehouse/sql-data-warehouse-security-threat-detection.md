---
title: "SQL veri ambarı tehdit algılama ile çalışmaya başlama"
description: "Tehdit algılama ile çalışmaya nasıl başlayacağınız"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="71170-103">Tehdit algılama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="71170-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71170-104">Denetim</span><span class="sxs-lookup"><span data-stu-id="71170-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="71170-105">Tehdit algılama</span><span class="sxs-lookup"><span data-stu-id="71170-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="71170-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="71170-106">Overview</span></span>
<span data-ttu-id="71170-107">Tehdit algılama veritabanına olası güvenlik tehditlerini gösteren anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="71170-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="71170-108">Tehdit algılama Önizleme aşamasındadır ve SQL Data Warehouse için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="71170-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="71170-109">Tehdit algılama, müşterilerin algılamak ve anormal etkinlikler güvenlik uyarıları sağlayarak göründüklerinde olası risklere yanıt sağlayan bir güvenlik yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="71170-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="71170-110">Kullanıcıları kullanarak şüpheli olayları Araştır [Azure SQL veri ambarı denetimi](sql-data-warehouse-auditing-overview.md) bunlar erişim, ihlal ya da veri ambarındaki yararlanma girişimi sonucu olmadığını belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="71170-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="71170-111">Tehdit algılama adresi olası tehditlere Uzman güvenlik olması veya sistemleri izleme Gelişmiş Güvenlik yönetmek zorunda kalmadan veri ambarına basit kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="71170-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="71170-112">Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="71170-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="71170-113">SQL ekleme veri güdümlü uygulamaları saldırmak için kullanılıyorsa Internet üzerinde ortak Web uygulaması güvenlik sorunlarını biridir.</span><span class="sxs-lookup"><span data-stu-id="71170-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="71170-114">Saldırganlar ihlal veya veritabanındaki verileri değiştirmek için uygulama giriş alanları, kötü amaçlı SQL deyimleri eklemesine uygulama güvenlik açıkları yararlanın.</span><span class="sxs-lookup"><span data-stu-id="71170-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="71170-115">Tehdit algılama veritabanınız için ayarlama</span><span class="sxs-lookup"><span data-stu-id="71170-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="71170-116">Azure portalında başlatma [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71170-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="71170-117">İzlemek istediğiniz SQL veri ambarı yapılandırma dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="71170-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="71170-118">Ayarlar dikey penceresinde seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="71170-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Gezinti Bölmesi][1]
3. <span data-ttu-id="71170-120">İçinde **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler tehdit algılama ayarlar.</span><span class="sxs-lookup"><span data-stu-id="71170-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="71170-122">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="71170-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="71170-123">Güvenlik Uyarıları anormal veri ambarı etkinlikler algılandığında alacak e-postaları listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71170-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="71170-124">Tıklatın **kaydetmek** içinde **denetim ve tehdit algılama** yeni veya güncelleştirilmiş denetim kaydetmek ve tehdit algılama ilkesi için yapılandırma dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="71170-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Gezinti Bölmesi][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="71170-126">Anormal veri ambarı etkinlikleri şüpheli bir olay algılandığında keşfedin</span><span class="sxs-lookup"><span data-stu-id="71170-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="71170-127">Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="71170-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="71170-128">E-posta anormal etkinlikler, veritabanı adı, sunucu adını ve olay süresi yapısını dahil olmak üzere şüpheli güvenlik olayı üzerinde bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="71170-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="71170-129">Ayrıca, olası nedenler bilgileri sağlarız ve önerilen eylemleri araştırmak ve veritabanına olası tehdidi azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="71170-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Gezinti Bölmesi][4]
2. <span data-ttu-id="71170-131">E-posta ile tıklayın **Azure SQL denetim günlüğü** Azure Klasik Portalı'nı başlatın ve ilgili denetim kayıtları şüpheli olay sırada geçici göstermek bağlantı.</span><span class="sxs-lookup"><span data-stu-id="71170-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Gezinti Bölmesi][5]
3. <span data-ttu-id="71170-133">Denetim kayıtlarının SQL deyimini gibi şüpheli veritabanı etkinlikleri hakkında daha fazla ayrıntı görüntülemek için tıklatın başarısızlık nedeni ve istemci IP.</span><span class="sxs-lookup"><span data-stu-id="71170-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Gezinti Bölmesi][6]
4. <span data-ttu-id="71170-135">Denetim kayıtlarının dikey penceresinde tıklayın **Excel'de açın** açmak için önceden yapılandırılmış excel almak ve daha derin denetim günlüğü şüpheli olay sırada geçici analizini çalıştırmak için şablon.</span><span class="sxs-lookup"><span data-stu-id="71170-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="71170-136">
   **Not:** Excel 2010 veya üzeri, güç sorgu ve **hızlı Birleştir** ayarı gereklidir</span><span class="sxs-lookup"><span data-stu-id="71170-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Gezinti Bölmesi][7]
5. <span data-ttu-id="71170-138">Yapılandırmak için **hızlı Birleştir** - ayarlamayı **POWER QUERY** Şerit sekmesi, select **seçenekleri** Seçenekleri iletişim kutusunu görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="71170-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="71170-139">Gizlilik bölümünü seçin ve ikinci seçeneği 'Gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' - belirtin:</span><span class="sxs-lookup"><span data-stu-id="71170-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Gezinti Bölmesi][8]
6. <span data-ttu-id="71170-141">SQL denetim günlüklerini yüklemek için sekme doğru ayarlandığından ve 'Data' Şerit'i seçin ve 'Tümünü Yenile' düğmesini tıklatın ayarlarını parametrelerinde emin olun.</span><span class="sxs-lookup"><span data-stu-id="71170-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Gezinti Bölmesi][9]
7. <span data-ttu-id="71170-143">Sonuçları görünür **SQL denetim günlüklerini** algılandı anormal etkinlikler daha derin çözümlenmesi çalıştırın ve güvenlik olay uygulamanızda etkisini olanak tanıyan sayfası.</span><span class="sxs-lookup"><span data-stu-id="71170-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
