---
title: "MySQL için Azure veritabanı bir sunucuya geri yükleme | Microsoft Docs"
description: "Bu makalede, Azure portalını kullanarak MySQL için Azure veritabanındaki bir sunucuyu geri yüklemek açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a>Yedekleme ve MySQL için Azure portalını kullanarak Azure veritabanı bir sunucuya geri yükleme

## <a name="backup-happens-automatically"></a>Yedekleme otomatik olarak gerçekleşir
Azure veritabanı için MySQL kullanırken, veritabanı hizmeti yedekleme hizmetinin her 5 dakikada bir otomatik olarak yapar. 

Temel katman ve 35 gün kullanırken yedeklemeler 7 gün için kullanılabilir olan standart katmanı kullanırken. Daha fazla bilgi için bkz: [Azure veritabanı için MySQL hizmet katmanları](concepts-service-tiers.md)

Bu otomatik yedekleme özelliğini kullanarak, sunucu ve tüm veritabanlarını içine bir önceki noktası zaman içinde yeni bir sunucuya geri yükleyebilirsiniz.

## <a name="restore-in-the-azure-portal"></a>Azure portalında geri yükleme
Azure veritabanı için MySQL sağlar, sunucu saati ve içine bir noktaya geri geri yüklemek sunucu yeni bir kopyasını için. Bu yeni sunucu verilerinizi kurtarmak için kullanabilirsiniz. 

Örneğin, bir tablo yanlışlıkla varsa bugün öğlen bırakılan, zaman öğlen hemen önce geri yükleme ve bu sunucunun yeni kopyadan eksik tablo ve veri almak.

Aşağıdaki adımları örnek sunucunun saat içinde bir noktaya geri:

1. Oturum [Azure portalı](https://portal.azure.com/)

2. MySQL sunucusu için Azure veritabanınızı bulun. Sol bölmede seçin **tüm kaynakları**, ardından listeden sunucunuzu seçin.

3.  Sunucu genel bakış dikey üst kısmında tıklayın **geri** araç çubuğunda. Geri yükleme dikey pencere açılır.
![Geri düğmesini tıklatın](./media/howto-restore-server-portal/click-restore-button.png)

4. Gerekli bilgileri geri yükleme formu doldurun:

- **Geri yükleme noktası (UTC)**: Tarih Seçici ve Saat Seçici kullanarak bir noktası geri yüklemek için zaman içinde seçin. Belirtilen süre UTC biçiminde kitabıdır olasılıkla yerel saati UTC dönüştürmeniz gerekir.
- **Yeni bir sunucuya geri**: var olan sunucuya geri yüklemek için yeni bir sunucu adı sağlayın.
- **Konum**: bölge seçimi otomatik olarak kaynak sunucu bölge ile doldurur ve değiştirilemez.
- **Fiyatlandırma katmanı**: fiyatlandırma katmanı seçimi otomatik olarak kaynak sunucuyla aynı fiyatlandırma katmanı doldurur ve burada değiştirilemez. 
![PITR geri yükleme](./media/howto-restore-server-portal/pitr-restore.png)

5. Tıklatın **Tamam** zaman içinde bir noktaya geri yüklemenizi sunucuyu geri yüklemek için. 

6. Geri yükleme tamamlandıktan sonra veritabanları beklendiği gibi yüklendi doğrulamak için oluşturulan yeni sunucu bulun.

## <a name="next-steps"></a>Sonraki adımlar
- [MySQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)