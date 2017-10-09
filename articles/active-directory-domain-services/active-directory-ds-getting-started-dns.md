---
title: "Azure Active Directory etki alanı Hizmetleri: Güncelleştirme hello Azure sanal ağı için DNS ayarlarını | Microsoft Docs"
description: "Azure Active Directory Etki Alanı Hizmetleri ile çalışmaya başlama"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Azure Active Directory Domain Services'i etkinleştirme (Önizleme)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Görev 4: Hello Azure sanal ağı için DNS ayarlarını güncelleştirme
Yapılandırma Görevleri önceki hello Azure Active Directory etki alanı Hizmetleri dizininiz için başarıyla etkinleştirdiniz. Merhaba sonraki hello sanal ağ içinde bilgisayarlara bağlanmak ve bu hizmetleri kullanan tooensure bir görevdir. Bu makalede, Azure Active Directory etki alanı Hizmetleri hello sanal ağda kullanılabilir olduğu sanal ağ toopoint toohello iki IP adreslerinizi hello DNS sunucusu ayarlarını güncelleştirin.

tooupdate hello DNS sunucusu ayarını Azure Active Directory etki alanı Hizmetleri, aşağıdaki adımları tam hello etkinleştirdiğiniz hello sanal ağ için:

1. Merhaba **genel bakış** sekmesi listeler bir dizi **gerekli yapılandırma adımları** toobe gerçekleştirilen yönetilen etki alanınızın tam olarak sağlandıktan sonra. Merhaba ilk yapılandırma adımı **sunucu için DNS ayarlarını güncelleştirme sanal ağınızı**.

    ![Etki Alanı Hizmetleri - Tamamen hazır haldeki Genel Bakış sekmesi](./media/getting-started/domain-services-provisioned-overview.png)

2. Etki alanınız tamamen hazır hale getirildiğinde bu kutucukta iki IP adresi görüntülenir. Bu IP adreslerinden her biri, yönetilen etki alanınıza yönelik bir etki alanı denetleyicisini temsil eder.

3. toocopy hello ilk IP adresi tooclipboard, hello Kopyala düğmesine bir sonraki tooit tıklayın. Merhaba ardından **yapılandırmak DNS sunucuları** düğmesi.

4. Merhaba ilk IP adresi hello yapıştırma **eklemek DNS sunucusu** metin kutusuna hello **DNS sunucuları** dikey. Kaydırma yatay toocopy hello ikinci IP adresi sol toohello ve hello yapıştırma **eklemek DNS sunucusu** metin kutusu.

    ![Etki Alanı Hizmetleri - DNS'yi güncelleştirme](./media/getting-started/domain-services-update-dns.png)

5. Tıklatın **kaydetmek** tooupdate hello DNS sunucuları hello sanal ağ için bittiğinde.

> [!NOTE]
> Merhaba ağdaki sanal makinelerden yalnızca bir yeniden başlatma sonrasında hello yeni DNS ayarlarını alın. Tooget hello güncelleştirilen DNS ayarlarını hemen gereksinim duyduğunuzda hello portal, PowerShell veya CLI hello yeniden tetikleyin.
>
>

## <a name="next-step"></a>Sonraki adım
[Görev 5: parola eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme](active-directory-ds-getting-started-password-sync.md)
