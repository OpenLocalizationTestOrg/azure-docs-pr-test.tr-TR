## <a name="prepare-your-raspberry-pi"></a>Böğürtlenli Pi hazırlama

### <a name="install-raspbian"></a>Raspbian yükleyin

Bu hello Raspberry Pi'yi kullanarak ilk kez kullanıyorsanız, hello Seti'nde bulunan hello SD kart üzerinde NOOBS kullanarak tooinstall hello Raspbian işletim sistemi gerekir. Merhaba [Raspberry Pi yazılım Kılavuzu] [ lnk-install-raspbian] açıklar nasıl tooinstall Raspberry Pi'yi işletim sisteminde. Bu öğretici, Raspberry Pi'yi hello Raspbian işletim sisteminin yüklü olduğu varsayılır.

> [!NOTE]
> Hello dahil hello SD kart [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] yüklü NOOBS zaten. Merhaba Raspberry Pi'yi bu kartından önyükleme ve tooinstall hello Raspbian işletim sistemi seçin.

### <a name="set-up-hello-hardware"></a>Merhaba donanımı kurma

Bu öğretici hello dahil hello BME280 algılayıcı kullanır [Raspberry Pi 3 için Microsoft Azure IOT Starter Kit] [ lnk-starter-kits] toogenerate telemetri verileri. Merhaba Raspberry Pi'yi bir yöntem çağırma hello çözüm panosundan işlerken bir LED tooindicate kullanır.

Merhaba ekmek panosunda Hello bileşenleri şunlardır:

- Kırmızı ışığı
- 220 Ohm Direnci (kırmızı, kırmızı, Kahverengi)
- BME280 algılayıcısı

Merhaba Aşağıdaki diyagram gösterir nasıl tooconnect donanımınız:

![Raspberry Pi'yi için donanım Kurulumu][img-connection-diagram]

Merhaba aşağıdaki tabloda hello Raspberry Pi'yi toohello bileşenlerini hello breadboard hello bağlantılarından özetlenmektedir:

| Raspberry Pi            | Breadboard             |Renk         |
| ----------------------- | ---------------------- | ------------- |
| GND (PIN 14)            | LED - ve PIN (18A)      | Mor          |
| GPCLK0 (PIN 7)          | Direnç (25A)         | Orange          |
| SPI_CE0 (PIN 24)        | CS (39A)               | Mavi          |
| SPI_SCLK (PIN 23)       | SCK (36A)              | Sarı        |
| SPI_MISO (PIN 21)       | SDO (37A)              | Beyaz         |
| SPI_MOSI (PIN 19)       | SDI (38A)              | Yeşil         |
| GND (PIN 6)             | GND (35A)              | Siyah         |
| 3.3 V (PIN 1)           | 3Vo (34A)              | Kırmızı           |

toocomplete hello donanım Kurulum şunları yapmanız gerekir:

- Merhaba Seti'nde dahil, Raspberry Pi'yi toohello güç kaynağı bağlayın.
- Kit içinde bulunan hello Ethernet kablosu kullanarak Raspberry Pi'yi tooyour ağınıza bağlayın. Alternatif olarak, ayarlayabilirsiniz [kablosuz bağlantı] [ lnk-pi-wireless] Raspberry Pi'yi için.

Merhaba donanım Kurulumu Raspberry Pi'yi tamamladınız.

### <a name="sign-in-and-access-hello-terminal"></a>Oturum açma ve hello terminal erişim

İki seçenek tooaccess, Raspberry Pi'yi bir terminal ortamına sahip:

- Klavye varsa ve bağlı tooyour Raspberry Pi'yi izlemek, hello Raspbian GUI tooaccess bir terminal penceresi kullanabilirsiniz.

- Erişim hello komut satırında Masaüstü makinenizden SSH kullanarak, Raspberry Pi'yi.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Merhaba GUI içinde bir terminal penceresi kullanın

Merhaba varsayılan kimlik bilgilerini Raspbian olan kullanıcı adı **PI** ve parola **raspberry**. Merhaba Görev Çubuğu'nda hello GUI, hello başlatabilirsiniz **Terminal** gibi bir izleyici arar hello simgesini kullanarak yardımcı programı.

#### <a name="sign-in-with-ssh"></a>Oturum SSH oturum

Komut satırı erişimi tooyour Raspberry Pi'yi için SSH kullanabilirsiniz. Merhaba makale [SSH (Secure Shell)] [ lnk-pi-ssh] açıklar nasıl tooconfigure, Raspberry Pi'yi üzerinde SSH ve nasıl tooconnect gelen [Windows] [ lnk-ssh-windows] veya [Linux ve Mac OS][lnk-ssh-linux].

Kullanıcı adıyla oturum **PI** ve parola **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>İsteğe bağlı: Raspberry Pi'yi üzerinde bir klasör paylaşın

İsteğe bağlı olarak, masaüstü ortamınızı, Raspberry Pi'yi tooshare bir klasör isteyebilirsiniz. Bir klasör paylaşımı, tercih edilen Masaüstü metin düzenleyici, toouse sağlar (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Raspberry Pi'yi tooedit dosyalarda `nano` veya `vi`.

tooshare Windows, bir klasör Raspberry Pi'yi hello üzerinde Samba sunucusu yapılandırın. Alternatif olarak, hello yerleşik kullanın [SFTP](https://www.raspberrypi.org/documentation/remote-access/) masaüstünüzde SFTP istemci ile sunucu.

### <a name="enable-spi"></a>SPI etkinleştir

Merhaba örnek uygulamayı çalıştırmadan önce hello Raspberry Pi'yi hello seri çevre arabirimi (SPI) veri yoluna etkinleştirmeniz gerekir. Merhaba Raspberry Pi'yi hello BME280 algılayıcı aygıtla hello SPI veri yolu iletişim kurar. Aşağıdaki komut tooedit hello yapılandırma dosyasına hello kullan:

```sh
sudo nano /boot/config.txt
```

Merhaba satırı bulun:

`#dtparam=spi=on`

- toouncomment hello satırı Sil hello `#` hello başlangıç.
- Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).
- tooenable SPI hello Raspberry Pi'yi yeniden başlatın. Yeniden başlatma hello terminal bağlantısını keser, yeniden yeniden başlatıldığında hello Raspberry Pi'yi içinde toosign gerekir:

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