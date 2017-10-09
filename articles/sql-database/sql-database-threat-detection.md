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
# <a name="sql-database-threat-detection"></a>SQL veritabanı tehdit algılama

SQL tehdit algılama olağan dışı ve zararlı denemeleri tooaccess veya yararlanma veritabanı gösteren anormal etkinlikler algılar.

## <a name="overview"></a>Genel Bakış

SQL tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar.  Kullanıcılar, şüpheli veritabanı etkinliklerini, olası güvenlik açıkları ve SQL ekleme saldırıları yanı sıra anormal veritabanı erişimi desenleri bağlı bir uyarı alırsınız. SQL tehdit algılama uyarıları şüpheli etkinlik ayrıntılarını sağlayın ve eylem nasıl önerilir tooinvestigate ve hello tehdidi azaltmak. Kullanıcıları kullanarak hello şüpheli olayları Araştır [SQL veritabanı denetimi](sql-database-auditing.md) bir girişim tooaccess sağlamazsa toodetermine ihlal etme veya hello veritabanındaki verileri yararlanma. Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan kolaylaştırır veya sistemleri izleme Gelişmiş Güvenlik yönetin.

Örneğin, SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir. Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini uygulama giriş alanlarına ihlal veya hello veritabanındaki verileri değiştirme yararlanın.

SQL tehdit algılama uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/), ve her korumalı SQL veritabanı sunucusu aynı fiyat hello $15/düğümü/SQL her korumalı burada ay, adresindeki Azure Güvenlik Merkezi standart katmanı olarak Fatura edilecek Veritabanı sunucusu, bir düğüm olarak sayılır. Tootry davet ediyoruz için 60 gün onu boş. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Tehdit algılama'hello Azure portal veritabanınızda için ayarlama
1. Hello Azure başlatma sırasında portal [https://portal.azure.com](https://portal.azure.com).
2. Merhaba SQL toomonitor istediğiniz veritabanını toohello yapılandırma dikey gidin. Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**. 
    ![Gezinti Bölmesi][1]
3. Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** hello tehdit algılama ayarlarını görüntüler denetim.
  
    ![Gezinti Bölmesi][2]
4. Kapatma **ON** tehdit algılama.
5. Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları Hello listesini yapılandırın.
6. Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ayarlar.
       
    ![Gezinti Bölmesi][3]

## <a name="set-up-threat-detection-using-powershell"></a>PowerShell kullanarak tehdit saptamayı ayarlama

Bir komut dosyası örneği için bkz: [denetim ve tehdit algılama PowerShell kullanarak yapılandırmanız](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Şüpheli bir olay algılandığında anormal veritabanı etkinliklerini keşfedin
1. Anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız. <br/>
   Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını, uygulama adı ve hello olay süresi dahil olmak üzere bilgileri sağlarız. Ayrıca, hello e-posta olası nedenler bilgileri sağlarız ve önerilen eylemler tooinvestigate ve hello olası tehdit toohello veritabanı azaltmak.<br/>
     
    ![Gezinti Bölmesi][4]
2. Merhaba e-posta uyarısı doğrudan bağlantı toohello SQL denetim günlüğü içerir. Bu bağlantı başlatır hello Azure portal ve açılır hello SQL denetim kayıtlarının hello şüpheli olay hello sırada etrafında'yı tıklatın. Bir denetim kaydı tooview hello şüpheli veritabanı etkinliklerini, yürütüldüğü daha kolay toofind hello SQL deyimlerini yapma hakkında daha fazla ayrıntı tıklayın (kimin, ne yaptığını ve ne zaman) ve hello olay yasal veya kötü amaçlı olup olmadığını belirlemek (örn. uygulama Güvenlik Açığı tooSQL ekleme yararlanan, birisi ihlal hassas verileri, vb.).<br/>
   ![Gezinti Bölmesi][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Tehdit algılama uyarıları hello Azure portal veritabanınızda keşfedin

SQL veritabanı tehdit algılama, uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/en-us/services/security-center/). Merhaba veritabanı dikey penceresinde hello Azure portal parçaları hello etkin tehditleri durumunu içinde dinamik bir SQL güvenlik kutucuğu. 

   ![Gezinti Bölmesi][6]
   
1. Merhaba SQL güvenlik kutucuğa tıklandığında hello Azure Güvenlik Merkezi uyarıları dikey penceresini başlatır ve hello veritabanında algılanan etkin SQL tehditleri genel bir bakış sağlar. 

  ![Gezinti Bölmesi][7]

2. Belirli bir uyarıya tıklayarak, ek ayrıntıları ve bu tehdit araştırma ve gelecekte tehditlere düzeltme eylemleri sağlar.

  ![Gezinti Bölmesi][8]


## <a name="next-steps"></a>Sonraki adımlar

* Tehdit algılama hakkında daha fazla bilgi için başlangıç adresini ziyaret [Azure blogu](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* Daha fazla bilgi edinmek [Azure SQL veritabanı denetimi](sql-database-auditing.md)
* Daha fazla bilgi edinmek [Azure Güvenlik Merkezi](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Fiyatlandırma hakkında daha fazla ayrıntı için lütfen bkz hello [SQL Database fiyatlandırması sayfası](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* PowerShell komut dosyası örneği için bkz: [PowerShell kullanarak denetim ve tehdit algılama yapılandırın](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


