---
title: "Azure veritabanı için MySQL için SSL bağlantısı | Microsoft Docs"
description: "Azure veritabanı MySQL ve düzgün şekilde SSL bağlantılarını kullanmak için ilişkili uygulamalar için yapılandırma için bilgiler"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="a9bc2-103">MySQL için Azure veritabanındaki SSL bağlantısı</span><span class="sxs-lookup"><span data-stu-id="a9bc2-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="a9bc2-104">MySQL için Azure veritabanı, veritabanı sunucunuzun Güvenli Yuva Katmanı (SSL) kullanarak istemci uygulamalara bağlanma destekler.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="a9bc2-105">Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "ortadaki adam" saldırılarına karşı uygulamanız ile sunucu arasındaki veri akışını şifreleyerek korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="a9bc2-106">Varsayılan ayarları</span><span class="sxs-lookup"><span data-stu-id="a9bc2-106">Default settings</span></span>
<span data-ttu-id="a9bc2-107">Varsayılan olarak, veritabanı hizmeti SSL bağlantıları için MySQL bağlanırken gerektirecek şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="a9bc2-108">Kaçının mümkün olduğunca SSL seçeneği devre dışı bırakılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="a9bc2-109">Azure portalı üzerinden MySQL sunucusu için yeni bir Azure veritabanı ve CLI sağlanırken, SSL bağlantılarını zorlama varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="a9bc2-110">Benzer şekilde, SSL kullanarak, veritabanı sunucunuza bağlanmak yaygın diller için gerekli parametreler sunucunuz Azure portalında altındaki "Bağlantı dizelerini" Ayarları'nda önceden tanımlanmış bağlantı dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="a9bc2-111">SSL parametre örneğin bağlayıcı göre değişir "ssl = true" veya "sslmode = gerektirir" veya "sslmode = gerekli" ve diğer Çeşitleme.</span><span class="sxs-lookup"><span data-stu-id="a9bc2-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="a9bc2-112">Etkinleştirme veya uygulama geliştirirken, SSL bağlantısı devre dışı bırakma hakkında bilgi edinmek için lütfen [SSL nasıl yapılandırılacağı](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a9bc2-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9bc2-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9bc2-113">Next steps</span></span>
[<span data-ttu-id="a9bc2-114">MySQL için Azure veritabanı için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="a9bc2-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
