---
title: "İlk Azure veritabanı için MySQL veritabanı - Azure CLI aaaDesign | Microsoft Docs"
description: "Bu öğretici açıklar nasıl toocreate Azure veritabanı için MySQL sunucusunu yönetmek ve Azure CLI 2.0 hello komut satırından kullanma veritabanı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>İlk Azure veritabanınızı MySQL veritabanı için tasarlama

Azure veritabanı için MySQL bir hello MySQL Community Edition veritabanı altyapısını temel Microsoft bulut ilişkisel veritabanı hizmetidir. Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları toolearn nasıl kullanacağınız için:

> [!div class="checklist"]
> * MySQL için Azure bir veritabanı oluşturun
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bir veritabanı
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

Hello Azure bulut Kabuk hello tarayıcıda kullanabilir veya [yükleme Azure CLI 2.0]( /cli/azure/install-azure-cli) kendi bilgisayar toorun hello kod blokları bu öğreticideki üzerinde.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin. [az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Oluşturma bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) ile [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `mycliresource` hello içinde `westus` konumu.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>MySQL için Azure Veritabanı sunucusu oluşturma
MySQL sunucusu hello az mysql server ile oluşturmak için komutu bir Azure veritabanı oluşturun. Bir sunucu birden çok veritabanını yönetebilir. Genellikle her proje veya kullanıcı için farklı bir veritabanı kullanılır.

Merhaba aşağıdaki örnek bir Azure veritabanı bulunan MySQL sunucusu için oluşturur `westus` hello kaynak grubunda `mycliresource` adla `mycliserver`. Merhaba sunucu sahip bir yönetici oturumu adlı `myadmin` ve parola `Password01!`. Merhaba sunucusu ile oluşturulur **temel** performans katmanı ve **50** hello Server'daki tüm hello veritabanları arasında paylaşılan birimler işlem. İşlem ve depolama yukarı veya aşağı hello uygulamanızın gereksinimlerine bağlı olarak ölçekleme yapabilirsiniz.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Güvenlik duvarı kuralını yapılandırma
MySQL sunucu düzeyinde güvenlik duvarı kuralı ile Merhaba az mysql server güvenlik duvarı kuralı oluşturmak için komutu bir Azure veritabanı oluşturun. Sunucu düzeyinde güvenlik duvarı kuralı gibi bir dış uygulamaya izin verir **mysql** komut satırı aracını veya MySQL çalışma ekranı tooconnect tooyour sunucu hello Azure MySQL hizmeti güvenlik duvarı üzerinden. 

Merhaba aşağıdaki örnek bir önceden tanımlanmış adres aralığı için bir güvenlik duvarı kuralı oluşturur. Bu örnek hello tüm olası IP adresleri aralığı gösterir.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Merhaba bağlantı bilgilerini alma

tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

Merhaba, JSON biçiminde sonucudur. Merhaba Not **fullyQualifiedDomainName** ve **Admınıstratorlogın**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
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

## <a name="connect-toohello-server-using-mysql"></a>MySQL kullanarak toohello sunucusuna bağlan
Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish MySQL sunucusu için bağlantı tooyour Azure veritabanı. Bu örnekte, hello komut şöyledir:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Boş veritabanı oluşturma
Bağlı toohello sunucu olduğunuzda, boş bir veritabanı oluşturun.
```sql
mysql> CREATE DATABASE mysampledb;
```

Merhaba isteminde komut tooswitch hello bağlantı toothis yeni oluşturulan veritabanı aşağıdaki hello çalıştırın:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Merhaba veritabanında tabloları oluşturma
Nasıl tooconnect toohello Azure veritabanı MySQL veritabanı için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.

İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin. Envanter bilgilerini depolayan bir tablo oluşturalım.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Merhaba tablolara veri yükleme
Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz. Merhaba açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Sorgulamak ve hello hello tablolarındaki verileri güncelleyin
Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.
```sql
SELECT * FROM inventory;
```

Ayrıca hello tablolardaki hello verileri güncelleştirebilirsiniz.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

veri aldığınızda hello satır buna göre güncelleştirilir.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Zaman içinde veritabanı tooa önceki bir noktaya geri
Bu tablo yanlışlıkla silinmiş düşünün. Bu, kolayca kurtaramazsınız şeydir. Azure veritabanı için MySQL toogo geri tooany noktası hello zamanda son too35 günleri sağlar ve zaman tooa yeni sunucu bu noktaya geri yükleme. Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz. Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.

Geri yükleme Hello için aşağıdaki bilgilerle hello gerekir:

- Geri yükleme noktası: bir noktası hello sunucu değiştirilmeden önce oluşan zamanında seçin. Büyüktür veya toohello kaynak veritabanının en eski yedekleme değerine eşit gerekir.
- Hedef sunucu: toorestore için istediğiniz yeni bir sunucu adı sağlayın
- Kaynak sunucu: Merhaba toorestore gelen istediğiniz hello sunucunun adını belirtin
- Konumu: Hello bölge seçemezsiniz, varsayılan olarak hello kaynak sunucu ile aynı.

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

toorestore hello sunucu ve [tooa noktası zaman geri](./howto-restore-server-portal.md) hello tablo silinmeden önce. Sunucu tooa farklı bir noktaya geri yükleme zamanında oluşturur yinelenen yeni bir sunucu hello özgün sunucusu olarak hello bir noktada, belirttiğiniz gibi hello saklama süresi içinde olmasını sağlanan, [hizmet katmanı](./concepts-service-tiers.md).

## <a name="next-steps"></a>Sonraki Adımlar
Bu öğreticide için öğrenilen:
> [!div class="checklist"]
> * MySQL için Azure bir veritabanı oluşturun
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bir veritabanı
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

> [!div class="nextstepaction"]
> [Azure veritabanı için MySQL - Azure CLI örnekleri](./sample-scripts-azure-cli.md)
