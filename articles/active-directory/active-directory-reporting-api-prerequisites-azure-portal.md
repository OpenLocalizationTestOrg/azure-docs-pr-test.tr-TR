---
title: aaaPrerequisites tooaccess hello Azure AD raporlama API'si | Microsoft Docs
description: "Merhaba Önkoşullar tooaccess hello Azure AD raporlama API'si hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Önkoşullar tooaccess hello Azure AD raporlama API'si

Merhaba [API'leri raporlama Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello verilerle sağlayın. Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.

API kullandığı raporlama hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize erişim toohello web API'leri. 

tooget erişim toohello raporlama verileri hello API aracılığıyla, toohave atanan rollerin aşağıdaki hello biri gerekir:

- Güvenlik okuyucusu
- Güvenlik Yöneticisi
- Genel yönetici


tooprepare raporlama API'si, erişim toohello yapmanız gerekir:

1. Bir uygulamayı kaydetme 
2. İzinleri 
3. Yapılandırma ayarlarını toplayın 

Sorularınız, sorunları veya Geri bildiriminiz için lütfen [bir destek bileti dosya](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Bir Azure Active Directory uygulamayı kaydetme

Bir komut dosyası kullanarak API raporlama hello erişiyorsanız bile tooregister uygulama gerekir. Bu size verir bir **uygulama kimliği**, yetkilendirme çağrısı için gerekli olduğu ve kod tooreceive belirteçleri sağlar.

tooconfigure dizin tooaccess hello Azure AD raporlama API'nizi, Azure portalı, aynı zamanda hello üyesi olan Azure yönetici hesabı ile toohello içinde imzalamalısınız **genel yönetici** Azure AD kiracınızda dizin rolü .

> [!IMPORTANT]
> Bu gibi "Yönetici" ayrıcalıkları olan kimlik bilgileri altında çalışan uygulamalar çok güçlü olabilir, bu nedenle lütfen emin tookeep hello uygulamanın kimliği/parola kimlik bilgileri güvenli.
> 


**bir Azure Active Directory uygulaması tooregister:**

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Merhaba üzerinde **Azure Active Directory** dikey penceresinde tıklatın **uygulama kayıtlar**.

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Merhaba üzerinde **uygulama kayıtlar** hello araç çubuğunda hello üstte dikey tıklayın **yeni uygulama kaydı**.

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Merhaba üzerinde **oluşturma** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. Merhaba, **adı** metin kutusuna, türü `Reporting API application`.

    b. Olarak **uygulama türü**seçin **Web uygulaması / API**.

    c. Merhaba, **oturum açma URL'si** metin kutusuna, türü `https://localhost`.

    d. **Oluştur**'a tıklayın. 


## <a name="grant-permissions"></a>İzinleri 

Merhaba amacı, bu adımı uygulamanız toogrant olan **dizin verilerini okuma** izinleri toohello **Windows Azure Active Directory** API.

![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant, API uygulama izni toouse hello:**

1. Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.

2. Merhaba üzerinde **raporlama API'si uygulama** hello araç çubuğunda hello üstte dikey tıklayın **ayarları**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **gerekli izinleri**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Merhaba üzerinde **gerekli izinleri** dikey penceresinde hello **API** tıklatın **Windows Azure Active Directory**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Merhaba üzerinde **erişimi etkinleştir** dikey penceresinde, select **dizin verilerini okuma**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Merhaba üstte Hello araç çubuğunda **kaydetmek**.

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Yapılandırma ayarlarını toplayın 
Bu bölümde, nasıl gösterilir dizininizden ayarları aşağıdaki tooget hello:

* Etki alanı adı
* İstemci kimliği
* Gizli anahtar

Bu değerleri çağrıları toohello raporlama API yapılandırırken gerekir. 

### <a name="get-your-domain-name"></a>Etki alanı adınızı alma

**tooget etki alanı adınızı:**

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Merhaba üzerinde **Azure Active Directory** dikey penceresinde tıklatın **etki alanı adları**.

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Etki alanı adınızı hello etki alanları listesinden kopyalayın.


### <a name="get-your-applications-client-id"></a>Uygulamanızın istemci kimliği alın

**tooget uygulamanızın istemci kimliği:**

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.

3. Merhaba üzerinde **raporlama API'si uygulama** dikey penceresine, hello **uygulama kimliği**,'ı tıklatın **tıklatın toocopy**.

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Uygulamanızın istemci parolası mı almak
tooget uygulamanızın istemci gizli, toocreate yeni bir anahtar gerekir ve bu değer daha sonra artık olası tooretrieve olmadığından hello yeni anahtarı kaydetme sırasında değerini kaydedin.

**tooget uygulamanızın istemci parolası:**

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.
   
    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Merhaba üzerinde **uygulama kayıtlar** hello uygulamalar listesinde, dikey tıklayın **raporlama API'si uygulama**.


3. Merhaba üzerinde **raporlama API'si uygulama** hello araç çubuğunda hello üstte dikey tıklayın **ayarları**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Merhaba üzerinde **ayarları** dikey penceresinde hello **APIR erişim** 'yi tıklatın **anahtarları**. 

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Merhaba üzerinde **anahtarları** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:

    ![Uygulamayı Kaydet](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. Merhaba, **açıklama** metin kutusuna, türü `Reporting API`.

    b. Olarak **Expires**seçin **2 yıl içinde**.

    c. **Kaydet** düğmesine tıklayın.

    d. Merhaba anahtar değerini kopyalayın.


## <a name="next-steps"></a>Sonraki Adımlar
* , Tooaccess hello Azure AD verilerden hello gibi raporlama API programlı bir şekilde? Kullanıma [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).
* Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).  

