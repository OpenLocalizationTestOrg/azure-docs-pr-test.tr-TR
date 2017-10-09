<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla tooinstall normal düzeltmeleri
1. Toohello cihaz seri konsoluna bağlayın. Daha fazla bilgi için bkz: [1. adım: toohello seri konsol bağlantısı](../articles/storsimple/storsimple-update-device.md#step1).
2. Merhaba seri konsol menüsünde seçeneğini 1, **oturum oturum tam erişim**. Merhaba parolayı girin. Merhaba varsayılan parola **Parola1**.
3. Merhaba komut satırına aşağıdakini yazın:
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Bu komut yalnızca tooregular düzeltmeleri uygular. Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir.
    > Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, hello yük devretme sistem kullanılabilirliğini veya işlem etkilemez.

4. İstendiğinde, hello düzeltme dosyalarını içeren hello yolu toohello ağ paylaşılan klasöründe sağlayın.
5. Onayınız istenir. Tür **Y** tooproceed hello düzeltme yüklemesi ile.

