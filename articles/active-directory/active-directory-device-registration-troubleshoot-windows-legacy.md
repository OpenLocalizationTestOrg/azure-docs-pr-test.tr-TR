---
title: "Windows alt düzey istemciler için katılmış bilgisayarları Azure AD etki alanının otomatik kayıt sorunlarını giderme | Microsoft Docs"
description: "Azure AD etki alanının otomatik kayıt sorunlarını giderme bilgisayarları Windows alt düzey istemciler için katıldı."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a>Otomatik kaydı etki alanının sorun giderme bilgisayarlar, alt düzey istemciler için Windows Azure AD alanına katılmış 

Bu konuda, yalnızca aşağıdaki istemciler için geçerlidir: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Windows 10 veya Windows Server 2016 için bkz: [etki alanının otomatik kaydı sorun giderme alanına katılmış bilgisayarları Azure AD ile – Windows 10 ve Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-device-registration-get-started.md).
 
Bu konu, sorun giderme ile ilgili olası sorunları gidermek nasıl yönergelerini sağlar.  
Başarılı sonuç için dikkat edilecek bazı noktalar: 

- Bu istemciler üzerinde Azure AD kaydını kullanıcı/cihaz değil. Örnek: jdoe ve jharnett bu cihazda oturum açarsanız kullanıcı bilgisi sekmesinde bu kullanıcılardan her biri için ayrı bir kayıt (DeviceID) oluşturulur.  

- Kayıt kutunun dışında bu istemciler, oturum açma veya kilit ve kilidini denemek için yapılandırılır ve bu Görev Zamanlayıcı görevi kullanılarak tetiklenir 5 dakikalık gecikme olabilir. 

- Bir yeniden yükleyin ve işletim sistemi veya bir el ile kaydı yeniden kaydettirin üzerinde Azure AD yeni bir kayıt oluşturabilir ve Azure portalında kullanıcı bilgileri sekmesi altında birden çok giriş neden olur. 


## <a name="step-1-retrieve-the-registration-status"></a>1. adım: kayıt durumunu alma 

**Kayıt durumunu doğrulamak için:**  

1. Komut istemini yönetici olarak açın 

2. Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Bu komut, birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a>2. adım: kayıt durumunu değerlendirme 

Birleşim başarılı olmadıysa iletişim kutusu oluştu sorun hakkında ayrıntılar sağlar.

**En yaygın sorunları şunlardır:**

- Yanlış yapılandırılmış AD FS veya Azure AD

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Bir etki alanı kullanıcısı olarak imzalı değil

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Bir kotasına ulaşıldı

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Hizmeti yanıt vermiyor 

    ![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Olay günlüğünde altında durum bilgisi bulabilirsiniz **uygulamaları ve Hizmetleri Log\Microsoft-çalışma alanına katılma**.
  
**Başarısız bir kayıt için en yaygın nedenler şunlardır:** 

- Bilgisayarınız bir şirket içi bağlantısı olmadan VPN'yi veya kuruluşunuzun iç ağ üzerinde değil AD etki alanı denetleyicisi.

- Bilgisayarınıza yerel bilgisayar hesabı ile oturum. 

- Hizmet yapılandırma sorunları: 

  - Federasyon sunucusunu desteklemek üzere yapılandırılmış **WIAORMULTIAUTHN**. 

  - Bilgisayar için ait olduğu AD ormanında Azure AD'de doğrulanmış etki alanı adınızı işaret eden bir hizmet bağlantı noktası nesne yok.

  - Bir kullanıcı cihaz sınırına ulaştı. Azure Active Directory cihaz kaydı ile çalışmaya başlama bakın.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md) 
