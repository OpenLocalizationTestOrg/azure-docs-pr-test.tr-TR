---
title: "etki alanına katılmış Windows cihazlarının Azure Active Directory ile aaaHow tooconfigure otomatik kayıt | Microsoft Docs"
description: "Etki alanına katılmış Windows cihazları tooregister, Azure Active Directory ile otomatik olarak ve sessiz bir şekilde ayarlayın."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydına başlarken

Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için hello temelidir. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hello hello kullanıcı oturum açtığında kullanılan tooauthenticate hello cihaz olan bir kimliğe sahip cihazı sağlar. Kimliği doğrulanmış hello cihaz ve hello cihazın hello öznitelikleri hello bulutta ve şirket içi barındırılan uygulamalar için kullanılan tooenforce koşullu erişim ilkeleri olabilir.

Microsoft Intune gibi bir mobil cihaz birleştirildiğinde çözümü ile birleştirildiğinde Azure Active Directory'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar. Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.
Azure Active Directory cihaz kaydı Azure Active Directory cihaz kaydı tarafından etkinleştirilen senaryolar iOS, Android ve Windows için destek içerir aygıtlar. hello Azure AD cihaz kaydı'nı kullanan bireysel senaryolar daha fazla özel gereksinime ve platform desteğine sahip olabilir. 

Bu senaryolar aşağıdaki gibidir:

- **Microsoft Intune ile Office 365 uygulamaları için koşullu erişim:** BT yöneticileri, koşullu erişim cihaz ilkeleri toosecure şirket kaynaklarına, hazırlayabilirsiniz, hello aynı zaman uyumlu cihazlara izin verme bilgi çalışanları sırada tooaccess hello Hizmetleri. Daha fazla bilgi edinmek için bkz. Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri.

- **Olan koşullu erişim tooapplications şirket içinde barındırılan:** olan uygulamalar Windows Server 2012 R2 ile AD FS toouse yapılandırılmış için kayıtlı cihazlara erişim ilkeleri ile kullanabilirsiniz. Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory cihaz kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory Cihaz Kaydı'nı ayarlama

toosetup cihaz kaydı, birden fazla seçeneği vardır:

- Aygıtlar kayıt birleştirilmiş tooAzure AD etki alanı. Bu konu hakkında daha fazla bilgi için kullanıcılar toojoin Azure AD etki alanı için gereken Azure AD katılımı ve hello ayarları hakkında daha fazla bilgi edinebilirsiniz.

- Cihazlar, kullanıcılar iş veya Okul tooWindows kişisel bir cihazı veya Mobil cihazların kaydı gerektiren tooa iş kaynaklarına bağlandığınızda hesapları kaydedilebilir. tooensure Bu, Azure AD cihaz kaydı hello Azure Portalı'nı etkinleştirmeniz gerekir. 

- Cihazlar, geleneksel etki alanına katılan makineler için otomatik cihaz kaydı kullanılarak kaydedilebilir. tooensure bunu ile otomatik cihaz kaydı devam etmeden önce ilk kurulum Azure AD Connect gerekir.

En son yönergeler için bkz: [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md).  
Ayrıca gözden geçirin ve da etkinleştirebilir veya Azure Active Directory'de Yönetici portalı hello kullanarak kayıtlı cihazları devre dışı bırakın.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Hello Azure Active Directory cihaz kaydı hizmetini etkinleştirme

**tooenable hello Azure Active Directory cihaz kayıt hizmeti:**

1.  İçinde toohello Microsoft Azure portalında yönetici olarak oturum açın.

2.  Merhaba soldaki bölmede bulunan seçin **Active Directory**.

3.  Merhaba dizin sekmesinde dizininizi seçin.

4.  **Yapılandır**'a tıklayın.

5.  Çok kaydırma**aygıtları**.

6.  Select tüm kullanıcılar için AZURE AD ile CİHAZLARINI KAYDEDEBİLİR.

7.  Merhaba en büyük sayı seçin aygıtların kullanıcı başına tooauthorize istiyor.

Office 365 için Microsoft Intune veya mobil cihaz yönetimi ile Merhaba kayıt cihaz kaydı gerektirir. Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** devre dışı bırakılır. Lütfen doğru şekilde yapılandırıldığından ve hello uygun lisans sahip olduğundan emin olun.

Varsayılan olarak, iki öğeli kimlik doğrulama hello hizmeti için etkin değil. Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir.

- Bu hizmet için iki öğeli kimlik doğrulama istemeden önce Azure Active Directory'de iki öğeli kimlik doğrulama sağlayıcısını yapılandırmak ve kullanıcı hesaplarınızı çok faktörlü kimlik doğrulaması için yapılandırmanız gerekir, bkz: çok faktörlü kimlik doğrulaması ekleme tooAzure Active Directory

- Windows Server 2012 R2 ile AD FS kullanıyorsanız, AD FS'de iki öğeli kimlik doğrulama modülünü yapılandırmanız gerekir, bkz: Active Directory Federasyon Hizmetleri ile çok faktörlü kimlik doğrulaması kullanarak.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Azure Active Directory'de cihaz nesnelerini görüntüleme ve yönetme

Hello Azure yönetici portalından görüntülemek, engelleme ve aygıtların engellemesini kaldırmak. Engellenen bir cihaz artık yapılandırılmış tooallow yalnızca kayıtlı aygıtların erişim tooapplications sahip olur.

**tooview ve Azure Active Directory'de cihaz nesnelerini yönetme:**
 
1.  Üzerinde toohello Microsoft Azure portalında yönetici olarak oturum açın.

2.  Merhaba soldaki bölmede bulunan seçin **Active Directory**.

3.  Dizininizi seçin.

4.  Seçin **kullanıcılar**. 

5.  Toosee hello cihazların istediğiniz hello kullanıcı'yı tıklatın.

6.  Seçin **aygıtları**.

7.  Seçin **kayıtlı cihazlar**.

Şimdi, gözden geçirin, engelleyebilir veya hello kullanıcının kayıtlı aygıtların engellemesini kaldırmak.
Şirket içi etki alanına katılmış ve otomatik olarak kaydedilmiş Windows 10 cihazları hello kullanıcılar sekmesi altında görünmez. Lütfen hello Get-MsolDevice PowerShell komut toofind tüm kurumsal aygıtları kullanın. 


## <a name="next-steps"></a>Sonraki adımlar

toosetup otomatik cihaz kaydı bkz [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md).


