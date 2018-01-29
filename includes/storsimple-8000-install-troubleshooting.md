<!--author=alkohli last changed: 08/29/17-->

## <a name="troubleshooting-update-failures"></a>Güncelleştirme hatalarını giderme
**Yükseltme öncesi denetimlerin başarısız olduğuna dair bir bildirim görürseniz ne yapmalısınız?**

Ön denetim başarısız olursa, sayfanın sonundaki ayrıntılı bildirim çubuğuna baktığınızdan emin olun. Bu, hangi ön denetimin başarısız olduğuna dair yönlendirme sağlar. Örneğin, denetleyici sistem durumu denetimi ve donanım bileşen sistem durumu denetimi başarısız olan bir bildirim alın. Git **İzleyici > donanım durumu**. Her iki denetleyicilerinin sağlıklı ve çevrimiçi olduğundan emin olmanız gerekir. StorSimple cihazı tüm donanım bileşenleri bu dikey pencerede sağlıklı olmasını gösterilir emin olmanız gerekir. Ardından güncelleştirmeleri yüklemeyi deneyebilirsiniz. Donanım bileşeni sorunlarını çözemiyorsanız, sonraki adımlar için Microsoft Destek’e başvurmanız gerekecektir.

**“Güncelleştirmeler yüklenemedi” hata iletisini alırsanız ve hatanın nedeninin belirlemek için verilen tavsiye güncelleme sorun giderme kılavuzuna bakmak olduğunda ne yapmalısınız?**

Bunun muhtemel bir nedeni, Microsoft Update sunucularına bağlantınız olmamasıdır. Bu, yapılması gereken manuel bir denetimdir. Güncelleştirme sunucusu bağlantınız kesilirse, güncelleştirme işi başarısız olur. StorSimple cihazınızın Windows PowerShell arabiriminden aşağıdaki cmdlet'i çalıştırarak bağlantı denetleyebilirsiniz:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Cmdlet'i iki denetleyicide çalıştırın.

Bağlantı olduğunu doğruladıysanız ve bu sorunla karşılaşmaya devam ediyorsanız, lütfen sonraki adımlar için Microsoft Destek ile irtibat kurun.

**Cihazınızı Güncelleştirme 4’e güncelleştirirken ve her iki denetleyici de Güncelleştirme 4 çalıştırdığında bir güncelleştirme hatası görürseniz ne yapmalısınız?**

Güncelleştirme 4’ten itibaren, her iki denetleyici aynı yazılım sürümünü çalıştırıyorsa ve bir güncelleştirme hatası oluşursa, denetleyiciler kurtarma moduna girmemektedir. Cihaz yazılım düzeltmesi (1. sıra güncelleştirme) her iki denetleyiciye başarılı şekilde uygulandığında ancak diğer düzeltmeler (2. sıra ve 3. sıra) henüz uygulanmadığında bu durum meydana gelebilir. Güncelleştirme 4'ten itibaren, yalnızca iki denetleyici farklı yazılım sürümleri çalıştırıyorsa denetleyiciler kurtarma moduna geçer. 

Kullanıcı, her iki denetleyici Güncelleştirme 4 çalıştırırken bir güncelleme hatası görürse, birkaç saniye beklemelerini ve ardından güncelleştirmeyi yeniden denemelerini öneririz. Yeniden deneme başarısız olursa, Microsoft Destek ile irtibat kurmalıdırlar.
