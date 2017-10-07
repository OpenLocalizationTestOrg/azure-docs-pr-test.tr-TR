---
title: "Hızlı Başlangıç: MySQL için Azure Veritabanı sunucusu Oluşturma - Azure CLI | Microsoft Docs"
description: "Bu hızlı başlangıç nasıl toouse hello Azure CLI toocreate bir Azure kaynak grubu içindeki MySQL sunucusu için bir Azure veritabanı açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Azure CLI aracını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma
Bu hızlı başlangıç nasıl toouse hello Azure CLI toocreate bir Azure kaynak grubu içindeki MySQL sunucusu için bir Azure veritabanı yaklaşık beş dakika içinde açıklar. Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin. [az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Oluşturma bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) hello kullanarak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myresourcegroup` hello içinde `westus` konumu.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>MySQL için Azure Veritabanı sunucusu oluşturma
MySQL sunucusu için bir Azure veritabanı ile Merhaba oluşturma **az mysql sunucusu oluşturun** komutu. Bir sunucu birden çok veritabanını yönetebilir. Genellikle her proje veya kullanıcı için farklı bir veritabanı kullanılır.

Merhaba aşağıdaki örnek bir Azure veritabanı bulunan MySQL sunucusu için oluşturur `westus` hello kaynak grubunda `myresourcegroup` adla `myserver4demo`. Merhaba sunucu sahip bir yönetici oturumu adlı `myadmin` ve parola `Password01!`. Merhaba sunucusu ile oluşturulur **temel** performans katmanı ve **50** hello Server'daki tüm hello veritabanları arasında paylaşılan birimler işlem. İşlem ve depolama yukarı veya aşağı hello uygulamanızın gereksinimlerine bağlı olarak ölçekleme yapabilirsiniz.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Güvenlik duvarı kuralını yapılandırma
Hello kullanarak MySQL sunucu düzeyinde güvenlik duvarı kuralı için bir Azure veritabanı oluştur **az mysql server güvenlik duvarı kuralı oluşturmak** komutu. Sunucu düzeyinde güvenlik duvarı kuralı hello gibi bir dış uygulamaya verir **mysql.exe** komut satırı aracını veya MySQL çalışma ekranı tooconnect tooyour sunucu hello Azure MySQL hizmeti güvenlik duvarı üzerinden. 

Merhaba aşağıdaki örnek, bu örnekte hello tüm olası IP adres aralığı olan önceden tanımlanmış adres aralığı için bir güvenlik duvarı kuralı oluşturur.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>SSL ayarlarını yapılandırma
Varsayılan olarak sunucunuz ile istemci uygulamaları arasında SSL bağlantıları zorunlu tutulur.  Bu "hareket halinde" güvenliğini sağlar hello Internet üzerinden hello veri akışı şifreleme verileri.  Bu hızlı başlangıç daha kolay toomake, biz SSL bağlantıları için sunucunuzu devre dışı bırakın.  Üretim sunucuları için bunu yapmanız önerilmez.  Daha fazla bilgi için bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md).

Merhaba aşağıdaki örnek, MySQL server zorunlu SSL devre dışı bırakır.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Merhaba bağlantı bilgilerini alma

tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Merhaba, JSON biçiminde sonucudur. Merhaba Not **fullyQualifiedDomainName** ve **Admınıstratorlogın**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Merhaba mysql.exe komut satırı aracını kullanarak toohello sunucuya bağlanın
Hello kullanarak tooyour sunucusuna **mysql.exe** komut satırı aracı. MySQL'i [buradan](https://dev.mysql.com/downloads/) indirerek bilgisayarınıza yükleyebilirsiniz. Bunun yerine, ayrıca hello tıklatarak **deneyin** düğmesini kod örnekleri üzerinde veya hello `>_` hello üst sağ araç hello Azure portal ve başlatma hello düğmesinden **Azure bulut Kabuk**.

Merhaba sonraki komutları yazın: 

1. Sunucu toohello kullanarak bağlan **mysql** komut satırı aracı:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Sunucu durumunu görüntüleyin:
```sql
 mysql> status
```
Her şey yolunda giderse hello komut satırı aracı metin aşağıdaki hello çıkış:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Ek komutlar için bkz. [MySQL 5.7 Başvuru Kılavuzu - Bölüm 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Merhaba MySQL çalışma ekranı GUI aracını kullanarak toohello sunucuya bağlanın
1.  Merhaba, istemci bilgisayardaki MySQL çalışma ekranı uygulaması başlatın. MySQL Workbench uygulamasını [buradan](https://dev.mysql.com/downloads/workbench/) indirip yükleyebilirsiniz.

2.  Merhaba, **yeni bağlantı kurma** iletişim kutusunda, aşağıdaki bilgilerle hello girin **parametreleri** sekmesi:

   ![yeni bağlantı oluştur](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Ayar** | **Önerilen Değer** | **Açıklama** |
|---|---|---|
|   Bağlantı Adı | Bağlantım | Bu bağlantı için bir etiket belirtin (herhangi bir şey olabilir) |
| Bağlantı Yöntemi | Standart (TCP/IP) seçeneğini belirleyin | TCP/IP Protokolü tooconnect tooAzure veritabanı için MySQL kullanmak > |
| Ana Bilgisayar Adı | myserver4demo.mysql.database.azure.com | Daha önce not aldığınız sunucu adı. |
| Bağlantı noktası | 3306 | MySQL için Hello varsayılan bağlantı noktası kullanılır. |
| Kullanıcı adı | myadmin@myserver4demo | Merhaba Sunucu Yöneticisi oturum açma, daha önce not ettiğiniz. |
| Parola | **** | Daha önce yapılandırılmış hello yönetici hesabı parolasını kullanın. |

Tıklatın **Bağlantıyı Sına** tüm parametrelerin doğru yapılandırılmışsa tootest.
Artık, hello bağlantıyı tıklatabilir toosuccessfully toohello sunucusuna bağlanın.

## <a name="clean-up-resources"></a>Kaynakları temizleme
Başka bir hızlı başlangıç/öğretici için bu kaynakları gerek duymuyorsanız, komutu aşağıdaki hello yaparak silebilirsiniz: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Azure CLI ile bir MySQL Veritabanı tasarlama](./tutorial-design-database-using-cli.md)
