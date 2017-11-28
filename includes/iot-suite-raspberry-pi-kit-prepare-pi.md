## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="e209f-101">Böğürtlenli Pi hazırlama</span><span class="sxs-lookup"><span data-stu-id="e209f-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="e209f-102">Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="e209f-102">Install Raspbian</span></span>

<span data-ttu-id="e209f-103">Raspberry Pi'yi kullanarak ilk kez kullanıyorsanız Seti'nde bulunan SD kart üzerinde NOOBS kullanarak Raspbian işletim sistemini yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e209f-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="e209f-104">[Raspberry Pi yazılım Kılavuzu] [ lnk-install-raspbian] , Raspberry Pi'yi bir işletim sistemi yüklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="e209f-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="e209f-105">Bu öğretici, Raspberry Pi'yi Raspbian işletim sisteminin yüklü olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="e209f-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="e209f-106">Dahil SD kart [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] yüklü NOOBS zaten.</span><span class="sxs-lookup"><span data-stu-id="e209f-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="e209f-107">Bu kartından Raspberry Pi'yi önyükleme ve Raspbian işletim sistemi yüklemek seçin.</span><span class="sxs-lookup"><span data-stu-id="e209f-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="e209f-108">Donanımı kurma</span><span class="sxs-lookup"><span data-stu-id="e209f-108">Set up the hardware</span></span>

<span data-ttu-id="e209f-109">Bu öğretici dahil BME280 algılayıcı kullanır [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] telemetri verileri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e209f-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="e209f-110">Bir LED Raspberry Pi'yi bir yöntem çağırma çözüm panosundan işlediğinde göstermek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="e209f-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="e209f-111">Ekmek Panosu bileşenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e209f-111">The components on the bread board are:</span></span>

- <span data-ttu-id="e209f-112">Kırmızı ışığı</span><span class="sxs-lookup"><span data-stu-id="e209f-112">Red LED</span></span>
- <span data-ttu-id="e209f-113">220 Ohm Direnci (kırmızı, kırmızı, Kahverengi)</span><span class="sxs-lookup"><span data-stu-id="e209f-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="e209f-114">BME280 algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="e209f-114">BME280 sensor</span></span>

<span data-ttu-id="e209f-115">Aşağıdaki diyagramda, donanım bağlanma gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e209f-115">The following diagram shows how to connect your hardware:</span></span>

