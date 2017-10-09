---
title: "aaaAzure veri Kataloğu önkoşulları | Microsoft Docs"
description: "Azure veri Kataloğu ile çalışmaya tooget ihtiyacınız hello önkoşullar hakkında bilgi edinin."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Azure Veri Kataloğu önkoşulları

Azure veri Kataloğu ayarlamadan önce birkaç care of tootake gerekir. Endişelenmeyin, bu işlem uzun sürmez.

## <a name="azure-subscription"></a>Azure aboneliği
tooset veri Kataloğu, hello sahibi veya bir Azure aboneliğinin ortak sahibi olmalıdır.

Azure abonelikleri erişim toocloud hizmet kaynakları veri Kataloğu gibi düzenlemenize yardımcı olur. Abonelikleri nasıl kaynak kullanımı bildirilen faturalandırılır ve ödendiği denetlemenize yardımcı. Abonelikler ve departman, proje, bölgesel ofise vb. göre farklılık planları alacak şekilde her abonelik bir ayrı faturalandırma ve ödeme ayarına sahip olabilir. Her bir bulut hizmeti tooa aboneliği aittir ve veri Kataloğu ayarlamak önce toohave bir abonelik gerekiyor. toolearn daha, fazla [hesapları, abonelikleri ve yönetici rollerini yönetme](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset veri Kataloğu'nu ayarlamak, bir Azure Active Directory (Azure AD) kullanıcı hesabıyla oturum açmanız gerekir.

Azure AD iş toomanage kimlik ve erişim, hem de hello Bulut ve şirket içi için kolay bir yol sağlar. Şirket içi web uygulaması ve kullanıcılar için çoklu oturum açma tooany bulut tek bir iş veya Okul hesabınızı kullanabilirsiniz. Azure AD tooauthenticate oturum açma veri kataloğu kullanır. toolearn daha, fazla [Azure Active Directory nedir?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Hello kullanarak [Azure portal](http://portal.azure.com/), oturum kişisel bir Microsoft hesabı veya bir Azure Active Directory oturum iş veya Okul hesabı. kullanarak tooset veri Kataloğu yukarı ya da hello Azure portal veya hello [veri Kataloğu portalını](http://www.azuredatacatalog.com), bir kişisel hesap bir Azure Active Directory hesabıyla oturum açması gerekir.
>
>

## <a name="active-directory-policy-configuration"></a>Active Directory ilke yapılandırması
Toohello veri Kataloğu portalında oturum açabildiğiniz, ancak toohello veri kaynağı kayıt aracını toosign çalıştığınızda bir durum karşılaşabilirsiniz, açmasını engelleyen bir hata iletisiyle karşılaşırsınız. Bu sorunu davranış yalnızca hello şirket ağda bulunuyorsanız veya yalnızca zaman dış hello şirket ağdan bağlantı kurduğunuz oluşabilecek oluşabilir.

Merhaba veri kaynağı kayıt aracını form kimlik doğrulaması toovalidate Active Directory, kullanıcı kimlik bilgilerini kullanır. başarıyla oturum toohelp, Active Directory yönetici hello genel kimlik doğrulama ilkesini form kimlik doğrulamasını etkinleştirmeniz gerekir.

Hello genel kimlik doğrulama İlkesi, hello ekran aşağıdaki gösterildiği gibi intranet için ayrı ayrı etkinse ve extranet bağlantıları, kimlik doğrulama yöntemleri olabilir. Bağlantı kurduğunuz hello ağ için form kimlik doğrulaması etkin değilse oturum açma hataları oluşabilir.

 ![Active Directory genel kimlik doğrulama İlkesi](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [kimlik doğrulaması ilkelerini yapılandırma](https://technet.microsoft.com/library/dn486781.aspx).
