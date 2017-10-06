---
title: "Azure Active Directory etki alanı Hizmetleri: SharePoint kullanıcı profili hizmeti için desteği etkinleştirme | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri yönetilen etki alanlarını toosupport profil eşitleme SharePoint sunucusu için yapılandırma"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Yönetilen etki alanı toosupport profil eşitleme SharePoint sunucusu için yapılandırma
SharePoint Server kullanıcı profili eşitleme için kullanılan bir kullanıcı profili hizmeti içerir. tooset hello kullanıcı profili hizmeti oluşturan bir Active Directory etki alanında verilen toobe uygun izinlerinizin olması gerekir. Daha fazla bilgi için bkz: [SharePoint Server 2013'te profil eşitleme için Active Directory etki alanı Hizmetleri izinleri](https://technet.microsoft.com/library/hh296982.aspx).

Bu makalede, Azure AD etki alanı Hizmetleri yönetilen etki alanlarını toodeploy hello SharePoint Server kullanıcı profili eşitleme hizmeti nasıl yapılandırabileceğiniz açıklanmaktadır.

## <a name="hello-aad-dc-service-accounts-group"></a>Merhaba 'AAD DC hizmet hesapları' grubu
Bir güvenlik grubu olarak adlandırılan '**AAD DC hizmet hesaplarını**' hello 'Kullanıcılar' kuruluş birimi, yönetilen etki alanınızda içinde kullanılabilir. Bu gruptaki hello görebilirsiniz **Active Directory Kullanıcıları ve Bilgisayarları** MMC ek bileşenini, yönetilen etki alanınızda.

![AAD DC hizmet hesaplarını güvenlik grubu](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Bu güvenlik grubunun üyeleri ayrıcalıkları aşağıdaki temsilci hello şunlardır:
- Merhaba 'Dizin değişiklikleri Çoğalt' ayrıcalık hello kök DSE Merhaba, etki alanı yönetilen.
- Merhaba hello yapılandırma adlandırma bağlamında 'Dizin değişiklikleri Çoğalt' ayrıcalığı (cn = yapılandırma kapsayıcısı) Merhaba yönetilen etki alanı.

Bu güvenlik grubunu ayrıca hello yerleşik grubunun bir üyesi olan **Pre-Windows 2000 Compatible Access**.

![AAD DC hizmet hesaplarını güvenlik grubu](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Yönetilen etki alanı toosupport SharePoint Server kullanıcı profili eşitleme etkinleştir
SharePoint kullanıcı profili eşitleme toohello için kullanılan hello hizmet hesabı ekleyebilirsiniz **AAD DC hizmet hesaplarını** grubu. Sonuç olarak, yeterli ayrıcalıkları tooreplicate değişiklikleri toohello dizin hello eşitleme hesabı alır. Bu yapılandırma adımı, SharePoint Server kullanıcı profili eşitleme toowork doğru sağlar.

![AAD DC hizmet hesapları - üyeleri Ekle](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC hizmet hesapları - üyeleri Ekle](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>İlgili İçerik
* [Teknik başvuru - SharePoint Server 2013'te profil eşitleme izinlerini verin Active Directory etki alanı Hizmetleri](https://technet.microsoft.com/library/hh296982.aspx)
