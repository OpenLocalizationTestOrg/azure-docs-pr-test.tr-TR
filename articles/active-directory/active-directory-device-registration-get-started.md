---
title: "Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma | Microsoft Docs"
description: "Azure Active Directory ile otomatik olarak ve sessiz bir şekilde kaydetmek için etki alanına katılmış Windows cihazları ayarlayın."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydına başlarken

Azure Active Directory cihaz kaydı, cihaz temelli koşullu erişim senaryoları için altyapıdır. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı, cihaza kullanıcı oturum açtığı zaman kimlik doğrulama için kullanılan kimliği sağlar. Kimliği doğrulanmış cihaz ve cihaz öznitelikleri böylece bulutta ve şirket içinde barındırılan uygulamalar için koşullu erişim ilkelerini zorlamak üzere kullanılabilir.

Microsoft Intune gibi bir mobil cihaz yönetimi (MDM) çözümü ile birleştirildiğinde Azure Active Directory'deki cihaz öznitelikleri cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu durum, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak için cihazlardan erişimi zorlayan koşullu erişim kuralları oluşturmanıza olanak sağlar. Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.
Azure Active Directory cihaz kaydı Azure Active Directory cihaz kaydı tarafından etkinleştirilen senaryolar iOS, Android ve Windows için destek içerir aygıtlar. Azure AD Cihaz Kaydı'nı kullanan bireysel senaryolar daha fazla özel gereksinime ve platform desteğine sahip olabilir. 

Bu senaryolar aşağıdaki gibidir:

- **Microsoft Intune ile Office 365 uygulamaları için koşullu erişim:** BT yöneticileri, bilgi çalışanları üzerinde uyumlu cihazların erişmesine izin vererek aynı anda sırada şirket kaynaklarına güvenli hale getirmek için koşullu erişim cihaz ilkeleri sağlayabilirler Hizmetler. Daha fazla bilgi edinmek için bkz. Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri.

- **Şirket içinde barındırılan uygulamalara koşullu erişim:** ile Windows Server 2012 R2 AD FS kullanmak üzere yapılandırılan uygulamalar için erişim ilkeleri ile kayıtlı cihazları kullanabilirsiniz. Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory cihaz kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Azure Active Directory Cihaz Kaydı'nı ayarlama

Kurulum bir aygıt kaydı için birçok seçeneğiniz vardır:

- Azure AD etki alanına katıldığında cihazlarını kaydedebilir. Bu konu hakkında daha fazla bilgi için Azure AD etki alanına katılmak için Azure AD birleştirme ve kullanıcılar için gerekli ayarları hakkında daha fazla bilgi edinebilirsiniz.

- Kullanıcıların iş veya Okul hesapları Windows kişisel bir cihazda veya Mobil cihazların kaydı gerektiren bir iş kaynaklarına bağladığınızda eklediğinizde aygıtları kaydedilebilir. Bunu sağlamak için Azure Portal'da Azure AD cihaz kaydı etkinleştirmeniz gerekir. 

- Cihazlar, geleneksel etki alanına katılan makineler için otomatik cihaz kaydı kullanılarak kaydedilebilir. Otomatik cihaz kaydı ile devam etmeden önce bu emin olmak için ilk kurulum Azure AD Connect gerekir.

En son yönergeler için bkz: [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md).  
Ayrıca gözden geçirin ve da etkinleştirebilir veya Azure Active Directory'de Yönetici portalı'nı kullanarak kayıtlı cihazları devre dışı bırakın.

## <a name="enable-the-azure-active-directory-device-registration-service"></a>Azure Active Directory cihaz kaydı hizmetini etkinleştirme

**Azure Active Directory cihaz kayıt hizmeti etkinleştirmek için:**

1.  Microsoft Azure portalında yönetici olarak oturum açın.

2.  Sol bölmede **Active Directory**'yi seçin.

3.  Dizin sekmesinde dizininizi seçin.

4.  **Yapılandır**'a tıklayın.

5.  Kaydırma **aygıtları**.

6.  Select tüm kullanıcılar için AZURE AD ile CİHAZLARINI KAYDEDEBİLİR.

7.  Kullanıcı başına yetkilendirmek istediğiniz maksimum cihaz sayısını seçin.

Office 365 için Microsoft Intune veya mobil cihaz yönetimi ile kayıt cihaz kaydı gerektirir. Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** devre dışı bırakılır. Lütfen doğru şekilde yapılandırıldığından ve uygun lisans sahip olduğundan emin olun.

Varsayılan olarak hizmet için iki öğeli kimlik doğrulama etkin değildir. Yine de bir cihaz kaydedilirken iki öğeli kimlik doğrulama önerilir.

- Bu hizmet için iki öğeli kimlik doğrulama istemeden önce Azure Active Directory'de iki öğeli kimlik doğrulama sağlayıcısını yapılandırmak ve kullanıcı hesaplarınızı çok faktörlü kimlik doğrulaması için yapılandırmanız gerekir, bkz: Azure çok faktörlü kimlik doğrulaması ekleme Active Directory

- Windows Server 2012 R2 ile AD FS kullanıyorsanız, AD FS'de iki öğeli kimlik doğrulama modülünü yapılandırmanız gerekir, bkz: Active Directory Federasyon Hizmetleri ile çok faktörlü kimlik doğrulaması kullanarak.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Azure Active Directory'de cihaz nesnelerini görüntüleme ve yönetme

Azure Yönetici portalından cihazları görüntüleyebilir, engelleyebilir ve engellerini kaldırabilirsiniz. Bu işlemden sonra, engellenen bir cihaz yalnızca kayıtlı cihazlara izin vermek için yapılandırılan uygulamalara erişim sağlayamaz.

**Azure Active Directory'de cihaz nesnelerini görüntülemek ve yönetmek için:**
 
1.  Microsoft Azure portalında yönetici olarak oturum açın.

2.  Sol bölmede **Active Directory**'yi seçin.

3.  Dizininizi seçin.

4.  Seçin **kullanıcılar**. 

5.  Aygıtları görmek istediğiniz kullanıcıyı tıklatın.

6.  Seçin **aygıtları**.

7.  Seçin **kayıtlı cihazlar**.

Şimdi, gözden geçirin, engelleyebilir veya kullanıcının kayıtlı aygıtların engellemesini kaldırmak.
Şirket içi etki alanına katılmış ve otomatik olarak kaydedilmiş Windows 10 cihazlarına, kullanıcılar sekmesi altında görünmez. Lütfen tüm kurumsal aygıtları bulmak için Get-MsolDevice PowerShell komutunu kullanın. 


## <a name="next-steps"></a>Sonraki adımlar

Otomatik cihaz kaydı kurulumu için bkz: [Azure Active Directory ile etki alanına katılmış Windows cihazlarının otomatik kaydını yapılandırma](active-directory-conditional-access-automatic-device-registration-setup.md).


