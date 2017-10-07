---
title: "Nasıl tooRestore PostgreSQL için Azure veritabanında bir sunucu | Microsoft Docs"
description: "Bu makalede nasıl toorestore PostgreSQL kullanmak için bir sunucu Azure veritabanındaki hello Azure portalı."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>Azure portal tooBackup ve geri yükleme PostgreSQL kullanmak için bir sunucu Azure veritabanında nasıl hello

## <a name="backup-happens-automatically"></a>Yedekleme otomatik olarak gerçekleşir
Azure veritabanı için PostgreSQL kullanırken, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar. 

Temel katman ve 35 gün kullanırken Hello yedeklemeler 7 gün boyunca kullanılabilir standart katmanı kullanırken. Daha fazla bilgi için bkz: [PostgreSQL hizmet katmanları için Azure veritabanı](concepts-service-tiers.md)

Bu otomatik yedekleme özelliğini kullanarak, hello server ve tüm veritabanlarının bir yeni sunucu tooan önceki zaman içinde nokta geri yükleyebilirsiniz.

## <a name="restore-in-hello-azure-portal"></a>Hello Azure portalına geri yükleme
Azure veritabanı PostgreSQL için saat ve yeni bir kopyasını tooa hello sunucusunun toorestore hello sunucusu geri tooa noktası sağlar. Bu yeni sunucu toorecover verilerinizi kullanabilirsiniz. 

Örneğin, bir tablo yanlışlıkla olduysa bugün öğlen bırakılan, toohello zaman öğlen hemen önce geri ve tablo ve bu kopyasını hello sunucu verilerinden eksik hello alın.

Merhaba aşağıdaki adımları hello örnek sunucu tooa sürede geri yükleme noktası:
1. Merhaba içine oturum [Azure portalı](https://portal.azure.com/)
2. Azure veritabanınız PostgreSQL sunucu için bulun. Hello Azure portal'ı tıklatın **tüm kaynakları** hello sol menüsünden ve hello adı yazın gibi **mypgserver 20170401**, varolan sunucunuz için toosearch. Merhaba arama sonucunda listelenen hello sunucu adına tıklayın. Merhaba **genel bakış** sayfası sunucunuz açar ve ek yapılandırma seçeneklerini sağlar.

   ![Azure portal - sunucunuz toolocate arama](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Hello sunucu genel bakış dikey penceresinde Hello üstte tıklatın **geri** hello araç. Merhaba geri yükleme dikey pencere açılır.

   ![Azure veritabanı için PostgreSQL - genel bakış - Geri Yükle düğmesi](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Merhaba geri yükleme formu hello gerekli bilgilerle doldurun:

   ![Azure veritabanı PostgreSQL - geri yüklemesi bilgi için ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Geri yükleme noktası**: bir noktası hello sunucu değiştirilmeden önce oluşan zaman seçin
  - **Hedef sunucu**: toorestore için istediğiniz yeni bir sunucu adı sağlayın
  - **Konum**: hello bölge seçemezsiniz, varsayılan olarak hello kaynak sunucu ile aynı.
  - **Fiyatlandırma katmanı**: bir sunucu geri yüklerken bu değer değiştirilemez. Merhaba kaynak sunucu ile aynı. 

5. Tıklatın **Tamam** toorestore hello sunucu toorestore tooa bir noktaya. 

6. Merhaba geri yükleme tamamlandıktan sonra verilerin beklenen şekilde geri tooverify hello oluşturulan yeni bir sunucu hello bulun.

## <a name="next-steps"></a>Sonraki adımlar
- [Azure veritabanı PostgreSQL için için bağlantı kitaplıkları](concepts-connection-libraries.md)
