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
# <a name="get-started-with-threat-detection"></a>Tehdit algılama ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Denetim](sql-data-warehouse-auditing-overview.md)
> * [Tehdit algılama](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar. Tehdit algılama Önizleme aşamasındadır ve SQL Data Warehouse için desteklenir.

Tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar. Kullanıcıları kullanarak hello şüpheli olayları Araştır [Azure SQL veri ambarı denetimi](sql-data-warehouse-auditing-overview.md) bir girişim tooaccess sağlamazsa toodetermine ihlal etme veya hello veri ambarındaki yararlanma.
Tehdit algılama toohello veri hello gerek toobe bir güvenlik Uzman ambar veya sistemleri izleme Gelişmiş Güvenlik yönetmek basit tooaddress olası tehditler kolaylaştırır.

Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar. SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir. Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini ihlal veya hello veritabanındaki verileri değiştirmek için uygulama giriş alanları içine yararlanın.

## <a name="set-up-threat-detection-for-your-database"></a>Tehdit algılama veritabanınız için ayarlama
1. Başlatma hello Azure portalında [https://portal.azure.com](https://portal.azure.com).
2. Merhaba SQL Data Warehouse toomonitor istediğiniz toohello yapılandırma dikey gidin. Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.
   
    ![Gezinti Bölmesi][1]
3. Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler hello tehdit algılama ayarları.
   
    ![Gezinti Bölmesi][2]
4. Kapatma **ON** tehdit algılama.
5. Güvenlik Uyarıları anormal veri ambarı etkinlikler algılandığında alacak e-postaları Hello listesini yapılandırın.
6. Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** yapılandırma dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ilkesi.
   
    ![Gezinti Bölmesi][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Anormal veri ambarı etkinlikleri şüpheli bir olay algılandığında keşfedin
1. Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız. <br/>
   Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını ve hello olay zaman dahil olmak üzere bilgileri sağlarız. Ayrıca, olası nedenler bilgileri sağlarız Eylemler tooinvestigate önerilen ve hello olası tehdit toohello veritabanı etkisini azaltır.<br/>
   
    ![Gezinti Bölmesi][4]
2. Hello postada hello üzerinde tıklatın **Azure SQL denetim günlüğü** hello Klasik Azure portalı başlatın ve hello ilgili denetim kayıtları hello şüpheli olay hello sırada geçici Göster bağlantı.
   
    ![Gezinti Bölmesi][5]
3. SQL deyimi gibi hello veritabanı kuşkulu etkinlikleri hakkında daha fazla ayrıntı Hello denetim kayıtları tooview üzerinde tıklatın başarısızlık nedeni ve istemci IP.
   
    ![Gezinti Bölmesi][6]
4. Merhaba denetimi kayıtları dikey penceresinde tıklayın **Excel'de Aç** tooopen önceden yapılandırılmış excel şablonu tooimport ve hello denetim günlüğü hello şüpheli olay hello sırada geçici çalışma daha derin çözümlenmesi.<br/>
   **Not:** Excel 2010 veya üzeri, Power Query ve hello **hızlı Birleştir** ayarı gereklidir
   
    ![Gezinti Bölmesi][7]
5. tooconfigure hello **hızlı Birleştir** ayarında - hello **POWER QUERY** Şerit sekmesi, select **seçenekleri** toodisplay hello Seçenekleri iletişim kutusu. Merhaba gizlilik bölümünü seçin ve 'Hello gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' hello ikinci seçeneği - belirtin:
   
    ![Gezinti Bölmesi][8]
6. tooload SQL denetim günlüklerini hello parametreleri hello Ayarlar sekmesinde doğru ayarlandığından ve ardından hello 'Verileri' Şerit'i seçin ve hello 'Tümünü Yenile' düğmesini tıklatın emin olun.
   
    ![Gezinti Bölmesi][9]
7. Merhaba sonuçları görünen hello **SQL denetim günlüklerini** toorun daha derin algılanan ve uygulamanızda hello güvenlik olayı hello etkisini hello anormal etkinlikler analizini sağlayan sayfası.

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
