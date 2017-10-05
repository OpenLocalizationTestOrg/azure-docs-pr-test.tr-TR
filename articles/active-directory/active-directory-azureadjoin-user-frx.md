---
title: "Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama | Microsoft Docs"
description: "Nasıl kullanıcıları Azure AD'ye katılımı kendi ilk çalıştırma deneyimi sırasında ayarlayabilirsiniz açıklayan bir konu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama
Windows 10'da, kullanıcıların cihazlarını Azure Active Directory (Azure AD) ilk çalıştırma deneyimi (FRX) birleştirebilirler. Bu, kuruluşların kendi çalışanlar veya Öğrenciler naylon cihazlara dağıtmak veya kendi aygıt (CYOD) seçmesini sağlayan olanak tanır.
Windows 10 Professional veya Windows 10 Enterprise Edition bir cihaz üzerinde yüklüyse, deneyimi Kurulum işlemi şirkete ait cihazlar için varsayılan olarak ayarlanır.

## <a name="to-join-a-device-to-azure-ad"></a>Bir aygıt için Azure AD katılmak için
1. Yeni aygıtınızı açın ve kurulum işlemini başlatamazsa, görmelisiniz **alma hazır** ileti. Cihazınızı ayarlamak için istemleri izleyin.
2. Bölge ve dil özelleştirerek başlatın. Ardından, Microsoft Yazılımı Lisans koşulları kabul edin.
   ![Bölgeniz için özelleştirme](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Internet'e bağlanmak için kullanmak istediğiniz ağı seçin.
4. Kişisel bir cihazı veya şirkete ait bir cihazı kullanıyorsanız olup olmadığını seçin. Şirkete ait ise, tıklatın **bu cihaz kuruluşuma ait**. Bu, Azure AD katılım deneyimi başlatır. Aşağıdaki Windows 10 Professional kullanıyorsanız görürsünüz bir ekrandır.
   <center>
   ![Bu bilgisayar ekran Kime ait](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Kuruluşunuz tarafından size sağlanan kimlik bilgilerini girin.
   <center>
   ![Oturum açma ekranı](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Eşleşen bir kiracı, kullanıcı adınızı girdikten sonra Azure AD içinde yer alır. Federe bir etki alanındaysa, şirket içi güvenli belirteç hizmeti (STS) sunucunuza--Örneğin, Active Directory Federasyon Hizmetleri (AD FS) yönlendirilir.
7. Federasyon olmayan bir etki alanındaki bir kullanıcı varsa, doğrudan Azure AD tarafından barındırılan sayfasında kimlik bilgilerinizi girin. Şirket markası yapılandırdıysanız, aynı zamanda, kuruluşunuzun logosu görebilir ve metin desteği.
8. Çok faktörlü kimlik doğrulaması sınaması için istenir. Bu sorunu BT yöneticisi tarafından yapılandırılabilir.
9. Azure AD, bu kullanıcı/cihaz kaydı mobil cihaz Yönetimi'nde gerekli olup olmadığını denetler.
10. Windows Azure AD'de kuruluşunuzun dizininde cihazı kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.
11. Yönetilen bir kullanıcı varsa, Windows, Masaüstü otomatik oturum açma işlemi aracılığıyla alır.
12. Bir Federasyon kullanıcısı varsa, kimlik bilgilerinizi girmeniz için Windows oturum açma ekranı yönlendirilir.

> [!NOTE]
> Windows out-of-box deneyiminde bir şirket içi Windows Server Active Directory etki alanına katılma desteklenmiyor. Bu nedenle, bir bilgisayarı bir etki alanına planlıyorsanız, bağlantıyı seçmelisiniz **Windows'u yerel hesapla ayarlamak** yerine. Önce uyguladığınız gibi etki alanı ayarlarından sonra bilgisayarınızda birleştirebilirsiniz.
> 
> 

## <a name="additional-information"></a>Ek bilgiler
* [Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

