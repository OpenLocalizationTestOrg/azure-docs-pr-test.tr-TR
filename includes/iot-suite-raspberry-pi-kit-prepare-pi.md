## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="e64e4-101">Böğürtlenli Pi hazırlama</span><span class="sxs-lookup"><span data-stu-id="e64e4-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="e64e4-102">Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="e64e4-102">Install Raspbian</span></span>

<span data-ttu-id="e64e4-103">Bu hello Raspberry Pi'yi kullanarak ilk kez kullanıyorsanız, hello Seti'nde bulunan hello SD kart üzerinde NOOBS kullanarak tooinstall hello Raspbian işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e64e4-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="e64e4-104">Merhaba [Raspberry Pi yazılım Kılavuzu] [ lnk-install-raspbian] açıklar nasıl tooinstall Raspberry Pi'yi işletim sisteminde.</span><span class="sxs-lookup"><span data-stu-id="e64e4-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="e64e4-105">Bu öğretici, Raspberry Pi'yi hello Raspbian işletim sisteminin yüklü olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="e64e4-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="e64e4-106">Hello dahil hello SD kart [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] yüklü NOOBS zaten.</span><span class="sxs-lookup"><span data-stu-id="e64e4-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="e64e4-107">Merhaba Raspberry Pi'yi bu kartından önyükleme ve tooinstall hello Raspbian işletim sistemi seçin.</span><span class="sxs-lookup"><span data-stu-id="e64e4-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="e64e4-108">Merhaba donanımı kurma</span><span class="sxs-lookup"><span data-stu-id="e64e4-108">Set up hello hardware</span></span>

<span data-ttu-id="e64e4-109">Bu öğretici hello dahil hello BME280 algılayıcı kullanır [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] toogenerate telemetri verileri.</span><span class="sxs-lookup"><span data-stu-id="e64e4-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="e64e4-110">Merhaba Raspberry Pi'yi bir yöntem çağırma hello çözüm panosundan işlerken bir LED tooindicate kullanır.</span><span class="sxs-lookup"><span data-stu-id="e64e4-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="e64e4-111">Merhaba ekmek panosunda Hello bileşenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e64e4-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="e64e4-112">Kırmızı ışığı</span><span class="sxs-lookup"><span data-stu-id="e64e4-112">Red LED</span></span>
- <span data-ttu-id="e64e4-113">220 Ohm Direnci (kırmızı, kırmızı, Kahverengi)</span><span class="sxs-lookup"><span data-stu-id="e64e4-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="e64e4-114">BME280 algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="e64e4-114">BME280 sensor</span></span>

<span data-ttu-id="e64e4-115">Merhaba Aşağıdaki diyagram gösterir nasıl tooconnect donanımınız:</span><span class="sxs-lookup"><span data-stu-id="e64e4-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Raspberry Pi'yi için donanım Kurulumu][img-connection-diagram]

<span data-ttu-id="e64e4-117">Merhaba aşağıdaki tabloda hello Raspberry Pi'yi toohello bileşenlerini hello breadboard hello bağlantılarından özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="e64e4-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="e64e4-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e64e4-118">Raspberry Pi</span></span>            | <span data-ttu-id="e64e4-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="e64e4-119">Breadboard</span></span>             |<span data-ttu-id="e64e4-120">Renk</span><span class="sxs-lookup"><span data-stu-id="e64e4-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="e64e4-121">GND (PIN 14)</span><span class="sxs-lookup"><span data-stu-id="e64e4-121">GND (Pin 14)</span></span>            | <span data-ttu-id="e64e4-122">LED - ve PIN (18A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="e64e4-123">Mor</span><span class="sxs-lookup"><span data-stu-id="e64e4-123">Purple</span></span>          |
| <span data-ttu-id="e64e4-124">GPCLK0 (PIN 7)</span><span class="sxs-lookup"><span data-stu-id="e64e4-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="e64e4-125">Direnç (25A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-125">Resistor (25A)</span></span>         | <span data-ttu-id="e64e4-126">Orange</span><span class="sxs-lookup"><span data-stu-id="e64e4-126">Orange</span></span>          |
| <span data-ttu-id="e64e4-127">SPI_CE0 (PIN 24)</span><span class="sxs-lookup"><span data-stu-id="e64e4-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="e64e4-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-128">CS (39A)</span></span>               | <span data-ttu-id="e64e4-129">Mavi</span><span class="sxs-lookup"><span data-stu-id="e64e4-129">Blue</span></span>          |
| <span data-ttu-id="e64e4-130">SPI_SCLK (PIN 23)</span><span class="sxs-lookup"><span data-stu-id="e64e4-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="e64e4-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-131">SCK (36A)</span></span>              | <span data-ttu-id="e64e4-132">Sarı</span><span class="sxs-lookup"><span data-stu-id="e64e4-132">Yellow</span></span>        |
| <span data-ttu-id="e64e4-133">SPI_MISO (PIN 21)</span><span class="sxs-lookup"><span data-stu-id="e64e4-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="e64e4-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-134">SDO (37A)</span></span>              | <span data-ttu-id="e64e4-135">Beyaz</span><span class="sxs-lookup"><span data-stu-id="e64e4-135">White</span></span>         |
| <span data-ttu-id="e64e4-136">SPI_MOSI (PIN 19)</span><span class="sxs-lookup"><span data-stu-id="e64e4-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="e64e4-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-137">SDI (38A)</span></span>              | <span data-ttu-id="e64e4-138">Yeşil</span><span class="sxs-lookup"><span data-stu-id="e64e4-138">Green</span></span>         |
| <span data-ttu-id="e64e4-139">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="e64e4-139">GND (Pin 6)</span></span>             | <span data-ttu-id="e64e4-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-140">GND (35A)</span></span>              | <span data-ttu-id="e64e4-141">Siyah</span><span class="sxs-lookup"><span data-stu-id="e64e4-141">Black</span></span>         |
| <span data-ttu-id="e64e4-142">3.3 V (PIN 1)</span><span class="sxs-lookup"><span data-stu-id="e64e4-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="e64e4-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="e64e4-143">3Vo (34A)</span></span>              | <span data-ttu-id="e64e4-144">Kırmızı</span><span class="sxs-lookup"><span data-stu-id="e64e4-144">Red</span></span>           |

