---
title: "aaaHow tooRestore Azure veritabanı için MySQL Server'da | Microsoft Docs"
description: "Bu makalede nasıl toorestore MySQL kullanmak için bir sunucu Azure veritabanındaki hello Azure portalı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Azure portal tooBackup ve geri yükleme MySQL kullanmak için bir sunucu Azure veritabanında nasıl hello

## <a name="backup-happens-automatically"></a>Yedekleme otomatik olarak gerçekleşir
Azure veritabanı için MySQL kullanırken, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar. 

Temel katman ve 35 gün kullanırken Hello yedeklemeler 7 gün boyunca kullanılabilir standart katmanı kullanırken. Daha fazla bilgi için bkz: [Azure veritabanı için MySQL hizmet katmanları](concepts-service-tiers.md)

Bu otomatik yedekleme özelliğini kullanarak, hello server ve tüm veritabanlarının bir yeni sunucu tooan önceki zaman içinde nokta geri yükleyebilirsiniz.

## <a name="restore-in-hello-azure-portal"></a>Hello Azure portalına geri yükleme
Azure veritabanı MySQL için saat ve yeni bir kopyasını tooa hello sunucusunun toorestore hello sunucusu geri tooa noktası sağlar. Bu yeni sunucu toorecover verilerinizi kullanabilirsiniz. 

Örneğin, bir tablo yanlışlıkla olduysa bugün öğlen bırakılan, toohello zaman öğlen hemen önce geri ve tablo ve bu kopyasını hello sunucu verilerinden eksik hello alın.

Merhaba aşağıdaki adımları hello örnek sunucu tooa sürede geri yükleme noktası:

1. Merhaba içine oturum [Azure portalı](https://portal.azure.com/)

2. MySQL sunucusu için Azure veritabanınızı bulun. Merhaba sol bölmesinde seçin **tüm kaynakları**, ardından hello listesinden sunucunuzu seçin.

3.  Hello sunucu genel bakış dikey penceresinde Hello üstte tıklatın **geri** hello araç. Merhaba geri yükleme dikey pencere açılır.
![Geri düğmesini tıklatın](./media/howto-restore-server-portal/click-restore-button.png)

4. Merhaba geri yükleme formu hello gerekli bilgilerle doldurun:

- **Geri yükleme noktası (UTC)**: hello Tarih Seçici ve Saat Seçici kullanarak, bir zaman içinde nokta toorestore seçin. Belirtilen başlangıç saati UTC biçiminde kitabıdır tooconvert hello yerel saati UTC gerekmesi muhtemeldir.
- **Toonew sunucuyu geri**: yeni bir sunucu adı toorestore hello varolan Server'a sağlayın.
- **Konum**: hello bölge seçim otomatik olarak hello kaynak sunucu bölge ile doldurur ve değiştirilemez.
- **Fiyatlandırma katmanı**: katmanı seçimi otomatik olarak fiyatlandırma hello aynı fiyatlandırma katmanı hello kaynak sunucu ve burada değiştirilemez hello ile doldurur. 
![PITR geri yükleme](./media/howto-restore-server-portal/pitr-restore.png)

5. Tıklatın **Tamam** toorestore hello sunucu toorestore tooa bir noktaya. 

6. Merhaba geri yükleme tamamlandıktan sonra veritabanları beklendiği gibi yüklendi tooverify hello oluşturulmuş yeni bir sunucu hello bulun.

## <a name="next-steps"></a>Sonraki adımlar
- [MySQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)