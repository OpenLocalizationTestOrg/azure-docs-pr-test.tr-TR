## <a name="install-hello-prerequisites"></a>Merhaba Önkoşulları Yükleme

1. Yükleme [Visual Studio 2015 veya 2017](https://www.visualstudio.com). Merhaba kullanabilirsiniz hello lisans gereksinimlerini karşılıyorsa Community Edition boş. Visual C++ emin tooinclude ve NuGet Paket Yöneticisi olmalıdır.

1. Yükleme [git](http://www.git-scm.com) ve git.exe hello komut satırından çalıştırabilir emin olun.

1. Yükleme [CMake](https://cmake.org/download/) ve cmake.exe hello komut satırından çalıştırabilir emin olun. CMake sürüm 3.7.2 veya üzeri önerilir. Merhaba **.msi** yükleyicisi, Windows hello kolay seçeneği bulunur. CMake toohello eklemek için yol hello yükleyici istediğinde geçerli kullanıcının en az hello.

1. Yükleme [Python 2.7](https://www.python.org/downloads/release/python-27). Python tooyour eklediğinizden emin olun `PATH` ortam değişkeninde **Denetim Masası -> Sistem -> Gelişmiş Sistem Ayarları -> ortam değişkenleri**.

1. Bir komut isteminde, aşağıdaki komut tooclone hello Azure IOT kenar GitHub depo tooyour yerel makine hello çalıştırın:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Nasıl toobuild hello örnek

Artık hello IOT kenar çalışma zamanı ve örnekleri yerel makinenizde oluşturabilirsiniz:

1. Açık bir **VS 2015 için geliştirici komut istemi** veya **VS 2017 için geliştirici komut istemi** komut istemi.

1. Merhaba yerel kopyasını toohello kök klasörüne gidin **IOT kenar** deposu.

1. Yapı betiği aşağıdaki gibi çalıştırın:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Bu komut dosyasını bir Visual Studio çözümü dosyası oluşturur ve hello çözüm oluşturur. Hello hello Visual Studio çözüm bulabilirsiniz **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu. Toobuild istiyorsanız ve hello birim testleri çalıştırma hello eklemek `--run-unittests` parametresi. Toobuild istiyorsanız ve hello son tooend testler hello eklemek `--run-e2e-tests`.

> [!NOTE]
> Merhaba her çalıştırdığınızda **build.cmd** komut dosyası, siler ve sonra da hello yeniden oluşturur **yapı** hello yerel kopyasını hello kök klasöründe klasöründe **IOT kenar** deposu.
