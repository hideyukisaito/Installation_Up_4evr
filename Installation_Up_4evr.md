本記事のオリジナル版は[こちら](http://blairneal.com/blog/installation-up-4evr/) - これをより簡単かつ常にアップデートしていくため、そして皆さんからの改善のヒントや提案を取り入れるためにここに投稿したかったのです - Linux/Windows 版 の作成も大歓迎です！

Github Flavored Markup での表示確認のため、編集には https://stackedit.io/# を使用しました。

---------
私は最近、2ヶ月の間毎日24時間、最小限の不具合で動作し続け、かつ人の監視の要らない、異なる構成の4つのインスタレーションをセットアップしなければなりませんでした。これは幾人ものメディア・アーティストたちがいつも必ず行うもので、そこには長期運用におけるたくさんの異なるトリックやヒントが存在します。私は自分の発見を共有したいと考えました。
ここに記すのはひとつのやり方であり、それぞれにまた違った方法があります。あなたが現場で見つけたヒントをぜひコメント欄で共有してください。

I had to do several searches in a couple different places to find all the information I needed to keep everything consistently up and bug free. Luckily most of the installations I was dealing with this time were fairly light in terms of resources and complications, but it’s always best practices to have a safety net.

通常は開梱したての真新しいコンピューターを扱うため、この手順もゼロから始めます。私が指摘するもののほとんどは初期状態では逆に設定されています。

ヒント：もし複数のマシンで行う場合、まず1台目ですべてのステップを完了したあと、他のマシンをターゲットディスクモードで起動し [Carbon Copy Cloner](http://www.bombich.com/ja) などを使用して1台目の環境をミラーリングすることで可能な限り一貫性を保てます。

**ステップ1: ソフトウェアとコンピューターを準備しよう**
-----------------------------------------------

何かを作る際には常にインスタレーションにおける長期運用のことを心に留めておきます。展示期間を通して調整の必要があるもの(または最後まで放っておいてもよいこと)は何かを考えましょう。私の経験上、それらをできるだけシンプルにしておけば Xcode を起動してコンパイルしたりアプリケーションを終了することなくオペレーターが修正や調整をするのが容易になります。物事をシンプルにすることに時間を使えば、何か不具合が起こったときのリモートデバッグが楽になるでしょう。

警告や何かのポップアップがアプリケーションの上に表示されないように、いくつかの初期設定を確認し、必要であればそれらをオフに設定する必要があります。この手順は OS X のバージョンごとに異なります。

Nick Hardeman 氏がこれらすべての属性値を一度に設定できるユーティリティを開発しています。[ここでチェックしてみてください](http://nickhardeman.com/610/openframeworks-configuring-osx-for-a-long-term-installation/)。

システム環境設定：

 - **デスクトップとスクリーンセーバー：** スクリーンセーバーの「開始までの時間」を「開始しない」に設定して無効化します。また、デスクトップの背景を黒、あるいはあなたのアプリないしはクライアントのロゴ画像にしておくことをおすすめします。それらを自動で切り替えるようにしてもよいでしょう。そして覚えておいて欲しいのは、**誰かに気付かれなければ壊れていないのと同じ**だということです。 :)
 - **省エネルギー：**ディスプレイとコンピューターのスリープを「しない」に設定します。また「停電後に自動的に再起動」と「コンピュータが操作不能になった場合に自動的に再起動」を有効にします（これらは OS X 10.7 以降で有効なオプションです）。※[訳注] Yosemite では項目がなくなっています。
 - **ユーザーとグループ：** 「ログインオプション」の中の「自動ログイン」を「入」に設定します。
 - **ソフトウェアアップデート：**自動アップデートを無効化します。
 - **共有：**コンピューターにディスプレイが接続されていないか、または物理的にアクセスできない場所にある場合、「画面共有」と「ファイル共有」をオンにしておくのを忘れないで下さい。この設定をおこなうことで、同じネットワーク上にある別のコンピューターからのアクセスと操作が可能になります（セキュリティ設定に気をつけてください）。
 - **ネットワーク：**インスタレーションが外部のネットワークまたはインターネットに接続する必要がない場合、Wifi をオフにしておくのは悪い考えではないでしょう。思わぬときに「ワイヤレスネットワークを選択してください」というポップアップが出るのを避けることができます。オプションで、いつも使用するネットワークが見つからないときに現れる新規ネットワークへの接続確認ダイアログをオフにすることもできます。
 - **Bluetooth：** If running without a mouse or keyboard plugged in, sometimes you can get the annoying  ”Bluetooth keyboard/mouse setup” pop up over your application. You can temporality disable these by going to the advanced settings within the Bluetooth Preferences. See below for it’s location in 10.6.
 - **セキュリティとプライバシー：** I would make sure that "Disable Automatic Login" is unchecked so you don't hit any surprises on reboots. If you’re really paranoid, you can even disable things like the IR remote receiver that still exists on some macs and definitely on Macbooks. This would keep pranksters with Apple TV remotes from “Front Rowing” your installation. To disable, go to Security->General->Advanced (in >10.8) and “Disable remote control IR receiver”.
 - **通知：** [通知センターを完全に無効化する](http://www.tekrevue.com/tip/how-to-completely-disable-notification-center-in-mac-os-x/)か、下の画像のように「おやすみモード」がずっと続くように時間を設定します。

![BluetoothSettings](images/Bluetooth_settings.png)

![SecuritySettings](images/Security_settings.png)

![SharingSettings](images/Sharing_settings.png)

![Login_items](images/Auto_login.png)

![Power_settings](images/PowerSettings.png)

![Update_disable](images/Auto_update_disable.png)

![Notification_Center](images/Notification_Center_disable.png)

また、「アプリケーション〜は予期せず終了しました」のダイアログとそれに続くバグリポートメニューを以下のコマンドまたは Problem Reporter.app をリネームすることで無効化できます。

```bash
sudo chmod 000 /System/Library/CoreServices/Problem\ Reporter.app
```

[Tinkertool](http://www.bresink.com/osx/TinkerTool.html) もまた OS X の .plist ファイルを変更することでシステム環境設定がカバーしていない様々な設定を有効化/無効化することができます。

その他にも ```/System/Library/CoreServices``` 内の各ファイルをリネームすることで一時的にその機能を無効化できます。
たとえば「通知センター」を「通知センター_DEACTIVATE」等にすれば、あのサイテーな通知センターのポップアップが現れることはなくなるでしょう。

OSX 10.9 以降、アップルは App Nap と呼ばれるおかしな機能を有効にしました。これは簡単に言えばアプリケーションがアクティブでないときにリソースの節約をおこなうものですが、問題を引き起こしもします。[こちらのページ](http://www.tekrevue.com/tip/disable-app-nap-os-x-mavericks/)に無効化する方法が記載されています。

必要であれば、以下のコマンドでデスクトップアイコンを非表示にできます。

```bash
defaults write com.apple.finder CreateDesktop -bool false
```


**ステップ2：ソフトウェアを起動する**
-------------------------------

ケーブルが抜けて電源が落ちてしまったりしても、誰もが予備バッテリーを用意できる予算やスペースを持っているわけではありません。
ステップ1で、停電やフリーズ後にマシン自体を自動で再起動する設定について書きましたが、デスクトップが晒されっぱなしにならないようにアプリケーションの再起動もおこなう必要があります。色々な方法がありますが、もっともシンプルなのは OSX のビルトインツールを使用する方法です。システム環境設定の「ユーザとグループ」から該当のアカウントの「ログイン項目」を開き、あなたのアプリケーションをドラッグ&ドロップします。こうすることでシステム起動時に自動的にアプリケーションが起動します。

![Login Items](images/Login_items.png)

**ステップ3：動かし続ける**
---------------------------

アプリケーションがきちんと動いているか確認するための方法をいくつか紹介します。

**Launchd デーモン**

ローンチデーモンはマシンの起動時にアプリケーションを読み込み、継続的に再起動をおこなうためのまた別の方法です。Launchd plists は cron の代わりとしても非常に有用で、カレンダーのスケジュールに沿って何かを定期的に実行することができます。Automator と iCal の組み合わせでも同様のことがおこなえるので、好みの方法を選ぶとよいでしょう。

[アップルのドキュメント](http://developer.apple.com/library/mac/#documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html)に Launch Agent と Launch Demon の様々な使い方が記載されています。

Launch Demon と Launch Agent の使い分けについては[こちら](http://techjournal.318.com/general-technology/launchdaemons-vs-launchagents/)を参照するとよいでしょう。一般的にはある物事をユーザのログイン時に実行したいかどうかによります。ごく普通のアプリケーションを起動させたい場合は Launch Agent が適しています。

デーモンには .app 自身ではなくアプリケーションパッケージ（アプリケーションアイコンを右クリックし「パッケージの内容を表示」を選択します）内の ```Contents/MacOS``` に入っているファイルを指定します。さもないとデーモンがアプリを起動してくれない！とハマることになります。

launchd の例は [admsyn](https://gist.github.com/4140204) を参照するとよいでしょう。

もちろん、上の gist に載っているテンプレートを使用してあなた自身の launchd 用 .plist を作成しても構いません。ターミナルで ```man launchd.plist``` と入力すればコントロール可能なオプションについてすべての情報が得られます。また、Lingon（App Store で 4.99ドル）もしくは [Lingon X](http://www.peterborgapps.com/lingon/) を使用すれば Launchd の設定がより楽になります。  

[訳注] 現在 App Store で販売されているのは Lingon 3 で、価格は1,200円です。上記 URL では Lingon X 2.0 が10ユーロで販売されています。通常の Lingon と Lingon X の違いについては[こちら](https://www.peterborgapps.com/lingon/#compare)。
 
Lingon で + をクリックすると、基本的なエージェントとなる plist が新規作成されます。この plist を以下のように設定しましょう。

![LingonSetup](images/LingonSetup.png)


One additional/optional thing you can add to this is to put an additional key in the plist for a “Successful Exit”. By adding this, your app won’t re-open when it has detected that it closed normally (ie You just hit escape intentionally, it didn’t crash). Can be useful if you’re trying to check something and OS X won’t stop re-opening the app on you. To easily add this to the key, click the advanced tab and click the checkbox for "Successful exit" - or just add it manually as it in the above screenshot.

**シェルスクリプト + cron ジョブ**

(以下の非常に有用な tips は [Kyle McDonald](http://kylemcdonald.net/) から得ました。)

This method is sort of deprecated in relation to the launchd method - you can run shell scripts with Lingon and launchd in the same manner as what we've got here. Shell scripting is your best friend. With the help of the script below and an application called CronniX (or use Lingon) , you will be able to use a cronjob to check the system’s list of currently running processes. If your app does not appear on the list, then the script will open it again, otherwise it won’t do anything. Either download the script or type the following into a text editor, replacing Twitter.app with your app’s name and filepath. Don’t forget the “.app” extension in the if statement!:

	\#!/bin/sh 
		if [ $(ps ax | grep -v grep | grep "Twitter.app" | wc -l) -eq 0 ] then
		echo "Twitter not running. opening..."
		open /Applications/Twitter.app 
		else
		echo "Twitter running" fi

Save that file as something like “KeepOpen.sh” and keep it next to your application or somewhere convenient.

After creating that file, you’ll need to make it executable. To do this, open the Terminal and in a new window type “chmod +x ” and then enter the path to the shell script you just created (you can either drag the shell script into the terminal window or manually type it). It would look something like this:

    	
    4Evr-MacBook-Pro:~ Forever4Evr$ chmod +x /Users/Forever4Evr/Desktop/KeepOpen.sh

After you have made it executable, you’re now ready to set it up as a cronjob. Tip: to test the script, you can change the extension at the end to KeepOpen.command as an alternative to opening it with Terminal, but the same thing gets done.

Cronjobs are just low level system tasks that are set to run on a timer. The syntax for cronjobs is outside of the scope of this walkthrough, but there are many sites available for that. Instead, the application CronniX can do a lot of the heavy lifting for you.

After downloading CronniX, open it up and create a new cronjob. In the window that opens,  in the command window, point it to your KeepOpen.sh file and  check all of the boxes in the simple tab for minute, hour, month, etc. This tells the job to run every minute, every hour, every day, every month. If you want it to run less frequently or at a different frequency, play around with the sliders.

![Cronnix_link](images/Cronnix-settings.png)

Now just hit “New” and then make sure to hit “Save” to save it into the system’s crontab. Now if you just wait a minute then it should open your app every minute on the minute. Maybe save this one for the very end if you have more to do :)

This is a great tool if there is an unintended crash because the app will never be down longer than a minute.

**Non-Cronjob - Shell Script Method**

    \#!/bin/bash
     
    while true
    do
    #using open to get focus
    echo "Trying to open empty example"
    open -a emptyExample
    sleep 10
    done

Just type this into a plaintext document and save it as something like ”KeepMyAppAlivePlz.command” and then use chmod as above to make the file executable  and then drop this in your login items as  above. This one will just continuously try and open your app every 10ms, but if it is already open, the OS knows to not try opening it a second, third, fourth time.

Make sure to check the Console.app for any errors that may have come through when no one caught them, whenever you check the installation in person or remotely. This is not a fix-all for buggy programming, just a helper to keep things running smooth. The more things you can do to leave yourself notes about why the crash happened, the faster you can address the core issue.

Applescript is also a very solid choice for doing some more OS specific work in terms of having odd menus clicked or keypresses sent in some order.

**ステップ4：定期的な再起動**
---------------------------

これについては都市伝説的なので、なぜいいアイデアなのか具体的な理由を知っている人がいたら教えてください。アプリケーションによっては手の出しようのないメモリリークやOSのバグに遭遇することがあります。そうなってしまった場合には、毎日ないし毎週再起動をおこなうのもよいアイデアです。

もっともシンプルな選択肢は「システム環境設定 -> 省エネルギー」を開いて「スケジュール...」をクリックして適当な時間を設定することです。必要であれば夜間やその他の使用されない時間帯にシステムを終了するよう設定して負荷を軽減することができます。発熱が問題を引き起こすこともあります。Heat can do funny things sometimes, so if you have a chance to get your computer to rest and the time to test it, definitely give this a shot…saves some energy too which is nice.

![Auto-reboot](images/Auto_reboot.png)

また、CronniX を使って任意の頻度でシステムの再起動をおこなうシェルスクリプトを設定することもできます。

そしてもう一つの選択肢は(あなたがターミナルやシェルスクリプトに関わりたくない場合) iCal を使って Automator の iCal イベントを呼び出すという方法です。スケジューリングについても、再起動スケジュールの可視化という点についても、おそらくこの方法はより簡単です。試しに Automator を起動して、新規 iCal イベント(カレンダーアラーム)を作成してみましょう。

![Automator Shell Script](images/Automator_example2.png)

期待した通りに動いたら保存します。保存すると iCal が起動しアクションとして登録されているので、あとは好きな頻度の繰り返しを設定するだけです。再起動やスクリプトの実行時にあなたへメールで知らせるなどの設定も可能です。

If you’d like to just close your programs and re-open them and there is a background and foreground do something like this (pauses are so the quitting and re-opening stuff has time to actually execute):

![AutomatorPause](images/Automator_example.png)

**ステップ5：リモートチェックイン**
---------------------------------

[SSH](http://www.mactricksandtips.com/2009/06/ssh-into-your-mac.html) で VNC（[RealVNC](http://realvnc.com/) と Chicken of the VNC がよく併用されます）を使用するための選択肢として [Logmein](http://www.logmein.com/) や [Teamviewer](http://teamviewer.com/) などの Web サービスがあります。どれを選ぶかはあなたにとって使いやすいかどうか、そしてどの程度リモートメンテナンスの必要があるのかによりますが、これらを使わずに後のステップで説明するロギング手法を使用する選択肢もあります。

インスタレーション用のマシンとあなたの PC との間で Dropbox フォルダを共有しておくと非常に便利です。ほとんどの画面共有サービスもファイル共有機能を持っていますが、Dropbox はただただ最高です。

ことディスプレイに画面表示をおこなわないインスタレーションにおいて、DHCP で動的に割り当てられた IP アドレスを確認するのは苦痛以外の何物でもありません。Robb Godshaw はこれを少しでも和らげるため、マシンの起動から30秒後に IP アドレスを読み上げさせる Automator スクリプトを書きました。[Instructables でダウンロードできます](http://www.instructables.com/id/Configuring-a-Mac-for-an-always-on-operation/steps/9)。

Step 6: テスト、テスト、テスト...
-------------------------

インスタレーションに向けてソフトウェアがばっちり整ったら、できる限り本番を想定した環境でこれまで見てきた方法と自動化のスクリプトをテストしてみましょう。

すべての物事を説明できるわけではないので、何かが起こってしまっても自分を責める必要はありません。しかしそのとき、このリストがあなたのフラストレーションを少しでも軽くする役に立てば幸いです。幸運を！


おまけ：ロギング
------------------------

数週間〜数ヶ月間運用する場合、リモートログインを必要としない監視方法を用意するとよいでしょう。おすすめは、特定の情報をテキストファイル（リンク済みの Dropbox で管理します）に書き込み、さらにそれを Web でチェックできるようにサーバーへアップロードする方法です。

インスタレーションの状態に関してどんな情報を得たいかによっていくつかの方法があります。

現在走っているプロセスをリストアップするためには以下のコマンドが使用できます。

    ps aux (or ps ax)


(ps コマンドについての情報は[こちら](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/ps.1.html)) – さらに、特定のアプリケーションに関する情報のみにフィルタリングします。

    ps aux | grep "TweetDeck"
    
こうすると以下のような結果が得られます。

    USER             PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
    laser          71564   0.4  1.7  4010724 140544   ??  S    Sun03PM  14:23.76 /Applications/TweetDeck.app/Contents/MacOS/TweetDeck -psn_0_100544477
    laser          95882   0.0  0.0  2432768    600 s000  S+   12:11PM   0:00.00 grep TweetDeck

CPU 使用量、メモリ使用量(全体に対する割合)、ステータス、起動日時、アップタイム等の情報が得られました。

これらを以下のようにしてテキストファイルに書き込みましょう。

    ps aux | grep 'TweetDeck' >> $HOME/Dropbox/InstallationLogs/BigImportantInstall/Number6ProcessLog.txt

この行の意味は次の通りです。

- 起動中のプロセスを教えて (```px aux```)
- "Tweetdeck" を含む行だけちょうだい (```grep 'Tweetdeck'```)
- そしてそれらをこの場所にあるテキストファイルに書き込んでね (```>> path\_to\_text\_file```)

デーモンや cron に設定できるように、これを実行可能なシェルスクリプトにする必要があります。ステップ 3 に戻って Lingon と launchd を使用したスクリプトの定期的な実行方法を思い出しましょう。指定したアプリケーションが起動していない場合、その grep プロセスのみが返ってきます。これを記録しておくのはいいことです。なぜなら、アプリケーションが起ち上がっていなければ何もログが残らないので、その状態がどれだけの時間続いているのか知る術がありません。ですがこの grep プロセスをロギングしておけば、少なくともそれをチェックしたことだけは分かります。また grep コマンドはより正確にチェックした時間を教えてくれます。他のアプリでは起動時間とアップタイムしか得られません。

もう少し突っ込んでみましょう。仮に、接続している Triplehead2Go がかなり不安定で、マシンの再起動後にプロジェクターがオフになっているなどしてディスプレイないしはプロジェクターを必ずしも認識してくれないという状況だとしても、現在有効な解像度をログ出力できるのです！ターミナルに以下の行を入力してみてください。

    system_profiler SPDisplaysDataType
    
接続中のディスプレイと、その解像度や名前を含むいくつかのメタデータを返します。

常に 3840x720 の解像度で動作していることを確認したいか、解像度が変更されたことを記録したいとします。以下の行を試してみましょう。

    system_profiler SPDisplaysDataType | grep Resolution

"Resolution: 3840×720" が返されます。そして、起動中のプロセスとアクティブな解像度を一緒に記録するシェルスクリプトは以下のようになります。

    #!/bin/bash
    ps aux | grep 'YourAppName' >> /Users/you/filepath/Install6ProcessLog.txt
    system_profiler SPDisplaysDataType | grep Resolution >> /Users/you/Dropbox/Install6ProcessLog.txt

ワクワクしてきましたか？さらに、見えないところでおかしなことが起こっていないか確認するために定期的にスクリーンショットを撮りたくなると思います。そこで次の行を書き加えてみましょう。

    screencapture ~/Desktop/$(date +%Y%m%d-%H%M%S).png

これで指定フォーマットの日時をファイル名としたスクリーンショットがデスクトップに保存されます。パスは必要に応じて変更してください。データ容量が大きい場合は表示に問題が起こることがあるので、5分よりも1時間おきくらいがよいと思います。いつもどおり、デプロイ前にテストしましょう！

さらに付け加えるなら、インスタレーションに関する各種情報の一覧表を生成する Web ページを作っておくと便利です。

このようなロガーでは不十分な場合はメールアラートが使えます。何らかの不具合をメールで通知するシステムを構築すれば手動でチェックする必要がなくなります。これはコマンドラインと手元のツールで実現できますが、手順はやや複雑です。これから説明するのはごく一般的な手順なので、それぞれの環境に合わせて適宜変更してください。

まず最初に postfix の設定をしましょう。これで簡単にターミナルからメールを送信できるようになります。[こちらに書いてある手順](http://benjaminrojas.net/configuring-postfix-to-send-mail-from-mac-os-x-mountain-lion/)にできる限り忠実に従ってください。

Gmail を使用している場合、アカウント情報は以下のようになるでしょう。

*InstallationSupport@gmail.com*

*pass: yourpassword*

記事のステップ1の passwd ファイルは以下のようになります。

*smtp.gmail.com:587 installationSupport@gmail.com:yourpassword*

さっそくテストしてみましょう。以下のコマンドを実行します。

	echo “Hello” | mail -s “test” “InstallationSupport@gmail.com”
	
次にこれをアプリケーションの死活監視をするプロセスと組み合わせます。以下のスクリプトを適宜調整すれば動作するでしょう。

    #!/bin/sh
    if [ $(ps ax | grep -v grep | grep "YourApp.app" | wc -l) -eq 0 ] ; #"YourApp.app" をあなたのアプリケーション名に置き換えてください     
    then
    	SUBJECT="Shit broke"
    	EMAIL="InstallationSupport" #宛先
    	EMAILMESSAGE="This could be for adding an attachment/logfile"
		echo "The program isn't open - trying to re-open">$SUBJECT
		date | mail -s "$SUBJECT" "$EMAIL"  "$EMAILMESSAGE"
     
		echo "YourApp not running. Opening..."
     
		open /Applications/YourApp.app #reopen the app - set this to an exact filepath
    else
		echo "YourApp is running"
    fi

最後に、上記のスクリプトが lanuchd で起動するよう、ステップ3の手順に従ってセットアップする必要があります。5分毎にチェックをおこない、もしもクラッシュしていたらメールを受け取ることができます。必要に応じて if 文の中の条件を変えれば、たとえば解像度の変更をモニタリングすることもできます。

メモリリーク・キラー
--------------------

アプリケーションのメモリ使用量が一定の値を超えた際に再起動をかける手順を上記のプロセスに組み合わせる方法については[こちらの記事](http://blairneal.com/blog/memory-leak-murderer/)が参考になります。

おまけ：MadMapper を使っているなら[この AppleScript](http://blairneal.com/blog/applescript-to-automatically-fullscreen-madmapper-for-installations/) が役に立ちます。MapMapper の起動、フルスクリーン表示メニューの選択、やっかいなダイアログで自動的に "OK" を選択する一連の作業をおこなってくれます

その他のリソース：
--------------------

**MAC OS X**

[ofxWatchdog](https://github.com/toolbits/ofxWatchdog) はアプリケーションに致命的なエラーが起こった場合でも強制的に再起動をかけ続けてくれる素晴らしいアドオンです。
This is an amazing addon for openFrameworks apps that keeps your application open even after a large range of failures: [ofxWatchdog](https://github.com/toolbits/ofxWatchdog)

[Configuring Mac OS X for Interactive Installations](http://vormplus.be/blog/article/configuring-mac-os-x-for-interactive-installations)

[ライブビジュアル / VJing 向けの同じような tips 集](http://vjforums.info/wiki/setting-up-os-x-for-vjing/)

[これまで書いてきた設定を一ヵ所でおこなうための Nick Hardeman によるユーティリティ](http://nickhardeman.com/610/openframeworks-configuring-osx-for-a-long-term-installation/)

同じくNick Hardeman による [ofxMacUtils](https://github.com/NickHardeman/ofxMacUtils)

**LINUX**

[https://github.com/openframeworks/ofBook/blob/master/chapters/installation_up_4evr_linux/chapter.md](https://github.com/openframeworks/ofBook/blob/master/chapters/installation_up_4evr_linux/chapter.md)

**RASPBERRY PI**

[https://sfpc.hackpad.com/rPi-run-4-ever-qFgafqYPM54](https://sfpc.hackpad.com/rPi-run-4-ever-qFgafqYPM54)

**WINDOWS** 

もしここで紹介してきたようなタスクを Windows でおこなう方法を探しているのなら、Stephen Schieberl による [StayUp](http://www.bantherewind.com/stayup) と名付けられた最高のスクリプトをチェックしてみてください。また [Restart on Crash](http://www.softpedia.com/get/System/File-Management/Restart-on-Crash.shtml) という記事や、OS の制御をスクリプティングするための [NirCmd](http://www.nirsoft.net/utils/nircmd.html) というツールも存在します。[Eva Schindling によるステップ・バイ・ステップのセットアップガイド](http://www.evsc.net/home/prep-windows-machine-for-fulltime-exhibition-setup)もぜひチェックすることをおすすめします。