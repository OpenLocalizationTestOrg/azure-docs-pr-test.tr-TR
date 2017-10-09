---
title: "Azure Active Directory B2C: Self Servis parola sıfırlama | Microsoft Docs"
description: "Azure Active Directory B2C içinde tüketicileriniz için nasıl tooset Self Servis parola sıfırlama gösteren bir konu"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: Self Servis parola sıfırlama tüketicileriniz ayarlama
Merhaba ile Self Servis parola sıfırlama özelliği, (kaydolan yerel hesaplar için) tüketicileriniz üzerinde kendi parolalarını sıfırlayabilir. Özellikle, uygulamanızın düzenli olarak kullanan tüketicilerin milyonlarca varsa bu destek ekibiniz üzerindeki hello yük önemli ölçüde azaltır. Şu anda yalnızca bir kurtarma yöntemi olarak doğrulanmış e-posta adresini kullanarak destekliyoruz. Ek kurtarma yöntemleri (doğrulanmış telefon numarası, güvenlik soruları, vb.) hello gelecekte ekleyeceğiz.

> [!NOTE]
> Bu makale tooself hizmeti parolasını geçerlidir hello bir oturum açma ilkesi bağlamında kullanılan sıfırlama. Tam olarak özelleştirilebilir parola sıfırlama ilkeleri uygulamanızdan çağrılan gerekirse bkz [bu makalede](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Varsayılan olarak, Self Servis parola dizininize sahip olmaz sıfırlama açık. Kullanım hello adımları tooturn, üzerinde:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Abonelik Yöneticisi hello gibi. Aynı iş veya Okul hesabı veya aynı Microsoft hesabını dizininize toocreate kullanılan hello hello budur.
2. Merhaba hello sol taraftaki gezinti çubuğunda toohello Active Directory uzantısına gidin.
3. Dizininizi hello altında Bul **Directory** sekmesinde ve tıklatın.
4. Merhaba tıklatın **yapılandırma** sekmesi.
5. Toohello aşağı **kullanıcı parolası sıfırlama İlkesi** bölümü ve iki durumlu hello **kullanıcılar parola sıfırlama için etkin** çok seçenek**Evet**. Bu hello fark **alternatif e-posta adresi** seçeneğini işaretli; olduğu gibi bırakın.
   
    ![Self servis parola sıfırlama](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Tıklatın **kaydetmek** hello sayfanın hello sonundaki. İşiniz bittiğinde!

tootest, kullanım hello "Şimdi Çalıştır" özelliğini yerel hesaplar için kimlik sağlayıcısı olarak sahip tüm oturum açma İlkesi'ni tıklatın. Merhaba yerel hesap oturum açma (burada, bir e-posta adresi ve parola veya kullanıcı adı ve parola girin) tıklatın sayfa **hesabınıza erişemiyor?** tooverify hello müşteri deneyimi.

> [!NOTE]
> Merhaba Self Servis parola sıfırlama sayfaları hello kullanarak özelleştirilebilir [şirket markası özelliğini](../active-directory/active-directory-add-company-branding.md).
> 
> 

