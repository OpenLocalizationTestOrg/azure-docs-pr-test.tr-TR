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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="9d9d1-103">MySQL için Azure veritabanındaki SSL bağlantısı</span><span class="sxs-lookup"><span data-stu-id="9d9d1-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="9d9d1-104">Azure veritabanı MySQL için Güvenli Yuva Katmanı (SSL) kullanarak, veritabanı sunucusu tooclient uygulamaları bağlanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="9d9d1-105">Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="9d9d1-106">Varsayılan ayarları</span><span class="sxs-lookup"><span data-stu-id="9d9d1-106">Default settings</span></span>
<span data-ttu-id="9d9d1-107">Varsayılan olarak, hello veritabanı hizmeti yapılandırılmış toorequire SSL bağlantılarını tooMySQL bağlanırken olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="9d9d1-108">Kaçının hello SSL seçeneği mümkün olduğunca devre dışı bırakılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="9d9d1-109">SSL bağlantıları zorlama hello Azure portal aracılığıyla MySQL sunucusu için yeni bir Azure veritabanı ve CLI sağlanırken, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="9d9d1-110">Benzer şekilde, SSL kullanarak yaygın diller tooconnect tooyour veritabanı sunucusu için gerekli hello parametreleri sunucunuz hello Azure portal'ın altındaki hello "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="9d9d1-111">Merhaba SSL parametre göre hello bağlayıcı, örneğin değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="9d9d1-112">nasıl uygulama geliştirirken tooenable veya devre dışı bırakma SSL bağlantısı başvurun çok toolearn[nasıl tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9d9d1-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d9d1-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d9d1-113">Next steps</span></span>
[<span data-ttu-id="9d9d1-114">MySQL için Azure veritabanı için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9d9d1-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
