---
title: "Sunucu, PostgreSQL için Azure veritabanında kaydeder | Microsoft Docs"
description: "Sorgu ve Hata günlüklerini PostgreSQL için Azure veritabanı'nda oluşturur."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 09/26/2017
ms.openlocfilehash: 696af85cd5609171a719a7e77efbfcdeba0aaaaa
ms.sourcegitcommit: 9c3150e91cc3075141dc2955a01f47040d76048a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/26/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Sunucu, Azure veritabanında PostgreSQL için kaydeder. 
Azure veritabanı PostgreSQL için oluşturur Sorgu ve hata günlükleri. Ancak, işlem günlükleri için erişim desteklenmiyor. Sorgu ve Hata günlüklerini tanımlamak, sorun giderme ve yapılandırma hataları ve performansın onarmak için kullanılabilir. Daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Sunucu günlüklerine erişme
Listesinde ve Azure portalını kullanarak Azure PostgreSQL server Hata günlüklerini indirin [Azure CLI](howto-configure-server-logs-using-cli.md)ve Azure REST API'lerini.

## <a name="log-retention"></a>Günlük tutma
Sistem günlüklerini kullanma için bekletme süresini ayarlayabilirsiniz **günlük\_bekletme\_süresi** sunucunuzla ilişkili parametre. Bu parametre için gün birimidir. Varsayılan değer 3 gündür. En yüksek değer 7 gündür. Sunucunuz yeterli olmalıdır tutulan günlük dosyalarını içerecek şekilde depolama tahsis edilir.
Günlük dosyaları her bir saat ya da 100 MB boyutuna döndür, hangisi önce gelirse.

## <a name="configure-logging-for-azure-postgresql-server"></a>Azure PostgreSQL sunucusu için günlük tutmayı yapılandırma
Sunucunuz için sorgu günlüğü ve hata günlüğünü etkinleştirebilirsiniz. Hata günlüklerini otomatik vakum, bağlantı ve kontrol noktaları bilgiler içerebilir.

İki sunucu parametrelerini ayarlayarak PostgreSQL DB Örneğiniz için sorgu günlüğü etkinleştirebilirsiniz: `log\_statement` ve `log\_min\_duration\_statement`.

**Günlük\_deyimi** parametre denetler hangi SQL deyimlerini kaydedilir. Bu parametre ayarını öneririz ***tüm*** tüm deyimleri; oturum için varsayılan değer Yok'tur.

**Günlük\_min\_süresi\_deyimi** parametre sınırı günlüğe kaydedilecek deyiminin milisaniye cinsinden ayarlar. Parametre ayarından daha uzun çalışan tüm SQL deyimlerini günlüğe kaydedilir. Bu parametre devre dışı ve varsayılan olarak 1 (-1) ayarlayın. Bu parametre etkinleştirme uygulamalarınızı iyileştirilmemiş sorgularda aşağı izlemek için faydalı olabilir.

**Günlük\_min\_iletileri** server günlüğüne yazılan düzeyleri ileti denetleme sağlar. Varsayılan uyarı. 

Bu ayarlar hakkında daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) belgeleri. Azure veritabanı PostgreSQL sunucu parametreleri için özellikle yapılandırmak için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirmek](howto-configure-server-parameters-using-cli.md).

## <a name="next-steps"></a>Sonraki adımlar
- Azure CLI komut satırı arabirimi kullanarak günlüklerine erişmek için bkz: [ve erişimi Yapılandır sunucu günlüklerini Azure CLI kullanarak](howto-configure-server-logs-using-cli.md).
- Sunucu parametreleri hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirmek](howto-configure-server-parameters-using-cli.md).
