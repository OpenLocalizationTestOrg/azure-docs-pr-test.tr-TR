## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="7dc22-101">Intel NUC hazırlama</span><span class="sxs-lookup"><span data-stu-id="7dc22-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="7dc22-102">Donanım kurulumu tamamlamak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7dc22-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="7dc22-103">Intel NUC Seti'nde bulunan güç kaynağı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7dc22-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="7dc22-104">Intel NUC Ethernet kablosu kullanarak ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7dc22-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="7dc22-105">Intel NUC ağ geçidi cihazınız donanım Kurulumu tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="7dc22-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="7dc22-106">Oturum açma ve terminal erişim</span><span class="sxs-lookup"><span data-stu-id="7dc22-106">Sign in and access the terminal</span></span>

<span data-ttu-id="7dc22-107">Intel NUC terminal ortamda erişmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="7dc22-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="7dc22-108">Klavye ve monitör, Intel NUC bağlı varsa, kabuk doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dc22-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="7dc22-109">Varsayılan kimlik bilgileri kullanıcı adı olan **kök** ve parola **kök**.</span><span class="sxs-lookup"><span data-stu-id="7dc22-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="7dc22-110">Masaüstü makinenizden SSH kullanarak, Intel NUC Kabuğu erişin.</span><span class="sxs-lookup"><span data-stu-id="7dc22-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="7dc22-111">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="7dc22-111">Sign in with SSH</span></span>

<span data-ttu-id="7dc22-112">SSH oturum oturum açmanız, Intel NUC IP adresi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7dc22-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="7dc22-113">Klavye ve monitör, Intel NUC bağlı varsa, `ifconfig` IP adresini bulmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="7dc22-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="7dc22-114">Alternatif olarak, ağınızdaki aygıtların adreslerini listelemek için yönlendiriciniz bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7dc22-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="7dc22-115">Kullanıcı adıyla oturum **kök** ve parola **kök**.</span><span class="sxs-lookup"><span data-stu-id="7dc22-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="7dc22-116">İsteğe bağlı: Intel NUC üzerinde bir klasör paylaşın</span><span class="sxs-lookup"><span data-stu-id="7dc22-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="7dc22-117">İsteğe bağlı olarak, masaüstü ortamınızı Intel NUC üzerinde bir klasör paylaşın isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dc22-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="7dc22-118">Bir klasör paylaşımı sağlar, tercih edilen Masaüstü metin düzenleyicisi kullanın (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Intel NUC dosyalarını düzenlemek için `nano` veya `vi`.</span><span class="sxs-lookup"><span data-stu-id="7dc22-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="7dc22-119">Bir klasörü Windows ile paylaşmak için Samba sunucu üzerinde Intel NUC yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7dc22-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="7dc22-120">Alternatif olarak, Masaüstü makinenizde SFTP istemci ile Intel NUC SFTP sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7dc22-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
