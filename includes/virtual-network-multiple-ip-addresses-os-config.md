## <span data-ttu-id="43f00-101"><a name="os-config"></a>IP adreslerini tooa VM işletim sistemi Ekle</span><span class="sxs-lookup"><span data-stu-id="43f00-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="43f00-102">Bağlanma ve oturum açma tooa VM birden çok özel IP adresleri ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="43f00-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="43f00-103">Toohello VM eklediğiniz tüm hello özel IP adresleri (Merhaba birincil dahil) el ile eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43f00-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="43f00-104">VM işletim sisteminiz için adımlara hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="43f00-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="43f00-105">Windows</span><span class="sxs-lookup"><span data-stu-id="43f00-105">Windows</span></span>

1. <span data-ttu-id="43f00-106">Bir komut isteminde *ipconfig/all* yazın.</span><span class="sxs-lookup"><span data-stu-id="43f00-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="43f00-107">Yalnızca hello gördüğünüz *birincil* (DHCP) aracılığıyla özel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="43f00-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="43f00-108">Tür *ncpa.cpl* hello komut istemi tooopen hello içinde **ağ bağlantıları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="43f00-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="43f00-109">Merhaba uygun bağdaştırıcısının hello özelliklerini açın: **yerel ağ bağlantısı**.</span><span class="sxs-lookup"><span data-stu-id="43f00-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="43f00-110">İnternet Protokolü sürüm 4 (IPv4) öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43f00-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="43f00-111">Seçin **IP adresini izleyen kullanım hello** ve değerleri aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="43f00-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="43f00-112">**IP adresi**: hello girin *birincil* özel IP adresi</span><span class="sxs-lookup"><span data-stu-id="43f00-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="43f00-113">**Alt ağ maskesi**: Alt ağınıza göre ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="43f00-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="43f00-114">Örneğin, hello alt ağ bir/24 ise alt sonra hello alt ağ maskesi 255.255.255.0 olan.</span><span class="sxs-lookup"><span data-stu-id="43f00-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="43f00-115">**Varsayılan ağ geçidi**: Merhaba hello alt ağdaki ilk IP adresi.</span><span class="sxs-lookup"><span data-stu-id="43f00-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="43f00-116">10.0.0.0/24 alt ağınız varsa, hello ağ geçidi IP adresi 10.0.0.1 değil.</span><span class="sxs-lookup"><span data-stu-id="43f00-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="43f00-117">Tıklatın **aşağıdaki DNS sunucu adreslerini kullan hello** ve değerleri aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="43f00-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="43f00-118">**Tercih edilen DNS sunucusu**: Kendi DNS sunucunuzu kullanmıyorsanız 168.63.129.16 girin.</span><span class="sxs-lookup"><span data-stu-id="43f00-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="43f00-119">Kendi DNS sunucusu kullanıyorsanız, sunucunuz için başlangıç IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="43f00-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="43f00-120">Merhaba tıklatın **Gelişmiş** düğmesini tıklatın ve ek IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="43f00-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="43f00-121">Her adım 8 toohello NIC hello birincil IP adresi için aynı alt ağda belirtilen Merhaba ile listelenmiş hello ikincil özel IP adresleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="43f00-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="43f00-122">Yukarıdaki hello adımları doğru uygulamazsanız bağlantı tooyour VM kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="43f00-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="43f00-123">5. adım için girilen hello bilgileri devam etmeden önce doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="43f00-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="43f00-124">Tıklatın **Tamam** tooclose genişletme hello TCP/IP ayarları ve ardından **Tamam** yeniden tooclose hello bağdaştırıcı ayarları.</span><span class="sxs-lookup"><span data-stu-id="43f00-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="43f00-125">RDP bağlantınız yeniden kurulur.</span><span class="sxs-lookup"><span data-stu-id="43f00-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="43f00-126">Bir komut isteminde *ipconfig/all* yazın.</span><span class="sxs-lookup"><span data-stu-id="43f00-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="43f00-127">Eklediğiniz tüm IP adresleri gösterilir ve DHCP kapatılır.</span><span class="sxs-lookup"><span data-stu-id="43f00-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="43f00-128">Doğrulama (Windows)</span><span class="sxs-lookup"><span data-stu-id="43f00-128">Validation (Windows)</span></span>

