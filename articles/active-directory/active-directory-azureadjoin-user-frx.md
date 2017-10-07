---
title: "Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Kurulum sırasında Azure AD ile yeni bir cihaz ayarlama
Windows 10'da, kullanıcıların kendi aygıtlarını tooAzure Active Directory (Azure AD) hello ilk çalıştırma deneyimi (FRX) birleştirebilirsiniz. Bu kuruluşların toodistribute naylon aygıtları tootheir çalışanlar veya Öğrenciler izin verir veya kendi aygıt (CYOD) seçmesini sağlar.
Windows 10 Professional veya Windows 10 Enterprise Edition bir cihaz üzerinde yüklüyse, hello şirkete ait cihazlar için varsayılan toohello Kurulum işlemi karşılaşırsınız.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin aygıt tooAzure AD
1. Yeni aygıtınızı açın ve hello Kurulum işlemini başlatamazsa, hello görmelisiniz **alma hazır** ileti. Cihazınızı yukarı Hello istemleri tooset izleyin.
2. Bölge ve dil özelleştirerek başlatın. Ardından hello Microsoft Yazılımı Lisans koşulları kabul edin.
   ![Bölgeniz için özelleştirme](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Toouse toohello Internet bağlanmak için hello ağı seçin.
4. Kişisel bir cihazı veya şirkete ait bir cihazı kullanıyorsanız olup olmadığını seçin. Şirkete ait ise, tıklatın **toomy kuruluş bu cihaz ait**. Bu hello Azure AD katılım deneyimi başlatır. Aşağıdaki Windows 10 Professional kullanıyorsanız görürsünüz bir ekrandır.
   <center>
   ![Bu bilgisayar ekran Kime ait](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Tooyou kuruluşunuz tarafından sağlanan hello kimlik bilgilerini girin.
   <center>
   ![Oturum açma ekranı](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Eşleşen bir kiracı, kullanıcı adınızı girdikten sonra Azure AD içinde yer alır. Federe bir etki alanındaysa, yeniden yönlendirilen tooyour şirket içi güvenli belirteç hizmeti (STS) sunucu--Örneğin, Active Directory Federasyon Hizmetleri (AD FS) olacaktır.
7. Federasyon olmayan bir etki alanındaki bir kullanıcı varsa, doğrudan hello üzerinde Azure AD tarafından barındırılan sayfasında kimlik bilgilerinizi girin. Şirket markası yapılandırdıysanız, aynı zamanda, kuruluşunuzun logosu görebilir ve metin desteği.
8. Çok faktörlü kimlik doğrulaması sınaması için istenir. Bu sorunu BT yöneticisi tarafından yapılandırılabilir.
9. Azure AD, bu kullanıcı/cihaz kaydı mobil cihaz Yönetimi'nde gerekli olup olmadığını denetler.
10. Windows hello aygıt hello kuruluşunuzun dizininde Azure AD'de kaydeder ve uygun durumlarda mobil cihaz Yönetimi'nde kaydeder.
11. Yönetilen bir kullanıcı varsa, Windows hello otomatik oturum açma işlemi aracılığıyla toohello masaüstüne alır.
12. Bir Federasyon kullanıcısı varsa, yönlendirilmiş toohello Windows oturum açma kimlik bilgilerinizi tooenter ekran.

> [!NOTE]
> Merhaba Windows bir şirket içi Windows Server Active Directory etki alanına katılma out-of-box deneyimi desteklenmiyor. Toojoin bilgisayar tooa etki alanı planlıyorsanız, bu nedenle, hello bağlantı seçmelisiniz **Windows'u yerel hesapla ayarlamak** yerine. Önce uyguladığınız gibi bilgisayarınızda hello etki alanından hello ayarları sonra birleştirebilirsiniz.
> 
> 

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

