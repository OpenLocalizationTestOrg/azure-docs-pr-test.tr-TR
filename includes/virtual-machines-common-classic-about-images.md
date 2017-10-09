

Görüntüleri Azure tooprovide içinde kullanılan bir işletim sistemine sahip yeni bir sanal makine. Görüntüyü bir veya daha fazla veri diski de sahip olabilir. Görüntüleri çeşitli kaynaklardan kullanılabilir:

* Azure'un sunduğu hello görüntülerinde [Market](https://azure.microsoft.com/gallery/virtual-machines/). Windows Server'ın en son sürümleri ve hello Linux işletim sistemi dağıtımlarını vardır. Bazı görüntüleri de SQL Server gibi uygulamalar içerir. MSDN avantaj ve MSDN Kullandıkça Öde aboneler erişim tooadditional görüntülerine sahip.
* Merhaba açık kaynak topluluğu sunar görüntüleri üzerinden [VM deposu](http://vmdepot.msopentech.com/List/Index).
* Ayrıca depolayın ve kendi görüntülerini Azure üzerinde bir görüntü olarak kullanmak için mevcut bir Azure sanal makine yakalama veya görüntüyü karşıya kullanın.

## <a name="about-vm-images-and-os-images"></a>VM görüntüleri ve işletim sistemi görüntüleri hakkında
Azure'da iki görüntü türleri kullanılabilir: *VM görüntüsü* ve *işletim sistemi görüntüsü*. Merhaba görüntü oluşturulduğunda tüm diskleri tooa sanal makineye bağlı ve bir VM görüntüsü bir işletim sistemini içerir. Bir VM görüntüsü hello yeni resim türünde. VM görüntüleri sunulmadan önce Azure görüntüdeki genelleştirilmiş bir işletim sistemi ve hiçbir ek disk olabilir. Yalnızca genelleştirilmiş bir işletim sistemini içeren bir VM görüntüsü olan temelde hello görüntüsü hello işletim sistemi görüntüsü hello özgün türü ile aynı.

Azure'da sanal makine veya başka bir yerde çalışan bir sanal makine göre kendi görüntülerinizden kopyalayın ve karşıya yükleme oluşturabilirsiniz. Birden fazla sanal makine toouse bir görüntü toocreate istiyorsanız, tooprepare gerekir, genelleme tarafından bir görüntü olarak kullanmak için. toocreate bir Windows Server görüntüsü, çalışma hello Sysprep komut hello sunucu toogeneralize üzerinde bu hello .vhd dosyası karşıya yüklemeden önce. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://go.microsoft.com/fwlink/p/?LinkId=392030) ve [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). VM Hello, Sysprep çalıştırılmadan önce yedekleyin. Bir Linux görüntü oluşturma dağıtım göre değişir. Genellikle, toorun belirli toohello dağıtım ve hello Azure Linux Aracısı çalıştırma komutları kümesi gerekir.
