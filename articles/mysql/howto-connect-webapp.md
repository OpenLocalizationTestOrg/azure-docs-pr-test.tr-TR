---
title: "aaaConnect mevcut Azure App Service tooAzure veritabanı için MySQL | Microsoft Docs"
description: "Nasıl tooproperly bağlanacağını var olan bir Azure uygulama hizmeti tooAzure veritabanı için MySQL için yönergeler"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>MySQL sunucusu için var olan bir Azure uygulama hizmeti tooAzure veritabanına bağlan
Bu belge açıklar tooconnect var olan bir Azure uygulama hizmeti tooyour Azure veritabanı nasıl MySQL sunucusu için.

## <a name="before-you-begin"></a>Başlamadan önce
İçinde toohello oturum [Azure portal](https://portal.azure.com). MySQL sunucusu için bir Azure veritabanı oluşturun. Ayrıntılar için çok başvurun[toocreate Azure veritabanı nasıl portalından MySQL sunucusu için](quickstart-create-mysql-server-database-using-azure-portal.md) veya [toocreate Azure veritabanı nasıl CLI kullanarak MySQL sunucusu için](quickstart-create-mysql-server-database-using-azure-cli.md).

Şu anda iki çözümleri tooenable erişimden Azure App Service tooan Azure veritabanı için MySQL vardır. Her iki çözüm de sunucu düzeyinde güvenlik duvarı kurallarını ayarlama içerir.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Çözüm 1 - tüm IP'ler bir güvenlik duvarı kuralı tooallow oluşturma
Azure veritabanı MySQL için bir güvenlik duvarı tooprotect verilerinizi kullanarak erişim güvenliği sağlar. MySQL sunucusu için Azure App Service tooAzure veritabanı bağlantı tuttuğunuzda göz önünde bu hello giden uygulama hizmeti IP'leri doğası gereği dinamik. 

Azure uygulama hizmetiniz hello kullanılabilirliğini tooensure, bu çözüm tooallow tüm IP'ler kullanmanızı öneririz.

> [!NOTE]
> Microsoft Azure Hizmetleri tooconnect tooAzure veritabanı için tüm IP'ler için MySQL izin vererek uzun vadeli bir çözüm tooavoid için çalışmaktadır.

1. Ayarlar altında hello MySQL server dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey hello Azure veritabanı için MySQL için.

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Girin **kural adı**, **başlangıç IP**, ve **bitiş IP**. Daha sonra **Kaydet**'e tıklayın.
   - Kural adı: izin ver-tüm-IP'leri
   - Başlangıç IP: 0.0.0.0
   - Bitiş IP: 255.255.255.255

   ![Azure portal - tüm IP'leri Ekle](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Çözüm 2 - oluşturmak bir güvenlik duvarı kuralı tooexplicitly giden IP'leri izin ver
Tüm Azure uygulama hizmetiniz, giden IP'leri hello açıkça ekleyebilirsiniz.

1. Merhaba App Service özellikleri dikey penceresinde, görüntülemek, **giden IP adresi**.

   ![Azure portal - görünüm giden IP'leri](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. Merhaba MySQL bağlantı güvenlik dikey penceresinde, giden IP'leri tek tek ekleyin.

   ![Azure portal - açık IP'leri Ekle](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Çok unutmayın**kaydetmek** , güvenlik duvarı kuralları.

Hello Azure uygulama hizmeti tookeep IP adresleri sabiti zaman içinde çalışır ancak burada hello IP adresleri değişebilir durumlar vardır. Örneğin, uygulama dönüştürür zaman hello bir ölçeklendirme işlemi oluşur veya tooincrease hello kapasite merkezleri yeni makineler Azure bölgesel verilerinde zaman eklenir. Değişiklik Hello IP adresleri kullanılırken hello uygulama kapalı kalma süresi, artık bağlanabilir hello olay karşılaşması toohello MySQL sunucu. Bu olası çözümleri önceki hello birini seçerken göz önünde bulundurun.

## <a name="ssl-configuration"></a>SSL yapılandırması
Azure veritabanı MySQL için varsayılan olarak SSL etkin sahiptir. Uygulamanızı SSL tooconnect toohello veritabanı kullanmıyorsa, MySQL sunucusundaki SSL toodisable gerekir. Ayrıntılar için tooconfigure SSL, bkz: [SSL kullanarak Azure veritabanı için MySQL ile](howto-configure-ssl.md).

## <a name="next-steps"></a>Sonraki adımlar
Bağlantı dizeleri hakkında daha fazla bilgi için çok başvuran[bağlantı dizeleri](howto-connection-string.md).
