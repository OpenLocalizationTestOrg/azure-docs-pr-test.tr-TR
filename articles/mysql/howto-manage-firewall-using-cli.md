---
title: "aaaCreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme | Microsoft Docs"
description: "Bu makalede nasıl toocreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI komut satırını kullanarak yönetebilirsiniz."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme
MySQL sunucusu için belirli bir IP adresi veya IP adresi aralığı Yöneticiler toomanage erişim tooan Azure veritabanı sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin. Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silme, liste ve sunucunuzun güvenlik duvarı kuralları toomanage göster. Genel Bakış Azure veritabanı için MySQL güvenlik duvarları için bkz: [Azure veritabanı için MySQL server güvenlik duvarı kuralları](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Ön koşullar
* [Azure CLI 2.0 yükleyin](https://docs.microsoft.com/cli/azure/install-azure-cli)
* PostgreSQL ve MySQL Hizmetleri için Azure Python SDK yükleme
* Hello Azure CLI bileşeni PostgreSQL ve MySQL hizmeti yükleyin
* MySQL için Azure Veritabanı sunucusu oluşturma

## <a name="firewall-rule-commands"></a>Güvenlik duvarı kuralı komutlar:
Merhaba **az mysql server güvenlik duvarı kuralı** komutu, Azure CLI toocreate kullanıldığında, silme, listesinde, Göster ve güvenlik duvarı kurallarını güncelleştir.

Komutlar:
- **oluşturma**: bir Azure MySQL server güvenlik duvarı kuralı oluşturun.
- **silme**: Azure MySQL server güvenlik duvarı kuralını siler.
- **Liste** : hello Azure MySQL server güvenlik duvarı kuralları listesi.
- **Göster** : güvenlik duvarı kuralı Azure MySQL server hello ayrıntılarını gösterin.
- **Güncelleştirme**: bir Azure MySQL server güvenlik duvarı kuralı güncelleştirin.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>Oturum açma tooAzure ve MySQL sunucuları için Azure veritabanınızı listesi
Güvenli bir şekilde Azure CLI ile Azure hesabınıza bağlanın. Kullanım hello **az oturum açma** toodo bu komutu.

1. Komut hello komut satırından aşağıdaki hello çalıştırın.
```azurecli
az login
```
Bu komut, bir kod toouse hello sonraki adımda çıkarır.

2. Bir web tarayıcısı tooopen hello sayfası kullanmak [https://aka.ms/devicelogin](https://aka.ms/devicelogin) ve hello kodu girin.

3. Merhaba isteminde Azure kimlik bilgilerinizi kullanarak oturum açın.

4. Oturumunuzla yetkilendirildikten sonra Aboneliklerin listesini hello konsolunda basılır. İlerleyen kullanılan istenen hello abonelik tooset hello geçerli abonelik toobe Hello kimliğini kopyalayın.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Merhaba adlarını değilseniz hello Azure veritabanları MySQL sunucuları abonelik ve kaynak grubunuz için listeleyin.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Kullanılan toospecify olacağı hello adı özniteliği listeleme hello hangi MySQL server toowork unutmayın. Bu sunucu toousing hello adı özniteliği tooconfirm adının doğru olduğundan için gerekirse, hello ayrıntılarınızı doğrulayın:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralları listesi 
Hello sunucu adını ve hello kaynak grubu adı, liste hello var olan sunucu güvenlik duvarı kuralları hello sunucuda kullanma. Bu hello sunucu adı özniteliği hello belirtilen dikkat edin **--server** geçin ve değil hello **--ad** geçin.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
varsa, varsayılan değer JSON olarak biçimlendirmek istiyorsanız hello çıktı hello kuralları listeler. Merhaba anahtar kullanabilir **--çıktı tablosu** daha okunabilir bir tablo biçiminde hello çıktı olarak için.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Güvenlik duvarı kuralı Azure veritabanı için MySQL sunucusu oluşturun.
Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, hello sunucusunda yeni bir güvenlik duvarı kuralı oluşturun. Merhaba kural toocover bir dizi IP adreslerini tooallow erişim hello kuralı, hello başlangıç IP ve bitiş IP için bir ad sağlayın.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Erişime izin toobe için tekil bir IP adresi, sağlayın IP başlangıç ve bitiş IP, bu örnekteki hello gibi hello aynı adres.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Başarı hello komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı güncelleştirme güvenlik duvarı kuralı 
Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı hello sunucuda güncelleştirin. Merhaba mevcut güvenlik duvarı kuralı giriş ve hello başlangıç IP ve bitiş IP öznitelikleri tooupdate olarak Hello adını sağlayın.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Başarı hello komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.

> [!NOTE]
> Merhaba güvenlik duvarı kuralı mevcut değilse hello güncelleştirme komutu tarafından oluşturulur.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanında güvenlik duvarı kuralı ayrıntıları göster
Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, hello mevcut güvenlik duvarı kuralı bilgileri hello sunucusundan gösterir. Merhaba mevcut güvenlik duvarı kuralı Hello adını girdi olarak sağlayın.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Başarı hello komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralını siler
Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı hello sunucudan kaldırın. Merhaba mevcut güvenlik duvarı kuralı Hello adını sağlayın.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Başarı hiçbir çıktısı yok. Başarısızlık durumunda, hello hata iletisi metni döndürülür.

## <a name="next-steps"></a>Sonraki adımlar
- Hakkında daha iyi anlamak [Azure veritabanı için MySQL Server güvenlik duvarı kuralları](./concepts-firewall-rules.md)
- [Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme](./howto-manage-firewall-using-portal.md)
