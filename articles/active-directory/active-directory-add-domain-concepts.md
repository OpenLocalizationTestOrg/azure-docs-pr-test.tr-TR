---
title: "Azure Active Directory'de özel etki alanı adlarını aaaConceptual genel bakış | Microsoft Docs"
description: "Federasyon için çoklu oturum açma dahil olmak üzere Azure Active Directory'de özel etki alanı adlarını kullanarak için hello kavramsal çerçeve açıklar"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Azure Active Directory'de özel etki alanı adlarına kavramsal genel bakış
Bir etki alanı adı, birçok dizin kaynaklar için önemli bir tanımlayıcı bir parçası olarak şunlar olabilir:

* Bir kullanıcı için bir kullanıcı adı veya e-posta adresi
* bir grup için başlangıç adresi
* bir uygulama için Hello uygulama kimliği URI'si

Azure Active Directory'de (Azure AD) bir kaynak hello kaynak içeren toobe hello dizine ait zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz. Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Hello Azure AD Yönetim Merkezi'nde etki alanınızın nasıl toomanage adları için bkz: [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).

Azure AD etki alanı adları genel benzersiz. Özel etki alanı adı aynı anda yalnızca bir Azure AD Kiracı tarafından kullanılabilir. Bir Azure AD dizini bir etki alanı adı doğruladı, ardından başka bir Azure AD dizini doğrulayın veya aynı etki alanı adı kullanın.

## <a name="initial-and-custom-domain-names"></a>İlk ve özel etki alanı adları
Her etki alanı adını Azure AD'de bir ilk etki alanı adı ya da bir özel etki alanı adı değil.

Her Azure AD hello form contoso.onmicrosoft.com bir ilk etki alanı adı ile birlikte gelir. Bu örnekte "contoso.onmicrosoft.com," Bu üçüncü düzey etki alanı adı Hello dizin, genellikle hello dizin oluşturan hello Yöneticisi tarafından oluşturulduğunda kuruldu. Dizin Hello ilk etki alanı adı değiştirilmiş veya silinmiş. Merhaba ilk etki alanı adı, tam olarak işlevsel olsa da, öncelikle bir özel etki alanı adı kadar önyükleme mekanizması olarak kullanılan toobe doğrulanır yöneliktir.

Çoğu üretim ortamlarında, en az bir doğrulanmış özel etki alanı, "contoso.com" gibi bir dizine sahip ve görünür tooend kullanıcıları, özel etki alanıdır. Özel etki alanı kullanımlar, web sitesi barındırma gibi sahibi ve "contoso.com" gibi belirli bir kuruluş tarafından kullanılan bir etki alanı adı içindir. Toosign toohello şirket ağı veya toosend kullanın ve e-posta almak hello kullanıcı adının bir parçası olduğundan bu etki alanı adı tanıdık tooemployees değildir.

Azure AD tarafından kullanılabilmesi için önce hello özel etki alanı adı eklenen tooyour dizin olmalıdır ve doğrulandı.

## <a name="verified-and-unverified-domain-names"></a>Doğrulanmış ve doğrulanmamış etki alanı adları
Merhaba ilk etki alanı adı bir dizin için örtük olarak Azure AD tarafından doğrulanmış olarak değerlendirilir. Yönetici bir özel etki alanı adı tooan Azure AD eklediğinde, başlangıçta doğrulanmamış bir durumda değil. Azure AD tüm dizin kaynakları toouse doğrulanmamış etki alanı adı izin vermez. Bu, belirli bir etki alanı adı yalnızca bir dizini kullanabilir ve sahip olduğu hello kuruluş hello etki alanı adını kullanır gerçekte bu etki alanı adı sağlar.

