---
title: "Azure Active Directory denetim günlükleri ile Azure günlük tümleştirme | Microsoft Docs"
description: "Azure günlük tümleştirme hizmeti yüklemek ve Azure denetim günlükleri günlüklerinden tümleştirme hakkında bilgi edinin"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Azure Active Directory denetim günlüklerini tümleştirme

Azure Active Directory (Azure AD) denetim olayları Azure Active Directory'de oluştu ayrıcalıklı Eylemler belirlemenize yardımcı olur. Gözden geçirerek izleyebilirsiniz olay türlerini görebilirsiniz [Azure Active Directory Denetim Raporu olayları](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Bu makaledeki adımları denemeden önce gözden geçirmeniz gerekir [başlama](security-azure-log-integration-get-started.md) makalesini inceleyip var. adımlarını tamamlayın.

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a>Azure Active directory tümleştirme adımları denetim günlükleri

1. Komut istemi açın ve şu komutu çalıştırın:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Şu komutu çalıştırın: 
 
   ``azlog createazureid``

   Bu komut için Azure oturum açma bilgilerinizi ister. Komutu daha sonra bir Azure Active Directory oturum açma kullanıcı bir yönetici, bir ortak yönetici veya sahibi olduğu Azure abonelikleri barındıran Azure AD kiracılar hizmet sorumlusu oluşturur. Oturum açma kullanıcı yalnızca Konuk kullanıcı olarak Azure AD kiracısı ise komut başarısız olur. Azure kimlik doğrulaması Azure AD üzerinden yapılır. Azure günlük tümleştirmesi için bir hizmet sorumlusu oluşturma Azure aboneliklerinden okuma erişimi verilir Azure AD kimlik oluşturur.

3. Kiracı kimliğinizi sağlamak için aşağıdaki komutu çalıştırın Komutu çalıştırmak için Kiracı yöneticisi rolünün üyesi olması gerekir.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Örnek:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Azure Active Directory denetim günlüğü JSON dosyalarını bunları oluşturulduğunu doğrulamak için aşağıdaki klasörler denetleyin:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Aşağıdaki video bu makalede ele alınan adımları gösterir:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Güvenlik bilgileri ve Olay yönetimi (SIEM) sistem bilgileri JSON dosyalarında getiren ayrıntılı yönergeler için SIEM satıcınıza başvurun.

Topluluk Yardım ile de kullanılabilir [Azure günlük tümleştirme MSDN Forumu](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Bu forumda birbirine soruları yanıtlar, ipuçları ve püf noktaları ile desteklemek için Azure günlük tümleştirme topluluk kişilere sağlar. Ayrıca, Azure günlük tümleştirme takım Bu forumda izler ve mümkün olduğunca yardımcı olur.

Ayrıca açabilirsiniz bir [destek isteği](../azure-supportability/how-to-create-azure-support-request.md). Seçin **günlük tümleştirme** destek isteyen hizmet olarak.

## <a name="next-steps"></a>Sonraki adımlar
Azure günlük tümleştirmesi hakkında daha fazla bilgi için bkz:

* [Microsoft Azure günlük tümleştirme Azure günlükleri için](https://www.microsoft.com/download/details.aspx?id=53324): Bu Yükleme Merkezi sayfası ayrıntıları, sistem gereksinimleri ve yükleme yönergeleri için Azure günlük tümleştirme sağlar.
* [Azure günlük tümleştirme giriş](security-azure-log-integration-overview.md): Bu makalede Azure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı tanıtılır.
* [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): Bu blog gönderisine Splunk, HP ArcSight ve IBM QRadar iş ortağı çözümleri ile çalışmak için Azure günlük tümleştirmesini yapılandırma gösterilmektedir.
* [Azure günlük tümleştirme SSS](security-azure-log-integration-faq.md): Bu makalede Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.
* [Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme](../security-center/security-center-integrating-alerts-with-log-integration.md): Bu makalede, Güvenlik Merkezi uyarılarını eşitlemek nasıl gösterilmektedir, sanal makine güvenlik ile birlikte olayları Azure tanılama ve Azure denetim günlükleri, günlük analizi ile toplanan veya SIEM çözümü.
* [Azure tanılama ve Azure için yeni özellikler denetim günlüklerini](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): Bu blog gönderisine Azure denetim günlükleri tanıtır ve yardımcı diğer özellikleri Azure kaynaklarınızı işlemleri alın.
