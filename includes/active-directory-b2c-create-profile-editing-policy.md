tooenable profil düzenleme uygulamanızdaki bir profili ilkesi düzenleme toocreate gerekir. Bu ilke tüketicileri profil düzenleme ve hello içeriğini Merhaba uygulaması başarılı tamamlanma alacak belirteçleri sırasında gidecek hello deneyimleri açıklanmaktadır.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Merhaba ilkeleri ayarları bölümünde **profili ilkeleri düzenleme** tıklatıp **+ Ekle**.

![İlkeleri düzenleme profili seçin ve hello Ekle düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Bir ilke girin **adı** uygulama tooreference için. Örneğin, `SiPe` girin.

**Kimlik sağlayıcıları**’nı seçin ve **Yerel Hesapla Oturum Aç**’ı işaretleyin. İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz. **Tamam** düğmesine tıklayın.

![Yerel hesap oturum açma kimlik sağlayıcısı olarak seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

**Profil öznitelikleri**’ni seçin. Öznitelikleri hello tüketici görüntüleyebilir ve bunların profilinde düzenleyebilirsiniz seçin. Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin. **Tamam** düğmesine tıklayın.

![Bazı öznitelikler seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

**Uygulama talepleri**’ni seçin. Başarılı bir profili düzenleme deneyimi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin. Örneğin, **Görünen Ad** ve **Posta Kodu**’nu seçin.

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Tıklatın **oluşturma** tooadd hello ilkesi. Hello ilkesi olarak listelenen **B2C_1_SiPe**. Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.

Açık hello İlkesi seçerek **B2C_1_SiPe**. Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Ayar      | Değer  |
| ------------ | ------ |
| **Uygulamalar** | Contoso B2C uygulaması |
| **Yanıt URL'sini seçin** | `https://localhost:44316/` |

Yeni bir tarayıcı sekmesi açar ve müşteri deneyimi yapılandırıldığı şekilde düzenleyerek hello profil doğrulayabilirsiniz.

> [!NOTE]
> İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.
>