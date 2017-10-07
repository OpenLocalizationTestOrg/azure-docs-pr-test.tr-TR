---
title: "Son kullanıcı kimlik doğrulaması: Data Lake Store Azure Active Directory ile | Microsoft Docs"
description: "Bilgi nasıl Azure Active Directory kullanarak Data Lake Store ile tooachieve son kullanıcı kimlik doğrulaması"
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
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Azure Active Directory kullanarak Data Lake Store ile son kullanıcı kimlik doğrulaması
> [!div class="op_single_selector"]
> * [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md)
> * [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store, Azure Active Directory kimlik doğrulaması için kullanır. Azure Data Lake Store veya Azure Data Lake Analytics ile çalışan bir uygulama geliştirme önce ilk tooauthenticate yönteminizi karar vermeniz gerekir uygulamanızı Azure Active Directory'ye (Azure AD). Merhaba iki ana seçenekleri şunlardır:

* Son kullanıcı kimlik doğrulaması (Bu makalede)
* Hizmetten hizmete kimlik doğrulaması

Ekli tooeach yapılan istek tooAzure Data Lake Store veya Azure Data Lake Analytics alır bir OAuth 2.0 belirteç ile sağlanan uygulamanızda hem bu seçenekleri sonuçlanır.

Bu makale konuşmaları konusunda oluşturma bir **son kullanıcı kimlik doğrulaması için Azure AD yerel uygulaması**. Hizmetten hizmete kimlik doğrulaması için Azure AD uygulama yapılandırma hakkında yönergeler için bkz [hizmeti için kimlik doğrulaması Azure Active Directory kullanarak Data Lake Store ile](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

* Abonelik kimliği Hello Azure Portal ' alabilirsiniz. Örneğin, hello Data Lake Store hesabı dikey penceresinden kullanılabilir.
  
    ![Abonelik kimliği alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Azure AD etki alanı adı. Vurgulama hello fare hello sağ üst köşesindeki hello Azure Portal tarafından alabilir. Aşağıdaki Hello ekran görüntüsünde hello etki alanı adıdır **contoso.onmicrosoft.com**, ve hello GUID köşeli ayraçlar içinde hello Kiracı kimliği. 
  
    ![AAD etki alanı alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Son kullanıcı kimlik doğrulaması
Azure AD ile tooyour uygulamada bir son kullanıcı toolog isterseniz, önerilen yaklaşımı hello budur. Uygulamanızın mümkün tooaccess hello Azure kaynaklarıyla olacaktır aynı erişim düzeyini oturum hello son kullanıcı olarak. Son kullanıcıların kimlik bilgilerini düzenli aralıklarla uygulama toomaintain erişiminizi sırayla tooprovide gerekir.

Merhaba son kullanıcı oturum açma sahip hello uygulamanız bir erişim belirteci ve bir yenileme belirteci verilir sonucudur. ekli tooeach isteği tooData Lake Store veya Data Lake Analytics yapılan Hello erişim belirtecini alır ve varsayılan olarak bir saat için geçerli olduğundan. Merhaba yenileme belirteci yeni bir erişim belirteci ve düzenli olarak kullandıysanız için geçerli varsayılan olarak, tootwo hafta yukarı kullanılan tooobtain olabilir. Son kullanıcı oturum açma için iki farklı yaklaşım kullanabilirsiniz.

### <a name="using-hello-oauth-20-pop-up"></a>Merhaba OAuth 2.0 açılır kullanma
Uygulamanızın hangi hello son kullanıcı kimlik bilgilerini girebilirsiniz bir OAuth 2.0 yetkilendirme açılır tetikleyebilir. Bu açılır pencere hello Azure AD iki öğeli kimlik doğrulamasını (2FA) işlemiyle gerektiğinde de çalışır. 

> [!NOTE]
> Bu yöntem henüz hello Azure AD Authentication Library (ADAL) Python veya Java için desteklenmiyor.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Kullanıcı kimlik bilgilerini doğrudan geçirme
Uygulamanızın doğrudan kullanıcı kimlik bilgilerini tooAzure AD sağlayabilirsiniz. Bu yöntem yalnızca Kuruluş Kimliği kullanıcı hesaplarıyla çalışır; uyumlu değil kişisel ile / "live ID" kullanıcı hesapları da dahil olmak üzere, bitiş @outlook.com veya @live.com. Ayrıca, bu yöntem, Azure AD iki öğeli kimlik doğrulamasını (2FA) gerektiren kullanıcı hesaplarını ile uyumlu değil.

### <a name="what-do-i-need-toouse-this-approach"></a>Ne bu yaklaşım toouse ihtiyacım?
* Azure AD etki alanı adı. Bu, zaten bu makalenin hello önkoşul olarak listelenir.
* Azure AD **yerel uygulama**
* Hello Azure AD yerel uygulama için uygulama kimliği
* Azure AD yerel uygulaması hello için yeniden yönlendirme URI'si
* Yetki verilmiş izinleri ayarlayın


## <a name="step-1-create-an-active-directory-native-application"></a>1. adım: Active Directory yerel uygulama oluşturma

Oluşturun ve Azure AD yerel uygulaması son kullanıcı kimlik doğrulaması için Azure Data Lake Azure Active Directory'yi kullanarak Store ile yapılandırın. Yönergeler için bkz: [Azure AD uygulaması oluşturmasına](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Bağlantı yukarıdaki hello Hello yönergeleri aşağıdaki hatayla seçtiğinizden emin olun **yerel** hello ekran görüntüsünde gösterildiği gibi uygulama türü için.

![Web uygulaması oluşturma](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "yerel uygulama oluştur")

## <a name="step-2-get-application-id-and-redirect-uri"></a>2. adım: uygulama kimliği alma ve yeniden yönlendirme URI'si

Bkz: [hello uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Merhaba Klasik Azure portalı hello istemci kimliği olarak da bilinir) tooretrieve hello uygulamanın uygulama kimliğini hello Azure AD yerel.

tooretrieve hello yeniden yönlendirme URI'si, hello adımları izleyin.

1. Hello Azure Portalı ' seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz hello Azure AD yerel uygulama'yı tıklatın.

2. Merhaba gelen **ayarları** Merhaba uygulaması için dikey tıklayın **yeniden yönlendirme URI'ler**.

    ![Get yeniden yönlendirme URI'si](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Görüntülenen hello değerini kopyalayın.


## <a name="step-3-set-permissions"></a>3. adım: İzinleri ayarlama

1. Hello Azure Portalı ' seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz hello Azure AD yerel uygulama'yı tıklatın.

2. Merhaba gelen **ayarları** Merhaba uygulaması için dikey tıklayın **gerekli izinleri**ve ardından **Ekle**.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. Merhaba, **eklemek API erişimini** dikey penceresinde'ı tıklatın **bir API seçin**, tıklatın **Azure Data Lake**ve ardından **seçin**.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  Merhaba, **API erişimini eklemek** dikey penceresinde tıklatın **izinler seçeneğini belirleyin**, Seç onay kutusunu toogive hello **tooData Lake Store tam erişim**ve ardından **seçin **.

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    **Bitti**’ye tıklayın.

5. Yineleme hello en son iki adımı toogrant izinlerini **Windows Azure Hizmet Yönetimi API'si** de.
   
## <a name="next-steps"></a>Sonraki adımlar
Bu makalede Azure AD yerel uygulaması oluşturulur ve hello bilgileri istemci uygulamalarınızı .NET SDK'sı, Java SDK'sı, REST API vb. kullanarak yazmanız gerekir. Şimdi toouse hello Azure AD web uygulama toofirst Data Lake Store ile nasıl kimlik doğrulaması hakkında konuşun ve hello deposu üzerinde başka işlemler gerçekleştirmek makaleler aşağıdaki toohello devam edebilirsiniz.

* [.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-net-sdk.md)
* [Azure Data Lake Java SDK'sını kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-java-sdk.md)
* [Azure Data Lake REST API kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-rest-api.md)

