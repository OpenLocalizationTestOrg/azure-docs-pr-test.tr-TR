---
title: "aaaServer PostgreSQL için Azure veritabanı'nda oturum | Microsoft Docs"
description: "Sorgu ve Hata günlüklerini PostgreSQL için Azure veritabanı'nda oluşturur."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Sunucu, Azure veritabanında PostgreSQL için kaydeder. 
Azure veritabanı PostgreSQL için oluşturur Sorgu ve hata günlükleri. Ancak, erişim tootransaction günlükleri desteklenmiyor. Bu günlükler kullanılan tooidentify olması, sorun giderme ve yapılandırma hataları ve alt en iyi performans onarın. Daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Erişim sunucu günlükleri
Liste ve hello Azure Portal kullanarak Azure PostgreSQL server Hata günlüklerini indirin [Azure CLI](howto-configure-server-logs-using-cli.md) ve Azure REST API'lerini.

## <a name="log-retention"></a>Günlük tutma
Sistem günlüklerini kullanarak hello saklama süresi ayarlayabilirsiniz **günlük\_bekletme\_süresi** sunucunuzla ilişkili parametre. Bu parametre için Hello birimi (tooconfirm gerekir) gündür. üç gün Hello varsayılan değerdir. Merhaba en yüksek değer 7 gündür. Sunucunuz yeterli ayrılan depolama alanı toocontain korunur hello günlük dosyalarını olması gerektiğini unutmayın.
Her bir saat ya da 100 MB boyutu Hello günlük dosyalarının döndürüleceğini, hangisi önce gelirse.

## <a name="configure-logging-for-azure-postgresql-server"></a>Azure PostgreSQL sunucusu için günlük tutmayı yapılandırma
Sunucunuz için sorgu günlüğü ve hata günlüğünü etkinleştirebilirsiniz. Hata günlüklerini otomatik vakum, bağlantı ve kontrol noktaları bilgiler içerebilir.

İki sunucu parametrelerini ayarlayarak PostgreSQL DB Örneğiniz için sorgu günlüğü etkinleştirebilirsiniz: günlük\_deyimi ve günlük\_min\_süresi\_deyimi.

Merhaba **günlük\_deyimi** parametre denetler hangi SQL deyimlerini kaydedilir. Bu parametre çok ayarı öneririz***tüm*** toolog tüm deyimleri; hello varsayılan değer yok (gereklidir tooconfirm).

Merhaba **günlük\_min\_süresi\_deyimi** parametre hello sınırı oturum deyimi toobe milisaniye cinsinden ayarlar. Merhaba parametre ayarı daha uzun süre çalışan tüm SQL deyimlerini günlüğe kaydedilir. Bu parametre (gerek tooconfirm) varsayılan olarak devre dışı bırakılmış ve ayarlanmış toominus 1 (-1) olur. Bu parametre etkinleştirme uygulamalarınızı iyileştirilmemiş sorgularda aşağı izlemek için faydalı olabilir.

Merhaba **günlük\_min\_iletileri** hangi ileti düzeyleri toohello server günlüğüne yazılan toocontrol sağlar. Merhaba varsayılan uyarı. (tooconfirm gerekir)

Bu ayarlar hakkında daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) belgeleri. Azure veritabanı PostgreSQL sunucu parametreleri için özellikle yapılandırmak için bkz: [Azure veritabanı PostgreSQL için sunucu günlüklerine](concepts-server-logs.md).

## <a name="next-steps"></a>Sonraki adımlar
- Azure CLI komut satırı arabirimini kullanarak tooaccess günlüklerine bakın [Azure CLI kullanarak ve erişimi Yapılandır sunucu günlükleri](howto-configure-server-logs-using-cli.md)
- Sunucu parametreleri hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirmek](howto-configure-server-parameters-using-cli.md).