<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall StorSimple için Windows PowerShell aracılığıyla Bakım modu düzeltmeleri
> [!IMPORTANT]
> Bakım modunda tooapply hello düzeltme önce bir denetleyicisinde gerekir ve ardından üzerindeki diğer denetleyicisi hello.
> 
> 

1. Merhaba aygıt bakım moduna yerleştirin. Bkz: [2. adım: girin Bakım modu](../articles/storsimple/storsimple-update-device.md#step2) yönelik yönergeler tooenter Bakım modu.
2. tooapply hello düzeltme, türü:
   
     `Start-HcsHotfix` 
3. İstendiğinde, hello düzeltme dosyalarını içeren hello yolu toohello ağ paylaşılan klasöründe sağlayın.
4. Onayınız istenir. Tür **Y** tooproceed hello düzeltme yüklemesi ile.
5. Sonra hello düzeltme bir denetleyicisinde oturum açma toohello diğer denetleyicisi uyguladınız. Merhaba önceki denetleyici için yaptığınız gibi hello düzeltmeyi uygulayın.
6. Merhaba düzeltmeleri uyguladıktan sonra bakım modundan çıkın. Bkz: [4. adım: çıkış Bakım modu](../articles/storsimple/storsimple-update-device.md#step4) yönergeler için.