<span data-ttu-id="e64e4-145">toocomplete hello donanım Kurulum şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e64e4-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="e64e4-146">Merhaba Seti'nde dahil, Raspberry Pi'yi toohello güç kaynağı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e64e4-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="e64e4-147">Kit içinde bulunan hello Ethernet kablosu kullanarak Raspberry Pi'yi tooyour ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e64e4-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="e64e4-148">Alternatif olarak, ayarlayabilirsiniz [kablosuz bağlantı] [ lnk-pi-wireless] Raspberry Pi'yi için.</span><span class="sxs-lookup"><span data-stu-id="e64e4-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="e64e4-149">Merhaba donanım Kurulumu Raspberry Pi'yi tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="e64e4-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="e64e4-150">Oturum açma ve hello terminal erişim</span><span class="sxs-lookup"><span data-stu-id="e64e4-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="e64e4-151">İki seçenek tooaccess, Raspberry Pi'yi bir terminal ortamına sahip:</span><span class="sxs-lookup"><span data-stu-id="e64e4-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="e64e4-152">Klavye varsa ve bağlı tooyour Raspberry Pi'yi izlemek, hello Raspbian GUI tooaccess bir terminal penceresi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e64e4-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="e64e4-153">Erişim hello komut satırında Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi.</span><span class="sxs-lookup"><span data-stu-id="e64e4-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="e64e4-154">Merhaba GUI içinde bir terminal penceresi kullanın</span><span class="sxs-lookup"><span data-stu-id="e64e4-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="e64e4-155">Merhaba varsayılan kimlik bilgilerini Raspbian olan kullanıcı adı **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e64e4-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="e64e4-156">Merhaba Görev Çubuğu'nda hello GUI, hello başlatabilirsiniz **Terminal** gibi bir izleyici arar hello simgesini kullanarak yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="e64e4-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="e64e4-157">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="e64e4-157">Sign in with SSH</span></span>

<span data-ttu-id="e64e4-158">Komut satırı erişimi tooyour Raspberry Pi'yi için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e64e4-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="e64e4-159">Merhaba makale [SSH (Secure Shell)] [ lnk-pi-ssh] açıklar nasıl tooconfigure, Raspberry Pi'yi üzerinde SSH ve nasıl tooconnect gelen [Windows] [ lnk-ssh-windows] veya [Linux ve Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="e64e4-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="e64e4-160">Kullanıcı adıyla oturum **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e64e4-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="e64e4-161">İsteğe bağlı: Raspberry Pi'yi üzerinde bir klasör paylaşın</span><span class="sxs-lookup"><span data-stu-id="e64e4-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="e64e4-162">İsteğe bağlı olarak, masaüstü ortamınızı, Raspberry Pi'yi tooshare bir klasör isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e64e4-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="e64e4-163">Bir klasör paylaşımı, tercih edilen Masaüstü metin düzenleyici, toouse sağlar (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Raspberry Pi'yi tooedit dosyalarda `nano` veya `vi`.</span><span class="sxs-lookup"><span data-stu-id="e64e4-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="e64e4-164">tooshare Windows, bir klasör Raspberry Pi'yi hello üzerinde Samba sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e64e4-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="e64e4-165">Alternatif olarak, hello yerleşik kullanın [SFTP](https://www.raspberrypi.org/documentation/remote-access/) masaüstünüzde SFTP istemci ile sunucu.</span><span class="sxs-lookup"><span data-stu-id="e64e4-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="e64e4-166">SPI etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e64e4-166">Enable SPI</span></span>

<span data-ttu-id="e64e4-167">Merhaba örnek uygulamayı çalıştırmadan önce hello Raspberry Pi'yi hello seri çevre arabirimi (SPI) veri yoluna etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e64e4-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="e64e4-168">Merhaba Raspberry Pi'yi hello BME280 algılayıcı aygıtla hello SPI veri yolu iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="e64e4-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="e64e4-169">Aşağıdaki komut tooedit hello yapılandırma dosyasına hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e64e4-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="e64e4-170">Merhaba satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="e64e4-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="e64e4-171">toouncomment hello satırı Sil hello `#` hello başlangıç.</span><span class="sxs-lookup"><span data-stu-id="e64e4-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="e64e4-172">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e64e4-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="e64e4-173">tooenable SPI hello Raspberry Pi'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e64e4-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="e64e4-174">Yeniden başlatma hello terminal bağlantısını keser, yeniden yeniden başlatıldığında hello Raspberry Pi'yi içinde toosign gerekir:</span><span class="sxs-lookup"><span data-stu-id="e64e4-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/