---
title: "Azure veritabanı için MySQL için aaaSSL bağlantısı | Microsoft Docs"
description: "Azure veritabanı MySQL ve ilişkili uygulamalar tooproperly için yapılandırma bilgileri SSL bağlantılarını kullanın"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>MySQL için Azure veritabanındaki SSL bağlantısı
Azure veritabanı MySQL için Güvenli Yuva Katmanı (SSL) kullanarak, veritabanı sunucusu tooclient uygulamaları bağlanmayı destekler. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.

## <a name="default-settings"></a>Varsayılan ayarları
Varsayılan olarak, hello veritabanı hizmeti yapılandırılmış toorequire SSL bağlantılarını tooMySQL bağlanırken olması gerekir.  Kaçının hello SSL seçeneği mümkün olduğunca devre dışı bırakılması önerilir. 

SSL bağlantıları zorlama hello Azure portal aracılığıyla MySQL sunucusu için yeni bir Azure veritabanı ve CLI sağlanırken, varsayılan olarak etkindir. 

Benzer şekilde, SSL kullanarak yaygın diller tooconnect tooyour veritabanı sunucusu için gerekli hello parametreleri sunucunuz hello Azure portal'ın altındaki hello "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir. Merhaba SSL parametre göre hello bağlayıcı, örneğin değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.

nasıl uygulama geliştirirken tooenable veya devre dışı bırakma SSL bağlantısı başvurun çok toolearn[nasıl tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Sonraki adımlar
[MySQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
