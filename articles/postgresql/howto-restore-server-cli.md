---
title: "Nasıl tooback ayarlama ve Azure veritabanındaki bir sunucu için PostgreSQL geri | Microsoft Docs"
description: "Azure CLI tooback yukarı ve kullanarak Azure veritabanındaki bir sunucu için geri PostgreSQL nasıl hello öğrenin."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Azure CLI tooback yukarı ve kullanarak Azure veritabanındaki bir sunucu için geri PostgreSQL nasıl hello

Azure veritabanı sunucusu veritabanı tooan PostgreSQL toorestore için 7 too35 günden yayılan önceki tarih kullanın.

## <a name="prerequisites"></a>Ön koşullar
toocomplete bu nasıl-tooguide, gerekir:
- Bir [PostgreSQL sunucu ve veritabanı için Azure veritabanı](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Yükleme ve yerel olarak hello Azure CLI kullanıyorsanız, bu nasıl tooguide Azure CLI Sürüm 2.0 veya üstü kullanmanızı gerektirir. hello Azure CLI komut isteminde tooconfirm hello sürümü girin `az --version`. bkz: tooinstall veya yükseltme, [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>Yedekleme otomatik olarak gerçekleşir
Azure veritabanı için PostgreSQL kullandığınızda, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar. 

Temel katman için hello yedeklemeler 7 gün için kullanılabilir. Standart katmanı için hello yedeklemeleri 35 gün için kullanılabilir. Daha fazla bilgi için bkz: [Azure veritabanı fiyatlandırma katmanlarına PostgreSQL için](concepts-service-tiers.md).

Bu otomatik yedekleme özelliği ile Merhaba sunucusu ve onun veritabanları tooan önceki tarih geri yükleyin veya zaman.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Bir veritabanı tooa önceki süre hello Azure CLI kullanarak geri yükleme noktası
PostgreSQL toorestore hello sunucu tooa önceki bir noktaya için Azure Database kullanın. geri hello veri kopyalanan tooa yeni sunucu ve hello var olan sunucu olduğu gibi bırakılır. Örneğin, bir tablo bugün öğlen yanlışlıkla kesilirse toohello zaman öğlen hemen önce geri yükleyebilirsiniz. Ardından, tablo ve hello server geri hello kopyasını verilerinden eksik hello alabilir. 

toorestore hello sunucu, kullanım hello Azure CLI [az postgres server geri](/cli/azure/postgres/server#restore) komutu.

### <a name="run-hello-restore-command"></a>Merhaba geri yükleme komutunu çalıştırın

hello Azure CLI komut isteminde toorestore hello sunucusu hello aşağıdaki komutu girin:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Merhaba `az postgres server restore` komutu şu parametreler hello gerektirir:
| Ayar | Önerilen değer | Açıklama  |
| --- | --- | --- |
| kaynak grubu |  myResourceGroup |  Merhaba kaynak sunucunun bulunduğu kaynak grubu.  |
| ad | mypgserver geri | Merhaba geri yükleme komutu tarafından oluşturulan yeni bir sunucu hello Hello adı. |
| zaman içinde geri yükleme noktası | 2017-04-13T13:59:00Z | Zaman toorestore bir nokta seçin. Bu tarih ve saat hello kaynak sunucunun yedekleme saklama dönemi içinde olmalıdır. Merhaba ISO8601 tarih ve saat biçimini kullanın. Örneğin, kendi yerel saat dilimi gibi kullanabilir `2017-04-13T05:59:00-08:00`. Örneğin, UTC Zulu dili biçiminde hello de kullanabilirsiniz `2017-04-13T13:59:00Z`. |
| Kaynak sunucusu | mypgserver 20170401 | Merhaba adı veya hello kaynak sunucu toorestore kimliği. |

Bir sunucu tooan geri önceki bir noktaya, yeni bir sunucu oluşturulur. Merhaba özgün sunucusu ve onun hello veritabanlarından zaman içinde nokta kopyalanan toohello yeni sunucu belirtilir.

geri hello sunucu kalması için hello konum ve fiyatlandırma katmanı değerlerini aynı hello özgün sunucusu olarak hello. 

Merhaba `az postgres server restore` komut zaman uyumlu olur. Merhaba server geri yüklendikten sonra onu yeniden toorepeat hello işlemi için farklı bir noktaya zamanında kullanabilirsiniz. 

Merhaba sonra geri yükleme işlemi tamamlandığında, hello yeni sunucu bulun ve hello veri beklendiği gibi geri yüklendiğini doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar
[Azure veritabanı PostgreSQL için için bağlantı kitaplıkları](concepts-connection-libraries.md)
