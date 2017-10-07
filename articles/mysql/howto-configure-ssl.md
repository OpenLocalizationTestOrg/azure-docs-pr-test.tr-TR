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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>SSL'yi yapılandırma Bağlantısı'nda uygulama toosecurely tooAzure veritabanı için MySQL bağlanmak
Azure veritabanı MySQL için Güvenli Yuva Katmanı (SSL) kullanarak MySQL server tooclient uygulamaları için Azure veritabanınızı bağlanmayı destekler. Veritabanı sunucunuz ve istemci uygulamalarınız arasında SSL bağlantılarını zorlamayı "Merhaba ortadaki adam" saldırılarına karşı hello veri akışı hello sunucusu ve uygulamanız arasındaki şifreleyerek korunmasına yardımcı.

## <a name="step-1-obtain-ssl-certificate"></a>1. adım: SSL sertifikası alın
Azure veritabanınızla MySQL sunucusu için SSL üzerinden Hello gerekli olan sertifika toocommunicate karşıdan [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) ve hello sertifika dosya tooyour yerel kaydedin Sürücü (Bu öğretici ile c:\ssl kullandık).
**Microsoft Internet Explorer ve Microsoft Edge:** hello yükleme tamamlandıktan sonra hello sertifika tooBaltimoreCyberTrustRoot.crt.pem yeniden adlandırın.

## <a name="step-2-bind-ssl"></a>2. adım: SSL bağlama
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>SSL üzerinden Hello MySQL çalışma ekranı kullanarak tooserver bağlanma
MySQL çalışma ekranı tooconnect SSL üzerinden güvenli bir şekilde yapılandırın. Toohello gidin **SSL** hello MySQL çalışma ekranı hello Kurulum yeni bağlantı iletişim kutusu üzerinde sekmesindedir. Merhaba Hello dosya konumu girin **BaltimoreCyberTrustRoot.crt.pem** hello içinde **SSL CA dosyasını:** alan.
![özelleştirilmiş döşeme Kaydet](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>SSL üzerinden Hello MySQL CLI kullanarak tooserver bağlanma
Merhaba MySQL komut satırı arabirimi kullanarak, hello aşağıdaki komutu yürütün:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>3. adım: Azure SSL bağlantılarını zorlama 
### <a name="using-azure-portal"></a>Azure portalını kullanma
Hello Azure portal kullanarak Azure veritabanınız için MySQL server ve tıklatın ziyaret **bağlantı güvenliği**. Merhaba iki durumlu düğme tooenable kullanın veya hello devre dışı bırakma **Zorla SSL bağlantısı** ayarı. Daha sonra **Kaydet**'e tıklayın. Microsoft önerir tooalways etkinleştirmek **Zorla SSL bağlantısı** için Gelişmiş güvenlik ayarı.
![Enable ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Azure CLI’yı kullanma
Etkinleştirmek veya devre dışı hello **ssl zorlama** etkin veya devre dışı değerleri sırasıyla Azure CLI kullanarak parametre.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Adım 4: SSL bağlantısı doğrulama
Merhaba mysql yürütme **durum** SSL kullanarak tooyour MySQL server bağlı komutu tooverify:
```dos
mysql> status
```
Merhaba bağlantı hello çıkış gözden geçirerek şifrelenir onaylayın. Göstermesi gerekir: **SSL: şifre kullanımda olan AES256 SHA** 

## <a name="sample-code"></a>Örnek kod
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki çeşitli uygulama bağlantı seçenekleri gözden [Azure veritabanı için MySQL için bağlantı kitaplıkları](concepts-connection-libraries.md)
