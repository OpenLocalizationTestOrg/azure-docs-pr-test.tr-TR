---
title: "Azure bulut Kabuğu (Önizleme) dosyalarında kalıcı | Microsoft Docs"
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
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Azure bulut Kabuk dosyalarında Sürdür
Bulut Kabuk oturumlarında dosyaları kalıcı hale getirmek için Azure File storage yararlanır.

## <a name="set-up-a-clouddrive-file-share"></a>Ayarlanmış bir `clouddrive` dosya paylaşımı
İlk Başlat, bulut Kabuk oturumlarında dosyaları kalıcı hale getirmek için yeni veya varolan bir dosya paylaşımı ilişkilendirmek isteyip istemediğinizi sorar.

### <a name="create-new-storage"></a>Yeni depolama alanı oluşturma

Temel ayarlar kullanın ve yalnızca bir abonelik seçin, bulut Kabuk üç kaynakları en yakın olan desteklenen bölgede sizin adınıza oluşturur:
* Kaynak grubu:`cloud-shell-storage-<region>`
* Depolama hesabı:`cs<uniqueGuid>`
* Dosya Paylaşımı:`cs-<user>-<domain>-com-<uniqueGuid>`

![Abonelik ayarı](media/basic-storage.png)

Dosya Paylaşımı bağladığı olarak `clouddrive` içinde `$Home` dizin. Dosya Paylaşımı Ayrıca, sizin yerinize oluşturulur ve otomatik olarak güncelleştirir ve devam ederse, 5 GB görüntü depolamak için kullanılan, `$Home` dizin. Bu tek seferlik bir işlemdir ve dosya paylaşımı sonraki oturumlarda otomatik olarak bağlar.

### <a name="use-existing-resources"></a>Var olan kaynakları kullanın

Gelişmiş seçeneğini kullanarak, var olan kaynakların ilişkilendirebilirsiniz. Depolama Kurulum istemi belirdiğinde seçin **Göster Gelişmiş ayarları** ek seçenekleri görüntülemek için. Var olan dosya paylaşımları kalıcı hale getirmek için 5 GB kullanıcı görüntüsü almak, `$Home` dizin. Aşağı açılır menüler yerel olarak yedekli & coğrafi olarak yedekli depolama hesapları ve bulut Kabuk bölgeniz için filtrelenir.

