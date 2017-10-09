## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="acbea-101">Intel NUC hazırlama</span><span class="sxs-lookup"><span data-stu-id="acbea-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="acbea-102">toocomplete hello donanım Kurulum şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="acbea-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="acbea-103">Merhaba Seti'nde dahil, Intel NUC toohello güç kaynağı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="acbea-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="acbea-104">Ethernet kablosu kullanarak Intel NUC tooyour ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="acbea-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="acbea-105">Intel NUC ağ geçidi cihazınız hello donanım Kurulumu tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="acbea-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="acbea-106">Oturum açma ve hello terminal erişim</span><span class="sxs-lookup"><span data-stu-id="acbea-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="acbea-107">İki seçenek tooaccess, Intel NUC bir terminal ortamına sahip:</span><span class="sxs-lookup"><span data-stu-id="acbea-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="acbea-108">Klavye varsa ve bağlı tooyour Intel NUC izlemek, hello Kabuğu doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbea-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="acbea-109">Merhaba varsayılan kimlik bilgileri olan kullanıcı adı **kök** ve parola **kök**.</span><span class="sxs-lookup"><span data-stu-id="acbea-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="acbea-110">Masaüstü makinenizden SSH kullanarak, Intel NUC erişim hello Kabuğu.</span><span class="sxs-lookup"><span data-stu-id="acbea-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="acbea-111">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="acbea-111">Sign in with SSH</span></span>

<span data-ttu-id="acbea-112">toosign SSH oturum Intel NUC başlangıç IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="acbea-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="acbea-113">Klavye varsa ve bağlı tooyour Intel NUC izlemek, hello kullan `ifconfig` komut toofind başlangıç IP adresi.</span><span class="sxs-lookup"><span data-stu-id="acbea-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="acbea-114">Alternatif olarak, ağınızdaki aygıtların tooyour yönlendirici toolist hello adreslerini bağlayın.</span><span class="sxs-lookup"><span data-stu-id="acbea-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="acbea-115">Kullanıcı adıyla oturum **kök** ve parola **kök**.</span><span class="sxs-lookup"><span data-stu-id="acbea-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="acbea-116">İsteğe bağlı: Intel NUC üzerinde bir klasör paylaşın</span><span class="sxs-lookup"><span data-stu-id="acbea-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="acbea-117">İsteğe bağlı olarak, masaüstü ortamınızı, Intel NUC tooshare bir klasör isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbea-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="acbea-118">Bir klasör paylaşımı, tercih edilen Masaüstü metin düzenleyici, toouse sağlar (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Intel NUC tooedit dosyalarda `nano` veya `vi`.</span><span class="sxs-lookup"><span data-stu-id="acbea-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="acbea-119">tooshare Windows, bir klasör, Intel NUC hello üzerinde Samba sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="acbea-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="acbea-120">Alternatif olarak, Masaüstü makinenizde SFTP istemci ile Merhaba Intel NUC hello SFTP sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="acbea-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
