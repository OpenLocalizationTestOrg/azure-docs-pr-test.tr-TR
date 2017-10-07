---
title: "Kullanıcılarınız için Azure AD'ye katılımı ayarlama aaaSetting | Microsoft Docs"
description: "Yöneticilerin, şirket içi dizin ve cihaz kaydı için Azure AD Katılımını nasıl ayarlayacakları açıklanmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Kuruluşunuzda Azure AD'ye Katılımı ayarlama
Azure Active Directory katılımını (Azure AD katılımı) ayarlamadan önce tooeither eşitleme gereksinim yukarı şirket içi dizininize kullanıcılar toohello Bulut veya el ile Azure AD'de yönetilen hesapları oluşturun.

Şirket içi kullanıcıların tooAzure AD eşitlemeye için ayrıntılı yönergeler [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

toomanually oluşturmak ve kullanıcıların Azure AD'de yönetmek, çok bakın[Azure AD'de kullanıcı yönetimi](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Cihaz kaydı oluşturma
1. Toohello üzerinde Azure portal yönetici olarak oturum açın.
2. Merhaba soldaki bölmede bulunan seçin **Active Directory**.
3. Merhaba üzerinde **Directory** sekmesinde, dizininizi seçin.
4. Select hello **yapılandırma** sekmesi.
5. Toohello Git **aygıtları** bölümü.
6. Merhaba üzerinde **aygıtları** sekmesinde, hello aşağıdakileri ayarlayın:  
   * **En büyük sayı, CİHAZLARI kullanıcı başına**: hello en fazla bir kullanıcı Azure AD'de sahip cihaz sayısını seçin.  Bir kullanıcı bu kota ulaşırsa, bir veya daha fazla var olan cihazlarının kaldırılana kadar bunlar mümkün tooadd ek cihazlar olmaz.
   * **İSTE MULTİ-FACTOR AUTH tooJOIN AYGITLARI**: kullanıcılar gerekli tooprovide olup ayarlamak ikinci bir kimlik doğrulama faktörü toojoin kendi cihaz tooAzure AD. Azure çok faktörlü kimlik doğrulaması hakkında daha fazla bilgi için bkz: [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **USERS MAY AZURE AD birleştirme AYGITLARI**: hello kullanıcılar ve toojoin aygıtları tooAzure AD izin verilen grubu seçin.
   * **Ek Yöneticiler ON AZURE AD alanına KATILAN CİHAZLAR**: Azure AD Premium veya Enterprise Mobility Suite (EMS) hello ile hangi kullanıcılara yerel yönetici hakları verilen seçebilirsiniz toohello aygıt. Varsayılan olarak genel yöneticilere ve cihaz sahiplerine yerel yönetici hakları verilir.

<center>![Cihaz kaydı ayarlama](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

Kullanıcılarınız için Azure AD'ye katılımı ayarladıktan sonra tooAzure AD aracılığıyla kendi Kurumsal veya kişisel aygıtlar bağlanabilir.

Tooenable kullanıcılar tooset Azure AD'ye katılımı kullanabileceğiniz hello üç senaryolar şunlardır:

* Kullanıcıların katılma şirkete ait bir cihazı doğrudan tooAzure AD.
* Kullanıcıları etki alanına katılma bir şirketin aygıt toohello şirket içi Active Directory ve hello aygıt tooAzure AD genişletir.
* Kullanıcıların iş veya Okul tooWindows kişisel bir cihazda hesapları

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

