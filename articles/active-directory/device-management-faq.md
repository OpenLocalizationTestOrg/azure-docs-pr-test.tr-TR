---
title: "aaaAzure Active Directory cihaz yönetimi ile ilgili SSS | Microsoft Docs"
description: "Azure Active Directory cihaz Yönetimi SSS."
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a>Azure Active Directory cihaz yönetimi ile ilgili SSS

**S: hello aygıt son kayıtlı. Kullanıcı bilgilerimi hello Azure portal'ın altında hello aygıt neden göremiyorum?**

**Y:** ile otomatik cihaz kaydı etki alanına katılan Windows 10 cihazları gösterme altında hello kullanıcı bilgileri.
Tüm cihazlar toouse PowerShell toosee gerekir. 

Yalnızca hello aşağıdaki cihazları hello kullanıcı bilgileri altında listelenmiştir:

- Birleştirilmiş Kurumsal olmayan tüm kişisel cihazlar 
- Tüm Windows 10 olmayan / Windows Server 2016 
- Tüm Windows dışı cihazlar 

---

**S: neden hello Azure portalında Azure Active Directory'de kayıtlı tüm hello cihazlar görebilirim değil mi?** 

**Y:** şu anda bulunmamaktadır hiçbir şekilde toosee tüm kayıtlı cihazlar hello Azure portalı. Tüm cihazlar Azure PowerShell toofind kullanabilirsiniz. Daha fazla ayrıntı için bkz: Merhaba [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet'i.

--- 

**Hangi hello cihaz kayıt durumu hello istemcisinin nasıl bilebilirim s: mi?**

**Y:** hello cihaz kayıt durumu bağlıdır:

- Hangi hello cihaz
- Nasıl kaydedildi 
- Tooit ilgili tüm ayrıntıları. 
 

---

**I silinmiş bir aygıt neden olduğundan hello Azure portalı veya Windows PowerShell kullanarak hala kayıtlı olarak listeleniyor?**

**Y:** bu tasarım gereğidir. Merhaba aygıt erişim tooresources hello buluta sahip olmaz. Tooremove hello aygıt istiyorsanız ve yeniden kaydettirin işlemi el ile Merhaba cihazda gerçekleştirilen toobe olması gerekir. 

Windows 10 ve Windows Server 2016'de, şirket içi AD etki alanına katılmış:

1.  Merhaba komut istemini yönetici olarak açın.

2.  Türü`dsregcmd.exe /debug /leave`

3.  Oturumu kapatın ve yeniden hello aygıtı kaydeden tootrigger hello de zamanlanmış görevi açın. 

Şirket içi diğer Windows platformları için AD etki alanına katılmış:

1.  Merhaba komut istemini yönetici olarak açın.
2.  `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"` yazın.
3.  `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"` yazın.

---

**Azure Portalı'nda yinelenen aygıt girişleri neden görüyor musunuz?**

**A:**

-   Windows 10 ve Windows Server 2016 yinelenen denemeleri toounjoin olan ve yeniden katılabilir, aynı aygıt hello için yinelenen giriş olabilir. 

-   Ekleme iş veya Okul hesabınızla kullandıysanız, eklemek iş veya Okul hesabını kullanan her bir windows kullanıcı hello ile yeni bir cihaz kaydı oluşturmak aynı aygıt adı.

-   Şirket içi diğer Windows platformları AD etki alanına katılmış otomatik kayıt kullanarak yeni bir cihaz kaydı ile Merhaba oluşturur hello cihazda oturum her etki alanı kullanıcı için aynı aygıt adı. 

-   Temizlendiğinde bir AADJ makine yeniden yükledikten ve hello ile aynı yeniden birleştirilmiş adı, başka bir kayıtla hello olarak gösterilir aynı aygıt adı.

---

**Neden kullanıcı hello Azure portal devre dışı bırakan bir aygıttan hala kaynaklarına erişebilir mi?**

**Y:** uygulanan revoke toobe tooan saattir yukarı alabilir.

>[!Note] 
>Kaybolan cihazlarda, kullanıcılar hello aygıt erişemiyor hello aygıt tooensure silme öneririz. Daha fazla ayrıntı için bkz: [cihazları Yönetim için ıntune'a kaydetme](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**Kullanıcılarım "Buradan var. alınamıyor" neden görüyor musunuz?**

**Y:** belirli koşullu erişim kuralları toorequire belirli cihaz durumu yapılandırdıktan ve hello cihaz hello ölçütleri karşılamadığında, kullanıcıların engellenir ve bu ileti görür. Merhaba aygıt lütfen hello kuralları değerlendirin ve bu ileti mümkün toomeet hello ölçütleri tooavoid içindir.

---


**S: hello cihaz kaydını hello kullanıcı bilgisi'hello Azure portal'ın altında görmek ve hello durumu hello istemcide kayıtlı olarak görebilirsiniz. Koşullu erişim kullanarak ayarlarım doğru miyim?**

**Y:** hello aygıt kaydı (DeviceID) hello Azure portal durumuna gerekir eşleşen hello istemci ve koşullu erişim için herhangi bir değerlendirme ölçütleri karşılayan. Daha fazla ayrıntı için bkz: [Azure Active Directory cihaz kaydı ile çalışmaya başlama](active-directory-device-registration.md).

---

**Neden bir "kullanıcı adı veya parola, yanlış" iletisi alıyorum bir aygıt için t yalnızca tooAzure AD katılmış?**

**Y:** bu senaryo için yaygın nedenler şunlardır:

- Kullanıcı kimlik bilgilerinizi artık geçerli değildir.

- Bilgisayarınızı Azure Active Directory ile oluşturulamıyor toocommunicate ' dir. Tüm ağ bağlantısı sorunlarını denetleyin.

- Hello Azure AD katılım Önkoşullar karşılanmadı. Lütfen başlangıç adımları izlediğinizden emin olun [bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-overview.md).  

- Federe oturum açma bilgileri, Federasyon sunucusu toosupport bir WS-Trust etkin uç noktası gerektirir. 

---

**S: neden hello görüyorum "... Oops bir hata oluştu!" çalıştığımda iletişim Bilgisayarımda katılma?**

**Y:** bu bir Intune ile Azure Active Directory kaydını ayarlama sonucudur. Daha fazla ayrıntı için bkz: [Windows cihaz yönetimini ayarlama](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**Neden bir PC başarısız hata bilgilerini almadım rağmen my girişimi toojoin mı?**

**Y:** bir nedeni bu hello kullanıcı toohello aygıtı hello yerleşik Yönetici hesabını kullanarak oturum olması. Lütfen farklı bir yerel hesap Azure Active Directory katılım toocomplete hello Kurulum kullanmadan önce oluşturun. 

---

**S: otomatik cihaz kaydı hello kurulumu için yönergeler nereden bulabilirim?**

**Y:** ayrıntılı yönergeler için bkz: [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**S: sorun giderme nereden bulabilirim hello otomatik cihaz kaydı hakkında bilgi mi?**

**Y:** sorun giderme bilgileri için bkz:

- [Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme](active-directory-device-registration-troubleshoot-windows.md)

- [Windows alt düzey istemciler için alanına katılmış bilgisayarları tooAzure AD otomatik kaydı etki alanının sorun giderme](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

