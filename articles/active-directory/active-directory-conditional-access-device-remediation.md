---
title: "aaaYou alınamıyor var. hello edilecektir Azure portalından bir Windows aygıtının | Microsoft Docs"
description: "Burada yapamazsınız öğrenin get buradan gelir vardır ve bu iletişim kutusuna çalıştıran tooavoid iade edilemedi."
services: active-directory
keywords: "cihaz temelli koşullu erişim, cihaz kaydı, cihaz kaydını etkinleştirme, cihaz kaydı ve MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Bir Windows cihazında bu uygulamaya buradan erişemezsiniz

Örneğin, kuruluşunuzun SharePoint Online intranetine erişim denemesi sırasında, *bu uygulamaya buradan erişemezsiniz* ifadesini içeren bir sayfa ile karşılaşabilirsiniz. Yöneticiniz belirli koşullar altında erişim tooyour kurumunuzun kaynaklarına engelleyen bir koşullu erişim ilkesi yapılandırmış için bu sayfayı görüyorsunuz. Gerekli toocontact yardım masasına veya bu sorun çözüldüğünde, yönetici tooget olabilir ancak kendiniz ilk deneyebileceğiniz birkaç şey vardır.

Kullanıyorsanız bir **Windows** aygıt, aşağıdaki hello kontrol etmelidir:

- Desteklenen bir tarayıcı mı kullanıyorsunuz?

- Cihazınızda desteklenen bir Windows sürümü çalıştırıyor musunuz?

- Cihazınız uyumlu mu?






## <a name="supported-browser"></a>Desteklenen tarayıcı

Yöneticiniz bir koşullu erişim ilkesi yapılandırdıysa, kuruluşunuzun kaynaklarına yalnızca desteklenen bir tarayıcı kullanarak erişebilirsiniz. Bir Windows cihazda yalnızca **Internet Explorer** ve **Edge** desteklenir.

Merhaba hata sayfasının ayrıntıları bölümünü hello bakarak tooan desteklenmeyen tarayıcı nedeniyle bir kaynağa erişemiyor olup olmadığını, kolayca tanımlayabilirsiniz:

![Desteklenmeyen tarayıcılar için "Oraya buradan ulaşamazsınız" iletisi](./media/active-directory-conditional-access-device-remediation/02.png "Senaryo")

Merhaba yalnızca düzeltme toouse Merhaba uygulaması cihaz platformunuz için destekleyen bir tarayıcı ' dir. Desteklenen tarayıcıların tam listesi için bkz. [desteklenen tarayıcılar](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Desteklenen Windows sürümleri

Merhaba aşağıdaki hello Windows işletim sistemi, Cihazınızda hakkında doğru olması gerekir: 

- Cihazınızda bir Windows masaüstü işletim sistemi çalıştırıyorsanız, 7 veya üzeri toobe Windows gerekir.
- Cihazınızda bir Windows server işletim sistemi çalıştırıyorsanız, Windows Server 2008 R2 toobe gerekiyor veya sonraki bir sürümü. 


## <a name="compliant-device"></a>Uyumlu cihaz

Yöneticiniz erişim tooyour kuruluşunuzun kaynaklardan yalnızca uyumlu cihazların izin veren bir koşullu erişim ilkesi yapılandırılmış. Cihazınızı ya da birleştirilmiş tooyour olmalıdır uyumlu toobe şirket içi Active Directory veya tooyour Azure Active Directory birleştirilmiş.

Bir kaynak hello hata sayfasının ayrıntıları bölümünü hello bakarak uyumlu değil tooa aygıt son erişemiyor olup olmadığını, kolayca tanımlayabilirsiniz:
 
![Kaydedilmemiş cihazlar için "Oraya buradan ulaşamazsınız" iletileri](./media/active-directory-conditional-access-device-remediation/01.png "Senaryo")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>Birleşik aygıt tooan içi Active Directory mi?

**Cihazınızı katılmışsa tooan Active Directory, kuruluşunuzda şirket içi:**