![Raspberry Pi'yi için donanım Kurulumu][img-connection-diagram]

<span data-ttu-id="e209f-117">Aşağıdaki tabloda Raspberry Pi'yi bağlantılarından breadboard bileşenleri için özetlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="e209f-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="e209f-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e209f-118">Raspberry Pi</span></span>            | <span data-ttu-id="e209f-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="e209f-119">Breadboard</span></span>             |<span data-ttu-id="e209f-120">Renk</span><span class="sxs-lookup"><span data-stu-id="e209f-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="e209f-121">GND (PIN 14)</span><span class="sxs-lookup"><span data-stu-id="e209f-121">GND (Pin 14)</span></span>            | <span data-ttu-id="e209f-122">LED - ve PIN (18A)</span><span class="sxs-lookup"><span data-stu-id="e209f-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="e209f-123">Mor</span><span class="sxs-lookup"><span data-stu-id="e209f-123">Purple</span></span>          |
| <span data-ttu-id="e209f-124">GPCLK0 (PIN 7)</span><span class="sxs-lookup"><span data-stu-id="e209f-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="e209f-125">Direnç (25A)</span><span class="sxs-lookup"><span data-stu-id="e209f-125">Resistor (25A)</span></span>         | <span data-ttu-id="e209f-126">Orange</span><span class="sxs-lookup"><span data-stu-id="e209f-126">Orange</span></span>          |
| <span data-ttu-id="e209f-127">SPI_CE0 (PIN 24)</span><span class="sxs-lookup"><span data-stu-id="e209f-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="e209f-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="e209f-128">CS (39A)</span></span>               | <span data-ttu-id="e209f-129">Mavi</span><span class="sxs-lookup"><span data-stu-id="e209f-129">Blue</span></span>          |
| <span data-ttu-id="e209f-130">SPI_SCLK (PIN 23)</span><span class="sxs-lookup"><span data-stu-id="e209f-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="e209f-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="e209f-131">SCK (36A)</span></span>              | <span data-ttu-id="e209f-132">Sarı</span><span class="sxs-lookup"><span data-stu-id="e209f-132">Yellow</span></span>        |
| <span data-ttu-id="e209f-133">SPI_MISO (PIN 21)</span><span class="sxs-lookup"><span data-stu-id="e209f-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="e209f-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="e209f-134">SDO (37A)</span></span>              | <span data-ttu-id="e209f-135">Beyaz</span><span class="sxs-lookup"><span data-stu-id="e209f-135">White</span></span>         |
| <span data-ttu-id="e209f-136">SPI_MOSI (PIN 19)</span><span class="sxs-lookup"><span data-stu-id="e209f-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="e209f-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="e209f-137">SDI (38A)</span></span>              | <span data-ttu-id="e209f-138">Yeşil</span><span class="sxs-lookup"><span data-stu-id="e209f-138">Green</span></span>         |
| <span data-ttu-id="e209f-139">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="e209f-139">GND (Pin 6)</span></span>             | <span data-ttu-id="e209f-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="e209f-140">GND (35A)</span></span>              | <span data-ttu-id="e209f-141">Siyah</span><span class="sxs-lookup"><span data-stu-id="e209f-141">Black</span></span>         |
| <span data-ttu-id="e209f-142">3.3 V (PIN 1)</span><span class="sxs-lookup"><span data-stu-id="e209f-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="e209f-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="e209f-143">3Vo (34A)</span></span>              | <span data-ttu-id="e209f-144">Kırmızı</span><span class="sxs-lookup"><span data-stu-id="e209f-144">Red</span></span>           |

<span data-ttu-id="e209f-145">Donanım kurulumu tamamlamak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e209f-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="e209f-146">Raspberry Pi'yi Seti'nde bulunan güç kaynağı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e209f-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="e209f-147">Raspberry Pi'yi kit içinde bulunan Ethernet kablosu kullanarak ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e209f-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="e209f-148">Alternatif olarak, ayarlayabilirsiniz [kablosuz bağlantı] [ lnk-pi-wireless] Raspberry Pi'yi için.</span><span class="sxs-lookup"><span data-stu-id="e209f-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="e209f-149">Raspberry Pi'yi donanım Kurulumu tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="e209f-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="e209f-150">Oturum açma ve terminal erişim</span><span class="sxs-lookup"><span data-stu-id="e209f-150">Sign in and access the terminal</span></span>

<span data-ttu-id="e209f-151">Raspberry Pi'yi terminal ortamda erişmek için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="e209f-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="e209f-152">Klavye ve monitör, Raspberry Pi'yi bağlı varsa, bir terminal penceresi erişmek için Raspbian GUI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e209f-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="e209f-153">Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi komut satırında erişin.</span><span class="sxs-lookup"><span data-stu-id="e209f-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="e209f-154">GUI içinde bir terminal penceresi kullanın</span><span class="sxs-lookup"><span data-stu-id="e209f-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="e209f-155">Kullanıcı adı Raspbian için varsayılan kimlik bilgileri olan **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e209f-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="e209f-156">GUI görev çubuğunda, başlatabilirsiniz **Terminal** gibi bir izleyici arar simgesini kullanarak yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="e209f-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="e209f-157">Oturum SSH oturum</span><span class="sxs-lookup"><span data-stu-id="e209f-157">Sign in with SSH</span></span>

<span data-ttu-id="e209f-158">SSH, Raspberry Pi'yi komut satırı erişimi için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e209f-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="e209f-159">Makaleyi [SSH (Secure Shell)] [ lnk-pi-ssh] , Raspberry Pi'yi SSH yapılandırma ve bağlanması açıklar [Windows] [ lnk-ssh-windows] veya [ Linux ve Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="e209f-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="e209f-160">Kullanıcı adıyla oturum **PI** ve parola **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e209f-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="e209f-161">İsteğe bağlı: Raspberry Pi'yi üzerinde bir klasör paylaşın</span><span class="sxs-lookup"><span data-stu-id="e209f-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="e209f-162">İsteğe bağlı olarak, masaüstü ortamınızı ile Raspberry Pi'yi üzerinde bir klasör paylaşın isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e209f-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="e209f-163">Bir klasör paylaşımı sağlar, tercih edilen Masaüstü metin düzenleyicisi kullanın (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Raspberry Pi'yi dosyalarını düzenlemek için `nano` veya `vi`.</span><span class="sxs-lookup"><span data-stu-id="e209f-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="e209f-164">Bir klasörü Windows ile paylaşmak için Samba sunucu üzerinde Raspberry Pi'yi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e209f-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="e209f-165">Alternatif olarak, yerleşik kullanın [SFTP](https://www.raspberrypi.org/documentation/remote-access/) masaüstünüzde SFTP istemci ile sunucu.</span><span class="sxs-lookup"><span data-stu-id="e209f-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="e209f-166">SPI etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e209f-166">Enable SPI</span></span>

<span data-ttu-id="e209f-167">Örnek uygulamayı çalıştırmadan önce seri çevre arabirimi (SPI) veri yoluna Raspberry Pi'yi etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e209f-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="e209f-168">Raspberry Pi'yi BME280 algılayıcı aygıtla SPI veri yolu üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="e209f-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="e209f-169">Yapılandırma dosyasını düzenlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e209f-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="e209f-170">Satırı bulun:</span><span class="sxs-lookup"><span data-stu-id="e209f-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="e209f-171">Satırı açıklamadan çıkarın, silinecek `#` başlangıç.</span><span class="sxs-lookup"><span data-stu-id="e209f-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="e209f-172">Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve düzenleyiciden çıkın (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e209f-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="e209f-173">SPI etkinleştirmek için Raspberry Pi'yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e209f-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="e209f-174">Terminal yeniden başlatmadan bağlantısını keser, yeniden Raspberry Pi'yi yeniden başlatıldığında oturum açmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e209f-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

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