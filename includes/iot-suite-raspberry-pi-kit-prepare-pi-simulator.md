## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="e2a8a-101">Böğürtlenli Pi hazırlama</span><span class="sxs-lookup"><span data-stu-id="e2a8a-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="e2a8a-102">Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="e2a8a-102">Install Raspbian</span></span>

<span data-ttu-id="e2a8a-103">Bu hello Raspberry Pi'yi kullanarak ilk kez kullanıyorsanız, hello Seti'nde bulunan hello SD kart üzerinde NOOBS kullanarak tooinstall hello Raspbian işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="e2a8a-104">Merhaba [Raspberry Pi yazılım Kılavuzu] [ lnk-install-raspbian] açıklar nasıl tooinstall Raspberry Pi'yi işletim sisteminde.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="e2a8a-105">Bu öğretici, Raspberry Pi'yi hello Raspbian işletim sisteminin yüklü olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="e2a8a-106">Hello dahil hello SD kart [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] yüklü NOOBS zaten.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="e2a8a-107">Merhaba Raspberry Pi'yi bu kartından önyükleme ve tooinstall hello Raspbian işletim sistemi seçin.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

<span data-ttu-id="e2a8a-108">toocomplete hello donanım Kurulum şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2a8a-108">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="e2a8a-109">Merhaba Seti'nde dahil, Raspberry Pi'yi toohello güç kaynağı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-109">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="e2a8a-110">Kit içinde bulunan hello Ethernet kablosu kullanarak Raspberry Pi'yi tooyour ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-110">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="e2a8a-111">Alternatif olarak, ayarlayabilirsiniz [kablosuz bağlantı] [ lnk-pi-wireless] Raspberry Pi'yi için.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="e2a8a-112">Merhaba donanım Kurulumu Raspberry Pi'yi tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-112">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="e2a8a-113">Oturum açma ve hello terminal erişim</span><span class="sxs-lookup"><span data-stu-id="e2a8a-113">Sign in and access hello terminal</span></span>

<span data-ttu-id="e2a8a-114">İki seçenek tooaccess, Raspberry Pi'yi bir terminal ortamına sahip:</span><span class="sxs-lookup"><span data-stu-id="e2a8a-114">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="e2a8a-115">Klavye varsa ve bağlı tooyour Raspberry Pi'yi izlemek, hello Raspbian GUI tooaccess bir terminal penceresi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-115">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="e2a8a-116">Erişim hello komut satırında Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-116">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="e2a8a-117">Merhaba GUI içinde bir terminal penceresi kullanın</span><span class="sxs-lookup"><span data-stu-id="e2a8a-117">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="e2a8a-118">Merhaba varsayılan kimlik bilgilerini Raspbian olan kullanıcı adı **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-118">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="e2a8a-119">Merhaba Görev Çubuğu'nda hello GUI, hello başlatabilirsiniz **Terminal** gibi bir izleyici arar hello simgesini kullanarak yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-119">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="e2a8a-120">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="e2a8a-120">Sign in with SSH</span></span>

<span data-ttu-id="e2a8a-121">Komut satırı erişimi tooyour Raspberry Pi'yi için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-121">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="e2a8a-122">Merhaba makale [SSH (Secure Shell)] [ lnk-pi-ssh] açıklar nasıl tooconfigure, Raspberry Pi'yi üzerinde SSH ve nasıl tooconnect gelen [Windows] [ lnk-ssh-windows] veya [Linux ve Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="e2a8a-122">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="e2a8a-123">Kullanıcı adıyla oturum **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="e2a8a-124">İsteğe bağlı: Raspberry Pi'yi üzerinde bir klasör paylaşın</span><span class="sxs-lookup"><span data-stu-id="e2a8a-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="e2a8a-125">İsteğe bağlı olarak, masaüstü ortamınızı, Raspberry Pi'yi tooshare bir klasör isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-125">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="e2a8a-126">Bir klasör paylaşımı, tercih edilen Masaüstü metin düzenleyici, toouse sağlar (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Raspberry Pi'yi tooedit dosyalarda `nano` veya `vi`.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-126">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="e2a8a-127">tooshare Windows, bir klasör Raspberry Pi'yi hello üzerinde Samba sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-127">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="e2a8a-128">Alternatif olarak, hello yerleşik kullanın [SFTP](https://www.raspberrypi.org/documentation/remote-access/) masaüstünüzde SFTP istemci ile sunucu.</span><span class="sxs-lookup"><span data-stu-id="e2a8a-128">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/