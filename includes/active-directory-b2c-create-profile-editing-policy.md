Uygulamanızda profili düzenlemeyi etkinleştirmek için bir ilke düzenleme profili oluşturmanız gerekir. Bu ilke, tüketicilerin profil düzenleme sırasında karşılaşacağı deneyimleri ve işlem başarıyla tamamlandığında uygulamanın alacağı belirteçlerin içeriğini açıklar.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Ayarların ilkeler bölümünde **Profil düzenleme ilkeleri**’ni seçip **+ Ekle**’ye tıklayın.

![Profil düzenleme ilkelerini seçin ve Ekle düğmesine tıklayın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Uygulamanızın başvuracağı ilke **Adını** girin. Örneğin, `SiPe` girin.

**Kimlik sağlayıcıları**’nı seçin ve **Yerel Hesapla Oturum Aç**’ı işaretleyin. İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz. **Tamam** düğmesine tıklayın.

![Kimlik sağlayıcısı olarak Yerel Hesapla Oturum Aç’ı seçin ve Tamam düğmesine tıklayın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

**Profil öznitelikleri**’ni seçin. Tüketicinin profilinde görüntüleyebileceği ve düzenleyebileceği öznitelikleri seçin. Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin. **Tamam** düğmesine tıklayın.

![Bazı öznitelikleri seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

**Uygulama talepleri**’ni seçin. Başarılı bir profil düzenleme deneyiminden sonra uygulamanıza geri gönderilen yetkilendirme belirteçlerinde döndürülmesini istediğiniz talepleri seçin. Örneğin, **Görünen Ad** ve **Posta Kodu**’nu seçin.

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

İlkeyi eklemek için **Oluştur**’a tıklayın. İlke **B2C_1_SiPe** olarak listelenir. Ada **B2C_1_** öneki eklenir.

**B2C_1_SiPe** adını seçerek ilkeyi açın. Tabloda belirtilen ayarlarını doğrulayın, ardından **Şimdi Çalıştır**’a tıklayın.

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Ayar      | Değer  |
| ------------ | ------ |
| **Uygulamalar** | Contoso B2C uygulaması |
| **Yanıt URL'sini seçin** | `https://localhost:44316/` |

Yeni bir tarayıcı sekmesi açılır. Buradan, profil düzenleme için yapılandırılan tüketici deneyimini doğrulayabilirsiniz.

> [!NOTE]
> İlke oluşturma ve güncelleştirmelerinin etkili olması bir dakika kadar alabilir.
>