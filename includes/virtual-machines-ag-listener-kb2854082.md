Ardından, herhangi bir hello küme sunucusunda, Windows Server 2008 R2 veya Windows Server 2012 çalıştırıyorsanız, bu hello düzeltme doğrulamanız gerekir [KB2854082](http://support.microsoft.com/kb/2854082) her hello şirket içi sunucular veya hello kümesinin parçası olan Azure VM'ler yüklenir. Ayrıca herhangi bir sunucu veya hello kümedeki ancak hello kullanılabilirlik grubu içinde değil VM bu düzeltmenin yüklü olması gerekir.

Merhaba Uzak Masaüstü oturumunda hello küme düğümlerinin her biri için indirme [KB2854082](http://support.microsoft.com/kb/2854082) tooa yerel dizin. Ardından, sırayla her küme düğümünde hello düzeltmeyi yükleyin. Merhaba Küme hizmeti hello küme düğümü üzerinde şu anda çalışıyorsa hello sunucusu hello hello düzeltme yükleme sonunda yeniden başlatılır.

> [!WARNING]
> Merhaba Küme hizmetini durdurma veya hello sunucunun yeniden başlatılması hello çekirdek, küme ve hello kullanılabilirlik grubunun sağlığını etkileyen ve küme toogo çevrimdışı neden olabilir. toomaintain hello yüksek kullanılabilirlik kümenizin yüklemesi sırasında emin olun:
> 
> * Merhaba, en uygun çekirdek sistem kümedir. 
> * Herhangi bir düğümde hello düzeltmeyi yüklemeden önce tüm küme düğümleri çevrimiçi değil.
> * Merhaba kümedeki herhangi bir düğümde hello düzeltmeyi yüklemeden önce hello düzeltme yükleme toorun toocompletion tam olarak hello sunucunun yeniden başlatılması gibi bir düğümde izin verin.
> 
> 

