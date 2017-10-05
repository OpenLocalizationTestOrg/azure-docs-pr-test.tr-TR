---
title: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme | Microsoft Docs"
description: "Bu makalede, oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI komut satırını kullanarak yönetme açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme
Azure veritabanı için MySQL sunucusu için belirli bir IP adresi veya IP adresi aralığı erişimi yönetmek üzere yöneticiler sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin. Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silin, listeleyin ve sunucunuzu yönetmek için güvenlik duvarı kuralları gösterir. Genel Bakış Azure veritabanı için MySQL güvenlik duvarları için bkz: [Azure veritabanı için MySQL server güvenlik duvarı kuralları](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Ön koşullar
* [Azure CLI 2.0 yükleyin](https://docs.microsoft.com/cli/azure/install-azure-cli)
* PostgreSQL ve MySQL Hizmetleri için Azure Python SDK yükleme
* Azure CLI bileşeni PostgreSQL ve MySQL hizmeti yükleyin
* MySQL için Azure Veritabanı sunucusu oluşturma

## <a name="firewall-rule-commands"></a>Güvenlik duvarı kuralı komutlar:
**Az mysql server güvenlik duvarı kuralı** komut oluşturma, silme, liste, Göster ve güvenlik duvarı kurallarını güncelleştir için Azure CLI üzerinden kullanılır.

Komutlar:
- **oluşturma**: bir Azure MySQL server güvenlik duvarı kuralı oluşturun.
- **silme**: Azure MySQL server güvenlik duvarı kuralını siler.
- **Liste** : Azure MySQL server güvenlik duvarı kuralları listesi.
- **Göster** : güvenlik duvarı kuralı Azure MySQL server ayrıntılarını gösterin.
- **Güncelleştirme**: bir Azure MySQL server güvenlik duvarı kuralı güncelleştirin.

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a>Azure ve listesine Azure veritabanınızı MySQL sunucuları için oturum açma
Güvenli bir şekilde Azure CLI ile Azure hesabınıza bağlanın. Kullanım **az oturum açma** Bunu yapmak için komutu.

1. Komut satırından aşağıdaki komutu çalıştırın.
```azurecli
az login
```
Bu komutun çıkışı, sonraki adımda kullanılacak bir kod olacaktır.

2. Web tarayıcısı kullanarak [https://aka.ms/devicelogin](https://aka.ms/devicelogin) adresine gidin ve kodu girin.

3. İstendiğinde, Azure kimlik bilgilerinizi kullanarak oturum açın.

4. Oturumunuzla yetkilendirildikten sonra konsolda Aboneliklerin listesini basılır. İleri taşıma kullanılacak şu anki aboneliği ayarlamak için istenen abonelik kimliğini kopyalayın.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Adlarını değilseniz MySQL sunucuları abonelik ve kaynak grubunuz için Azure veritabanlarını listeler.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Üzerinde çalışmak için MySQL sunucuyu belirtmek için kullanılan listenin adı özniteliği unutmayın. Gerekirse, adının doğru olduğunu doğrulamak için name özniteliği kullanarak bu sunucu için ayrıntıları onaylayın:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralları listesi 
Sunucu adı ve kaynak grubu adı kullanarak, sunucu üzerinde var olan sunucunun güvenlik duvarı kuralları listesi. Sunucu adı özniteliği belirtilen bildirimi **--sunucu** geçiş ve **--adı** geçin.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
Çıktı varsa JSON biçiminde varsayılan kuralları listeler. Anahtar kullanabilir **--çıktı tablosu** çıktı olarak daha okunabilir bir tablo biçiminde için.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Güvenlik duvarı kuralı Azure veritabanı için MySQL sunucusu oluşturun.
Azure MySQL sunucu adını ve kaynak grubu adı kullanarak, sunucu üzerinde yeni bir güvenlik duvarı kuralı oluşturun. Kural, başlangıç IP ve bir IP adresi aralığı kapsayacak şekilde bitiş IP kuralı için erişimine izin vermek için bir ad sağlayın.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Erişim izin verilmesi tekil için bir IP adresi, bu örnekte olduğu gibi IP başlangıç ve bitiş IP aynı adresi belirtin.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Başarılı, komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz güvenlik duvarı kuralı ayrıntılarını listeler. Çıkış hatası varsa, hata iletisi metni yerine gösterir.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı güncelleştirme güvenlik duvarı kuralı 
Azure MySQL sunucu adı ve kaynak grubu adı kullanarak, sunucuda mevcut bir güvenlik duvarı kuralı güncelleştirin. Var olan güvenlik duvarı kuralı adı girişi ve başlangıç güncelleştirmek için IP ve bitiş IP öznitelikleri sağlar.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Başarılı, komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz güvenlik duvarı kuralı ayrıntılarını listeler. Çıkış hatası varsa, hata iletisi metni yerine gösterir.

> [!NOTE]
> Güvenlik duvarı kuralı mevcut değilse güncelleştirme komutu tarafından oluşturulur.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanında güvenlik duvarı kuralı ayrıntıları göster
Azure MySQL sunucu adını ve kaynak grubu adı kullanarak, var olan Güvenlik Duvarı'nı sunucudan kural ayrıntılarını gösterir. Var olan güvenlik duvarı kuralının adını girdi olarak sağlayın.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Başarılı, komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz güvenlik duvarı kuralı ayrıntılarını listeler. Çıkış hatası varsa, hata iletisi metni yerine gösterir.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralını siler
Azure MySQL sunucu adı ve kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı sunucudan kaldırın. Var olan güvenlik duvarı kuralının adını sağlayın.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Başarı hiçbir çıktısı yok. Başarısızlık durumunda, hata iletisi metni döndürülür.

## <a name="next-steps"></a>Sonraki adımlar
- Hakkında daha iyi anlamak [Azure veritabanı için MySQL Server güvenlik duvarı kuralları](./concepts-firewall-rules.md)
- [Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure Portalı'nı kullanarak yönetme](./howto-manage-firewall-using-portal.md)
