---
title: "SQL veri ambarı tehdit algılama ile aaaGet başlatıldı"
description: "Tooget tehdit algılama ile çalışmaya nasıl"
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
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="340fa-103">Tehdit algılama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="340fa-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="340fa-104">Denetim</span><span class="sxs-lookup"><span data-stu-id="340fa-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="340fa-105">Tehdit algılama</span><span class="sxs-lookup"><span data-stu-id="340fa-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="340fa-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="340fa-106">Overview</span></span>
<span data-ttu-id="340fa-107">Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="340fa-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="340fa-108">Tehdit algılama Önizleme aşamasındadır ve SQL Data Warehouse için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="340fa-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="340fa-109">Tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="340fa-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="340fa-110">Kullanıcıları kullanarak hello şüpheli olayları Araştır [Azure SQL veri ambarı denetimi](sql-data-warehouse-auditing-overview.md) bir girişim tooaccess sağlamazsa toodetermine ihlal etme veya hello veri ambarındaki yararlanma.</span><span class="sxs-lookup"><span data-stu-id="340fa-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="340fa-111">Tehdit algılama toohello veri hello gerek toobe bir güvenlik Uzman ambar veya sistemleri izleme Gelişmiş Güvenlik yönetmek basit tooaddress olası tehditler kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="340fa-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="340fa-112">Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="340fa-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="340fa-113">SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir.</span><span class="sxs-lookup"><span data-stu-id="340fa-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="340fa-114">Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini ihlal veya hello veritabanındaki verileri değiştirmek için uygulama giriş alanları içine yararlanın.</span><span class="sxs-lookup"><span data-stu-id="340fa-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="340fa-115">Tehdit algılama veritabanınız için ayarlama</span><span class="sxs-lookup"><span data-stu-id="340fa-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="340fa-116">Başlatma hello Azure portalında [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="340fa-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="340fa-117">Merhaba SQL Data Warehouse toomonitor istediğiniz toohello yapılandırma dikey gidin.</span><span class="sxs-lookup"><span data-stu-id="340fa-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="340fa-118">Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="340fa-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Gezinti Bölmesi][1]
3. <span data-ttu-id="340fa-120">Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler hello tehdit algılama ayarları.</span><span class="sxs-lookup"><span data-stu-id="340fa-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Gezinti Bölmesi][2]
4. <span data-ttu-id="340fa-122">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="340fa-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="340fa-123">Güvenlik Uyarıları anormal veri ambarı etkinlikler algılandığında alacak e-postaları Hello listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="340fa-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="340fa-124">Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** yapılandırma dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ilkesi.</span><span class="sxs-lookup"><span data-stu-id="340fa-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Gezinti Bölmesi][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="340fa-126">Anormal veri ambarı etkinlikleri şüpheli bir olay algılandığında keşfedin</span><span class="sxs-lookup"><span data-stu-id="340fa-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="340fa-127">Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="340fa-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="340fa-128">Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını ve hello olay zaman dahil olmak üzere bilgileri sağlarız.</span><span class="sxs-lookup"><span data-stu-id="340fa-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="340fa-129">Ayrıca, olası nedenler bilgileri sağlarız Eylemler tooinvestigate önerilen ve hello olası tehdit toohello veritabanı etkisini azaltır.</span><span class="sxs-lookup"><span data-stu-id="340fa-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Gezinti Bölmesi][4]
2. <span data-ttu-id="340fa-131">Hello postada hello üzerinde tıklatın **Azure SQL denetim günlüğü** hello Klasik Azure portalı başlatın ve hello ilgili denetim kayıtları hello şüpheli olay hello sırada geçici Göster bağlantı.</span><span class="sxs-lookup"><span data-stu-id="340fa-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Gezinti Bölmesi][5]
3. <span data-ttu-id="340fa-133">SQL deyimi gibi hello veritabanı kuşkulu etkinlikleri hakkında daha fazla ayrıntı Hello denetim kayıtları tooview üzerinde tıklatın başarısızlık nedeni ve istemci IP.</span><span class="sxs-lookup"><span data-stu-id="340fa-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Gezinti Bölmesi][6]
4. <span data-ttu-id="340fa-135">Merhaba denetimi kayıtları dikey penceresinde tıklayın **Excel'de Aç** tooopen önceden yapılandırılmış excel şablonu tooimport ve hello denetim günlüğü hello şüpheli olay hello sırada geçici çalışma daha derin çözümlenmesi.</span><span class="sxs-lookup"><span data-stu-id="340fa-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="340fa-136">
   **Not:** Excel 2010 veya üzeri, Power Query ve hello **hızlı Birleştir** ayarı gereklidir</span><span class="sxs-lookup"><span data-stu-id="340fa-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Gezinti Bölmesi][7]
5. <span data-ttu-id="340fa-138">tooconfigure hello **hızlı Birleştir** ayarında - hello **POWER QUERY** Şerit sekmesi, select **seçenekleri** toodisplay hello Seçenekleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="340fa-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="340fa-139">Merhaba gizlilik bölümünü seçin ve 'Hello gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' hello ikinci seçeneği - belirtin:</span><span class="sxs-lookup"><span data-stu-id="340fa-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Gezinti Bölmesi][8]
6. <span data-ttu-id="340fa-141">tooload SQL denetim günlüklerini hello parametreleri hello Ayarlar sekmesinde doğru ayarlandığından ve ardından hello 'Verileri' Şerit'i seçin ve hello 'Tümünü Yenile' düğmesini tıklatın emin olun.</span><span class="sxs-lookup"><span data-stu-id="340fa-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Gezinti Bölmesi][9]
7. <span data-ttu-id="340fa-143">Merhaba sonuçları görünen hello **SQL denetim günlüklerini** toorun daha derin algılanan ve uygulamanızda hello güvenlik olayı hello etkisini hello anormal etkinlikler analizini sağlayan sayfası.</span><span class="sxs-lookup"><span data-stu-id="340fa-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
