<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla tooinstall Bakım modu güncelleştirmeleri
1. Henüz yapmadıysanız, erişim hello cihaz seri konsoluna ve seçenek 1, **oturum oturum tam erişim**. 
2. Merhaba parolayı girin. Merhaba varsayılan parola **Parola1**.
3. Merhaba komut satırına aşağıdakini yazın:
   
     `Get-HcsUpdateAvailability` 
4. Güncelleştirmeler varsa ve kesintiye uğratan veya benzer hello güncelleştirmelerin olup olmadığını size bildirilecek. tooapply kesintiye uğratan güncelleştirmelerini, bakım moduna tooput hello aygıt gerekir. Bkz: [2. adım: girin Bakım modu](../articles/storsimple/storsimple-update-device.md#step2) yönergeler için.
5. Cihazınızı bakım modunda olduğunda hello komut satırına aşağıdakini yazın:`Start-HcsUpdate`
6. Onayınız istenir. Merhaba güncelleştirmeleri onayladıktan sonra şu anda erişen hello denetleyicisine yüklenir. Merhaba güncelleştirmeler yüklendikten sonra hello denetleyicisi yeniden başlatılır. 
7. Güncelleştirmeleri Hello durumunu izleyin. Şunu yazın:
   
    `Get-HcsUpdateStatus`
   
    Merhaba, `RunInProgress` olan `True`, hello güncelleştirmesidir devam ediyor. Varsa `RunInProgress` olan `False`, o hello güncelleştirmesi tamamlandı gösterir.  
8. Merhaba güncelleştirme hello geçerli denetleyicisine yüklenir ve yeniden başlatıldıktan toohello başka denetleyicisine bağlanmak ve 1 ile 6 arasındaki adımları gerçekleştirin.
9. Hem denetleyicileri güncelleştirildikten sonra bakım modundan çıkın. Bkz: [4. adım: çıkış Bakım modu](../articles/storsimple/storsimple-update-device.md#step4) yönergeler için.

