---
title: "Azure Storage ile kullanılan aaaSecurity özellikleri | Microsoft Docs"
description: " Bu makalede Azure Storage ile kullanılan hello çekirdek Azure güvenlik özelliklerine genel bakış sağlar. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Azure depolama güvenliğine genel bakış
Azure Storage hello bulut depolama dayanıklılık, kullanılabilirlik ve ölçeklenebilirlik toomeet hello müşterilerin ihtiyaçlarını kullanan modern uygulamalar için çözümüdür. Azure depolama kapsamlı bir güvenlik özellikleri sağlar:

* Merhaba depolama hesabı rol tabanlı erişim denetimi ve Azure Active Directory kullanılarak güvenli hale getirilebilir.
* Verileri bir uygulama ile Azure arasında aktarımda istemci tarafı şifreleme, HTTPS veya SMB 3.0 kullanarak güvenli hale getirilebilir.
* Verileri otomatik olarak şifrelenir toobe ayarlanabilir zaman tooAzure depolama hizmeti şifrelemesi kullanarak depolama yazılır.
* Sanal makineler tarafından kullanılan işletim sistemi ve veri diskleri Azure Disk şifrelemesi kullanılarak şifrelenmiş toobe ayarlayabilirsiniz.
* Azure depolama atanmış erişim toohello veri nesneleri, paylaşılan erişim imzaları kullanılarak verilebilir.
* Depolama eriştiklerinde birisi tarafından kullanılan hello kimlik doğrulama yöntemi, depolama çözümlemeleri kullanarak izlenebilir.

