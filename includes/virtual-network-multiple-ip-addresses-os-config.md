## <a name="os-config"></a>IP adreslerini tooa VM işletim sistemi Ekle

Bağlanma ve oturum açma tooa VM birden çok özel IP adresleri ile oluşturulur. Toohello VM eklediğiniz tüm hello özel IP adresleri (Merhaba birincil dahil) el ile eklemeniz gerekir. VM işletim sisteminiz için adımlara hello tamamlayın:

### <a name="windows"></a>Windows

1. Bir komut isteminde *ipconfig/all* yazın.  Yalnızca hello gördüğünüz *birincil* (DHCP) aracılığıyla özel IP adresi.
2. Tür *ncpa.cpl* hello komut istemi tooopen hello içinde **ağ bağlantıları** penceresi.
3. Merhaba uygun bağdaştırıcısının hello özelliklerini açın: **yerel ağ bağlantısı**.
4. İnternet Protokolü sürüm 4 (IPv4) öğesine çift tıklayın.
5. Seçin **IP adresini izleyen kullanım hello** ve değerleri aşağıdaki hello girin:

    * **IP adresi**: hello girin *birincil* özel IP adresi
    * **Alt ağ maskesi**: Alt ağınıza göre ayarlanır. Örneğin, hello alt ağ bir/24 ise alt sonra hello alt ağ maskesi 255.255.255.0 olan.
    * **Varsayılan ağ geçidi**: Merhaba hello alt ağdaki ilk IP adresi. 10.0.0.0/24 alt ağınız varsa, hello ağ geçidi IP adresi 10.0.0.1 değil.
    * Tıklatın **aşağıdaki DNS sunucu adreslerini kullan hello** ve değerleri aşağıdaki hello girin:
        * **Tercih edilen DNS sunucusu**: Kendi DNS sunucunuzu kullanmıyorsanız 168.63.129.16 girin.  Kendi DNS sunucusu kullanıyorsanız, sunucunuz için başlangıç IP adresi girin.
    * Merhaba tıklatın **Gelişmiş** düğmesini tıklatın ve ek IP adreslerini ekleyin. Her adım 8 toohello NIC hello birincil IP adresi için aynı alt ağda belirtilen Merhaba ile listelenmiş hello ikincil özel IP adresleri ekleyin.
        >[!WARNING] 
        >Yukarıdaki hello adımları doğru uygulamazsanız bağlantı tooyour VM kaybedebilir. 5. adım için girilen hello bilgileri devam etmeden önce doğru olduğundan emin olun.

    * Tıklatın **Tamam** tooclose genişletme hello TCP/IP ayarları ve ardından **Tamam** yeniden tooclose hello bağdaştırıcı ayarları. RDP bağlantınız yeniden kurulur.

6. Bir komut isteminde *ipconfig/all* yazın. Eklediğiniz tüm IP adresleri gösterilir ve DHCP kapatılır.


### <a name="validation-windows"></a>Doğrulama (Windows)

ikincil IP yapılandırmanızı doğru şekilde kullanarak ekledikten sonra genel IP ilişkili hello aracılığıyla Internet'ten yukarıdaki adımları mümkün tooconnect toohello olduğunuz tooensure, komutu aşağıdaki hello kullanın:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Merhaba yapılandırma kendisiyle ilişkili bir ortak IP adresi varsa, ikincil IP yapılandırmaları için yalnızca toohello Internet ping atabilir. Birincil IP yapılandırmaları için bir ortak IP adresi gerekli tooping toohello Internet değildir.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Bir terminal penceresi açın.
2. Merhaba kök kullanıcı olduğundan emin olun. Değilse, komutu aşağıdaki hello girin:

    ```bash
    sudo -i
    ```

3. Güncelleştirme hello yapılandırma dosyası hello ağ arabiriminin ('eth0' varsayılarak).

    * Dhcp için var olan satır öğesi Hello tutun. daha önce olduğu gibi hello birincil IP adresinin yapılandırılmış kalır.
    * Ek bir statik IP adresi için bir yapılandırma komutları aşağıdaki hello ile ekleyin:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Bir .cfg dosyası görmeniz gerekir.
4. Açık hello dosyası. Merhaba dosya hello sonunda satırlardan hello görmeniz gerekir:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Bu dosya mevcut hello satırları sonra satırlardan hello ekleyin:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Komutu aşağıdaki hello kullanarak Hello dosyayı kaydedin:

    ```bash
    :wq
    ```

7. Ağ arabirimiyle komutu aşağıdaki hello sıfırlama hello:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Uzak bağlantı kullanıyorsanız, aynı satır hello ifdown ve ifup çalıştırın.
    >

8. Başlangıç IP adresi ile komutu aşağıdaki hello toohello ağ arabirimi eklenir doğrulayın:

    ```bash
    ip addr list eth0
    ```

    Merhaba listesinin bir parçası eklediğiniz adres hello IP görmeniz gerekir.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS ve diğerleri)

1. Bir terminal penceresi açın.
2. Merhaba kök kullanıcı olduğundan emin olun. Değilse, komutu aşağıdaki hello girin:

    ```bash
    sudo -i
    ```

3. Parolanızı girin ve istenen yönergeleri izleyin. Merhaba kök kullanıcının olduktan sonra komutu aşağıdaki hello ile toohello ağ betikler klasörüne gidin:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Liste hello komutu aşağıdaki hello kullanarak ifcfg dosyaları ile ilgili:

    ```bash
    ls ifcfg-*
    ```

    Görmeniz gerekir *ifcfg eth0* hello dosyalardan biri olarak.

5. tooadd bir IP adresi bir yapılandırma dosyası için aşağıda gösterildiği gibi oluşturun. Her IP yapılandırması için bir dosya oluşturulmalıdır.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Açık hello *ifcfg-eth0:0* komutu aşağıdaki hello dosyasıyla:

    ```bash
    vi ifcfg-eth0:0
    ```

7. İçerik toohello dosyası ekleme *eth0:0* bu durumda, komutu aşağıdaki hello ile. Emin tooupdate bilgi IP adresinizi temel.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Komutu aşağıdaki hello ile Merhaba dosyayı kaydedin:

    ```bash
    :wq
    ```

9. Hello ağ hizmetlerini yeniden başlatın ve aşağıdaki komutları hello çalıştırarak hello değişiklikleri başarılı olduğundan emin olun:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Eklediğiniz, adres hello IP görmelisiniz *eth0:0*, döndürülen hello listesinde.

### <a name="validation-linux"></a>Doğrulama (Linux)

ikincil IP yapılandırmanızı hello genel IP aracılığıyla Internet'ten mümkün tooconnect toohello olduğunuz tooensure ilişkili, hello aşağıdaki komutu kullanın:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Merhaba yapılandırma kendisiyle ilişkili bir ortak IP adresi varsa, ikincil IP yapılandırmaları için yalnızca toohello Internet ping atabilir. Birincil IP yapılandırmaları için bir ortak IP adresi gerekli tooping toohello Internet değildir.

Linux ikincil NIC toovalidate giden bağlantısını çalışırken VM'ler için tooadd uygun yolları gerekebilir. Vardır birçok yolu toodo bu. Lütfen Linux dağıtımınız için uygun belgelere bakın. Merhaba aşağıdaki bir yöntem tooaccomplish budur:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Tooreplace emin olun:
    - **10.0.0.5** hello özel IP adresiyle bir ortak IP adresi ilişkili tooit
    - **10.0.0.1** tooyour varsayılan ağ geçidi
    - **eth2** ikincil NIC toohello adı
