<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="1aae2-101">Merhaba seri Konsolu aracılığıyla tooconnect</span><span class="sxs-lookup"><span data-stu-id="1aae2-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="1aae2-102">Seri kabloyu toohello aygıtınızı (doğrudan veya bir USB seri bağdaştırıcısı aracılığıyla) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1aae2-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="1aae2-103">Açık hello **Denetim Masası**ve ardından hello açın **Aygıt Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="1aae2-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="1aae2-104">Merhaba COM bağlantı noktası hello aşağıdaki çizimde gösterildiği gibi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1aae2-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Seri konsol üzerinden bağlanma](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="1aae2-106">PuTTY’yi başlatın.</span><span class="sxs-lookup"><span data-stu-id="1aae2-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="1aae2-107">Merhaba sağ bölmede, hello değiştirme **bağlantı türü** çok**seri**.</span><span class="sxs-lookup"><span data-stu-id="1aae2-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="1aae2-108">Merhaba sağ bölmede, hello uygun COM bağlantı noktasını yazın.</span><span class="sxs-lookup"><span data-stu-id="1aae2-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="1aae2-109">Merhaba seri yapılandırma parametrelerinin gibi ayarlandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="1aae2-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="1aae2-110">Hız: 115.200</span><span class="sxs-lookup"><span data-stu-id="1aae2-110">Speed: 115,200</span></span>
   * <span data-ttu-id="1aae2-111">Veri bitleri: 8</span><span class="sxs-lookup"><span data-stu-id="1aae2-111">Data bits: 8</span></span>
   * <span data-ttu-id="1aae2-112">Dur bitleri: 1</span><span class="sxs-lookup"><span data-stu-id="1aae2-112">Stop bits: 1</span></span>
   * <span data-ttu-id="1aae2-113">Eşlik: Yok</span><span class="sxs-lookup"><span data-stu-id="1aae2-113">Parity: None</span></span>
   * <span data-ttu-id="1aae2-114">Akış denetimi: Yok</span><span class="sxs-lookup"><span data-stu-id="1aae2-114">Flow control: None</span></span>
     
     <span data-ttu-id="1aae2-115">Bu ayarlar, aşağıdaki çizimde hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1aae2-115">These settings are shown in hello following illustration.</span></span>
     
     ![PuTTY ayarları](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="1aae2-117">Merhaba varsayılan akış denetimi ayarı çalışmazsa hello akış denetimi tooXON/XOFF ayarlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1aae2-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="1aae2-118">Tıklatın **açık** toostart seri oturumu.</span><span class="sxs-lookup"><span data-stu-id="1aae2-118">Click **Open** toostart a serial session.</span></span>

