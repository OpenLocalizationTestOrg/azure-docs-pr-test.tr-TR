---
title: "Azure bulut Kabuğu (Önizleme) aaaPersist dosyaları | Microsoft Docs"
description: "Azure bulut Kabuk dosyaları nasıl devam ederse gözden geçirme."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Azure bulut Kabuk dosyalarında Sürdür
Bulut Kabuk oturumlarında Azure dosya depolama toopersist dosyaları yararlanır.

## <a name="set-up-a-clouddrive-file-share"></a>Ayarlanmış bir `clouddrive` dosya paylaşımı
Bulut Kabuk ilk Başlat, yeni veya varolan bir dosya paylaşımı toopersist dosyalardaki oturumları tooassociate ister.

### <a name="create-new-storage"></a>Yeni depolama alanı oluşturma

Temel ayarlar kullanın ve yalnızca bir abonelik seçin, bulut Kabuk üç kaynakları tooyou en yakın olan desteklenen hello bölgede sizin adınıza oluşturur:
* Kaynak grubu:`cloud-shell-storage-<region>`
* Depolama hesabı:`cs<uniqueGuid>`
* Dosya Paylaşımı:`cs-<user>-<domain>-com-<uniqueGuid>`

![Merhaba abonelik ayarı](media/basic-storage.png)

Merhaba dosya paylaşımı bağladığı olarak `clouddrive` içinde `$Home` dizin. Merhaba dosya paylaşımının ayrıca ve, otomatik olarak oluşturulan bir 5 GB görüntüsü güncelleştirir ve devam ederse kullanılan toostore olduğundan, `$Home` dizin. Bu tek seferlik bir işlemdir ve sonraki oturumlarda hello dosya paylaşımına otomatik olarak bağlar.

### <a name="use-existing-resources"></a>Var olan kaynakları kullanın

Gelişmiş seçeneği hello kullanarak, var olan kaynakların ilişkilendirebilirsiniz. Merhaba depolama Kurulum istemi belirdiğinde seçin **Göster Gelişmiş ayarları** tooview ek seçenekler. Var olan dosya paylaşımları alma 5 GB kullanıcı görüntü toopersist, `$Home` dizin. Merhaba aşağı açılır menüler yerel olarak yedekli & coğrafi olarak yedekli depolama hesapları ve bulut Kabuk bölgeniz için filtrelenir.

