<span data-ttu-id="cadc4-101">tooenable profil düzenleme uygulamanızdaki bir profili ilkesi düzenleme toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="cadc4-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="cadc4-102">Bu ilke tüketicileri profil düzenleme ve hello içeriğini Merhaba uygulaması başarılı tamamlanma alacak belirteçleri sırasında gidecek hello deneyimleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cadc4-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="cadc4-103">Merhaba ilkeleri ayarları bölümünde **profili ilkeleri düzenleme** tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cadc4-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![İlkeleri düzenleme profili seçin ve hello Ekle düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="cadc4-105">Bir ilke girin **adı** uygulama tooreference için.</span><span class="sxs-lookup"><span data-stu-id="cadc4-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="cadc4-106">Örneğin, `SiPe` girin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="cadc4-107">**Kimlik sağlayıcıları**’nı seçin ve **Yerel Hesapla Oturum Aç**’ı işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="cadc4-108">İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cadc4-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="cadc4-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cadc4-109">Click **OK**.</span></span>

![Yerel hesap oturum açma kimlik sağlayıcısı olarak seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="cadc4-111">**Profil öznitelikleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-111">Select **Profile attributes**.</span></span> <span data-ttu-id="cadc4-112">Öznitelikleri hello tüketici görüntüleyebilir ve bunların profilinde düzenleyebilirsiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="cadc4-113">Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="cadc4-114">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cadc4-114">Click **OK**.</span></span>

![Bazı öznitelikler seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="cadc4-116">**Uygulama talepleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-116">Select **Application claims**.</span></span> <span data-ttu-id="cadc4-117">Başarılı bir profili düzenleme deneyimi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="cadc4-118">Örneğin, **Görünen Ad** ve **Posta Kodu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="cadc4-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="cadc4-120">Tıklatın **oluşturma** tooadd hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="cadc4-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="cadc4-121">Hello ilkesi olarak listelenen **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="cadc4-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="cadc4-122">Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.</span><span class="sxs-lookup"><span data-stu-id="cadc4-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="cadc4-123">Açık hello İlkesi seçerek **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="cadc4-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="cadc4-124">Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="cadc4-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="cadc4-126">Ayar</span><span class="sxs-lookup"><span data-stu-id="cadc4-126">Setting</span></span>      | <span data-ttu-id="cadc4-127">Değer</span><span class="sxs-lookup"><span data-stu-id="cadc4-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="cadc4-128">**Uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="cadc4-128">**Applications**</span></span> | <span data-ttu-id="cadc4-129">Contoso B2C uygulaması</span><span class="sxs-lookup"><span data-stu-id="cadc4-129">Contoso B2C app</span></span> |
| <span data-ttu-id="cadc4-130">**Yanıt URL'sini seçin**</span><span class="sxs-lookup"><span data-stu-id="cadc4-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="cadc4-131">Yeni bir tarayıcı sekmesi açar ve müşteri deneyimi yapılandırıldığı şekilde düzenleyerek hello profil doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cadc4-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="cadc4-132">İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cadc4-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>