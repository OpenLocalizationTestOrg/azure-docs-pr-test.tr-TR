---
title: "aaaTroubleshooting karma Azure Active Directory birleştirilmiş alt düzey aygıtları | Microsoft Docs"
description: "Karma Azure Active Directory sorun giderme alt düzey aygıtları katıldı."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Alt düzey aygıtları birleştirilmiş karma Azure Active Directory sorun giderme 

Bu konuda geçerli yalnızca toohello cihazları aşağıdaki gibidir: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Windows 10 veya Windows Server 2016 için bkz: [sorun giderme karma Azure Active Directory'ye katılmış Windows 10 ve Windows Server 2016 cihazları](device-management-troubleshoot-hybrid-join-windows-current.md).

Bu konu, sahibi olduğunuzu varsayar [yapılandırılmış karma Azure Active Directory'ye katılmış cihazları](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello senaryolar:

- Cihaz temelli koşullu erişim

- [Kurumsal Dolaşım ayarları](active-directory-windows-enterprise-state-roaming-overview.md)

- [İş İçin Windows Hello](active-directory-azureadjoin-passport-deployment.md) 





Bu konu, nasıl tooresolve olası sorunlar konusunda yönergeler sorun giderme konusunda sağlar.  

**Bilmeniz gerekenler:** 

- Hello en fazla kullanıcı başına aygıtları Aygıt odaklı sayısıdır. Örneğin, varsa *jdoe* ve *jharnett* oturum açma tooa aygıt ayrı bir kayıt (DeviceID) Merhaba, bunların her biri için oluşturulduğunda **kullanıcı** bilgileri sekmesi.  

- Merhaba ilk kaydı / katılma aygıtların yapılandırılmış tooperform girişiminde oturum açma veya kilitleme veya kilidini. Bir Görev Zamanlayıcı görevi tarafından tetiklenen 5 dakikalık gecikme olabilir. 

- Merhaba işletim sistemi veya el ile yeniden unregister ve yeniden kaydolun yeni bir kayıt üzerinde Azure AD oluşturup hello kullanıcı bilgileri sekmesi altında birden çok giriş sonuçlarında hello Azure portalı. 


## <a name="step-1-retrieve-hello-registration-status"></a>1. adım: hello kayıt durumunu alma 

**tooverify hello kayıt durumu:**  

1. Bir yönetici olarak açın hello komut istemi 

2. Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Bu komut hello birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>2. adım: hello karma Azure AD katılım durumunu değerlendirme 

Merhaba karma Azure AD birleştirme başarılı olmadıysa hello iletişim kutusu oluştu hello sorun hakkında ayrıntılar sağlar.

**Merhaba en sık karşılaşılan sorunları şunlardır:**

- Yanlış yapılandırılmış AD FS veya Azure AD

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Bir etki alanı kullanıcısı olarak imzalı değil

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Bir kotasına ulaşıldı

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Merhaba hizmeti yanıt vermiyor 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Merhaba olay günlüğünde altında hello durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.
  
**Merhaba başarısız karma Azure AD birleştirme en yaygın nedenleri şunlardır:** 

- Bilgisayarınız üzerinde değil hello kuruluşunuzun iç ağ ya da bir VPN bağlantısı tooan olmadan şirket içi AD etki alanı denetleyicisi.

- Yerel bilgisayar hesabı olan tooyour bilgisayarında günlüğe kaydedilir. 

- Hizmet yapılandırma sorunları: 

  - Merhaba Federasyon sunucusu yapılandırılmış toosupport bırakıldı **WIAORMULTIAUTHN**. 

  - Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret eden bir hizmet bağlantı noktası nesne yok.

  - Bir kullanıcı aygıtları hello sınırına ulaştı. 

## <a name="next-steps"></a>Sonraki adımlar

Merhaba soruları için bkz [aygıt yönetimi hakkında SSS](device-management-faq.md)  