1. İş hesabınızı (Active Directory hesabınızla) kullanarak tooWindows içinde oturum emin olun.
2. Bir sanal özel ağ (VPN) veya DirectAccess üzerinden iç kurumsal ağa tooyour bağlayın.
3. Bağlantı kurulduktan sonra basın hello Windows logosu tuşu + L hello anahtar toolock Windows oturumunuzu.
4. İş hesabınızın kimlik bilgilerini girerek Windows oturumunuzun kilidini açın.
5. Bir dakika bekleyin ve ardından tooaccess hello uygulaması veya hizmeti yeniden deneyin.
6. Görürseniz aynı hello hello sayfasında, **daha fazla ayrıntı** bağlamak ve ardından hello ayrıntılarla yöneticinize başvurun.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>Birleştirilmemiş aygıt tooan içi Active Directory mi?

Cihazınızı katılmadı tooan şirket içi Active Directory ve Windows 10 çalıştıran, iki seçeneğiniz vardır:

* Azure AD'ye Katılım’ı çalıştırmak
* Çalışmanızı ekleyin veya Okul hesabı tooWindows

Bu iki seçenek arasındaki farklar hakkında bilgi edinmek için bkz. [Çalışma alanınızda Windows 10 cihazlarını kullanma](active-directory-azureadjoin-windows10-devices.md).  
Cihazınız:

- Tooyour kuruluş ait, Azure AD katılım çalıştırmanız gerekir.
- Kişisel bir cihazı veya bir Windows phone çalışmanızı ekleyin veya Okul hesabı tooWindows gerekir 



#### <a name="azure-ad-join-on-windows-10"></a>Windows 10’da Azure AD Join

Merhaba, aygıt tooAzure AD olan adımları toojoin hello sürüm olarak Windows 10 üzerinde çalıştırılan bağlıdır. toodetermine hello hello çalıştırmak, Windows 10 işletim sistemi sürümü **winver** komutu: 

![Windows sürümü](./media/active-directory-conditional-access-device-remediation/03.png )


**Windows 10 Yıldönümü Güncelleştirmesi (Sürüm 1607):**

1. Açık hello **ayarları** uygulama.
2. **Hesaplar** > **İş veya okul erişimi** öğesine tıklayın.
3. **Bağlan**'a tıklayın.
4. Tıklatın **bu aygıt tooAzure AD katılma**.
5. Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.
6. Oturumu kapatın ve iş hesabınızla oturum açın.
7. Tooaccess hello uygulama yeniden deneyin.

**Windows 10 Kasım 2015 Güncelleştirmesi (Sürüm 1511):**

1. Açık hello **ayarları** uygulama.
2. **Sistem** > **Hakkında** öğesine tıklayın.
3. **Azure AD'ye Katıl**’a tıklayın.
4. Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.
5. Oturumu kapatın ve ardından iş hesabınızla (Azure AD hesabınız) oturum açın.
6. Tooaccess hello uygulama yeniden deneyin.


#### <a name="workplace-join-on-windows-81"></a>Windows 8.1’de Workplace Join

Cihazınızı etki alanına katılmış değil ve bir çalışma alanına katılma Windows 8.1, toodo çalıştıran ve Microsoft Intune kaydederseniz adımları izleyerek hello:

1. **PC Ayarları**'nı açın.
2. **Ağ** > **Çalışma Alanı**’na tıklayın.
3. **Katıl**’a tıklayın.
4. Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.
5. **Aç**’a tıklayın.
6. Tooaccess hello uygulama yeniden deneyin.



#### <a name="add-your-work-or-school-account-toowindows"></a>Çalışmanızı ekleyin veya Okul hesabı tooWindows 


**Windows 10 Yıldönümü Güncelleştirmesi (Sürüm 1607):**

1. Açık hello **ayarları** uygulama.
2. **Hesaplar** > **İş veya okul erişimi** öğesine tıklayın.
3. **Bağlan**'a tıklayın.
4. Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.
5. Tooaccess hello uygulama yeniden deneyin.


**Windows 10 Kasım 2015 Güncelleştirmesi (Sürüm 1511):**

1. Açık hello **ayarları** uygulama.
2. **Hesaplar** > **Hesaplarınız** öğesine tıklayın.
3. **İş veya okul hesabı ekle**’ye tıklayın.
4. Tooyour kuruluş kimliğini, çok faktörlü kimlik doğrulaması istenir ve sonra görüntülenen hello adımları sağlayın.
5. Tooaccess hello uygulama yeniden deneyin.





## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory koşullu erişimi](active-directory-conditional-access.md)

