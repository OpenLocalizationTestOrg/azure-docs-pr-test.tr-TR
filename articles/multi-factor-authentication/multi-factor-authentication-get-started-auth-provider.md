---
title: "aaaGet Azure multi-Factor Auth sağlayıcısını kullanmaya | Microsoft Docs"
description: "Bilgi nasıl toocreate Azure multi-Factor Auth sağlayıcısı."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Azure Multi-Factor Auth Sağlayıcısını kullanmaya başlama
İki adımlı doğrulama, Azure Active Directory’ye sahip genel yöneticiler ve Office 365 kullanıcıları için varsayılan olarak kullanılabilir durumdadır. Ancak, tootake avantajlarından istiyorsanız [Gelişmiş Özellikler](multi-factor-authentication-whats-next.md) hello tam sürüm Azure çok faktörlü kimlik doğrulama (MFA) satın sonra.

Azure multi-Factor Auth sağlayıcısı kullanılan tootake özelliklerinden hello MFA tam sürümünü Azure tarafından sağlanan. **Azure MFA, Azure AD Premium veya Enterprise Mobility + Security (EMS) lisansı olmayan** kullanıcılara yöneliktir.  Azure MFA, Azure AD Premium ve EMS hello varsayılan olarak Azure mfa tam sürümünü içerir. Lisanslarınız varsa bir Azure Multi-Factor Auth Sağlayıcısına ihtiyacınız yoktur.

Bir Azure multi-Factor Auth sağlayıcısı gerekli toodownload hello SDK ' dir.

> [!IMPORTANT]
> toodownload SDK Merhaba, Azure MFA, AAD Premium veya EMS lisansları olsa bile toocreate Azure multi-Factor Auth sağlayıcısı gerekir.  Bu amaç için Azure multi-Factor Auth sağlayıcısı oluşturmak ve lisansları zaten varsa, emin toocreate hello sağlayıcısı hello ile olması **etkin kullanıcı başına** modeli. Ardından, hello Azure MFA, Azure AD Premium veya EMS lisansları içeren hello sağlayıcısı toohello dizini bağlayın. Bu yapılandırma, sahip olduğunuz lisans hello sayısından iki aşamalı doğrulamayı gerçekleştirme daha fazla benzersiz kullanıcı varsa, yalnızca faturalandırılır olmasını sağlar.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Azure Multi-Factor Auth Sağlayıcısı nedir?

Azure multi-Factor Authentication için lisans yoksa, kullanıcılarınız için bir kimlik doğrulama sağlayıcısı toorequire iki aşamalı doğrulamayı oluşturabilirsiniz. Özel uygulama geliştirme ve tooenable Azure MFA istiyorsanız, bir kimlik doğrulama sağlayıcısı oluşturmanız ve [hello SDK Yükle](multi-factor-authentication-sdk.md).

