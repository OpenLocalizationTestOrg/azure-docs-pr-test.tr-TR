---
title: "Windows 10 deneyimleri için etki alanına katılmış cihazları Azure AD'ye bağlanma | Microsoft Docs"
description: "Yöneticiler cihazlarının kurumsal ağ etki alanına katılmasını sağlamak için Grup İlkesi nasıl yapılandırabileceğiniz açıklanmaktadır."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a>Windows 10 deneyiminden faydalanmak için, etki alanına katılan cihazları Azure AD'ye bağlama
Etki alanına katılma, geleneksel bir şekilde kuruluşların son 15 yıl ve daha fazlası için iş için cihazları bağlandınız ' dir. Kullanıcıların cihazlarına, Windows Server Active Directory (Active Directory) işlerini kullanarak oturum açın veya Okul hesapları etkin ve izin verilen tam olarak bu cihazları yönetmek için BT. Kuruluşlar, genellikle kullanıcılara cihazları sağlamak için görüntü oluşturma yöntemleri kullanır ve genellikle bunları yönetmek için Grup İlkesi veya System Center Configuration Manager (SCCM) kullanın.


Azure Active Directory (Azure AD) aygıtları bağladıktan sonra Windows 10 etki alanına katılma ile aşağıdaki avantajları sağlar:

* Çoklu oturum açma (SSO) Azure AD kaynaklara her yerden
* İş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak kurumsal Windows mağazası erişimi
* Kurumsal uyumlu kullanıcı cihaz üzerinden iş veya Okul hesapları (Microsoft hesabı gereklidir) kullanarak Dolaşım ayarları
* Güçlü kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla iş için Windows Hello ve Windows Hello
* Kurumsal cihaz Grup İlkesi ayarları ile uyumlu cihazlara erişimi sınırlandırma

## <a name="prerequisites"></a>Ön koşullar
Etki alanına katılma yararlı olacak şekilde devam eder. Ancak, için SSO Azure AD yararları almak için iş veya Okul hesapları ve erişim ayarlarının Windows Mağazası'na iş veya Okul hesaplarıyla dolaşım, aşağıdakiler gerekir:

* Azure AD aboneliği
* Azure AD ile şirket içi dizin genişletmek için azure AD Connect
* Etki alanına katılmış cihazları Azure AD'ye bağlamak için ayarlanmış İlkesi
* Cihazlar için Windows 10 derleme (derleme 10551 ya da daha yeni)

Windows Hello iş ve Windows Hello için etkinleştirmek için ayrıca aşağıdakiler gerekir:

- **Ortak anahtar altyapısı (PKI)** kullanıcı sertifikaları verme için.

- **System Center Configuration Manager geçerli dalının** -sürüm 1606 ya da daha iyi yüklemeniz gerekir.  
Daha fazla bilgi için bkz. 
    - [System Center Configuration Manager belgeleri](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager ekip blogu](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [İşletme ayarlarını System Center Configuration Manager için Windows Hello](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

PKI Dağıtımı gereksinimini alternatif olarak, aşağıdakileri yapabilirsiniz:

* Windows Server 2016 Active Directory etki alanı Hizmetleri ile birkaç etki alanı denetleyicilerine sahip.

Koşullu erişimi etkinleştirmek için hiçbir ek dağıtımı ile etki alanına katılmış cihazları erişmesine izin vermek Grup İlkesi ayarları oluşturabilirsiniz. Cihaz uyumluluğuna göre erişim denetimini yönetmek için aşağıdakiler gerekir:

* System Center Configuration Manager geçerli dalının (1606 veya üstü) için iş senaryoları için Windows Hello

## <a name="deployment-instructions"></a>Dağıtım yönergeleri

Dağıtmak için listelenen adımları [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Sonraki adım
* [Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

