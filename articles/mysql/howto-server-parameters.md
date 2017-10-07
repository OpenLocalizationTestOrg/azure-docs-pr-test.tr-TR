---
title: "aaaHow tooConfigure Azure veritabanı için MySQL Server parametrelerinde | Microsoft Docs"
description: "Bu makalede, Azure veritabanındaki tooconfigure kullanılabilir sunucu parametreleri MySQL kullanmak için Azure portalını nasıl hello açıklanmaktadır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Azure veritabanı içindeki tooconfigure sunucu parametreleri MySQL kullanmak için Azure portal nasıl hello

Azure veritabanı MySQL için bazı sunucu parametreleri yapılandırmasını destekler. Bu makalede tooconfigure hello Azure portal ve listeleri hello kullanarak bu parametreleri nasıl desteklediği açıklanır parametreleri, hello varsayılan değerler ve geçerli değerleri hello aralığı. Tüm sunucu parametreleri ayarlanabilir. Yalnızca Burada listelenen olanları hello desteklenir.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Azure portalındaki tooServer parametreler dikey gidin

Toohello Azure portalında oturum açın ve Azure veritabanınız MySQL sunucu adı için'i tıklatın. Merhaba altında **ayarları** 'yi tıklatın **sunucu parametreleri** tooopen hello sunucu parametreler dikey hello Azure veritabanı için MySQL için.

![Azure portal sunucusu parametreler dikey](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Yapılandırılabilir sunucu parametrelerin listesi

Aşağıdaki tablonun hello şu anda desteklenen hello sunucu parametreleri listeler. uygulama gereksinimleri tooyour göre Hello parametreleri yapılandırılabilir.

> [!div class="mx-tableFixed"]
|Parametre Adı|Varsayılan değer|Aralık|Açıklama|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Denetimleri ikili günlük kaydetme bekler hello ikili günlük dosyası toodisk eşitlemeden önce kaç tane mikrosaniye hello.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|Merhaba sayısı üst sınırı işlemleri toowait önce binlog-Grup-yürütme-sync-delay belirtildiği gibi hello geçerli gecikme durduruluyor.|
|character_set_server|LATIN1|BIG5, UTF8MB4, vb.|Charset_name hello varsayılan sunucu karakter kümesi olarak kullanın.|
|div_precision_increment|4|0-30|Hangi tooincrease hello ölçek bölme işlemlerinin hello sonucunun tarafından basamak sayısı.|
|group_concat_max_len|1024|4-16777216|Maksimum sonuç hello GROUP_CONCAT() için bayt cinsinden izin verilen uzunluk.|
|innodb_adaptive_hash_index|AÇIK|AÇIK, KAPALI|Olup innodb Uyarlamalı karma dizinleri etkin veya devre dışı bırakılan.|
|innodb_lock_wait_timeout|50|1-3600|Merhaba süreyi saniye cinsinden bir InnoDB işlem için bir satır kilidi vazgeçmeden önce bekler.|
|interactive_timeout|1800|10-1800|Saniye hello sunucu sayısını kapatmadan önce etkileşimli bir bağlantı faaliyete bekler.|
|log_bin_trust_function_creators|KAPALI|AÇIK, KAPALI|Bu değişken ikili günlük kaydı etkinleştirildiğinde geçerlidir. Bu oluşturucuları olabilir saklı işlevi değil toohello ikili günlük yazılan güvenli olmayan olaylar toobe neden depolanan toocreate işlevleri güvenilir olup olmadığını denetler.|
|log_queries_not_using_indexes|KAPALI|AÇIK, KAPALI|Günlükleri sorgularını tooretrieve tüm satırları tooslow sorgu günlüğü bekleniyordu.|
|log_slow_admin_statements|KAPALI|AÇIK, KAPALI|Yavaş yönetim deyimleri toohello yavaş sorgu günlüğüne hello deyimlerinde içerir.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Sınırları sorgularını toohello yavaş sorgu günlüğü yazılabilir dakikada sayısı hello.|
|long_query_time|10|1-1E + 100|Bir sorgu birçok saniye bundan daha uzun sürüyorsa, hello sunucu hello Slow_queries durum değişkenine artırır.|
|max_allowed_packet|536870912|1024-1073741824|bir paket veya herhangi bir üretilen Ara dize ya da hello mysql_stmt_send_long_data() C API işlevi tarafından gönderilen herhangi bir parametre Hello en büyük boyutu.|
|min_examined_row_limit|0|0-18446744073709551615|Merhaba yavaş sorgu günlüğü satırlara yapılandırılmış hello sayısından fazla sorguları günlüğe kaydeder. |
|server_id|3293747068|1000-4294967295|Çoğaltma toogive kullanılan hello sunucu kimliği her ana ve benzersiz bir kimlik slave.|
|slave_net_timeout|60|30-3600|hello bağlantı kesildi, hello bağımlı varsaymadan önce hello ana sunucudan daha fazla veri saniye toowait Hello sayısı hello okuma iptal eder ve tooreconnect çalışır.|
|slow_query_log|KAPALI|AÇIK, KAPALI|Etkinleştirmek veya hello yavaş sorgu günlüğü devre dışı.|
|sql_mode|Seçili 0|ALLOW_INVALID_DATES, IGNORE_SPACE, vb.|Merhaba geçerli sunucu SQL modu.|
|time_zone|SİSTEM|Örnekler: -8:00, +05: 30|Merhaba sunucu saat dilimi.|
|wait_timeout|120|60-240|Merhaba saniye hello sunucu sayısını kapatmadan önce etkileşimsiz bağlantı faaliyete bekler.|

## <a name="next-steps"></a>Sonraki adımlar
- [MySQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
