---
title: "Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama | Microsoft Docs"
description: "Ayarlar menüsünde aracılığıyla Azure ad kullanıcıların nasıl katılabilirsiniz açıklanmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama
Zaten Windows 7 veya Windows 8 kullanıyorsanız ve bilgisayarınızı veya Cihazınızı Windows 10'a yükseltildikten ayarlar menüsünü kullanarak Azure Active Directory (Azure AD) katılabilirsiniz.

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a>Azure AD için Ayarlar menüsünden katılmak için
1. Gelen **Başlat** menüsünde tıklatın **ayarları** düğmesini seçin.
2. Gelen **ayarları**seçin **sistem**->**hakkında**->**katılma Azure AD**.
   
   <center>
   ![Ayarlar menüsünde Azure AD katılım](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Tıklatın **devam** Azure AD katılım ileti penceresinde.
   
   <center>
   ![Azure AD birleştirme ileti penceresinde](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Oturum açma kimlik bilgilerinizi sağlayın. Bu oturum açma deneyimini tam kimlik doğrulaması için gereken tüm adımları içerir. Federasyon Kiracı parçası ise, yöneticiniz size kuruluşunuz tarafından barındırılan bir Federasyon deneyim sağlayacaktır.
   <center>
   ![Oturum açma kimlik bilgilerini sağlamanız](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Kuruluşunuz, Azure AD ile katılmak için Azure multi-Factor Authentication yapılandırdıysa, devam etmeden önce ikinci Faktörlü sağlar.
6. Tıklatın **kabul** üzerinde **bu cihazın yönetilmesine izin** ekran.
7. "Cihazınız artık kuruluşunuzun Azure AD'de katıldı" iletisini görmeniz gerekir.

## <a name="additional-information"></a>Ek bilgiler
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)