<span data-ttu-id="43f00-129">ikincil IP yapılandırmanızı doğru şekilde kullanarak ekledikten sonra genel IP ilişkili hello aracılığıyla Internet'ten yukarıdaki adımları mümkün tooconnect toohello olduğunuz tooensure, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="43f00-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="43f00-130">Merhaba yapılandırma kendisiyle ilişkili bir ortak IP adresi varsa, ikincil IP yapılandırmaları için yalnızca toohello Internet ping atabilir.</span><span class="sxs-lookup"><span data-stu-id="43f00-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="43f00-131">Birincil IP yapılandırmaları için bir ortak IP adresi gerekli tooping toohello Internet değildir.</span><span class="sxs-lookup"><span data-stu-id="43f00-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="43f00-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="43f00-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="43f00-133">Bir terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="43f00-133">Open a terminal window.</span></span>
2. <span data-ttu-id="43f00-134">Merhaba kök kullanıcı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="43f00-134">Make sure you are hello root user.</span></span> <span data-ttu-id="43f00-135">Değilse, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="43f00-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="43f00-136">Güncelleştirme hello yapılandırma dosyası hello ağ arabiriminin ('eth0' varsayılarak).</span><span class="sxs-lookup"><span data-stu-id="43f00-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="43f00-137">Dhcp için var olan satır öğesi Hello tutun.</span><span class="sxs-lookup"><span data-stu-id="43f00-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="43f00-138">daha önce olduğu gibi hello birincil IP adresinin yapılandırılmış kalır.</span><span class="sxs-lookup"><span data-stu-id="43f00-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="43f00-139">Ek bir statik IP adresi için bir yapılandırma komutları aşağıdaki hello ile ekleyin:</span><span class="sxs-lookup"><span data-stu-id="43f00-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="43f00-140">Bir .cfg dosyası görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43f00-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="43f00-141">Açık hello dosyası.</span><span class="sxs-lookup"><span data-stu-id="43f00-141">Open hello file.</span></span> <span data-ttu-id="43f00-142">Merhaba dosya hello sonunda satırlardan hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="43f00-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="43f00-143">Bu dosya mevcut hello satırları sonra satırlardan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="43f00-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="43f00-144">Komutu aşağıdaki hello kullanarak Hello dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="43f00-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="43f00-145">Ağ arabirimiyle komutu aşağıdaki hello sıfırlama hello:</span><span class="sxs-lookup"><span data-stu-id="43f00-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="43f00-146">Uzak bağlantı kullanıyorsanız, aynı satır hello ifdown ve ifup çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="43f00-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="43f00-147">Başlangıç IP adresi ile komutu aşağıdaki hello toohello ağ arabirimi eklenir doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="43f00-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="43f00-148">Merhaba listesinin bir parçası eklediğiniz adres hello IP görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43f00-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="43f00-149">Linux (Redhat, CentOS ve diğerleri)</span><span class="sxs-lookup"><span data-stu-id="43f00-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="43f00-150">Bir terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="43f00-150">Open a terminal window.</span></span>
2. <span data-ttu-id="43f00-151">Merhaba kök kullanıcı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="43f00-151">Make sure you are hello root user.</span></span> <span data-ttu-id="43f00-152">Değilse, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="43f00-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="43f00-153">Parolanızı girin ve istenen yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="43f00-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="43f00-154">Merhaba kök kullanıcının olduktan sonra komutu aşağıdaki hello ile toohello ağ betikler klasörüne gidin:</span><span class="sxs-lookup"><span data-stu-id="43f00-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="43f00-155">Liste hello komutu aşağıdaki hello kullanarak ifcfg dosyaları ile ilgili:</span><span class="sxs-lookup"><span data-stu-id="43f00-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="43f00-156">Görmeniz gerekir *ifcfg eth0* hello dosyalardan biri olarak.</span><span class="sxs-lookup"><span data-stu-id="43f00-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="43f00-157">tooadd bir IP adresi bir yapılandırma dosyası için aşağıda gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="43f00-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="43f00-158">Her IP yapılandırması için bir dosya oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43f00-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="43f00-159">Açık hello *ifcfg-eth0:0* komutu aşağıdaki hello dosyasıyla:</span><span class="sxs-lookup"><span data-stu-id="43f00-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="43f00-160">İçerik toohello dosyası ekleme *eth0:0* bu durumda, komutu aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="43f00-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="43f00-161">Emin tooupdate bilgi IP adresinizi temel.</span><span class="sxs-lookup"><span data-stu-id="43f00-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="43f00-162">Komutu aşağıdaki hello ile Merhaba dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="43f00-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="43f00-163">Hello ağ hizmetlerini yeniden başlatın ve aşağıdaki komutları hello çalıştırarak hello değişiklikleri başarılı olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="43f00-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="43f00-164">Eklediğiniz, adres hello IP görmelisiniz *eth0:0*, döndürülen hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="43f00-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="43f00-165">Doğrulama (Linux)</span><span class="sxs-lookup"><span data-stu-id="43f00-165">Validation (Linux)</span></span>

<span data-ttu-id="43f00-166">ikincil IP yapılandırmanızı hello genel IP aracılığıyla Internet'ten mümkün tooconnect toohello olduğunuz tooensure ilişkili, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="43f00-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="43f00-167">Merhaba yapılandırma kendisiyle ilişkili bir ortak IP adresi varsa, ikincil IP yapılandırmaları için yalnızca toohello Internet ping atabilir.</span><span class="sxs-lookup"><span data-stu-id="43f00-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="43f00-168">Birincil IP yapılandırmaları için bir ortak IP adresi gerekli tooping toohello Internet değildir.</span><span class="sxs-lookup"><span data-stu-id="43f00-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="43f00-169">Linux ikincil NIC toovalidate giden bağlantısını çalışırken VM'ler için tooadd uygun yolları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="43f00-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="43f00-170">Vardır birçok yolu toodo bu.</span><span class="sxs-lookup"><span data-stu-id="43f00-170">There are many ways toodo this.</span></span> <span data-ttu-id="43f00-171">Lütfen Linux dağıtımınız için uygun belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="43f00-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="43f00-172">Merhaba aşağıdaki bir yöntem tooaccomplish budur:</span><span class="sxs-lookup"><span data-stu-id="43f00-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="43f00-173">Tooreplace emin olun:</span><span class="sxs-lookup"><span data-stu-id="43f00-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="43f00-174">**10.0.0.5** hello özel IP adresiyle bir ortak IP adresi ilişkili tooit</span><span class="sxs-lookup"><span data-stu-id="43f00-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="43f00-175">**10.0.0.1** tooyour varsayılan ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="43f00-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="43f00-176">**eth2** ikincil NIC toohello adı</span><span class="sxs-lookup"><span data-stu-id="43f00-176">**eth2** toohello name of your secondary NIC</span></span>
