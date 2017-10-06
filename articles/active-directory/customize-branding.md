---
title: "oturum açma işleminiz sayfa hello Azure Active Directory aaaCustomize | Microsoft Docs"
description: "Bilgi nasıl tooadd şirket markasıyla toohello Azure oturum açma sayfası"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Hızlı Başlangıç: Azure AD içinde tooyour oturum açma sayfası markalama şirket ekleme
tooavoid Karışıklığı önlemek için birçok şirket tüm hello Web siteleri ve yönettikleri hizmetlerde tooapply tutarlı bir görünüm istiyor. Azure Active Directory (Azure AD) toocustomize hello hello oturum açma sayfası şirket Logonuzla ve özel renk düzenleri görünümünü sağlayarak bu yeteneği sağlar. Merhaba oturum açma sayfası 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar tooOffice içinde oturum açtığınızda görüntülenen hello sayfasıdır. Kimlik bilgilerinizi bu sayfayı tooenter ile etkileşim.

> [!NOTE]
> * Şirket markası yalnızca toohello Premium veya Azure AD Basic sürümüne yükselttiyseniz kullanılamıyor veya bir Office 365 lisansına sahip. toolearn bir özellik, lisans türü tarafından desteklenip desteklenmediğini denetleyin hello [Azure Active Directory fiyatlandırma bilgileri sayfası](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Azure Active Directory Premium ve Basic sürümleri Azure Active Directory Merhaba Dünya çapındaki örneğini kullanan Çin müşteriler için kullanılabilir. Azure Active Directory Premium ve Basic sürümleri şu anda Çin'de 21Vianet tarafından işletilen hello Microsoft Azure hizmetindeki desteklenmez. Daha fazla bilgi için bize hello başvurun [Azure Active Directory Forumu](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Merhaba oturum açma sayfasını özelleştirme

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Kullanıcılar bir kiracıya özgü URL gibi eriştiğinde marka özelleştirmeleri görünür hello Azure AD oturum açma sayfasında şirket [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Kullanıcıların www.office.com gibi genel bir URL'yi ziyaret ettiğinizde hello oturum açma sayfası şirket hello sistem hello kullanıcı olan bilmiyor çünkü özelleştirmeler markası içermiyor. Kullanıcılar kendi kullanıcı Kimliğini girin veya kullanıcı kutucuğunu seçtikten sonra şirket markası gösterir.

> [!NOTE]
> * Etki alanı adınızı hello "Etkin" olarak görünmesi gereken **etki alanları** kısmı hello yapılandırılmış markalama Azure portalı. Daha fazla bilgi için bkz: [özel etki alanı ekleme](add-custom-domain.md).
> * Oturum açma sayfası markalama toohello oturum açma sayfası kişisel Microsoft hesapları üzerinden taşımak değil. Çalışanlarınıza veya iş konuklar kişisel bir Microsoft hesabıyla oturum açarsanız, oturum açma sayfası hello kuruluşunuzun markası yansıtmaz.


### <a name="banner-logo"></a>Başlık logosu 

Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Merhaba başlık logosu hello oturum açma ve hello erişim paneli sayfası görüntülenir.<br>Merhaba kullanıcı adı genellikle girildikten sonra müşteri hello kullanıcının kuruluş belirlendikten sonra hello oturum açma sayfasında bu gösterir.  | Saydam JPG veya PNG<br>En fazla yükseklik: 36 piksel<br>En büyük genişliği: 245 piksel | Kuruluşunuzun logosu burada kullanın.<br>Saydam bir görüntü kullanın. Merhaba arka plan beyaz olacağını varsaymayın.<br>Logonuzun çevresindeki dolgunun hello görüntüde eklemeyin veya logonuzun orantısız küçük arar.

### <a name="username-hint"></a>Kullanıcı adı İpucu   
Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Merhaba ipucu metnini hello kullanıcı adı alanında özelleştirir. | Unicode metin too64 karakterleri ayarlama<br>Yalnızca düz metin | Konuk kullanıcılar, kuruluşun toosign tooyour uygulamasında dışında bekliyorsanız, bu ayarladığınız değil öneririz.
            
### <a name="sign-in-page-text"></a>Oturum açma sayfası metni   
Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Bu hello oturum açma hello formunun altında görünür ve kullanılan toocommunicate hello telefon numarası tooyour yardım masasına veya yasal bildirim gibi ek bilgileri olabilir. | Unicode metin too256 karakterleri ayarlama<br>Yalnızca düz metin (bağlantılar veya HTML etiketleri olmadan) 

### <a name="sign-in-page-image"></a>Oturum açma sayfası görüntüsü  
Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Bu hello oturum açma sayfası hello arka planda görünür bağlantılı toohello Center hello görüntülenebilir alanının ve ölçeklendirme ve toofill kırpma hello tarayıcı penceresi.  <br>Bu görüntü cep telefonları gibi dar ekranlarda gösterilmez.<br>Merhaba sayfa yüklendiğinde 0.55 opaklık siyah maskeyle bizim koduna göre bu görüntünün üzerinde uygulanır. | JPG veya PNG<br>Görüntü boyutları: 1920 x 1080 piksel<br>Dosya boyutu: &gt; 300 KB | <br>Görüntüleri kullanmak hiç burada güçlü konu odak. oturum açma Hello donuk form bu görüntüyü hello merkezi görünür ve hello görüntü hello tarayıcı penceresinde hello boyutuna bağlı olarak, herhangi bir bölümünü kapsar.<br>Merhaba dosya boyutu olası tooensure hızlı yükleme süreleri olabildiğince küçük tutun. 

### <a name="background-color"></a>Arka plan rengi
Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Bu renk hello arka plan görüntüsü düşük bant genişliğine sahip bağlantılarda yerine kullanılır. |   RGB renk onaltılık (örnek: #FFFFFF | Merhaba başlık logosu hello birincil rengini veya kuruluş renginiz kullanarak öneririz.

### <a name="show-option-tooremain-signed-in"></a>Açık seçeneği tooremain Göster
Açıklama | Kısıtlamalar | Öneriler
------- | ------- | ----------
Azure AD oturum açma verir hello kullanıcı hello seçeneği tooremain oturumu kapatın ve yeniden tarayıcısında açın. Bu toohide bu seçeneği kullanın.<br>Bu çok "Hayır" olarak toohide bu seçenek, kullanıcılarınızın. | &nbsp; | Bu, oturum yaşam etkilemez.<br>SharePoint Online ve Office 2010 özelliklerinden bazıları mümkün toochoose tooremain açık olan kullanıcıların bağlıdır. Gizli bu toobe ayarlarsanız, kullanıcılarınızın ek ve beklenmeyen komut istemlerini toosign de görebilirsiniz.

> [!NOTE]
> Tüm öğeler isteğe bağlıdır. Örneğin, hiçbir arka plan görüntüsü bir başlık logosu belirtirseniz, hello oturum açma sayfası hello hedef sitede (örneğin, Office 365), logo ve hello arka plan resmini gösterir.

## <a name="add-company-branding-tooyour-directory"></a>Şirket tooyour dizin markası ekleme

1. Çok oturum[Azure portal hello](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.
4. Merhaba üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select hello **Düzenle** komutu.

    ![Özel marka Düzenle](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Toocustomize istediğiniz hello öğeleri değiştirin. Tüm öğeler isteğe bağlıdır.
6. **Kaydet** düğmesine tıklayın.

Oturum açma toohello yapılan değişiklikler marka tooappear sayfa için tooan saat sürebilir.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Dile özgü şirket tooyour dizin markası ekleme

1. İçinde toohello oturum [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.
4. Merhaba üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select hello **dil eklemek** komutu.

    ![Dile özgü marka öğeleri ekleme](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Toocustomize istediğiniz hello öğeleri değiştirin. Tüm öğeler isteğe bağlıdır.
6. **Kaydet** düğmesine tıklayın.

Oturum açma toohello yapılan değişiklikler marka tooappear sayfa için tooan saat sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
Bu hızlı başlangıç nasıl tooadd şirket markasıyla tooyour Azure AD directory öğrendiniz. 

Bağlantı tooconfigure hello Azure AD'den de Azure portalında marka şirket aşağıdaki hello kullanabilirsiniz.

> [!div class="nextstepaction"]
> [Şirket markası yapılandırma](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 