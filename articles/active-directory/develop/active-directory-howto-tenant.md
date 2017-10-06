---
title: "Azure AD kiracısı aaaHow tooget | Microsoft Docs"
description: "Nasıl tooget bir Azure Active Directory kaydı ve uygulamaları oluşturmak için Kiracı."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Nasıl tooget bir Azure Active Directory Kiracı
Azure Active Directory'de (Azure AD) [kiracı](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant), bir kuruluşun temsilcisidir.  Merhaba, bir kuruluşun alır ve bunu Azure, Microsoft Intune veya Office 365 gibi Microsoft bulut hizmetine kaydolduğunda sahibi Azure AD hizmeti adanmış bir örneğidir.  Her Azure AD kiracısı benzersizdir ve diğer Azure AD kiracılarından ayrıdır.  

Bir kiracı hello kullanıcılar bir şirket ve hello hakkında bilgileri - kendi parolalarını, kullanıcı profili verilerini, izinlerini ve benzeri barındırır.  Ayrıca, grupları, uygulamalar ve tooan kuruluşa ve kuruluşun ilgili diğer bilgileri de içerir.

tooallow Azure AD kullanıcıların toosign tooyour uygulamada kendi Kiracı uygulamanızı kaydetmeniz gerekir.  Bir Azure AD kiracısında uygulama yayımlamak **tamamen ücretsizdir**.  Hatta çoğu geliştirici, deneme, geliştirme, hazırlama ve test etme amacıyla çeşitli kiracılar ve uygulamalar oluşturur.  Gelişmiş dizin özelliklerinden tootake istediklerinde kaydolun ve uygulamanızı kullanan kuruluşlar toopurchase lisansları isteğe bağlı olarak seçebilirsiniz.

Peki, Azure AD kiracısını nasıl edinebilirsiniz?  Merhaba işlem bir biraz farklı olabilir:

* [Mevcut bir Office 365 aboneliğiniz varsa](#use-an-existing-office-365-subscription)
* [Bir Microsoft Hesabı ile ilişkili olan mevcut bir Azure aboneliğiniz varsa](#use-an-msa-azure-subscription)
* [Bir kuruluş hesabı ile ilişkili olan mevcut bir Azure aboneliğiniz varsa](#use-an-organizational-azure-subscription)
* [Yukarıdaki hello hiçbiri sahip değilseniz ve sıfırdan toostart istediğiniz](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Mevcut bir Office 365 aboneliğini kullanma
Mevcut bir Office 365 aboneliğiniz varsa zaten bir Azure AD kiracınız vardır! İçinde toohello oturum [Azure portal](https://portal.azure.com) ile O365 hesabınızı ve Azure AD kullanmaya başlayın.

## <a name="use-an-msa-azure-subscription"></a>MSA Azure aboneliğini kullanma
Daha önce bireysel Microsoft Hesabınız ile bir Azure aboneliğine kaydolduysanız kiracınız zaten mevcuttur!  Oturum zaman içinde toohello [Azure Portal](https://portal.azure.com), tooyour varsayılan Kiracı içinde otomatik olarak günlüğe kaydedilir. Uygun - boş toouse yazarken bu Kiracı bkz olan ancak toocreate bir kuruluş yöneticisi hesabı isteyebilirsiniz.

toodo, bu adımları izleyin.  Alternatif olarak, yeni bir kiracı toocreate istiyor ve benzer bir işlemi izleyerek Kiracı içinde bir yönetici oluşturmak.

1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com) bireysel hesabınızla
2. Merhaba portal toohello "Azure Active Directory" bölümüne gidin (Merhaba sol gezinti çubuğunda altında bulunan **daha Hizmetleri**)
3. Toohello "Varsayılan dizin" otomatik olarak imzalanmış, yoksa hesap adınızı hello sağ üst köşedeki tıklayarak dizinleri geçiş yapabilirsiniz.
4. Merhaba gelen **hızlı görevleri** bölümünde, seçin **kullanıcı ekleme**.
5. İçinde kullanıcı ekleme Formu'nu Merhaba, aşağıdaki ayrıntılara hello sağlayın:

   * Ad: (uygun bir değer seçin)
   * Kullanıcı adı: (bu yönetici için bir kullanıcı adı seçin)
   * Profil: (ad, son adı, iş unvanı ve bölüm için uygun değerleri hello doldurma)
   * Rol: Genel Yönetici
6. Tamamladığınızda, kullanıcı ekleme Formu'nu, Merhaba ve hello yeni yönetici kullanıcı hello geçici parola alma, bu yeni kullanıcı sipariş toochange hello parola ile toologin ihtiyaç duyacağınız bu parolayı emin toorecord olabilir. Merhaba parola da gönderebilirsiniz doğrudan alternatif bir e-posta kullanarak toohello kullanıcı.
7. Tıklayın **oluşturma** toocreate hello yeni kullanıcı.
8. toochange hello geçici parola, günlüğüne [https://login.microsoftonline.com](https://login.microsoftonline.com) bu yeni kullanıcı hesabı ve istendiğinde hello parolayı değiştirin.

## <a name="use-an-organizational-azure-subscription"></a>Kuruluş Azure aboneliği kullanma
Daha önce kuruluş hesabınızla bir Azure aboneliğine kaydolduysanız kiracınız zaten mevcuttur!  Merhaba, [Azure Portal](https://portal.azure.com), çok gittiğinizde kiracıyı bulmanız gerekir "Daha Hizmetleri" ve "Azure Active Directory."  Gördüğünüz gibi bu kiracıyı uygun ücretsiz toouse var.

## <a name="start-from-scratch"></a>Sıfırdan başlama
Tüm hello yukarıdaki arkadaşınızdan tooyou ise, endişelenmeyin.  Adresini ziyaret [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign Azure için yeni bir kuruluş ile.  Merhaba işlemi tamamladığınızda, kayıt sırasında seçtiğiniz hello etki alanı adıyla kendi Azure AD Kiracı sahip olur.  Merhaba, [Azure Portal](https://portal.azure.com), çok giderek kiracınızı bulabilirsiniz "Azure Active Directory'de" Merhaba sol NAV

Azure'a kaydolma hello işleminin bir parçası gerekli tooprovide kredi kartı bilgileri olacaktır.  Güvenle devam edebilirsiniz; Azure AD'de uygulama yayınlama veya yeni kiracı oluşturma işlemleri için sizden ücret tahsil edilmeyecektir.
