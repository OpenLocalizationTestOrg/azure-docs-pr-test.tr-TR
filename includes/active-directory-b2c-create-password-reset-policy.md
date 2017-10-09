<span data-ttu-id="f269e-101">uygulamanızda sıfırlama tooenable hassas parola toocreate bir parola sıfırlama İlkesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f269e-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="f269e-102">Bu hello Kiracı genelinde parola sıfırlama belirtilen seçeneği Not [burada](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="f269e-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="f269e-103">Bu ilke başarılı tamamlanma hello tüketicileri parola sıfırlama sırasında geçtikleri ve uygulama hello belirteçleri Merhaba içeriğine alacak hello deneyimleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f269e-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="f269e-104">Merhaba ilkeleri ayarları bölümünde **parola sıfırlama ilkeleri** tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f269e-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Oturum açma veya kaydolma İlkeleri'ni seçin ve hello Ekle düğmesini tıklatın](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="f269e-106">Bir ilke girin **adı** uygulama tooreference için.</span><span class="sxs-lookup"><span data-stu-id="f269e-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="f269e-107">Örneğin, `SSPR` girin.</span><span class="sxs-lookup"><span data-stu-id="f269e-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="f269e-108">**Kimlik sağlayıcıları**’nı seçin ve **E-posta adresi kullanarak parola sıfırla**’yı işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="f269e-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="f269e-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f269e-109">Click **OK**.</span></span>

![Bir kimlik sağlayıcısı e-posta adresini kullanarak parola sıfırlama seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="f269e-111">**Uygulama talepleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="f269e-111">Select **Application claims**.</span></span> <span data-ttu-id="f269e-112">Başarılı parola sıfırlama deneyiminizi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin.</span><span class="sxs-lookup"><span data-stu-id="f269e-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="f269e-113">Örneğin, **Kullanıcının Nesne Kimliği**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="f269e-113">For example, select **User's Object ID**.</span></span>

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="f269e-115">Tıklatın **oluşturma** tooadd hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="f269e-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="f269e-116">Hello ilkesi olarak listelenen **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="f269e-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="f269e-117">Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.</span><span class="sxs-lookup"><span data-stu-id="f269e-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="f269e-118">Açık hello İlkesi seçerek **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="f269e-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="f269e-119">Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="f269e-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="f269e-121">Ayar</span><span class="sxs-lookup"><span data-stu-id="f269e-121">Setting</span></span>      | <span data-ttu-id="f269e-122">Değer</span><span class="sxs-lookup"><span data-stu-id="f269e-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="f269e-123">**Uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="f269e-123">**Applications**</span></span> | <span data-ttu-id="f269e-124">Contoso B2C uygulaması</span><span class="sxs-lookup"><span data-stu-id="f269e-124">Contoso B2C app</span></span> |
| <span data-ttu-id="f269e-125">**Yanıt URL'sini seçin**</span><span class="sxs-lookup"><span data-stu-id="f269e-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="f269e-126">Yeni bir tarayıcı sekmesi açar ve müşteri deneyimi, uygulamanızda hello parola sıfırlama doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f269e-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="f269e-127">İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f269e-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
