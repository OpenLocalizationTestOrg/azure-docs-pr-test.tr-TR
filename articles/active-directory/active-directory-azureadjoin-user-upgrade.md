---
title: "Windows 10 cihaz ayarlarından Azure AD ile yukarı aaaSet | Microsoft Docs"
description: "Kullanıcıların tooAzure AD hello ayarları menüsü aracılığıyla nasıl katılabilirsiniz açıklanmaktadır."
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
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama
Zaten varsa Windows 7 veya Windows 8 ve bilgisayarınızı veya Cihazınızı kullanarak yükseltilmiş tooWindows 10 bırakıldı, tooAzure Active Directory (Azure AD) hello ayarları menüsü aracılığıyla katılabilirsiniz.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>hello ayarları menüsünden toojoin tooAzure AD
1. Hello gelen **Başlat** menüsünde hello tıklatın **ayarları** düğmesini seçin.
2. Gelen **ayarları**seçin **sistem**->**hakkında**->**katılma Azure AD**.
   
   <center>
   ![Hello ayarları menüsünden Azure AD katılım](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Tıklatın **devam** hello Azure AD katılım ileti penceresinde.
   
   <center>
   ![Azure AD birleştirme ileti penceresinde](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Oturum açma kimlik bilgilerinizi sağlayın. Bu oturum açma deneyimini gerekli toocomplete kimlik doğrulaması tüm hello adımları içerir. Federasyon Kiracı parçası ise, yöneticiniz size hello Federasyon kuruluşunuz tarafından barındırılan bir deneyim sunar.
   <center>
   ![Oturum açma kimlik bilgilerini sağlamanız](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Kuruluşunuz, tooAzure AD katılmak için Azure multi-Factor Authentication yapılandırdıysa, devam etmeden önce hello ikinci Faktörlü sağlar.
6. Tıklatın **kabul** hello üzerinde **yönetilen bu cihaz toobe izin** ekran.
7. "Cihazınız artık Azure AD alanına katılmış tooyour kuruluşta" hello iletisini görmeniz gerekir.

## <a name="additional-information"></a>Ek bilgiler
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)

