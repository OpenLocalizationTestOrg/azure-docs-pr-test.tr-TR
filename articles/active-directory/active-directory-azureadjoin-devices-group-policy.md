---
title: "Windows 10 için aaaConnect etki alanına katılmış aygıtlar tooAzure AD karşılaştığında | Microsoft Docs"
description: "Yöneticiler Grup İlkesi tooenable aygıtları toobe etki alanına katılmış toohello kuruluş ağı nasıl yapılandırabileceğiniz açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan
Etki alanına katılma hello geleneksel şekilde kuruluşlar iş hello son 15 yıl ve daha fazlası için Aygıtlar bağlı olur. Kullanıcıların toosign tootheir aygıtları, Windows Server Active Directory (Active Directory) işlerini kullanarak etkinleştirilmiş veya Okul hesapları ve izin verilen BT toofully bu aygıtları yönetin. Kuruluşlar genellikle yöntemleri tooprovision aygıtları toousers Imaging kullanır ve genellikle Grup İlkesi veya System Center Configuration Manager (SCCM) toomanage kullanması bunları.


Windows 10 etki alanına katılma ile Merhaba aygıtları tooAzure Active Directory (Azure AD) bağlandıktan sonra aşağıdaki avantajları sağlar:

* Çoklu oturum açma (SSO) tooAzure AD kaynaklara her yerden
* İş kullanarak toohello enterprise Windows mağazası erişmek veya Okul hesapları (Microsoft hesabı gereklidir)
* Kurumsal uyumlu kullanıcı cihaz üzerinden iş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak Dolaşım ayarları
* Güçlü kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla iş için Windows Hello ve Windows Hello
* Özelliği toorestrict kuruluş aygıt Grup İlkesi ayarları ile uyumlu toodevices erişim

## <a name="prerequisites"></a>Ön koşullar
Etki alanına katılma toobe yararlı devam eder. Ancak, hello Azure AD yararları SSO tooget, ayarlarla, gezici iş veya Okul hesapları ve çalışmak tooWindows deposuna erişim veya Okul hesapları, aşağıdaki hello gerekir:

* Azure AD aboneliği
* Azure AD Connect tooextend hello şirket içi dizin tooAzure AD
* Tooconnect etki alanına katılmış aygıtlar tooAzure AD ayarlanmış İlkesi
* Cihazlar için Windows 10 derleme (derleme 10551 ya da daha yeni)

İş ve Windows Hello için Windows Hello tooenable hello aşağıdakileri de gerekir:

- **Ortak anahtar altyapısı (PKI)** kullanıcı sertifikaları verme için.

- **System Center Configuration Manager geçerli dalının** -tooinstall sürümü 1606 veya üzeri gerekiyor.  
Daha fazla bilgi için bkz. 
    - [System Center Configuration Manager belgeleri](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager ekip blogu](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [İşletme ayarlarını System Center Configuration Manager için Windows Hello](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Bir alternatif toohello PKI Dağıtımı gereksinimini bunu hello aşağıdaki:

* Windows Server 2016 Active Directory etki alanı Hizmetleri ile birkaç etki alanı denetleyicilerine sahip.

tooenable koşullu erişim, hiçbir ek dağıtımı ile erişim toodomain katılmış cihazları izin ver Grup İlkesi ayarları oluşturabilirsiniz. Merhaba aygıt uyumluluğuna göre toomanage erişim denetimi hello aşağıdaki gerekir:

* System Center Configuration Manager geçerli dalının (1606 veya üstü) için iş senaryoları için Windows Hello

## <a name="deployment-instructions"></a>Dağıtım yönergeleri

toodeploy, listelenen hello adımları [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Sonraki adım
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