![Kaynak grubu ayarını hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Bir Azure kaynak İlkesi ile kaynak oluşturma kısıtla
Bulut Kabuğu'nda oluşturduğunuz depolama hesapları ile etiketlenmiş `ms-resource-usage:azure-cloud-shell`. Toodisallow kullanıcıların bulut Kabuğu'nda depolama hesapları oluşturmak istiyorsanız, oluşturma bir [etiketleri için Azure kaynak İlkesi](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) bu belirli etiketi tarafından tetiklenir.

## <a name="how-cloud-shell-works"></a>Bulut Kabuk nasıl çalışır?
Bulut kabuk dosyalar yöntemler aşağıdaki hello her ikisi de ile devam eder:
* Bir disk görüntüsünü oluşturma, `$Home` directory toopersist tüm içeriği hello dizini içinde. Merhaba disk görüntüsü belirtilen dosya paylaşımınıza kaydedildi `acc_<User>.img` adresindeki `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, ve değişiklikleri otomatik olarak eşitlenir.

* Belirtilen dosya paylaşımı olarak takma `clouddrive` içinde `$Home` doğrudan dosya paylaşımı etkileşim için dizin. `/Home/<User>/clouddrive`çok eşlenen`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Tüm dosyaları, `$Home` SSH anahtarları gibi dizini, bağlı dosya paylaşımında depolanan, kullanıcı disk görüntüsü kaldı. Bilgileri kalıcı sırasında en iyi yöntemleri uygulamak, `$Home` dizin ve bağlı dosya paylaşımı.

## <a name="use-hello-clouddrive-command"></a>Kullanım hello `clouddrive` komutu
Bulut kabuğunda denilen bir komut çalıştırabilirsiniz `clouddrive`, hangi, toomanually güncelleştirme hello dosya paylaşımı o takılı tooCloud Kabuk etkinleştirir.
![Merhaba "clouddrive" komutunu çalıştırarak](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Yeni bir bağlama`clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>El ile bağlama için Önkoşullar
Hello kullanarak bulut kabuğu ile ilişkili hello dosya paylaşımı güncelleştirebilirsiniz `clouddrive mount` komutu.

Varolan bir dosya paylaşımını bağlama hello depolama hesapları olması gerekir:
* Yerel olarak yedekli depolama veya coğrafi olarak yedekli depolama toosupport dosya paylaşımları.
* Atanan bölgenizde bulunur. Merhaba bölge ekleme olduğunda hello kaynak grubu adı içinde listelenen toois atanan `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Desteklenen depolama bölgeleri
Hello Azure dosyaları hello aynı bulunmalıdır bölge onlara bağlanması hello bulut Kabuk makine olarak. Bulut Kabuk kümeleri şu anda bölgeleri aşağıdaki hello mevcuttur:
|Alan|Bölge|
|---|---|
|Kuzey ve Güney Amerika|Doğu ABD, Orta Güney ABD, Batı ABD|
|Avrupa|Kuzey Avrupa, Batı Avrupa|
|Asya Pasifik|Hindistan Orta, Güneydoğu Asya|

### <a name="hello-clouddrive-mount-command"></a>Merhaba `clouddrive mount` komutu

> [!NOTE]
> Yeni bir dosya paylaşımı takma varsa, yeni bir kullanıcı görüntüsü için oluşturulur, `$Home` dizin, çünkü, önceki `$Home` görüntü hello önceki dosya paylaşımında tutulur.

Merhaba çalıştırmak `clouddrive mount` şu parametreler hello komutunu:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

Daha fazla ayrıntı tooview çalıştırın `clouddrive mount -h`, aşağıda gösterildiği gibi:

![Çalışan hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Çıkarın`clouddrive`
Bu bağlı tooCloud Kabuk dilediğiniz zaman bir dosya paylaşımı çıkarın. Dosya paylaşımınızı kaldırılan olduktan sonra bir sonraki oturumu istendiğinde toomount yeni bir dosya paylaşımı önceki tooyour olacaktır.

Bulut Kabuğu'ndan tooremove bir dosya paylaşımı:
1. `clouddrive unmount` öğesini çalıştırın.
2. Onayla ve hello istemleri onaylayın.

El ile silmeniz sürece dosya paylaşımınıza tooexist devam eder. Bulut Kabuk, artık bu dosya paylaşımı için sonraki oturumlarda arar.

Daha fazla ayrıntı tooview çalıştırın `clouddrive unmount -h`, aşağıda gösterildiği gibi:

![Çalışan hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> Bu komutu çalıştıran herhangi bir kaynağa silmez. El ile bir kaynak grubu, depolama hesabı veya dosya paylaşımı siliniyor eşlenen Kabuk kalıcı olarak silinecek tooCloud, `$Home` directory görüntü ve herhangi bir dosya paylaşımı dosyalarında. Bu eylem geri alınamaz.

## <a name="list-clouddrive-file-shares"></a>Liste `clouddrive` dosya paylaşımları
hangi dosya paylaşımı bağlı olarak toodiscover `clouddrive`, hello aşağıdaki komutu çalıştırarak `df` komutu. 

Merhaba dosya yolu tooclouddrive hello URL'de, depolama hesabı adı ve dosya paylaşımı gösterir. Örneğin, `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Aktarım yerel dosyaları tooCloud Kabuk
Merhaba `clouddrive` dizin eşitlemeler hello Azure portal depolama dikey ile. Bu dikey tootransfer yerel dosyaları tooor dosya paylaşımından kullanın. Merhaba dikey yenilediğinizde bulut Kabuk içinde dosyalar hello dosya depolama GUI yansıtılır.

### <a name="download-files"></a>Dosyaları indirme

![Yerel dosya listesi](media/download.png)
1. Hello Azure portal, toohello bağlı dosya paylaşımına gidin.
2. Merhaba hedef dosya seçin.
3. Select hello **karşıdan** düğmesi.

### <a name="upload-files"></a>Dosyaları karşıya yükleme

![Yerel dosya toobe karşıya](media/upload.png)
1. Tooyour bağlı dosya paylaşımına gidin.
2. Select hello **karşıya** düğmesi.
3. Merhaba dosya veya tooupload istediğiniz dosyaları seçin.
4. Merhaba karşıya yükleme onaylayın.

Erişilebilen hello dosyaların görmelisiniz, `clouddrive` bulut Kabuğu'nda dizin.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut Kabuk hızlı başlangıç](quickstart.md) <br>
[Azure File storage hakkında bilgi edinin](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Depolama etiketler hakkında bilgi edinin](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
