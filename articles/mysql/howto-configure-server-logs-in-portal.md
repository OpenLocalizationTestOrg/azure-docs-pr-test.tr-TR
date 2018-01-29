---
title: "Yapılandırma ve sunucu günlüklerini Azure veritabanı için Azure Portalı'nda MySQL erişim için | Microsoft Docs"
description: "Bu makalede, yapılandırmak ve Azure Portal'da MySQL için Azure veritabanı sunucusu günlüklerine erişmek açıklar."
services: mysql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 10/19/2017
ms.openlocfilehash: 89674c133b458c16fbdacd771be24830624dde7c
ms.sourcegitcommit: 2d1153d625a7318d7b12a6493f5a2122a16052e0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/20/2017
---
# <a name="configure-and-access-server-logs-in-the-azure-portal"></a>Yapılandırma ve erişim sunucusu Azure portalında oturum

Yapılandırma, liste indirin ve [Azure veritabanı için MySQL server günlüklerini](concepts-server-logs.md) Azure portalından.

## <a name="prerequisites"></a>Ön koşullar
Nasıl yapılır bu kılavuzu adım için gerekir:
- [MySQL sunucusu için Azure veritabanı](quickstart-create-mysql-server-database-using-azure-portal.md)

## <a name="configure-logging"></a>Günlük tutmayı yapılandırma
MySQL yavaş sorgu günlüğü erişimi yapılandırın. 

1. [Azure Portal](http://portal.azure.com/) oturum açın.

2. MySQL sunucusu için Azure veritabanınızı seçin.

3. Altında **izleme** kenar, select bölümünde **sunucu günlükleri**. 
   ![Select sunucusu günlükleri, yapılandırmak için tıklatın](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)

4. Başlığı seçin **günlüklerini etkinleştirmek ve günlük parametreleri yapılandırmak için burayı tıklatın** sunucu parametreleri görmek için.

5. Seçin **daha fazla Göster** genişletilmiş bir kullanılabilir parametrelerin listesini görmek için genişletici. 

   MySQL belgelerine bakın parametrelerinin tanımları hakkında daha fazla bilgi için [günlükleri](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).

   ![Daha uzun bir liste için Göster'i tıklatın](./media/howto-configure-server-logs-in-portal/2-show-more.png)

6. Ayarlamanız gereken parametrelerini değiştirin. Bu oturumda yaptığınız tüm değişiklikleri mor ile vurgulanır. 

   Parametreleri değişti sonra tıklayabilirsiniz **kaydetmek**. Veya **atmak** değişikliklerinizi.

   ![Kaydet'i tıklatın veya atın](./media/howto-configure-server-logs-in-portal/3-save-discard.png)

7. Tıklayarak günlükleri listesine dönmek **Kapat düğmesini** (X simgesi) üzerinde **sunucu parametreleri** sayfası.

## <a name="view-list-and-download-logs"></a>Listesini görüntülemek ve günlükleri indirmek
Günlüğe kaydetme başladıktan sonra kullanılabilir günlüklerini listesini görüntülemek ve sunucu günlüklerini bölmesinde ayrı günlük dosyalarını yükleyin. 

1. Azure Portalı'nı açın.

2. MySQL sunucusu için Azure veritabanınızı seçin.

3. Altında **izleme** kenar, select bölümünde **sunucu günlükleri**. Sayfa gösterildiği gibi günlük dosyalarının listesini gösterir:

   ![Günlükleri listesi](./media/howto-configure-server-logs-in-portal/4-server-logs-list.png)

   > [!TIP]
   > Günlük adlandırma kuralı **mysql - yavaş - < sunucu adı >-yyyymmddhh.log**. Tarih ve saat kullanılan dosya adı, günlük yayımlandığında saattir. Günlük dosyalarını Döndürülmüş her 24 saat veya 7.5 GB, hangisi gelir ilk.

4. Gerekirse, kullanın **arama kutusu** tarih/saat üzerine göre belirli bir günlük için hızlı bir şekilde daraltın. Arama günlüğü üzerinde adıdır.

5. Kullanarak tek tek günlük dosyaları karşıdan **karşıdan** düğmesini (ok simgesi) her tablo satırı günlük dosyasında yanındaki gösterildiği gibi:

   ![İndirme simgesine tıklayın](./media/howto-configure-server-logs-in-portal/5-download.png)


## <a name="next-steps"></a>Sonraki adımlar
- Bkz: [CLI erişim Server günlükleri](howto-configure-server-logs-in-cli.md) günlükleri programlı olarak indirmek hakkında bilgi edinmek için.
- Daha fazla bilgi edinmek [sunucu günlükleri](concepts-server-logs.md) MySQL için Azure veritabanında. 
- Parametre tanımları ve MySQL günlüğe kaydetme hakkında daha fazla bilgi için MySQL belgelerine bakın [günlükleri](https://dev.mysql.com/doc/refman/5.7/en/slow-query-log.html).