İki tür kimlik doğrulama sağlayıcıları ve Azure aboneliğinize nasıl doludur geçici hello fark ise. Merhaba başına kimlik doğrulama seçeneği bir ay içinde kiracınız karşı gerçekleştirilen kimlik doğrulama hello sayısını hesaplar. Bu, yalnızca gereken durumlarda (örneğin, özel bir uygulama için MFA'yı gerekli kıldıysanız) kimlik doğrulamasını kullanan belirli sayıda kullanıcınızın olması halinde en iyi seçenektir. Merhaba kullanıcı başına seçeneği bir ay içinde iki aşamalı doğrulamayı gerçekleştirmek kişiler kiracınızda hello sayısını hesaplar. Lisansına sahip olan bazı kullanıcılar varsa, ancak tooextend MFA toomore kullanıcıların Lisans sınırlarının dışına gerekir bu en iyi bir seçenektir.

## <a name="create-a-multi-factor-auth-provider"></a>Multi-Factor Auth Sağlayıcısı oluşturma
Aşağıdaki adımları toocreate Azure multi-Factor Auth sağlayıcısı hello kullanın. Azure çok faktörlü kimlik doğrulama sağlayıcıları yalnızca hello Klasik Azure portalı oluşturulabilir. Toohello Klasik Azure portalında oturum açın, Azure AD kiracınız olduğundan emin toomake denetleyin. [bir Azure aboneliği ile ilişkili](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) yönetici olarak.
2. Merhaba solda seçin **Active Directory**.
3. Merhaba üstünde hello Active Directory sayfasında seçin **çok faktörlü kimlik doğrulama sağlayıcıları**.
   
   ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Merhaba altında tıklatın **yeni**.
   
   ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. Uygulama Hizmetleri altında **Multi-Factor Auth Sağlayıcısı**'nı seçin.
   
   ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. **Hızlı Oluştur**’u seçin.
   
   ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Hello aşağıdaki alanları doldurun ve seçin **oluşturma**.
   1. **Ad** – hello hello multi-Factor Auth sağlayıcısının adı.
   2. **Kullanım Modeli**: İki seçenekten birini belirleyin:
      * Kimlik Doğrulaması Başına – kimlik doğrulaması başına ücretlendirilen satın alma modeli. Genellikle tüketiciyle karşılaşan uygulamada Azure Multi-Factor Authentication kullanan senaryolar için kullanılır.
      * Etkin Kullanıcı Başına - etkin kullanıcı başına ücretlendirilen satın alma modeli. Genellikle Office 365 gibi çalışan erişim tooapplications için kullanılır. Azure MFA için zaten lisansı olan kullanıcılarınız varsa bu seçeneği belirleyin.
   3. **Dizin** – hello Azure Active Directory Kiracı çok faktörlü kimlik doğrulama sağlayıcısı ile ilişkili o hello. Merhaba aşağıdakilere dikkat edin:
      * Azure AD directory toocreate multi-Factor Auth sağlayıcısı gerekli değildir. Bu kutu yalnızca toodownload hello Azure çok faktörlü kimlik doğrulama sunucusu veya SDK planlama, boş bırakın.
      * Merhaba multi-Factor Auth sağlayıcısı bir Azure AD directory tootake avantajlarından Gelişmiş Özellikler hello ile ilişkilendirilmiş olması gerekir.
      * Herhangi bir Azure AD dizini ile yalnızca bir multi-Factor Auth sağlayıcısı ilişkili olabilir.  
      ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Tıkladığınızda oluşturmak, hello çok faktörlü kimlik doğrulama sağlayıcısı oluşturulur ve görmelisiniz belirten iletiyi: **çok faktörlü kimlik doğrulama sağlayıcısı başarıyla oluşturuldu**. **Tamam**’a tıklayın.  
   
   ![MFA Sağlayıcısı oluşturma](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Multi-Factor Auth Sağlayıcınızı yönetme

Merhaba kullanım değiştiremezsiniz model (etkin kullanıcı başına veya kimlik doğrulaması başına) MFA sağlayıcısı oluşturulduktan sonra. Ancak, hello MFA sağlayıcısı silin ve farklı kullanım modeli biriyle oluşturun.

Merhaba geçerli multi-Factor Auth sağlayıcısı Azure AD dizini (Azure AD kiracısı olarak da bilinir) ile ilişkili ise, güvenli bir şekilde hello MFA sağlayıcısı silin ve bağlantılı toohello aynı Azure AD kiracısı olan bir oluşturun. Alternatif olarak, MFA için etkinleştirilen tüm kullanıcılar yeterli MFA, Azure AD Premium veya Enterprise Mobility + güvenlik (EMS) lisansı toocover satın aldıysanız, hello MFA sağlayıcısı tamamen silebilirsiniz.

MFA sağlayıcınızı bağlantılı tooan Azure AD Kiracı değil veya hello yeni MFA sağlayıcısı tooa farklı Azure AD Kiracı bağlamak, kullanıcı ayarlarını ve yapılandırma seçenekleri aktarılmaz. Ayrıca, Azure MFA sunucuları varolan aracılığıyla oluşturulan etkinleştirme kimlik bilgilerini kullanarak yeniden toobe yeni MFA sağlayıcısı hello. Merhaba MFA sunucuları toolink yeniden etkinleştirme bunları toohello yeni MFA sağlayıcısı telefon araması ve kısa mesaj kimlik doğrulamasını, ancak mobil uygulama bildirimleri hello mobil uygulama etkinleştirme kadar tüm kullanıcılar için çalışma durduracak etkilemez.

## <a name="next-steps"></a>Sonraki adımlar

[Merhaba multi-Factor Authentication SDK'sı yükle](multi-factor-authentication-sdk.md)

[Multi-Factor Authentication ayarlarını yapılandırma](multi-factor-authentication-whats-next.md)
