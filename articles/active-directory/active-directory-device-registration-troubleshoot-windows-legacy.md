---
title: "aaaTroubleshooting hello otomatik kaydı Azure AD etki alanına katılmış bilgisayarları Windows alt düzey istemciler için | Microsoft Docs"
description: "Sorun giderme Hello otomatik kaydı Azure AD etki alanı bilgisayarları Windows alt düzey istemciler için katıldı."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Windows alt düzey istemciler için alanına katılmış bilgisayarları tooAzure AD otomatik kaydı etki alanının sorun giderme 

Bu konuda geçerli yalnızca toohello istemcileri aşağıdaki gibidir: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Windows 10 veya Windows Server 2016 için bkz: [alanına katılmış bilgisayarları tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kaydı sorun giderme](active-directory-device-registration-troubleshoot-windows.md).

Bu konu, etki alanına katılmış aygıtlar otomatik kaydı nda olarak açıklanan yapılandırmış olduğunuz varsayılır, [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-device-registration-get-started.md).
 
Bu konu, nasıl tooresolve olası sorunlar konusunda yönergeler sorun giderme konusunda sağlar.  
Bazı şeyleri toonote başarılı sonuç için: 

- Bu istemciler üzerinde Azure AD kaydını kullanıcı/cihaz değil. Örnek: jdoe ve jharnett toothis aygıtta oturum açarsanız, hello kullanıcı bilgisi sekmesinde bu kullanıcılardan her biri için ayrı bir kayıt (DeviceID) oluşturulur.  

- Kayıt hello kutusu dışında bu istemciler, oturum açma veya kilit ve kilidini yapılandırılmış tootry değil ve bu Görev Zamanlayıcı görevi kullanılarak tetiklenir 5 dakikalık gecikme olabilir. 

- Bir yeniden yükleyin hello işletim sistemi veya el ile kaydı ve yeniden kaydolun üzerinde Azure AD yeni bir kayıt oluşturabilir ve birden çok giriş hello içinde hello kullanıcı bilgileri sekmesi altında Azure portal neden olur. 


## <a name="step-1-retrieve-hello-registration-status"></a>1. adım: hello kayıt durumunu alma 

**tooverify hello kayıt durumu:**  

1. Bir yönetici olarak açın hello komut istemi 

2. Türü`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Bu komut hello birleşim durumu hakkında daha fazla ayrıntı sağlayan bir iletişim kutusu görüntüler.

![Windows için çalışma alanına katılma](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>2. adım: hello kayıt durumunu değerlendirme 

Merhaba birleştirme başarılı olmadıysa hello iletişim kutusu oluştu hello sorun hakkında ayrıntılar sağlar.

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
  
**başarısız bir kayıt için Hello en yaygın nedenler şunlardır:** 

- Bilgisayarınız üzerinde değil hello kuruluşunuzun iç ağ ya da bir VPN bağlantısı tooan olmadan şirket içi AD etki alanı denetleyicisi.

- Yerel bilgisayar hesabı olan tooyour bilgisayarında günlüğe kaydedilir. 

- Hizmet yapılandırma sorunları: 

  - Merhaba Federasyon sunucusu yapılandırılmış toosupport bırakıldı **WIAORMULTIAUTHN**. 

  - Merhaba bilgisayar için ait olduğu hello AD ormanındaki Azure AD'de tooyour doğrulanmış etki alanı adına işaret eden bir hizmet bağlantı noktası nesne yok.

  - Bir kullanıcı aygıtları hello sınırına ulaştı. Azure Active Directory cihaz kaydı ile çalışmaya başlama bakın.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi için bkz: Merhaba [otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md) 
