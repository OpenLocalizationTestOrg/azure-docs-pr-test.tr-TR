---
title: "Var olan Azure App Service için MySQL Azure veritabanına bağlanmak | Microsoft Docs"
description: "Nasıl düzgün şekilde var olan bir Azure uygulama hizmeti için MySQL Azure veritabanına bağlanmak için yönergeler"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a>Var olan bir Azure uygulama hizmeti MySQL sunucusu için Azure veritabanına bağlan
Bu belgede, mevcut bir Azure uygulama hizmeti MySQL sunucusu için Azure veritabanına bağlanmak açıklanmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce
[Azure Portal](https://portal.azure.com)’da oturum açın. MySQL sunucusu için bir Azure veritabanı oluşturun. Ayrıntılar için başvurmak [portalından MySQL sunucusu için Azure veritabanı oluşturmak nasıl](quickstart-create-mysql-server-database-using-azure-portal.md) veya [CLI kullanarak MySQL sunucusu için Azure veritabanı oluşturmak nasıl](quickstart-create-mysql-server-database-using-azure-cli.md).

Şu anda bir Azure uygulama hizmeti bir erişimden Azure veritabanı için MySQL etkinleştirmek için iki çözümü vardır. Her iki çözüm de sunucu düzeyinde güvenlik duvarı kurallarını ayarlama içerir.

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a>Çözüm 1 - tüm IP'ler izin veren bir güvenlik duvarı kuralı oluşturma
Azure veritabanı için MySQL verilerinizi korumak için bir Güvenlik Duvarı'nı kullanarak erişim güvenliği sağlar. Bir Azure uygulama hizmetinden MySQL sunucusu için Azure veritabanına bağlanırken giden uygulama IP'leri hizmeti doğası gereği dinamik olduğunu aklınızda bulundurun. 

Azure uygulama hizmetiniz kullanılabilirliğini sağlamak için tüm IP'ler izin vermek için bu çözüm kullanmanızı öneririz.

> [!NOTE]
> Microsoft Azure Hizmetleri için tüm IP'ler için MySQL Azure veritabanına bağlanmak izin verme önlemek uzun vadeli bir çözüm için çalışmaktadır.

1. MySQL server dikey penceresinde, ayarlar altında başlığını tıklatın **bağlantı güvenliği** MySQL için Azure veritabanı için bağlantı güvenliği dikey penceresini açmak için.

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Girin **kural adı**, **başlangıç IP**, ve **bitiş IP**. Daha sonra **Kaydet**'e tıklayın.
   - Kural adı: izin ver-tüm-IP'leri
   - Başlangıç IP: 0.0.0.0
   - Bitiş IP: 255.255.255.255

   ![Azure portal - tüm IP'leri Ekle](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a>Çözüm 2 - açıkça giden IP'leri izin veren bir güvenlik duvarı kuralı oluşturma
Azure uygulama hizmetiniz tüm giden IP'leri açıkça ekleyebilirsiniz.

1. Uygulama hizmeti özellikler dikey penceresini görüntülemek, **giden IP adresi**.

   ![Azure portal - görünüm giden IP'leri](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. MySQL bağlantı güvenlik dikey penceresinde, giden IP'leri tek tek ekleyin.

   ![Azure portal - açık IP'leri Ekle](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Unutmayın **kaydetmek** , güvenlik duvarı kuralları.

IP adreslerini zamanla sabit tutmak Azure uygulama hizmeti çalışır ancak burada IP adresleri değişebilir durumlar vardır. Örneğin, zaman uygulama geri dönüştürüldüğünde ya da bir ölçeklendirme işlemi oluşur veya yeni makineler kapasiteyi artırmak için Azure bölgesel veri merkezleri zaman eklenir. IP adresleri, artık MySQL sunucusuna bağlanabilir durumunda uygulama kapalı kalma süresi karşılaşabilir. Bu olası Yukarıdaki çözümlerden birini seçerken göz önünde bulundurun.

## <a name="ssl-configuration"></a>SSL yapılandırması
Azure veritabanı MySQL için varsayılan olarak SSL etkin sahiptir. Uygulamanız veritabanına bağlanmak için SSL kullanmıyorsa, SSL MySQL sunucuda devre dışı bırakmanız gerekir. SSL, nasıl yapılandırılacağı hakkında ayrıntılı bilgi için bkz: [SSL kullanarak Azure veritabanı için MySQL ile](howto-configure-ssl.md).

## <a name="next-steps"></a>Sonraki adımlar
Bağlantı dizeleri hakkında daha fazla bilgi için bkz [bağlantı dizeleri](howto-connection-string.md).
