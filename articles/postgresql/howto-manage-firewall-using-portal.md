---
title: "aaaCreate ve PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak Azure veritabanını yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme
Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler tooaccess Azure veritabanı PostgreSQL sunucu için belirtilen bir IP adresi veya IP adresleri aralığını etkinleştirin. 

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Bir sunucu [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma
1. Ayarlar altında hello PostgreSQL sunucu dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey penceresinde hello Azure veritabanı PostgreSQL için.

  ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Tıklatın **eklemek IP** hello araç. Bu kural otomatik olarak hello Azure sistem tarafından algılanan olarak bilgisayarınızın hello IP adresiyle oluşturur.

  ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Merhaba yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın. Bazı durumlarda, Azure portal tarafından gözlenen hello IP adresi başlangıç IP adresinden kullanılan farklı olduğunda erişme hello Internet ve Azure sunucuları. Bu nedenle, beklendiği gibi toochange hello IP başlangıç ve bitiş IP toomake hello kural işlevi gerekebilir.
Bir arama motoru veya diğer çevrimiçi aracı toocheck kendi IP adresi ("Benim IP nedir" Örneğin, Bing arama) kullanın.

  ![Bing arama my IP nedir](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Ek adres aralıklarını ekleyin. Hello Azure veritabanı PostgreSQL Güvenlik Duvarı'nda Hello kurallarında, tek bir IP adresi veya adres aralığı belirtebilirsiniz. Toolimit hello kural tooone tek bir IP adresi, aynı hello alanında IP başlangıç ve bitiş IP adresi türü hello istiyorsanız. Merhaba Güvenlik Duvarı'nı açma hello geçerli kimlik bilgilerine sahip oldukları PostgreSQL sunucu toowhich Yöneticiler ve kullanıcılar toologin tooany veritabanında sağlar.

  ![Azure portal - güvenlik duvarı kuralları ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello. Merhaba güncelleştirme toohello güvenlik duvarı kuralları başarılı oldu hello onaylanmasını bekleyin.

  ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Var olan sunucu düzeyinde güvenlik duvarı kuralları hello Azure portal aracılığıyla yönetin
Merhaba adımları toomanage hello güvenlik duvarı kuralları yineleyin.
* tooadd hello geçerli bilgisayar düğmesini hello çok + **eklemek IP**. Tıklatın **kaydetmek** toosave hello değişiklikleri.
* Kural adı, IP adresi başlangıç ve bitiş IP adresi hello tooadd ek IP adreslerini yazın. Tıklatın **kaydetmek** toosave hello değişiklikleri.
* Mevcut bir kuralı toomodify hello kural hello alanlarında birini tıklatın ve değiştirin. Tıklatın **kaydetmek** toosave hello değişiklikleri.
* Mevcut bir kuralı toodelete hello üç nokta [...] ve silme Kaldır hello kuralı tıklayın. Tıklatın **kaydetmek** toosave hello değişiklikleri.

## <a name="next-steps"></a>Sonraki adımlar
- Benzer şekilde, çok komut dosyası oluşturabileceğiniz[oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme](howto-manage-firewall-using-cli.md)
- Tooan Azure veritabanı PostgreSQL sunucusu bağlanma konusunda yardım için bkz [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
