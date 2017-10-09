---
title: "Hizmetten hizmete kimlik doğrulaması: Data Lake Store Azure Active Directory ile | Microsoft Docs"
description: "Bilgi nasıl Azure Active Directory kullanarak Data Lake Store ile tooachieve hizmeti için kimlik doğrulaması"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Azure Active Directory kullanarak Data Lake Store ile hizmet kimlik doğrulaması
> [!div class="op_single_selector"]
> * [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md)
> * [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store, Azure Active Directory kimlik doğrulaması için kullanır. Azure Data Lake Store veya Azure Data Lake Analytics ile çalışan bir uygulama geliştirme önce ilk tooauthenticate yönteminizi karar vermeniz gerekir uygulamanızı Azure Active Directory'ye (Azure AD). Merhaba iki ana seçenekleri şunlardır:

* Son kullanıcı kimlik doğrulaması 
* Hizmetten hizmete kimlik doğrulaması (Bu makalede) 

Ekli tooeach yapılan istek tooAzure Data Lake Store veya Azure Data Lake Analytics alır bir OAuth 2.0 belirteç ile sağlanan uygulamanızda hem bu seçenekleri sonuçlanır.

Bu makale konuşmaları konusunda oluşturma bir **hizmeti için kimlik doğrulaması için Azure AD web uygulaması**. Son kullanıcı kimlik doğrulaması için Azure AD uygulama yapılandırma hakkında yönergeler için bkz [son kullanıcı kimlik doğrulaması Azure Active Directory kullanarak Data Lake Store ile](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>1. adım: bir Active Directory web uygulaması oluşturma

Oluşturun ve Azure AD web uygulaması hizmeti için kimlik doğrulaması için Azure Data Lake Azure Active Directory'yi kullanarak Store ile yapılandırın. Yönergeler için bkz: [Azure AD uygulaması oluşturmasına](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Bağlantı yukarıdaki hello Hello yönergeleri aşağıdaki hatayla seçtiğinizden emin olun **Web uygulaması / API** hello ekran görüntüsünde gösterildiği gibi uygulama türü için.

![Web uygulaması oluşturma](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "web uygulaması oluştur")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>2. adım: uygulama kimliği, kimlik doğrulama anahtarı ve Kiracı kimliği alma
Program aracılığıyla oturum açarken, uygulamanız için hello kimliği gerekir. Merhaba uygulama kendi kimlik bilgileri altında çalışıyorsa, ayrıca bir kimlik doğrulama anahtarı gerekir.

* Nasıl tooretrieve hello uygulama Kimliğini ve kimlik doğrulama uygulamanız için (aynı zamanda çağrılan hello gizli) anahtar ile ilgili yönergeler için bkz: [Get uygulama kimliği ile kimlik doğrulama anahtarı](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Nasıl tooretrieve hello Kiracı kimliği ile ilgili yönergeler için bkz: [alma Kiracı kimliği](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>3. adım: hello Azure AD uygulama toohello Azure Data Lake Store hesabına dosya veya klasör (yalnızca hizmeti için kimlik doğrulaması için) atama
1. Yeni toohello oturum [Azure portal](https://portal.azure.com) ve tooassociate hello daha önce oluşturduğunuz Azure Active Directory uygulaması ile istediğiniz hello Azure Data Lake Store hesabını açın.
2. Data Lake Store hesabı dikey pencerenizde, **Veri Gezgini**'ne tıklayın.
   
    ![Data Lake Store hesabında dizin oluşturmak](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Data Lake hesabında dizinler oluşturma")
3. Merhaba, **Veri Gezgini** dikey penceresinde hello dosya veya kendisi için tooprovide erişim toohello Azure AD uygulama istediğiniz ve ardından klasörü tıklatın **erişim**. tooconfigure erişim tooa dosyasını tıklatmalıdır **erişim** hello gelen **Dosya Önizleme** dikey.
   
    ![Data Lake dosya sisteminde ACL'leri ayarlamak](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Data Lake dosya sistemi üzerindeki ACL'lerin ayarlayın")
4. Merhaba **erişim** dikey penceresinde hello standart erişim listelenir ve özel erişim toohello kök atanmış. Merhaba tıklatın **Ekle** simgesi tooadd Özel düzey ACL'ler.
   
    ![Liste standart ve özel erişim](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "listesinde standart ve özel erişim")
5. Merhaba tıklatın **Ekle** simgesi tooopen hello **eklemek özel erişim** dikey. Bu dikey pencerede tıklatın **kullanıcı veya Grup Seç**ve ardından **kullanıcı veya Grup Seç** dikey penceresinde, önceden oluşturduğunuz hello Azure Active Directory Uygulama arayın. Grupları toosearch çok varsa, hello metin kutusu hello üst toofilter hello grup adı kullanın. Tooadd istediğiniz ve ardından hello grubu tıklatın **seçin**.
   
    ![Grup ekleme](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "grup ekleme")
6. Tıklatın **Select izinleri**, hello izinler seçeneğini belirleyin ve varsayılan olarak ACL tooassign hello izinleri istediğinizi ACL ya da her ikisini de erişim. **Tamam** düğmesine tıklayın.
   
    ![İzinleri toogroup Ata](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "izinleri toogroup atayın")
   
    Data Lake Store ve varsayılan/erişim ACL izinleri hakkında daha fazla bilgi için bkz: [Data Lake Store'da erişim denetimi](data-lake-store-access-control.md).
7. Merhaba, **eklemek özel erişim** dikey penceresinde tıklatın **Tamam**. Merhaba yeni eklenen grubuyla ilişkili hello izinleri şimdi hello listelenir **erişim** dikey.
   
    ![İzinleri toogroup Ata](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "izinleri toogroup atayın")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>4. adım: hello OAuth 2.0 belirteç uç noktası (yalnızca Java tabanlı uygulamalar için) alın.

1. Yeni toohello oturum [Azure portal](https://portal.azure.com) ve Active Directory hello sol bölmeden'ı tıklatın.

2. Merhaba sol bölmeden tıklatın **uygulama kayıtlar**.

3. Merhaba uygulama kayıtlar dikey Hello üstten tıklatın **uç noktaları**.

    ![OAuth belirteç uç noktası](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth belirteç uç noktası")

4. Uç noktaları Hello listeden hello OAuth 2.0 belirteç uç noktası kopyalayın.

    ![OAuth belirteç uç noktası](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth belirteç uç noktası")   

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede Azure AD web uygulaması oluşturulur ve .NET SDK'sı, Java SDK'sı vb. kullanarak Yazar istemci uygulamalarınızda gereksinim hello bilgileri toplanmaz. Şimdi toouse hello Azure AD web uygulama toofirst Data Lake Store ile nasıl kimlik doğrulaması hakkında konuşun ve hello deposu üzerinde başka işlemler gerçekleştirmek makaleler aşağıdaki toohello devam edebilirsiniz.

* [.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-net-sdk.md)
* [Azure Data Lake Java SDK'sını kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-java-sdk.md)

Bu makalede bir kullanıcının asıl yukarı ve uygulamanız için çalışan hello temel adımlar gerekli tooget gitti. Makaleler tooget daha fazla bilgi aşağıdaki hello arayabilirsiniz:
* [PowerShell toocreate hizmet sorumlusu kullanın](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Hizmet asıl kimlik doğrulaması için sertifika kimlik doğrulamasını kullan](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Diğer yöntemleri tooauthenticate tooAzure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


