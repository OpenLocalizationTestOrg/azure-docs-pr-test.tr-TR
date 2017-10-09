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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Hello Azure sanal ağı için DNS ayarlarını güncelleştirme
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Görev 4: Güncelleştirme hello Azure sanal ağı için DNS ayarları
Yapılandırma Görevleri önceki hello Azure Active Directory etki alanı Hizmetleri dizininiz için başarıyla etkinleştirdiniz. Merhaba sonraki hello sanal ağ içinde bilgisayarlara bağlanmak ve bu hizmetleri kullanan tooensure bir görevdir. Bu makalede, Azure Active Directory etki alanı Hizmetleri hello sanal ağda kullanılabilir olduğu sanal ağ toopoint toohello iki IP adreslerinizi hello DNS sunucusu ayarlarını güncelleştirin.

> [!NOTE]
> Azure Active Directory etki alanı Hizmetleri hello dizin için etkinleştirdikten sonra Azure Active Directory etki alanı üzerinde hello görüntülenen Hizmetleri hello IP adreslerini Not **yapılandırma** dizininizin sekmesi.
>
>

tooupdate hello DNS sunucusu ayarını Azure Active Directory etki alanı Hizmetleri, aşağıdaki adımları tam hello etkinleştirdiğiniz hello sanal ağ için:

1. Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol bölmesinde seçin **ağlar**.  
    Merhaba **ağlar** penceresi açılır.

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Merhaba üzerinde **sanal ağlar** sekmesi, select hello sanal ağ içinde etkin Azure Active Directory etki alanı Hizmetleri tooview özellikleri.
4. Merhaba tıklatın **yapılandırma** sekmesi.

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. Merhaba, **DNS sunucuları** bölümünde, hem de hello görüntülenen her hello IP adreslerini girin **etki alanı Hizmetleri** hello bölüm **yapılandırma** dizininizin sekmesi.
6. toosave hello DNS sunucusu ayarlarını hello pencerenin hello altındaki hello görev bölmesindeki bu sanal ağ tıklatın **kaydetmek**.

   ![Merhaba sanal ağ Hello DNS sunucusu ayarlarını güncelleştirme](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Merhaba ağdaki sanal makinelerden yalnızca bir yeniden başlatma sonrasında hello yeni DNS ayarlarını alın. Tooget hello güncelleştirilen DNS ayarlarını hemen gereksinim duyduğunuzda hello portal, PowerShell veya CLI hello yeniden tetikleyin.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Görev 5: [parola eşitleme tooAzure Active Directory etki alanı Hizmetleri'ni etkinleştirme](active-directory-ds-getting-started-password-sync.md)
