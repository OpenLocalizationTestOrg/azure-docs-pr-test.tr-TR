<span data-ttu-id="c8b30-101">tooenable oturum açma, uygulamanızda, bir oturum açma toocreate İlkesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8b30-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="c8b30-102">Bu ilke başarılı oturum açma işlemleri üzerinde tüketicileri oturum açma sırasında geçilir ve uygulama hello belirteçleri Merhaba içeriğine alacak hello deneyimleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c8b30-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="c8b30-103">Merhaba ilkeleri ayarları bölümünde **oturum açma veya kaydolma ilkeleri** tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c8b30-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Oturum açma veya kaydolma ilkeleri’ni seçin ve Ekle düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="c8b30-105">Bir ilke girin **adı** uygulama tooreference için.</span><span class="sxs-lookup"><span data-stu-id="c8b30-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="c8b30-106">Örneğin, `SiUpIn` girin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="c8b30-107">**Kimlik sağlayıcıları**’nı seçin ve **E-posta ile kaydolma**’yı işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="c8b30-108">İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b30-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="c8b30-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8b30-109">Click **OK**.</span></span>

![E-posta kaydolma kimlik sağlayıcısı olarak seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="c8b30-111">**Kaydolma öznitelikleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="c8b30-112">Öznitelikleri seçin toocollect hello tüketici gelen kayıt sırasında istiyor.</span><span class="sxs-lookup"><span data-stu-id="c8b30-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="c8b30-113">Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="c8b30-114">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8b30-114">Click **OK**.</span></span>

![Bazı öznitelikler seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="c8b30-116">**Uygulama talepleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-116">Select **Application claims**.</span></span> <span data-ttu-id="c8b30-117">Başarılı bir kayıt veya oturum açma deneyimi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="c8b30-118">Örneğin, **Görünen Ad**, **Kimlik Sağlayıcısı**, **Posta Kodu**, **Kullanıcı yeni** ve **Kullanıcının Nesne Kimliği**’ni işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="c8b30-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="c8b30-120">Tıklatın **oluşturma** tooadd hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="c8b30-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="c8b30-121">Hello ilkesi olarak listelenen **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="c8b30-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="c8b30-122">Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.</span><span class="sxs-lookup"><span data-stu-id="c8b30-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="c8b30-123">Açık hello İlkesi seçerek **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="c8b30-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="c8b30-124">Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="c8b30-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="c8b30-126">Ayar</span><span class="sxs-lookup"><span data-stu-id="c8b30-126">Setting</span></span>      | <span data-ttu-id="c8b30-127">Değer</span><span class="sxs-lookup"><span data-stu-id="c8b30-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="c8b30-128">**Uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="c8b30-128">**Applications**</span></span> | <span data-ttu-id="c8b30-129">Contoso B2C uygulaması</span><span class="sxs-lookup"><span data-stu-id="c8b30-129">Contoso B2C app</span></span> |
| <span data-ttu-id="c8b30-130">**Yanıt URL'sini seçin**</span><span class="sxs-lookup"><span data-stu-id="c8b30-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="c8b30-131">Yeni bir tarayıcı sekmesi açar ve yapılandırıldığı şekilde hello oturum açma veya kaydolma Müşteri Deneyimi doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b30-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="c8b30-132">İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8b30-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>