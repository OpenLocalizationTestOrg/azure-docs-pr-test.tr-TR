---
title: "Son kullanıcı kimlik doğrulaması: Data Lake Store Azure Active Directory ile | Microsoft Docs"
description: "Son kullanıcı kimlik doğrulaması Azure Active Directory'yi kullanarak Data Lake Store ile elde öğrenin"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Azure Active Directory kullanarak Data Lake Store ile son kullanıcı kimlik doğrulaması
> [!div class="op_single_selector"]
> * [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md)
> * [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store, Azure Active Directory kimlik doğrulaması için kullanır. Azure Data Lake Store veya Azure Data Lake Analytics ile çalışan bir uygulama geliştirme önce ilk uygulamanızı Azure Active Directory (Azure AD) ile kimlik doğrulama yönteminizi karar vermeniz gerekir. İki ana seçenekleri şunlardır:

* Son kullanıcı kimlik doğrulaması (Bu makalede)
* Hizmetten hizmete kimlik doğrulaması

Azure Data Lake Store veya Azure Data Lake Analytics yapılan her isteği iliştirilmiş bir OAuth 2.0 belirteç ile sağlanan uygulamanızda hem bu seçenekleri sonuçlanır.

Bu makale konuşmaları konusunda oluşturma bir **son kullanıcı kimlik doğrulaması için Azure AD yerel uygulaması**. Hizmetten hizmete kimlik doğrulaması için Azure AD uygulama yapılandırma hakkında yönergeler için bkz [hizmeti için kimlik doğrulaması Azure Active Directory kullanarak Data Lake Store ile](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* Abonelik kimliği Azure Portalı'ndan alabilirsiniz. Örneğin, Data Lake Store hesabı dikey penceresinden kullanılabilir.
  
    ![Abonelik kimliği alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Azure AD etki alanı adı. Azure portalının sağ üst köşedeki fare gelerek alabilir. Aşağıdaki ekran görüntüsünde etki alanı adıdır **contoso.onmicrosoft.com**, ve köşeli ayraçlar içinde GUID Kiracı kimliğidir. 
  
    ![AAD etki alanı alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Son kullanıcı kimlik doğrulaması
Bu, uygulamanızın Azure AD ile oturum açmak için bir son kullanıcı istiyorsanız önerilen yaklaşımdır. Uygulamanız, oturum açmış aynı düzeyde erişim son kullanıcı ile Azure kaynaklarına erişebilir olacaktır. Son kullanıcıların kimlik bilgilerini düzenli olarak erişim, uygulamanız için sırayla sağlamanız gerekir.

Oturum açma son kullanıcı sahip uygulamanız bir erişim belirteci ve bir yenileme belirteci verilir sonucudur. Erişim belirteci Data Lake Store veya Data Lake Analytics yapılan her isteği bağlı ve varsayılan olarak bir saat için geçerli olduğundan. Düzenli olarak kullanılan iki haftaya varsayılan olarak, geçerli olduğundan ve yenileme belirtecini yeni bir erişim belirteci almak için kullanılabilir. Son kullanıcı oturum açma için iki farklı yaklaşım kullanabilirsiniz.

### <a name="using-the-oauth-20-pop-up"></a>OAuth 2.0 açılır kullanma
Uygulamanız son kullanıcı kimlik bilgilerini girebilirsiniz bir OAuth 2.0 yetkilendirme açılır tetikleyebilir. Bu açılır pencere Azure AD iki öğeli kimlik doğrulamasını (2FA) işlemine gerektiğinde de çalışır. 

> [!NOTE]
> Bu yöntem henüz Azure AD Authentication Library (ADAL), Python veya Java için desteklenmiyor.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Kullanıcı kimlik bilgilerini doğrudan geçirme
Uygulamanızı Azure AD'ye doğrudan kullanıcı kimlik bilgilerini sağlayabilir. Bu yöntem yalnızca Kuruluş Kimliği kullanıcı hesaplarıyla çalışır; uyumlu değil kişisel ile / "live ID" kullanıcı hesapları da dahil olmak üzere, bitiş @outlook.com veya @live.com. Ayrıca, bu yöntem, Azure AD iki öğeli kimlik doğrulamasını (2FA) gerektiren kullanıcı hesaplarını ile uyumlu değil.

### <a name="what-do-i-need-to-use-this-approach"></a>Bu yaklaşımı kullanmak neler gerekir?
* Azure AD etki alanı adı. Bu, zaten bu makalede önkoşul olarak listelenir.
* Azure AD **yerel uygulama**
* Azure AD yerel uygulama için uygulama kimliği
* Azure AD yerel uygulama için yeniden yönlendirme URI'si
* Yetki verilmiş izinleri ayarlayın


## <a name="step-1-create-an-active-directory-native-application"></a>1. adım: Active Directory yerel uygulama oluşturma

Oluşturun ve Azure AD yerel uygulaması son kullanıcı kimlik doğrulaması için Azure Data Lake Azure Active Directory'yi kullanarak Store ile yapılandırın. Yönergeler için bkz: [Azure AD uygulaması oluşturmasına](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Yukarıdaki bağlantıyı kısmındaki yönergeleri izleyerek sırasında seçtiğinizden emin olun **yerel** aşağıdaki ekran görüntüsünde gösterildiği gibi uygulama türü için.

![Web uygulaması oluşturma](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "yerel uygulama oluştur")

## <a name="step-2-get-application-id-and-redirect-uri"></a>2. adım: uygulama kimliği alma ve yeniden yönlendirme URI'si

Bkz: [uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Azure Klasik Portalı'nda istemci kimliği olarak da bilinir) Azure AD yerel uygulamanın uygulama kimliğini almak için.

Yeniden yönlendirme URI'si almak için aşağıdaki adımları izleyin.

1. Azure Portalı'ndan seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz Azure AD yerel uygulama'yı tıklatın.

2. Gelen **ayarları** uygulama için dikey tıklayın **yeniden yönlendirme URI'ler**.

    ![Get yeniden yönlendirme URI'si](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Görüntülenen değer kopyalayın.


## <a name="step-3-set-permissions"></a>3. adım: İzinleri ayarlama

1. Azure Portalı'ndan seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz Azure AD yerel uygulama'yı tıklatın.

2. Gelen **ayarları** uygulama için dikey tıklayın **gerekli izinleri**ve ardından **Ekle**.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. İçinde **API erişimini eklemek** dikey penceresinde tıklatın **bir API seçin**, tıklatın **Azure Data Lake**ve ardından **seçin**.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  İçinde **eklemek API erişimini** dikey penceresinde tıklatın **izinler seçeneğini belirleyin**, vermek için bu onay kutusunu seçin **tam erişim Data Lake Store'a**ve ardından **seçin**.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    **Bitti**’ye tıklayın.

5. İzinleri vermek için son iki adımı yineleyin **Windows Azure Hizmet Yönetimi API'si** de.
   
## <a name="next-steps"></a>Sonraki adımlar
Bu makalede Azure AD yerel uygulaması oluşturulur ve .NET SDK'sı, Java SDK'sı, REST API vb. kullanarak Yazar istemci uygulamalarınızda gereksinim duyduğunuz bilgileri toplanmaz. İlk Data Lake Store ile kimlik doğrulaması ve depolama üzerinde başka işlemler gerçekleştirmek için Azure AD web uygulaması kullanma hakkında konuşun aşağıdaki makalelere şimdi devam edebilirsiniz.

* [.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-net-sdk.md)
* [Azure Data Lake Java SDK'sını kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-java-sdk.md)
* [Azure Data Lake REST API kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-rest-api.md)

