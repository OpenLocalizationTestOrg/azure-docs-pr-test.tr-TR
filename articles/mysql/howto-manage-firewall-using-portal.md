---
title: "aaaCreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme
Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler tooaccess Azure veritabanı MySQL sunucusu için belirtilen bir IP adresi veya IP adresi aralığı etkinleştirin. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma

1. Ayarlar altında hello MySQL server dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey hello Azure veritabanı için MySQL için.

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Tıklatın **eklemek IP** hello araç toocreate hello Azure sistem tarafından algılanan gibi bilgisayarınızın hello IP adresine sahip bir kural üzerinde.

   ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Merhaba yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın. Bazı durumlarda, Azure portal tarafından gözlenen hello IP adresi başlangıç IP adresinden kullanılan farklı olduğunda erişme hello Internet ve Azure sunucuları. Bu nedenle, beklendiği gibi toochange hello IP başlangıç ve bitiş IP toomake hello kural işlevi gerekebilir.

   Bir arama motoru veya diğer çevrimiçi aracı toocheck kendi IP adresini kullanın (örneğin, "IP adresimi nedir" için arama yapın).

   ![My IP nedir için Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Ek adres aralıklarını ekleyin. MySQL Güvenlik Duvarı'nda hello Azure veritabanı için Hello kuralları'nda tek bir IP adresi veya adres aralığı belirtebilirsiniz. Toolimit hello kural tooone tek bir IP adresi, aynı hello alanında IP başlangıç ve bitiş IP adresi türü hello istiyorsanız. Merhaba Güvenlik Duvarı'nı açma Yöneticiler ve kullanıcılar tooaccess hello MySQL server toowhich geçerli kimlik bilgilerine sahip oldukları herhangi bir veritabanı sağlar.

   ![Azure portal - güvenlik duvarı kuralları ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello. Merhaba güncelleştirme toohello güvenlik duvarı kuralları başarılı oldu hello onaylanmasını bekleyin.

   ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Var olan sunucu düzeyinde güvenlik duvarı kuralları hello Azure portal aracılığıyla yönetin
Merhaba adımları toomanage hello güvenlik duvarı kuralları yineleyin.
* tooadd hello geçerli bilgisayar, **+ IP eklemek**.
* tooadd ek IP adreslerini yazın hello **kural adı**, **başlangıç IP**, ve **bitiş IP**.
* Mevcut bir kuralı toomodify hello kural hello alanlarında birini tıklatın ve değiştirin.
* var olan toodelete kural hello üç nokta [...] ve'ı tıklatın **silmek**.
* Tıklatın **kaydetmek** toosave hello değişiklikleri.

## <a name="next-steps"></a>Sonraki adımlar
- MySQL sunucusu için Azure veritabanı tooan bağlanma konusunda yardım için bkz: [Azure veritabanı için MySQL için bağlantı kitaplıkları](./concepts-connection-libraries.md)
