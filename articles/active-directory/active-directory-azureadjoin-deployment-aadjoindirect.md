---
title: "aaaUsage senaryoları ve Azure AD katılım için dağıtım konuları | Microsoft Docs"
description: "Nasıl yöneticileri Azure AD'ye katılımı kendi son kullanıcıları için (çalışanlar, Öğrenciler, diğer kullanıcıları) ayarlayacakları açıklanmaktadır. Ayrıca, Azure AD katılım kullanarak hello farklı gerçek senaryolar anlatılmaktadır."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Kullanım senaryoları ve Azure AD katılım için dağıtım konuları
## <a name="usage-scenarios-for-azure-ad-join"></a>Azure AD katılım için kullanım senaryoları
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Senaryo 1: İşletmeler hello bulutta büyük ölçüde
Azure Active Directory katılım (Azure AD katılımı), şu anda çalışır ve hello bulut işinizde için kimlikleri yönetme veya toohello bulut yakında taşıyorsanız, yararlanabilirsiniz. Azure AD toosign tooWindows 10 içinde oluşturduğunuz bir hesap kullanabilirsiniz. Aracılığıyla [ilk çalıştırma deneyimi (FRX) işlemi hello](active-directory-azureadjoin-user-frx.md), Azure AD'den katılarak ya [hello ayarları menüsü](active-directory-azureadjoin-user-upgrade.md), kullanıcılarınızın kendi makineler tooAzure AD katılabilirsiniz.  Kullanıcılarınızın aynı zamanda çoklu oturum açma (SSO) keyfini çıkarabilirsiniz erişim çok tarayıcılarında veya Office uygulamalarında kaynakları, Office 365 gibi bulut.

### <a name="scenario-2-educational-institutions"></a>Senaryo 2: Eğitim kurumları
Eğitim kurumları genellikle iki kullanıcı türlerine sahip: Fakülte ve öğrenciler. Fakülte üyeleri hello kuruluş daha uzun vadeli üyeleri olarak kabul edilir. Şirket içi hesapları kullanabiliyor tercih edilir. Ancak Öğrenciler hello kuruluşun shorter-term üyeleridir ve hesaplarını Azure AD'de yönetilebilir. Bu dizin ölçek şirket içi depolanan olmak yerine toohello bulut gönderilemez anlamına gelir. Ayrıca Öğrenciler tooWindows kendi Azure AD hesapları ile de yükleyebilirsiniz toosign olması ve Office uygulamalarında tooOffice 365 kaynaklara erişmek anlamına gelir.

### <a name="scenario-3-retail-businesses"></a>Senaryo 3: Perakende işletmeler
Perakende işletmeler Mevsimlik çalışanları ve uzun vadeli çalışanların sahip. Genellikle şirket içi hesapları oluşturabilir ve etki alanına katılan makineler daha uzun vadeli tam zamanlı çalışanlar için kullanın. Ancak Mevsimlik çalışanlardır hello kuruluş shorter-term üyeleri ve bu arzu toomanage burada kullanıcı lisansları daha kolay taşınabilir geçici hesaplarını. Office 365 lisansına sahip hello bulutta, kullanıcı hesaplarını oluşturduğunuzda, bu kullanıcılar bunlar çıktıktan sonra lisansları ile daha fazla esneklik bakım yaparken tooWindows ve bir Azure AD hesabının Office uygulamalarıyla imzalama hello avantajlarını alır.

### <a name="scenario-4-additional-scenarios"></a>Senaryo 4: İlave senaryolar
Daha önce bahsedilen hello avantajları yanı sıra, kullanıcılarınızın kendi aygıtlarını tooAzure AD Basitleştirilmiş katılma deneyimi, verimli aygıt yönetimi, otomatik mobil cihaz Yönetimi kayıt ve oturum açma tek tooAzure nedeniyle katılma kalmaktan yararlanabilir AD ve şirket içi kaynaklar.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Azure AD katılım için dağıtım konuları
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Kullanıcıların toojoin şirkete ait bir cihazı etkinleştirme doğrudan tooAzure AD
Kuruluşlar, yalnızca bulut hesapları toopartner şirketler ve kuruluşlar sağlayabilir. Bu iş ortaklarının daha sonra kolayca şirket uygulamaları ve çoklu oturum açma ile kaynaklarına erişebilirsiniz. Birincil kimlik doğrulaması için Azure AD Bel Office 365 veya SaaS uygulamaları gibi hello bulut kaynaklara erişim geçerli toousers senaryodur.

### <a name="prerequisites"></a>Ön koşullar
**Merhaba Kurumsal düzeyde (Yönetici)**

* Azure Active Directory ile Azure aboneliği  

**Merhaba kullanıcı düzeyinde**

* Windows 10 (Professional ve Enterprise sürümleri)

### <a name="administrator-tasks"></a>Yönetici görevleri
* [Cihaz kaydı oluşturma](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Kullanıcı görevleri
* [Kurulum sırasında Azure AD ile yeni bir Windows 10 cihazı ayarlama](active-directory-azureadjoin-user-frx.md)
* [Merhaba Ayarlar'dan Azure AD ile Windows 10 cihazı ayarlama](active-directory-azureadjoin-user-upgrade.md)
* [Kişisel bir Windows 10 cihaz tooyour kuruluş katılma](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Windows 10 için kuruluşunuzdaki KCG etkinleştir
Kullanıcılar ve çalışanlar toouse kendi kişisel Windows cihazlarını (BYOD) tooaccess şirket uygulamalarına ve kaynaklarına ayarlayabilirsiniz. Kullanıcılarınızın Azure AD hesapları (iş veya Okul hesapları) tooa kişisel Windows aygıt tooaccess kaynaklarına güvenli ve uyumlu bir biçimde ekleyebilirsiniz.

### <a name="prerequisites"></a>Ön koşullar
**Merhaba Kurumsal düzeyde (Yönetici)**

* Azure AD aboneliği

**Merhaba kullanıcı düzeyinde**

* Windows 10 (Professional ve Enterprise sürümleri)

### <a name="administrator-tasks"></a>Yönetici görevleri
* [Cihaz kaydı oluşturma](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Kullanıcı görevleri
* [Kişisel bir Windows 10 cihaz tooyour kuruluş katılma](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport aracılığıyla parolası olmayan kimlikleri doğrulama](active-directory-azureadjoin-passport.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

