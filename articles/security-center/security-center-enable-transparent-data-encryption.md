---
title: "Azure Güvenlik Merkezi'nde saydam veri şifreleme aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek saydam veri şifreleme **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde saydam veri şifreleme etkinleştir
Azure Güvenlik Merkezi TDE zaten etkin değilse SQL veritabanlarını saydam veri şifreleme (TDE) etkinleştirmek önerir. TDE, verilerinizi korur ve veritabanınızı, ilişkili yedeklemelerinizi ve geri kalan, işlem günlüğü dosyalarını değişiklikleri tooyour uygulama gerek kalmadan şifreleyerek uyumluluk gereksinimlerinin karşılanmasına yardımcı olur. toolearn daha fazla [saydam veri şifrelemesi ile Azure SQL veritabanı](https://msdn.microsoft.com/library/dn948096).

Bu öneri toohello yalnızca Azure SQL Hizmeti uygulanır; sanal makinelerde çalışan SQL içermez.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek saydam veri şifreleme**.
   ![Saydam Veri Şifrelemesini Etkinleştirme][1]
2. Merhaba açılır **etkinleştirmek saydam veri şifreleme SQL veritabanlarında** dikey. Bir SQL veritabanı tooenable TDE seçin.
   ![SQL DB tooenable TDE seçin][2]
3. Merhaba üzerinde **saydam veri şifreleme** dikey penceresinde, select **ON** veri şifreleme ve select altında **kaydetmek** hello dikey pencerenin üst hello Şeritte.
   ![TDE üzerinde Aç][3]

   TDE etkinleştirildiğinde hello SQL veritabanı hello seçili **şifreleme durumu** çok değiştirecek**şifreli**.    

   ![Şifreleme durumu][4]

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Etkinleştirme saydam veri şifreleme." gösterdi. SQL TDE'nin hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Saydam veri şifrelemesi ile Azure SQL veritabanı](https://msdn.microsoft.com/library/dn948096)
* [Saydam veri şifreleme (TDE) ile çalışmaya başlama](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
