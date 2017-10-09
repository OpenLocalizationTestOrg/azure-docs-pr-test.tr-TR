tooenable oturum açma, uygulamanızda, bir oturum açma toocreate İlkesi gerekir. Bu ilke başarılı oturum açma işlemleri üzerinde tüketicileri oturum açma sırasında geçilir ve uygulama hello belirteçleri Merhaba içeriğine alacak hello deneyimleri açıklanmaktadır.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Merhaba ilkeleri ayarları bölümünde **oturum açma veya kaydolma ilkeleri** tıklatıp **+ Ekle**.

![Oturum açma veya kaydolma ilkeleri’ni seçin ve Ekle düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Bir ilke girin **adı** uygulama tooreference için. Örneğin, `SiUpIn` girin.

**Kimlik sağlayıcıları**’nı seçin ve **E-posta ile kaydolma**’yı işaretleyin. İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz. **Tamam** düğmesine tıklayın.

![E-posta kaydolma kimlik sağlayıcısı olarak seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

**Kaydolma öznitelikleri**’ni seçin. Öznitelikleri seçin toocollect hello tüketici gelen kayıt sırasında istiyor. Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin. **Tamam** düğmesine tıklayın.

![Bazı öznitelikler seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

**Uygulama talepleri**’ni seçin. Başarılı bir kayıt veya oturum açma deneyimi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin. Örneğin, **Görünen Ad**, **Kimlik Sağlayıcısı**, **Posta Kodu**, **Kullanıcı yeni** ve **Kullanıcının Nesne Kimliği**’ni işaretleyin.

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Tıklatın **oluşturma** tooadd hello ilkesi. Hello ilkesi olarak listelenen **B2C_1_SiUpIn**. Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.

Açık hello İlkesi seçerek **B2C_1_SiUpIn**. Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Ayar      | Değer  |
| ------------ | ------ |
| **Uygulamalar** | Contoso B2C uygulaması |
| **Yanıt URL'sini seçin** | `https://localhost:44316/` |

Yeni bir tarayıcı sekmesi açar ve yapılandırıldığı şekilde hello oturum açma veya kaydolma Müşteri Deneyimi doğrulayabilirsiniz.

> [!NOTE]
> İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.
>