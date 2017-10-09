---
title: "aaaAzure bulut Kabuğu (Önizleme) genel bakış | Microsoft Docs"
description: "Hello Azure bulut Kabuk genel bakış."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Azure bulut Kabuğu (Önizleme) genel bakış
Azure bulut Kabuk Azure kaynaklarını yönetmek için etkileşimli, tarayıcı erişilebilir bir kabuk ' dir.

![](media/overview-pic.png)

## <a name="features"></a>Özellikler
### <a name="browser-based-shell-experience"></a>Kabuk tarayıcı tabanlı deneyimi
Azure yönetim görevlerinizi aklınızda ile oluşturulan Kabuk etkinleştirir erişim tooa tarayıcı tabanlı komut satırı deneyimi bulut. Yerel makinede yalnızca hello bulut sağlayabilir şekilde untethered bulut Kabuk toowork yararlanın.

### <a name="pre-configured-azure-workstation"></a>Önceden yapılandırılmış Azure iş istasyonu
Bulut Kabuk popüler komut satırı araçları ile önceden yüklü olarak gelen ve daha hızlı çalışabilmeniz için dil desteği.

[Görünüm hello tam araç listesini Azure bulut Kabuğu burada.](features.md#tools)

### <a name="automatic-authentication"></a>Otomatik kimlik doğrulama
Bulut Kabuğu güvenli bir şekilde otomatik olarak her oturum için anında erişim tooyour kaynaklara hello Azure CLI 2.0 aracılığıyla üzerinde kimliğini doğrular.

### <a name="connect-your-azure-file-storage"></a>Azure dosya depolama birimini bağlayın
Bulut Kabuk makineler geçicidir ve sonuç olarak olarak oluşturulmuş bir Azure dosya paylaşımı toobe gerektiren `clouddrive` toopersist $Home dizin.
Üzerinde ilk kez başlatıldığında, sizin adınıza bir kaynak grubu, depolama hesabı ve dosya paylaşımı toocreate bulut Kabuk ister. Bu tek seferlik bir adımdır ve tüm oturumları için otomatik olarak eklenir. 

#### <a name="create-new-storage"></a>Yeni depolama alanı oluşturma
![](media/basic-storage.png)

Yerel olarak yedekli depolama (LRS) hesabı sizin adınıza bir varsayılan 5 GB disk görüntüsü içeren bir Azure dosya paylaşımı ile oluşturulabilir. Merhaba dosya paylaşımı bağladığı olarak `clouddrive` hello disk görüntüsü ile etkileşim için dosya paylaşımı kullanılan toosync olması ve $Home dizininize kalır. Normal depolama ücretleri.

Üç kaynakları sizin adınıza oluşturulacak:
1. Kaynak grubu adı:`cloud-shell-storage-<region>`
2. Adlı depolama hesabı:`cs<uniqueGuid>`
3. Adlı dosya paylaşımı:`cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> SSH anahtarları gibi $Home dizininizdeki tüm dosyalara, bağlı dosya paylaşımında depolanan kullanıcı disk görüntünüzdeki kalıcıdır. Dosyaları, $Home dizin ve bağlı dosya paylaşımı kaydedilirken en iyi yöntemleri uygulayın.

#### <a name="use-existing-resources"></a>Var olan kaynakları kullanın
![](media/advanced-storage.png)

Gelişmiş bir seçenek de izin verme, tooassociate mevcut kaynakları tooCloud Kabuk sağlanır. Merhaba depolama Kurulum istemiyle sunulduğunda "Gelişmiş Göster ayarları" tooselect Ek Seçenekler'i tıklatın. Bırakmalar atanmış olan bulut Kabuk bölge ve yerel olarak/genel-yedekli depolama hesapları için filtrelenir.

[Öğrenin bulut Kabuk depolama hakkında dosya paylaşımları güncelleştirme ve karşıya yükleme ve indirme dosyaları.] (kalıcı-shell-storage.md)

## <a name="concepts"></a>Kavramlar
* Bulut Kabuk bir oturuma özgü üzerinde kullanıcı başına sağlanan geçici bir makinede çalıştırır
* Bulut Kabuk etkileşimli etkinliği olmadan 20 dakika sonra zaman aşımına uğradı
* Bulut Kabuk yalnızca bağlı bir dosya paylaşımı ile erişilebilir
* Bulut Kabuk atanmış bir makine her kullanıcı hesabı
* İzinler normal bir Linux kullanıcı ayarlanır

[Tüm bulut Kabuk özellikleri hakkında daha fazla bilgi edinin.](features.md)

## <a name="examples"></a>Örnekler
* Oluşturma veya komut dosyaları tooautomate Azure Yönetimi düzenleme
* Aynı anda Azure portalı ve Azure CLI 2.0 aracılığıyla kaynaklarını yönetme
* Azure CLI 2.0 dediğini

[Bu örnekler hello bulut Kabuk hızlı başlangıç adresindeki deneyin.](quickstart.md)

## <a name="pricing"></a>Fiyatlandırma
Merhaba makine bulut Kabuk barındırma ücretsizdir, önkoşul bağlı Azure dosyasının ile toopersist $Home dizininize paylaşma. Normal depolama ücretleri.

## <a name="supported-browsers"></a>Desteklenen tarayıcılar
Bulut Kabuk Chrome, sınır ve Safari için önerilir. Bulut Kabuk Chrome, Firefox, Safari, IE ve kenar desteklense de, bulut Kabuk konu toospecific tarayıcı ayarları'dır.

## <a name="troubleshooting"></a>Sorun giderme
1. Bir Azure Active Directory aboneliğine kullanırken, depolama oluşturulamıyor son tooError: 400 DisallowedOperation. tooresolve Bu, lütfen depolama kaynaklarını oluşturabileceğinden Azure aboneliği kullanın. AD aboneliklerini erişilemiyor toocreate Azure kaynaklardır.

Belirli bilinen sınırlamalar ziyaret [bulut Kabuk sınırlamaları](limitations.md).
