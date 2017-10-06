---
title: "Office 365 aboneliğinize Azure aaaManage hello dizini | Microsoft Docs"
description: "Azure Active Directory ve hello Klasik Azure portalı kullanarak bir Office 365 aboneliği dizinini yönetme"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Azure'da Office 365 aboneliğinize Hello dizini yönetme
Bu makalede nasıl toomanage hello Klasik Azure portalı kullanarak bir Office 365 aboneliği için oluşturulmuş bir dizin. Merhaba Hizmet Yöneticisi veya bir Azure aboneliği toosign toohello Klasik Azure portalı içinde ortak yöneticisi olmanız gerekir. Henüz bir Azure aboneliğiniz yoksa hemen [30 günlük ücretsiz deneme sürümüne](https://azure.microsoft.com/trial/get-started-active-directory/) kaydolabilir ve bu bağlantıyı kullanarak ilk bulut çözümünüzü 5 dakikadan kısa bir sürede dağıtabilirsiniz. Olması emin toouse hello iş veya Okul hesabı tooOffice 365 toosign kullanın.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

Hello Azure aboneliği tamamladıktan sonra toohello Klasik Azure portalında oturum açın ve Azure hizmetlerine erişebilirsiniz. Merhaba Active Directory uzantısına tıklayın toomanage hello Office 365 kullanıcılarınızın kimliğini doğrulayan aynı dizin.

Merhaba işlem toomanage ek bir dizin, ayrıca bir Azure aboneliğiniz zaten varsa basittir. Örneğin, Michael Smith, Contoso.com için bir Office 365 aboneliğine sahip olabilir. Ayrıca msmith@hotmail.com şeklindeki Microsoft hesabını kullanarak kaydolduğu bir Azure aboneliği de mevcuttur. Bu durumda, iki dizini yönetir.

| Abonelik | Office 365 | Azure |
| --- | --- | --- |
|   Görünen ad |Contoso |Varsayılan Azure Active Directory (Azure AD) dizini |
|   Etki alanı adı |contoso.com |msmithhotmail.onmicrosoft.com |

Kullanıcı çok faktörlü kimlik doğrulaması gibi Azure AD özelliklerini etkinleştirebilmeniz için kendisine kendi Microsoft hesabı kullanarak tooAzure içinde açmış durumdayken toomanage hello kullanıcı kimlikleri hello Contoso dizininde istediği. Aşağıdaki diyagramda hello tooillustrate hello işlem yardımcı olabilir.

![Toomanage iki bağımsız dizini diyagram](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

Bu durumda, hello iki dizin birbirinden bağımsızdır.

## <a name="toomanage-two-independent-directories"></a>toomanage iki bağımsız dizini
Kendisine tooAzure içinde açmış durumdayken, Michael Smith toomanage için her iki dizini sipariş msmith@hotmail.com, kendisinin hello aşağıdaki adımları tamamlamanız gerekir:

> [!NOTE]
> Bu adımlar, yalnızca kullanıcı bir Microsoft hesabıyla oturum açmış durumdayken tamamlanabilir. Merhaba kullanıcı bir iş veya Okul hesabıyla oturum açtıysanız, seçeneği çok hello**var olan dizini kullan** kullanılamaz. Bir iş veya Okul hesabı yalnızca kendi ana dizini tarafından (burada hello iş veya Okul hesabı depolanır ve bu hello iş veya Okul sahip başka bir deyişle, hello dizin) doğrulanabilir.
>
>

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) olarak msmith@hotmail.com.
2. **New (Yeni)** > **App services (Uygulama hizmetleri)** > **Active Directory** > **Directory (Dizin)** > **Custom Create (Özel Oluştur)** düğmesine tıklayın.
3. Dizin ve select hello varolan kullan **şimdi oturumu kapattınız hazır toobe ben** onay kutusu.
4. Toohello içinde Klasik Azure portalında Contoso.onmicrosoft.com genel yönetici olarak oturum açın (örneğin, msmith@contoso.com).
5. Çok istendiğinde**hello Contoso dizini Azure ile kullan?**, tıklatın **devam**.
6. **Sign out now (Şimdi oturumu kapat)** seçeneğine tıklayın.
7. İçinde toohello olarak Klasik Azure portalında oturum msmith@hotmail.com. hello Contoso dizini ve hello varsayılan dizin hello Active Directory uzantısını görünür.

Bu adımları tamamladıktan sonra msmith@hotmail.com hello Contoso dizininde genel Yöneticisi.

## <a name="tooadminister-resources-as-hello-global-admin"></a>Genel yönetici hello gibi tooadminister kaynakları
Şimdi Jane Doe'nun gereken Web sitelerinizi yönetmek ve ilişkili veritabanı kaynakları hello Azure aboneliği için şimdi varsayalım msmith@hotmail.com. Aynen bunu yapmadan önce Michael Smith'in şu ek adımları toocomplete gerekir:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello Hizmet Yöneticisi hesabıyla hello Azure aboneliği için (Bu örnekte, msmith@hotmail.com).
2. Merhaba abonelik toohello Contoso dizinine aktarma: tıklatın **ayarları** > **abonelikleri** > merhaba aboneliği seçin > **dizini Düzenle** > seçin **Contoso (Contoso.com)**. Merhaba aktarımı, iş veya Okul parçası olarak hello aboneliğin ortak yöneticisi olan hesapları kaldırılır.
3. Jane Doe'yu hello aboneliğin ortak Yöneticisi eklemek: tıklatın **ayarları** > **Yöneticiler** > merhaba aboneliği seçin > **Ekle** > türü **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Sonraki adımlar
Hello abonelikler ve dizinler arasındaki ilişki hakkında daha fazla bilgi için bkz: [nasıl bir aboneliğin bir dizinle ilişkili olduğu](active-directory-how-subscriptions-associated-directory.md).
