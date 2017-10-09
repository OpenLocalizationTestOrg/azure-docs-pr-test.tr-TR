## <a name="build-iot-edge"></a>IOT kenar derleme

Bu öğretici hello Uzaktan izleme çözümü ile özel IOT kenar modülleri toocommunicate kullanır. Bu nedenle, özel kaynak kodu toobuild hello IOT kenar modüllerden gerekir. Aşağıdaki bölümlerde hello nasıl tooinstall IOT kenarı ve yapı özel IOT kenar modülü hello açıklanmaktadır.

### <a name="install-iot-edge"></a>IOT kenar yükleyin

Merhaba aşağıdaki adımlar nasıl tooinstall hello hello Intel NUC IOT kenar yazılımı önceden derlenmiş açıklamaktadır:

1. Gerekli hello akıllı paketi depoları komutları Intel NUC hello üzerinde aşağıdaki hello çalıştırarak yapılandırın:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Girin `y` zaman hello komut sizden çok**bu kanal içerir?**.

1. Merhaba akıllı Paket Yöneticisi hello aşağıdaki komutu çalıştırarak güncelleştirin:

    ```bash
    smart update
    ```

1. Merhaba aşağıdaki komutu çalıştırarak Hello Azure IOT kenar paketini yükle:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Merhaba yükleme tarafından çalışan hello "Hello world" örnek doğrulayın. Bu örnek, beş saniyede bir hello world ileti toohello log.txT dosyası yazar. Merhaba aşağıdaki komutları hello "Hello world" örnek çalıştırın:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Yoksay **geçersiz bağımsız değişken** hello örnek durdurduğunuzda iletileri.

    Komut tooview hello hello günlük dosyasının içeriğini aşağıdaki hello kullan:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Sorun giderme

Merhaba hata alırsanız, "hiçbir paket kul linux geliştirme sağlar.", hello Intel NUC yeniden başlatmayı deneyin.
