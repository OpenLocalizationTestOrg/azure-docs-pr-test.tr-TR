---
title: "aaaCreate ve PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak Azure veritabanını yönetme | Microsoft Docs"
description: "Bu makalede nasıl toocreate ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI komut satırını kullanarak yönetebilirsiniz."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme
Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler toomanage erişim tooan Azure veritabanı PostgreSQL sunucu için belirli bir IP adresi veya IP adresleri aralığını etkinleştirin. Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silme, liste ve sunucunuzun güvenlik duvarı kuralları toomanage göster. Genel Bakış Azure veritabanı için PostgreSQL güvenlik duvarları için bkz: [PostgreSQL sunucunun güvenlik duvarı kuralları için Azure veritabanı](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Bir [PostgreSQL sunucu ve veritabanı için Azure veritabanı](quickstart-create-server-database-azure-cli.md)
- Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>PostgreSQL için Azure veritabanı için güvenlik duvarı kurallarını yapılandırma
Merhaba [az postgres sunucu güvenlik duvarı kuralı](/cli/azure/postgres/server/firewall-rule) kullanılan tooconfigure güvenlik duvarı kuralları komutlardır.

## <a name="list-firewall-rules"></a>Liste güvenlik duvarı kuralları 
Merhaba toolist varolan hello çalıştırmak hello sunucuda Sunucu güvenlik duvarı kuralları [az postgres sunucu güvenlik duvarı kuralı listesi](/cli/azure/postgres/server/firewall-rule#list) komutu.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
varsa, varsayılan değer JSON olarak biçimlendirmek istiyorsanız hello çıktı hello kuralları listeler. Merhaba anahtar kullanabilir `--output table` daha okunabilir bir tablo biçiminde hello çıktı olarak için.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Güvenlik duvarı kuralı oluşturma
toocreate hello çalıştırmak hello sunucuda yeni bir güvenlik duvarı kuralı [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu. 

Bu örnekte tüm IP adresleri tooaccess hello server çeşitli verir **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow tekil bir IP adresi tooaccess sağlamak IP başlangıç ve bitiş IP, bu örnekteki hello gibi hello aynı adres.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Başarı hello komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Bir hata olduğunda hello showserror ileti metni yerine çıktı.

## <a name="update-firewall-rule"></a>Güncelleştirme güvenlik duvarı kuralı 
Hello kullanarak sunucu üzerinde var olan bir güvenlik duvarı kuralı güncelleştirme [az postgres sunucu güvenlik duvarı kuralı güncelleştirme](/cli/azure/postgres/server/firewall-rule#update) komutu. Merhaba mevcut güvenlik duvarı kuralı giriş ve hello başlangıç IP ve bitiş IP öznitelikleri tooupdate olarak Hello adını sağlayın.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Başarı hello komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Bir hata olduğunda hello showserror ileti metni yerine çıktı.
> [!NOTE]
> Merhaba güvenlik duvarı kuralı mevcut değilse hello güncelleştirme komutu tarafından oluşturulan.

## <a name="show-firewall-rule-details"></a>Güvenlik duvarı kuralı ayrıntıları göster
Çalıştırarak bir sunucu için kural ayrıntılarını hello mevcut güvenlik duvarı gösterebilir [az postgres sunucu güvenlik duvarı kuralı Göster](/cli/azure/postgres/server/firewall-rule#show) komutu.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Başarı hello komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler. Bir hata olduğunda hello showserror ileti metni yerine çıktı.

## <a name="delete-firewall-rule"></a>Güvenlik duvarı kuralını siler
toorevoke erişim hello sunucusundan bir IP aralığı için hello yürüterek mevcut bir güvenlik duvarı kuralını silme [az postgres sunucu güvenlik duvarı kuralı silme](/cli/azure/postgres/server/firewall-rule#delete) komutu. Merhaba mevcut güvenlik duvarı kuralı Hello adını sağlayın.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Başarı hiçbir çıktısı yok. Başarısızlık durumunda, hello hata iletisi metni döndürülür.

## <a name="next-steps"></a>Sonraki adımlar
- Benzer şekilde, bir web tarayıcısı çok kullanabileceğiniz[oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme](howto-manage-firewall-using-portal.md)
- Hakkında daha iyi anlamak [Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için](concepts-firewall-rules.md)
- Tooan Azure veritabanı PostgreSQL sunucusu bağlanma konusunda yardım için bkz [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)
