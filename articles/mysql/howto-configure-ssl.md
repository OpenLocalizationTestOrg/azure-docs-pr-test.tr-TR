---
title: "aaaConfigure SSL bağlantısı toosecurely tooAzure veritabanı için MySQL bağlanma | Microsoft Docs"
description: "SSL bağlantıları için nasıl tooproperly yapılandırmak Azure veritabanı MySQL ve ilişkili uygulamalar toocorrectly için yönergeleri kullanın"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="038e8-103">SSL'yi yapılandırma Bağlantısı'nda uygulama toosecurely tooAzure veritabanı için MySQL bağlanmak</span><span class="sxs-lookup"><span data-stu-id="038e8-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="038e8-104">Azure veritabanı MySQL için Güvenli Yuva Katmanı (SSL) kullanarak MySQL server tooclient uygulamaları için Azure veritabanınızı bağlanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="038e8-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="038e8-105">Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.</span><span class="sxs-lookup"><span data-stu-id="038e8-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="038e8-106">1. adım: SSL sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="038e8-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="038e8-107">Azure veritabanınızla MySQL sunucusu için SSL üzerinden Hello gerekli olan sertifika toocommunicate karşıdan [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) ve hello sertifika dosya tooyour yerel kaydedin Sürücü (Bu öğretici ile c:\ssl kullandık).</span><span class="sxs-lookup"><span data-stu-id="038e8-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="038e8-108">**Microsoft Internet Explorer ve Microsoft Edge:** hello yükleme tamamlandıktan sonra hello sertifika tooBaltimoreCyberTrustRoot.crt.pem yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="038e8-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="038e8-109">2. adım: SSL bağlama</span><span class="sxs-lookup"><span data-stu-id="038e8-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="038e8-110">SSL üzerinden Hello MySQL çalışma ekranı kullanarak tooserver bağlanma</span><span class="sxs-lookup"><span data-stu-id="038e8-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="038e8-111">MySQL çalışma ekranı tooconnect SSL üzerinden güvenli bir şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="038e8-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="038e8-112">Toohello gidin **SSL** hello MySQL çalışma ekranı hello Kurulum yeni bağlantı iletişim kutusu üzerinde sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="038e8-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="038e8-113">Merhaba Hello dosya konumu girin **BaltimoreCyberTrustRoot.crt.pem** hello içinde **SSL CA dosyasını:** alan.</span><span class="sxs-lookup"><span data-stu-id="038e8-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="038e8-114">![özelleştirilmiş döşeme Kaydet](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="038e8-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="038e8-115">SSL üzerinden Hello MySQL CLI kullanarak tooserver bağlanma</span><span class="sxs-lookup"><span data-stu-id="038e8-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="038e8-116">Merhaba MySQL komut satırı arabirimi kullanarak, hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="038e8-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="038e8-117">3. adım: Azure SSL bağlantılarını zorlama</span><span class="sxs-lookup"><span data-stu-id="038e8-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="038e8-118">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="038e8-118">Using Azure portal</span></span>
<span data-ttu-id="038e8-119">Hello Azure portal kullanarak Azure veritabanınız için MySQL server ve tıklatın ziyaret **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="038e8-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="038e8-120">Merhaba iki durumlu düğme tooenable kullanın veya hello devre dışı bırakma **Zorla SSL bağlantısı** ayarı.</span><span class="sxs-lookup"><span data-stu-id="038e8-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="038e8-121">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="038e8-121">Then click **Save**.</span></span> <span data-ttu-id="038e8-122">Microsoft önerir tooalways etkinleştirmek **Zorla SSL bağlantısı** için Gelişmiş güvenlik ayarı.</span><span class="sxs-lookup"><span data-stu-id="038e8-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="038e8-123">![Enable ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="038e8-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="038e8-124">Azure CLI’yı kullanma</span><span class="sxs-lookup"><span data-stu-id="038e8-124">Using Azure CLI</span></span>
<span data-ttu-id="038e8-125">Etkinleştirmek veya devre dışı hello **ssl zorlama** etkin veya devre dışı değerleri sırasıyla Azure CLI kullanarak parametre.</span><span class="sxs-lookup"><span data-stu-id="038e8-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="038e8-126">Adım 4: SSL bağlantısı doğrulama</span><span class="sxs-lookup"><span data-stu-id="038e8-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="038e8-127">Merhaba mysql yürütme **durum** SSL kullanarak tooyour MySQL server bağlı komutu tooverify:</span><span class="sxs-lookup"><span data-stu-id="038e8-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="038e8-128">Merhaba bağlantı hello çıkış gözden geçirerek şifrelenir onaylayın.</span><span class="sxs-lookup"><span data-stu-id="038e8-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="038e8-129">Göstermesi gerekir: **SSL: şifre kullanımda olan AES256 SHA**</span><span class="sxs-lookup"><span data-stu-id="038e8-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="038e8-130">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="038e8-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="038e8-131">PHP</span><span class="sxs-lookup"><span data-stu-id="038e8-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="038e8-132">Python</span><span class="sxs-lookup"><span data-stu-id="038e8-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="038e8-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="038e8-133">Next steps</span></span>
<span data-ttu-id="038e8-134">Aşağıdaki çeşitli uygulama bağlantı seçenekleri gözden [Azure veritabanı için MySQL için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="038e8-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
