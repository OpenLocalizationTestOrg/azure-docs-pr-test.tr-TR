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
ms.date: 05/10/2017
ms.openlocfilehash: 10f6c490a4fdb4c70cb80b035eaebb9d2ad2e699
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Sunucu, Azure veritabanında PostgreSQL için kaydeder. 
Azure veritabanı PostgreSQL için oluşturur Sorgu ve hata günlükleri. Ancak, işlem günlükleri için erişim desteklenmiyor. Bu günlükler tanımlamak, sorun giderme ve yapılandırma hataları ve alt en iyi performans onarmak için kullanılabilir. Daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Erişim sunucu günlükleri
Listesinde ve Azure Portalı'nı kullanarak Azure PostgreSQL server Hata günlüklerini indirin [Azure CLI](howto-configure-server-logs-using-cli.md) ve Azure REST API'lerini.

## <a name="log-retention"></a>Günlük tutma
Sistem günlüklerini kullanma için bekletme süresini ayarlayabilirsiniz **günlük\_bekletme\_süresi** sunucunuzla ilişkili parametre. Bu parametre için birim (onaylamak için gereklidir) gündür. Üç gün varsayılan değerdir. En yüksek değer 7 gündür. Sunucunuz yeterli sahip gerektiğini unutmayın tutulan günlük dosyalarını içerecek şekilde depolama tahsis edilir.
Her bir saat ya da 100 MB boyutu günlük dosyalarının döndürüleceğini, hangisi önce gelirse.

## <a name="configure-logging-for-azure-postgresql-server"></a>Azure PostgreSQL sunucusu için günlük tutmayı yapılandırma
Sunucunuz için sorgu günlüğü ve hata günlüğünü etkinleştirebilirsiniz. Hata günlüklerini otomatik vakum, bağlantı ve kontrol noktaları bilgiler içerebilir.

İki sunucu parametrelerini ayarlayarak PostgreSQL DB Örneğiniz için sorgu günlüğü etkinleştirebilirsiniz: günlük\_deyimi ve günlük\_min\_süresi\_deyimi.

**Günlük\_deyimi** parametre denetler hangi SQL deyimlerini kaydedilir. Bu parametre ayarını öneririz ***tüm*** tüm deyimleri; oturum için varsayılan değer yok (onaylamak için gereklidir) kullanılır.

**Günlük\_min\_süresi\_deyimi** parametre sınırı günlüğe kaydedilecek deyiminin milisaniye cinsinden ayarlar. Parametre ayarından daha uzun çalışan tüm SQL deyimlerini günlüğe kaydedilir. Bu parametre devre dışı ve 1 (-1) (onaylamak için gereklidir) varsayılan olarak ayarlayın. Bu parametre etkinleştirme uygulamalarınızı iyileştirilmemiş sorgularda aşağı izlemek için faydalı olabilir.

**Günlük\_min\_iletileri** server günlüğüne yazılan düzeyleri ileti denetleme sağlar. Varsayılan uyarı. (onaylamanız gerekir)

Bu ayarlar hakkında daha fazla bilgi için bkz: [hata bildirimi ve günlüğü](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) belgeleri. Azure veritabanı PostgreSQL sunucu parametreleri için özellikle yapılandırmak için bkz: [Azure veritabanı PostgreSQL için sunucu günlüklerine](concepts-server-logs.md).

## <a name="next-steps"></a>Sonraki adımlar
- Azure CLI komut satırı arabirimini kullanarak günlüklerine erişmek için bkz: [Azure CLI kullanarak ve erişimi Yapılandır sunucu günlükleri](howto-configure-server-logs-using-cli.md)
- Sunucu parametreleri hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirmek](howto-configure-server-parameters-using-cli.md).