---
title: "Sunucu parametreleri Azure veritabanında MySQL için yapılandırma | Microsoft Docs"
description: "Bu makalede, Azure portalını kullanarak MySQL için Azure veritabanı'nda kullanılabilir sunucu parametreleri yapılandırmak açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 718bbf359253849fbc989c563ffd6d1099f92348
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-server-parameters-in-azure-database-for-mysql-using-the-azure-portal"></a>Sunucu parametreleri Azure veritabanı'nda Azure portalını kullanarak MySQL için yapılandırma

Azure veritabanı MySQL için bazı sunucu parametreleri yapılandırmasını destekler. Bu makalede Azure Portalı'nı kullanarak bu parametreleri yapılandırmayı açıklar ve desteklenen parametreler, varsayılan değerleri ve geçerli değer aralığı listeler. Tüm sunucu parametreleri ayarlanabilir. Aşağıda listelenenler desteklenir.

## <a name="navigate-to-server-parameters-blade-on-azure-portal"></a>Azure Portal'da sunucu parametreleri dikey penceresine gidin

Azure portalında oturum açın ve Azure veritabanınız MySQL sunucu adı için'i tıklatın. Altında **ayarları** 'yi tıklatın **sunucu parametreleri** sunucu parametreler dikey Azure veritabanı için MySQL için açın.

![Azure portal sunucusu parametreler dikey](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Yapılandırılabilir sunucu parametrelerin listesi

Aşağıdaki tabloda şu anda desteklenen sunucu parametreleri listeler. Parametreleri uygulama gereksinimlerinize göre yapılandırılabilir.

> [!div class="mx-tableFixed"]
|Parametre Adı|Varsayılan değer|Aralık|Açıklama|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Denetimleri disk ikili günlük dosyasına eşitlemeden önce kaç tane mikrosaniye ikili günlük kaydetme bekler.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|Binlog-Grup-yürütme-sync-delay tarafından'belirlenen geçerli gecikme iptal etmeden önce beklemek için işlem maksimum sayısı.|
|character_set_server|LATIN1|BIG5, UTF8MB4, vb.|Charset_name varsayılan sunucu karakter kümesi olarak kullanın.|
|div_precision_increment|4|0-30|Bölme işlemleri sonucunu ölçeğini artırmak için basamak sayısı.|
|group_concat_max_len|1024|4-16777216|GROUP_CONCAT() için bayt cinsinden uzunluğu izin verilen maksimum sonuç.|
|innodb_adaptive_hash_index|AÇIK|AÇIK, KAPALI|Olup innodb Uyarlamalı karma dizinleri etkin veya devre dışı bırakılan.|
|innodb_lock_wait_timeout|50|1-3600|Saniye cinsinden süreyi InnoDB işlem için bir satır kilidi vazgeçmeden önce bekler.|
|interactive_timeout|1800|10-1800|Sunucu etkinliği etkileşimli bağlantıda kapatmadan önce bekleyeceği saniye sayısı.|
|log_bin_trust_function_creators|KAPALI|AÇIK, KAPALI|Bu değişken ikili günlük kaydı etkinleştirildiğinde geçerlidir. Bu, güvenli olmayan olayların ikili günlüğüne yazılması için neden saklı işlevlerin oluşturmamayı saklı işlevi oluşturucuları güvenilir olup olmadığını denetler.|
|log_queries_not_using_indexes|KAPALI|AÇIK, KAPALI|Yavaş sorgu günlüğü için tüm satırları almak için beklenen sorguları günlüğe kaydeder.|
|log_slow_admin_statements|KAPALI|AÇIK, KAPALI|Yavaş sorgu günlüğüne deyimlerinde yavaş yönetim deyimleri ekleyin.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Bu tür sorgular yavaş sorgu günlüğüne yazılan dakikada sayısını sınırlar.|
|long_query_time|10|1-1E + 100|Bir sorgu birçok saniye bundan daha uzun sürüyorsa, sunucunun Slow_queries durum değişkenine artırır.|
|max_allowed_packet|536870912|1024-1073741824|Bir paket veya herhangi bir üretilen Ara dize ya da C API işlevi mysql_stmt_send_long_data() tarafından gönderilen herhangi bir parametre en büyük boyutu.|
|min_examined_row_limit|0|0-18446744073709551615|Yavaş sorgu günlüğü satırlara yapılandırılmış sayısından fazla sorguları günlüğe kaydeder. |
|server_id|3293747068|1000-4294967295|Her ana verin ve benzersiz bir kimlik slave Çoğaltmada kullanılan sunucu kimliği.|
|slave_net_timeout|60|30-3600|Ana sunucudan daha fazla veri bağlantı kesildi, ikincil varsaymadan önce beklenecek saniye sayısını okuma durdurur ve yeniden bağlanmayı dener.|
|slow_query_log|KAPALI|AÇIK, KAPALI|Etkinleştirmek veya yavaş sorgu günlüğü devre dışı.|
|sql_mode|Seçili 0|ALLOW_INVALID_DATES, IGNORE_SPACE, vb.|Geçerli sunucu SQL modu.|
|time_zone|SİSTEM|Örnekler: -8:00, +05: 30|Sunucu saat dilimi.|
|wait_timeout|120|60-240|Sunucu etkinliğinin etkileşimsiz bağlantıda kapatmadan önce bekleyeceği saniye sayısı.|

## <a name="next-steps"></a>Sonraki adımlar
- [MySQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
