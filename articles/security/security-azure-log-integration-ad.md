---
title: "Azure Active Directory denetim günlükleri ile günlük tümleştirme aaaAzure | Microsoft Docs"
description: "Nasıl tooinstall Azure günlük tümleştirme hizmeti hello ve Azure denetim günlükleri günlüklerinden tümleştirmek öğrenin"
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
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Azure Active Directory denetim günlüklerini tümleştirme

Azure Active Directory (Azure AD) denetim olayları Azure Active Directory'de oluştu ayrıcalıklı Eylemler belirlemenize yardımcı olur. Merhaba türlerini gözden geçirerek izleyebilirsiniz olayların görebilirsiniz [Azure Active Directory Denetim Raporu olayları](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Bu makaledeki adımları hello çalışmadan önce hello gözden geçirmeniz gerekir [başlama](security-azure-log-integration-get-started.md) makalesi ve hello adımları tamamlayın.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Adımları toointegrate Azure Active directory denetim günlükleri

1. Merhaba komut istemi açın ve şu komutu çalıştırın:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Şu komutu çalıştırın: 
 
   ``azlog createazureid``

   Bu komut için Azure oturum açma bilgilerinizi ister. Merhaba komut sonra bir Azure Active Directory hizmet asıl hello Azure AD kiracılar oluşturur barındıran hello Azure abonelikleri hangi hello oturum açma kullanıcı olan bir yönetici, bir ortak yönetici veya bir sahip. Merhaba oturum açmış kullanıcının yalnızca bir Konuk kullanıcı hello Azure AD kiracısında ise hello komut başarısız olur. Kimlik doğrulama tooAzure Azure AD üzerinden yapılır. Azure günlük tümleştirmesi için bir hizmet sorumlusu oluşturma hello erişim tooread Azure aboneliklerinden verilir Azure AD kimlik oluşturur.

3. Çalışma hello aşağıdaki tooprovide Kiracı kimliğinizi komutu. Merhaba Kiracı Yönetici rolü toorun hello komutunu toobe üyesi gerekir.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Örnek:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Azure Active Directory denetim günlüğü JSON dosyalarını hello klasörleri tooconfirm aşağıdaki hello bunları oluşturulan denetleyin:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Merhaba aşağıdaki video bu makalede ele alınan hello adımları gösterir:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Merhaba bilgi hello JSON dosyalarında güvenlik bilgileri ve Olay yönetimi (SIEM) sistemi hale getirme ile ilgili ayrıntılı yönergeler için SIEM satıcınıza başvurun.

Topluluk Yardım hello kullanılabilir [Azure günlük tümleştirme MSDN Forumu](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Bu forumda kişilerin hello Azure günlük tümleştirme topluluk toosupport içinde birbirlerine sorular, yanıtlar, ipuçları ve püf noktaları sağlar. Ayrıca, hello Azure günlük tümleştirme takım Bu forumda izler ve mümkün olduğunca yardımcı olur.

Ayrıca açabilirsiniz bir [destek isteği](../azure-supportability/how-to-create-azure-support-request.md). Seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.

## <a name="next-steps"></a>Sonraki adımlar
Azure günlük tümleştirme hakkında daha fazla toolearn bakın:

* [Microsoft Azure günlük tümleştirme Azure günlükleri için](https://www.microsoft.com/download/details.aspx?id=53324): Bu Yükleme Merkezi sayfası ayrıntıları, sistem gereksinimleri ve yükleme yönergeleri için Azure günlük tümleştirme sağlar.
* [Giriş tooAzure günlük tümleştirme](security-azure-log-integration-overview.md): Bu makalede tooAzure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı tanıtılır.
* [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): Bu blog gönderisine nasıl tooconfigure Azure günlük tümleştirme toowork ile iş ortağı çözümleri Splunk, HP ArcSight ve IBM QRadar gösterir.
* [Azure günlük tümleştirme SSS](security-azure-log-integration-faq.md): Bu makalede Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.
* [Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme](../security-center/security-center-integrating-alerts-with-log-integration.md): Bu makale size nasıl toosync Güvenlik Merkezi, sanal makine güvenlik olaylarını Azure tanılama ve günlük analizi ile Azure denetim günlükleri tarafından toplanan birlikte uyarıları gösterir veya SIEM çözümü.
* [Azure tanılama ve Azure için yeni özellikler denetim günlüklerini](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): Bu blog gönderisine tooAzure denetim günlüklerini tanıtır ve yardımcı diğer özellikleri Azure kaynaklarınızı hello işlemlerini alın.