![Kaynak grubu ayarı](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Bir Azure kaynak İlkesi ile kaynak oluşturma kısıtla
Bulut Kabuğu'nda oluşturduğunuz depolama hesapları ile etiketlenmiş `ms-resource-usage:azure-cloud-shell`. Bulut Kabuğu'nda depolama hesapları oluşturma kullanıcıların engellemek istiyorsanız oluşturma bir [etiketleri için Azure kaynak İlkesi](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) bu belirli etiketi tarafından tetiklenir.

## <a name="how-cloud-shell-works"></a>Bulut Kabuk nasıl çalışır?
Bulut kabuk dosyalar aşağıdaki yöntemlerin her ikisi de ile devam eder:
* Bir disk görüntüsünü oluşturma, `$Home` dizini içindeki tüm içeriği kalıcı hale getirmek için dizin. Disk görüntüsü, belirtilen dosya paylaşımı olarak kaydedilir `acc_<User>.img` adresindeki `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, ve değişiklikleri otomatik olarak eşitlenir.

* Belirtilen dosya paylaşımı olarak takma `clouddrive` içinde `$Home` doğrudan dosya paylaşımı etkileşim için dizin. `/Home/<User>/clouddrive`eşlenmiş `fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Tüm dosyaları, `$Home` SSH anahtarları gibi dizini, bağlı dosya paylaşımında depolanan, kullanıcı disk görüntüsü kaldı. Bilgileri kalıcı sırasında en iyi yöntemleri uygulamak, `$Home` dizin ve bağlı dosya paylaşımı.

## <a name="use-the-clouddrive-command"></a>Kullanım `clouddrive` komutu
Bulut kabuğunda denilen bir komut çalıştırabilirsiniz `clouddrive`, bağlı dosya paylaşımı için bulut Kabuk el ile güncelleştirmeniz sağlar.
!["Clouddrive" komutunu çalıştırarak](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Yeni bir bağlama`clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>El ile bağlama için Önkoşullar
Kullanarak bulut kabuğu ile ilişkili dosya paylaşımı güncelleştirebilirsiniz `clouddrive mount` komutu.

Varolan bir dosya paylaşımını bağlama depolama hesapları olması gerekir:
* Yerel olarak yedekli depolama veya coğrafi olarak yedekli depolama dosya paylaşımları desteği.
* Atanan bölgenizde bulunur. Onboarding olduğunda, kaynak grubu adı atandığınız bölge listelenen `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Desteklenen depolama bölgeleri
Azure dosyaları kendilerine bağlanması bulut Kabuk makine ile aynı bölgede bulunmalıdır. Bulut Kabuk kümeleri şu anda aşağıdaki bölgelerde mevcuttur:
|Alan|Bölge|
|---|---|
|Kuzey ve Güney Amerika|Doğu ABD, Orta Güney ABD, Batı ABD|
|Avrupa|Kuzey Avrupa, Batı Avrupa|
|Asya Pasifik|Hindistan Orta, Güneydoğu Asya|

### <a name="the-clouddrive-mount-command"></a>`clouddrive mount` Komutu

> [!NOTE]
> Yeni bir dosya paylaşımı takma varsa, yeni bir kullanıcı görüntüsü için oluşturulur, `$Home` dizin, çünkü, önceki `$Home` görüntü önceki dosya paylaşımındaki tutulur.

Çalıştırma `clouddrive mount` komutunu aşağıdaki parametrelerle:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

Daha fazla ayrıntı görüntülemek için çalıştırın `clouddrive mount -h`, aşağıda gösterildiği gibi:

![Çalışan ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Çıkarın`clouddrive`
Bulut Kabuk herhangi bir anda takılı bir dosya paylaşımı çıkarın. Dosya paylaşımınızı kaldırılan olduktan sonra sonraki oturumunuz önce yeni bir dosya paylaşımını bağlama istenir.

Bulut Kabuğu'ndan bir dosya paylaşımını kaldırmak için:
1. `clouddrive unmount` öğesini çalıştırın.
2. Onayla ve istemleri onaylayın.

Dosya paylaşımınızı el ile silmediğiniz sürece var olmaya devam eder. Bulut Kabuk, artık bu dosya paylaşımı için sonraki oturumlarda arar.

Daha fazla ayrıntı görüntülemek için çalıştırın `clouddrive unmount -h`, aşağıda gösterildiği gibi:

![Çalışan ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> Bu komutu çalıştıran herhangi bir kaynağa silmez. El ile bir kaynak grubu, depolama hesabı veya Bulut Kabuk eşlenmiş dosya paylaşımı kalıcı olarak silindiğinde, `$Home` directory görüntü ve herhangi bir dosya paylaşımı dosyalarında. Bu eylem geri alınamaz.

## <a name="list-clouddrive-file-shares"></a>Liste `clouddrive` dosya paylaşımları
Hangi dosya paylaşımı olarak takılı bulmak için `clouddrive`, aşağıdaki komutu çalıştırarak `df` komutu. 

URL'de, depolama hesabı adı ve dosya paylaşımı clouddrive dosya yolu gösterir. Örneğin, `//storageaccountname.file.core.windows.net/filesharename`

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

## <a name="transfer-local-files-to-cloud-shell"></a>Bulut kabuğu için yerel dosya aktarımı
`clouddrive` Dizin eşitlemeler Azure portal depolama dikey ile. Bu dikey veya dosya paylaşımından yerel dosyalar aktarmak için kullanın. Dikey yenilediğinizde bulut Kabuk içinde dosyalar dosya depolama GUI yansıtılır.

### <a name="download-files"></a>Dosyaları indirme

![Yerel dosya listesi](media/download.png)
1. Azure portalında bağlı dosya paylaşımına gidin.
2. Hedef dosya seçin.
3. Seçin **karşıdan** düğmesi.

### <a name="upload-files"></a>Dosyaları karşıya yükleme

![Karşıya yüklenecek yerel dosyaları](media/upload.png)
1. Bağlı dosya paylaşımına gidin.
2. Seçin **karşıya** düğmesi.
3. Dosya veya karşıya yüklemek istediğiniz dosyaları seçin.
4. Karşıya yükleme onaylayın.

İçinde erişilebilir olan dosyaların görmelisiniz, `clouddrive` bulut Kabuğu'nda dizin.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut Kabuk hızlı başlangıç](quickstart.md) <br>
[Azure File storage hakkında bilgi edinin](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Depolama etiketler hakkında bilgi edinin](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
