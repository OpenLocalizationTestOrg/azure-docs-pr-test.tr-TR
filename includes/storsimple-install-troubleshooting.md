<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Güncelleştirme hatalarını giderme
**Yükseltme öncesi denetimleri hello bir bildirim görür ne başarısız olmuş?**

Ön denetim başarısız olursa, hello sayfanın hello hello ayrıntılı bildirim çubuğu adresindeki attıktan emin olun. Toowhich ön denetim başarısız oldu gibi bu kılavuz sağlar. Merhaba aşağıda böyle bir bildirim görüntülendiği bir örnek gösterilmektedir. Bu durumda, hello denetleyicisi sistem durumu denetimi ve donanım bileşen sistem durumu denetimi başarısız oldu. Merhaba altında **donanım durumu** bölümünde görebilirsiniz, her ikisi de **denetleyici 0** ve **Denetleyici 1** bileşenleri ilgilenilmesi gerekiyor.

  ![Ön denetim başarısız](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Her iki denetleyicilerinin sağlıklı ve çevrimiçi olduğundan emin toomake gerekir. Merhaba StorSimple cihazı tüm hello donanım bileşenleri toobe sağlıklı hello bakım sayfasında gösterildiğinden emin toomake de gerekir. Tooinstall güncelleştirmeleri daha sonra deneyebilirsiniz. Ardından mümkün toofix hello donanım bileşeni sorunları olup olmadığı, sonraki adımlar için toocontact Microsoft Support gerekir.

**Ne varsa, "güncelleştirmeleri yüklenemedi" hata iletisini alırsınız ve öneri hello sorun giderme kılavuzu toodetermine hello hello hatanın nedenini toorefer toohello güncelleştirme mi?**

Bağlantı toohello Microsoft Update sunucularına sahip olmayan bir büyük olasılıkla bunun nedeni olabilir. Gerçekleştirilen toobe gerektiren el ile denetim budur. Bağlantı toohello güncelleştirme sunucusu kaybederseniz, güncelleştirme işi başarısız olur. Merhaba Windows PowerShell arabiriminden StorSimple Cihazınızı cmdlet'i aşağıdaki hello çalıştırarak hello bağlantı denetleyebilirsiniz:

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Her iki denetleyicilerinde Hello cmdlet'ini çalıştırın.

Lütfen başlangıç bağlantı var ve bu sorunu toosee devam doğruladıysanız Microsoft Support sonraki adımlar için başvurun.

**Ne, aygıt tooUpdate 4 güncelleştirilirken bir güncelleştirme hatası görebilir ve güncelleştirme 4 çalıştıran her iki hello denetleyicilerinin?**

Hem hello denetleyicileri çalışan hello aynı yazılım sürümü ve güncelleştirme hatası olup olmadığını ise güncelleştirme 4, başlangıç, hello denetleyicileri kurtarma moduna girmez. Merhaba, bu durum ortaya çıkabilir aygıt yazılım düzeltme (1 sipariş) güncelleştirmedir uygulanan tooboth hello denetleyicileri diğer düzeltmeleri ancak başarıyla (2 sipariş ve 3 sipariş) henüz toobe uygulanır. Güncelleştirme 4'ten başlayarak, yalnızca hello iki denetleyicileri farklı yazılım sürümleri çalıştırıyorsanız hello denetleyicileri kurtarma moduna geçer. 

Güncelleştirme 4 hem denetleyicileri çalıştırırken hello kullanıcı güncelleştirmesi başarısız görürse, birkaç dakika bekleyin ve sonra yeniden güncelleştirilmesi öneririz. Ardından Hello yeniden deneme başarısız olursa, Microsoft Support başvurmalısınız.