Azure AD etki alanı adı sahipliğini hello etki alanı adı hizmeti (DNS) bölge dosyası hello etki alanı adı için belirli bir giriş arayarak doğrular. bir etki alanı adı sahipliğini tooverify, bir yönetici, hello DNS girişi Azure AD görünür ve bu girişi toohello DNS bölge dosyasına hello etki alanı adı için ekler Azure AD'den alır. Merhaba DNS bölge dosyasına hello etki alanı adı kayıt o etki alanı tarafından korunur. bir etki alanı için hello makalede gösterilen hello adımları tooverify [bir özel etki alanı tooyour Azure AD dizini ekleme](active-directory-add-domain.md).

Merhaba etki alanı adı için bir DNS girişi toohello bölge dosyasına ekleme e-posta veya web barındırma gibi diğer etki alanı Hizmetleri etkilemez.

## <a name="federated-and-managed-domain-names"></a>Federasyon ve yönetilen etki alanı adları
Azure AD'de bir özel etki alanı adı yapılandırılmış toogive kullanıcılar bir federe oturum açma deneyimini şirket içi Active Directory ve Azure AD arasında olabilir. Federasyon gerektirir için bir etki alanı yapılandırmak, Azure AD'de tooprivileged kaynakları güncelleştirir ve ayrıca Windows Server Active Directory tooyour. Bir Federasyon etki alanını Azure AD Connect'ten doldurulmalıdır yapılandırma veya PowerShell kullanarak. Özel bir etki alanı federasyonunu hello Klasik Azure Portalı ' başlatılamaz. [AD FS ile Azure AD Connect kullanıcı oturumu açma için yapılandırma hakkındaki bu video toolearn izleme](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Birleşik etki alanları bazen yönetilen etki alanı adı verilir. Merhaba ilk etki alanı Azure AD dizini için örtük olarak yönetilen bir etki alanı olarak değerlendirilir.

## <a name="primary-domain-names"></a>Birincil etki alanı adları
Merhaba bir dizin için birincil etki alanı adı yönetici hello yeni bir kullanıcı oluşturduğunda hello hello kullanıcı adının hello 'etki alanı' bölümü için varsayılan değer olarak önceden seçilmiş hello etki alanı adıdır [Azure portal](https://portal.azure.com/), ya da başka bir portal Merhaba Office 365 Yönetici portalı veya hello Microsoft Intune portalı gibi. Bir dizin yalnızca bir birincil etki alanı adı olabilir. Yönetici hello birincil etki alanı adı toobe herhangi birleşik olmadığı doğrulanmış özel etki alanı veya etki alanında ilk toohello değiştirebilirsiniz.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Azure AD etki alanı adlarını ve diğer Microsoft Online Services
Bir etki alanı adı Exchange Online, SharePoint Online ve Intune gibi başka bir Microsoft Online Service tarafından kullanılmadan önce Azure AD'de doğrulanması gerekir. Diğer hizmetlerin, belirli toohello hizmet bir veya daha fazla DNS girişlerini genellikle bir yönetici tooadd gerektirir.

Azure web uygulaması bir etki alanı kendi mekanizması tooverify sahipliğini kullanır. Azure web uygulaması üzerinde Azure AD kullanır bir abonelikte tarafından kullanım için önceden da doğrulandı olsa bile Azure AD ile kullanmak için bir etki alanı doğrulanmalıdır. Azure web uygulaması hello web uygulamasını güvenli hale getirdiği hello dizininden farklı bir dizinde doğrulandı bir etki alanı adı kullanabilirsiniz.

## <a name="managing-domain-names"></a>Etki alanı adlarını yönetme
Etki alanı yönetim görevlerini hello Klasik Azure portalı ve PowerShell tamamlanabilir. Birçok görevi hello Azure AD grafik API'si kullanılarak tamamlanabilir.

* [Ekleme ve özel etki alanı adını doğrulama](active-directory-add-domain.md)
* [Merhaba Klasik Azure Portalı'nda etki alanlarını yönetme](active-directory-add-manage-domain-names.md)
* [Azure AD PowerShell toomanage etki alanı adlarını kullanma](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Azure AD'de Hello Azure AD Graph API toomanage etki alanı adlarını kullanma](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

