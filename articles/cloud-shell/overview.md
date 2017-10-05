---
title: "Azure bulut Kabuğu (Önizleme) genel bakış | Microsoft Docs"
description: "Azure bulut Kabuk genel bakış."
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
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Azure bulut Kabuğu (Önizleme) genel bakış
Azure bulut Kabuk Azure kaynaklarını yönetmek için etkileşimli, tarayıcı erişilebilir bir kabuk ' dir.

![](media/overview-pic.png)

## <a name="features"></a>Özellikler
### <a name="browser-based-shell-experience"></a>Kabuk tarayıcı tabanlı deneyimi
Bulut Kabuk aklınızda Azure yönetim görevleri ile yerleşik bir tarayıcı tabanlı komut satırı deneyimi erişmesini sağlar. Bir yalnızca bulut yolla yerel makineden untethered çalışması için Dengeleme bulut Kabuk sağlayabilir.

### <a name="pre-configured-azure-workstation"></a>Önceden yapılandırılmış Azure iş istasyonu
Bulut Kabuk popüler komut satırı araçları ile önceden yüklü olarak gelen ve daha hızlı çalışabilmeniz için dil desteği.

[Tam araç listesi için Azure bulut Kabuk burada görüntüleyin.](features.md#tools)

### <a name="automatic-authentication"></a>Otomatik kimlik doğrulama
Bulut Kabuğu güvenli bir şekilde otomatik olarak her oturum için anlık kaynaklarınıza erişmek için Azure CLI 2.0 aracılığıyla üzerinde kimliğini doğrular.

### <a name="connect-your-azure-file-storage"></a>Azure dosya depolama birimini bağlayın
Bulut Kabuk makine geçicidir ve sonuç olarak Azure dosya paylaşımının olarak bağlanmasını gerektiren `clouddrive` $Home dizininize kalıcı hale getirmek için.
Bir kaynak oluşturmak için bulut Kabuk ister üzerinde ilk kez başlatıldığında, sizin adınıza grup, depolama hesabı ve dosya paylaşımı. Bu tek seferlik bir adımdır ve tüm oturumları için otomatik olarak eklenir. 

#### <a name="create-new-storage"></a>Yeni depolama alanı oluşturma
![](media/basic-storage.png)

Yerel olarak yedekli depolama (LRS) hesabı sizin adınıza bir varsayılan 5 GB disk görüntüsü içeren bir Azure dosya paylaşımı ile oluşturulabilir. Dosya Paylaşımı bağladığı olarak `clouddrive` eşitleme ve $Home dizininize kalıcı hale getirmek için kullanılan disk görüntüsü ile etkileşim için dosya paylaşımı. Normal depolama ücretleri.

Üç kaynakları sizin adınıza oluşturulacak:
1. Kaynak grubu adı:`cloud-shell-storage-<region>`
2. Adlı depolama hesabı:`cs<uniqueGuid>`
3. Adlı dosya paylaşımı:`cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> SSH anahtarları gibi $Home dizininizdeki tüm dosyalara, bağlı dosya paylaşımında depolanan kullanıcı disk görüntünüzdeki kalıcıdır. Dosyaları, $Home dizin ve bağlı dosya paylaşımı kaydedilirken en iyi yöntemleri uygulayın.

#### <a name="use-existing-resources"></a>Var olan kaynakları kullanın
![](media/advanced-storage.png)

Gelişmiş bir seçenek de bulut Kabuğu mevcut kaynaklarla ilişkilendirmek olanak sağlanır. Depolama Kurulum istemiyle sunulduğunda "Göster ayarları" Gelişmiş ek seçenekleri seçin. Bırakmalar atanmış olan bulut Kabuk bölge ve yerel olarak/genel-yedekli depolama hesapları için filtrelenir.

[Öğrenin bulut Kabuk depolama hakkında dosya paylaşımları güncelleştirme ve karşıya yükleme ve indirme dosyaları.] (kalıcı-shell-storage.md)

## <a name="concepts"></a>Kavramlar
* Bulut Kabuk bir oturuma özgü üzerinde kullanıcı başına sağlanan geçici bir makinede çalıştırır
* Bulut Kabuk etkileşimli etkinliği olmadan 20 dakika sonra zaman aşımına uğradı
* Bulut Kabuk yalnızca bağlı bir dosya paylaşımı ile erişilebilir
* Bulut Kabuk atanmış bir makine her kullanıcı hesabı
* İzinler normal bir Linux kullanıcı ayarlanır

[Tüm bulut Kabuk özellikleri hakkında daha fazla bilgi edinin.](features.md)

## <a name="examples"></a>Örnekler
* Oluşturma veya Azure Yönetimi otomatikleştirmek için komut dosyaları düzenleme
* Aynı anda Azure portalı ve Azure CLI 2.0 aracılığıyla kaynaklarını yönetme
* Azure CLI 2.0 dediğini

[Bulut Kabuk hızlı başlangıç, tüm bu örneklerde deneyin.](quickstart.md)

## <a name="pricing"></a>Fiyatlandırma
Bulut Kabuk barındıran makine, bir önkoşul $Home dizininize kalıcı hale getirmek için bir bağlı Azure dosya paylaşımı ile ücretsizdir. Normal depolama ücretleri.

## <a name="supported-browsers"></a>Desteklenen tarayıcılar
Bulut Kabuk Chrome, sınır ve Safari için önerilir. Bulut Kabuk Chrome, Firefox, Safari, IE ve kenar desteklense de, bulut Kabuk belirli tarayıcı ayarları tabi değil.

## <a name="troubleshooting"></a>Sorun giderme
1. Bir Azure Active Directory aboneliğine kullanırken, depolama hata nedeniyle oluşturulamıyor: 400 DisallowedOperation. Bu sorunu çözmek için lütfen depolama kaynaklarını oluşturabileceğinden Azure aboneliği kullanın. AD abonelikleri Azure kaynaklarını oluşturmak mümkün değildir.

Belirli bilinen sınırlamalar ziyaret [bulut Kabuk sınırlamaları](limitations.md).