Azure Storage güvenlik daha ayrıntılı bir bakış için bkz: Merhaba [Azure Storage Güvenlik Kılavuzu'nu](../storage/common/storage-security-guide.md). Bu kılavuz, derinlemesine hello güvenlik özelliklerine Azure depolama gibi depolama hesabı anahtarları, veri şifreleme Aktarımdaki ve rest ve depolama çözümlemeleri sağlar.

Bu makalede Azure Storage ile kullanılan Azure güvenlik özelliklerine genel bakış sağlar. Daha fazla bilgi için her bir özelliğin ayrıntılarını veren tooarticles bağlantılar sağlanmaktadır.

Bu makalede ele alınan hello çekirdek özellikler toobe şunlardır:

* Rol Tabanlı Access Control
* Atanmış erişim toostorage nesneleri
* Aktarımdaki şifreleme
* Şifreleme rest/depolama hizmeti şifrelemesi
* Azure Disk Şifrelemesi
* Azure Key Vault

## <a name="role-based-access-control-rbac"></a>Rol Tabanlı Erişim Denetimi (RBAC)
Rol tabanlı erişim denetimi (RBAC) ile depolama hesabınızın güvenliğini sağlayabilirsiniz. Erişimi kısıtlama tabanlı hello üzerinde [tooknow gerek](https://en.wikipedia.org/wiki/Need_to_know) ve [en az ayrıcalık](https://en.wikipedia.org/wiki/Principle_of_least_privilege) güvenlik ilkeleri kesinlik temelli tooenforce güvenlik ilkeleri veri erişimi için istediğiniz kuruluşlar için. Bu erişim haklarını hello uygun RBAC rolü toogroups ve belirli bir kapsamda uygulamaları atayarak verilir. Kullanabileceğiniz [yerleşik RBAC rolleri](../active-directory/role-based-access-built-in-roles.md), depolama hesabı katkıda bulunanlar gibi tooassign toousers ayrıcalıkları.

Daha fazla bilgi edinin:

* [Azure Active Directory Rol Tabanlı Erişim Denetimi](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Atanmış erişim toostorage nesneleri
Paylaşılan erişim imzası (SAS) depolama hesabınızda atanmış erişim tooresources sağlar. Merhaba SAS süre ve belirtilen bir izin kümesi ile belirli bir süre için izinleri tooobjects depolama hesabınızdaki bir istemci sınırlı verebilirsiniz anlamına gelir. Hesap erişim tuşlarınızı tooshare gerek kalmadan bu sınırlı izinleri verebilirsiniz. Merhaba SAS kimlik doğrulamalı erişim tooa depolama kaynağı için gerekli olan tüm hello bilgileri kendi sorgu parametrelerini kapsayan bir URI değil. tooaccess depolama kaynaklarını hello SAS ile Merhaba istemci yalnızca tooprovide hello SAS toohello uygun Oluşturucusu veya yöntem gerekir.

Daha fazla bilgi edinin:

* [Merhaba SAS modelini anlama](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Oluşturma ve bir SAS Blob storage'ı kullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
Şifreleme Aktarımdaki ağlar üzerinden iletilirken veri koruma, bir mekanizmadır. Azure Storage ile verileri kullanarak güvenliğini sağlayabilirsiniz:

* [Aktarım düzeyinde şifreleme](../storage/common/storage-security-guide.md#encryption-in-transit), içine veya dışına Azure Storage veri aktarırken HTTPS gibi.
* [Şifreleme wire](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), Azure dosya paylaşımları için SMB 3.0 şifreleme gibi.
* [İstemci tarafı şifreleme](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), depolama alanı biterse aktarıldıktan sonra depolama ve toodecrypt hello verisine transfer edilmeden önce tooencrypt hello veri.

İstemci tarafı şifreleme hakkında daha fazla bilgi edinin:

* [Microsoft Azure depolama için istemci tarafı şifreleme](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Bulut güvenlik denetimleri serisi: Aktarımdaki verileri şifreleme](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Bekleme sırasında şifreleme
Çoğu kuruluş için [bekleyen verileri şifreleme](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) veri gizliliği, uyumluluk ve veri egemenliği doğru zorunlu bir adımdır. "Bekleyen" olan verilerin şifrelenmesini sağlayan üç Azure özellikleri şunlardır:

* [Depolama hizmeti şifrelemesi](../storage/common/storage-security-guide.md#encryption-at-rest) toorequest hello depolama hizmeti otomatik olarak veri tooAzure depolama yazılırken şifrelemenizi sağlar.
* [İstemci tarafı şifreleme](../storage/common/storage-security-guide.md#client-side-encryption) bekleyen şifreleme hello özelliği de sağlar.
* [Azure Disk şifrelemesi](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) tooencrypt hello işletim sistemi ve bir Iaas sanal makine tarafından kullanılan veri disklerle sağlar.

Depolama hizmeti şifrelemesi hakkında daha fazla bilgi edinin:

* [Azure depolama hizmeti şifrelemesi](https://azure.microsoft.com/services/storage/) için kullanılabilir [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Diğer Azure depolama türleri hakkında daha fazla bilgi için bkz: [dosya](https://azure.microsoft.com/services/storage/files/), [Disk (Premium depolama)](https://azure.microsoft.com/services/storage/premium-storage/), [tablo](https://azure.microsoft.com/services/storage/tables/), ve [sıra](https://azure.microsoft.com/services/storage/queues/).
* [Rest verileri için Azure Storage hizmeti şifreleme](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Şifrelemesi
Sanal makineler (VM'ler) için Azure Disk şifrelemesi yardımcı olan adres Kurumsal güvenlik ve uyumluluk gereksinimleri (önyükleme ve veri diskleri dahil), VM diskleri şifreleyerek anahtarları ve, denetim ilkeleri ile [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/).

Disk şifrelemesi VM'ler için Linux ve Windows işletim sistemleri için çalışır. Ayrıca, koruma, yönetin ve disk şifreleme anahtarlarınızı kullanımını denetleme anahtar kasası toohelp kullanır. VM disklerinizi tüm hello verileri bekleyen endüstri standardı şifreleme teknolojisi Azure Storage hesaplarınızı kullanılarak şifrelenir. Disk şifrelemesi çözüm için Windows Hello temel [Microsoft BitLocker Sürücü Şifrelemesi](https://technet.microsoft.com/library/cc732774.aspx), ve hello Linux çözüm temel [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Daha fazla bilgi edinin:

* [Windows ve Linux Iaas sanal makineler için Azure Disk şifrelemesi](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Azure Key Vault
Azure Disk şifrelemesi kullanan [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) toohelp, denetlemek ve disk şifreleme anahtarları ve gizli anahtarları Azure bekleyen hello sanal makine disklerdeki tüm veriler şifrelenir sağlarken anahtar kasası aboneliğinizde yönetme Depolama alanı. Anahtar kasası tooaudit anahtarları ve ilke kullanım kullanmanız gerekir.

Daha fazla bilgi edinin:

* [Azure anahtar kasası nedir?](../key-vault/key-vault-whatis.md)
* [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md)
