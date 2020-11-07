# はじめに
GNS3はネットワーク機器をエミュレートし、PC上に仮想のネットワークを構築することができるフリーのアプリケーションです。机上でネットワーク機器の動作を確認することができるため、ネットワークの勉強に最適です。
自宅のMacにネットワークの勉強用にGNS3をインストールして、簡単なネットワークを組んで遊んでみたのでその方法を記します。

# 環境
今回はMac上のVirtualBoxにGNS3のVMを作成することとしました。
VirtualBoxのインストール方法は割愛します。

# GNS3のインストール
## MAC版
下記のサイトからGNS3を入手します。アカウントを持っていない場合は、右上の「Sign Up」から作成します。その後、「Free Download」->「Download」をクリック、Mac版のGNSダウンロードし、同サイトのInstall Guideを参考にインストールを行います。

https://www.gns3.com

## VirtualBox版
下記のサイトからVirtualBox用のGNS3 VMのイメージの圧縮ファイル「GNS3.VM.VirtualBox.X.X.XX.zip(X.X.XXはバージョン番号)」をダウンロードします（必ず上で入手したGNS3とバージョンを合わせます）。
圧縮ファイルを展開すると「GNS3 VM.ova」という名前のファイルができます。バーチャルボックスのメニューの「ファイル」->「仮想アプライアンスインポート」で「インポートしたい仮想アプライアンス」画面を開き、このファイルを選択してインポートを行うとVirtualBox上に「GNS3 VM」という仮想マシンが出来上がります(仮想マシンの設定はCPUの数を2に、RAMは4096MBにするのがネットでよく見かける設定です)。
出来上がった仮想マシンはVirtualBoxから立ち上げる必要がありません。立ち上げてしまった場合は「ShutDown」を選択して終わらせてください。

https://github.com/GNS3/gns3-gui/releases

# GNS3のセットアップ
MACにインストールしたGNS3を起動します。初めに「Setup Wizard」の「Server」選択画面が表示されます。選択肢の中から「Run applications in a virtual machine」を選択し「Next >」ボタンを押下します。

![SetupWizard.png](https://umidori.github.io/gns3_setup/SetupWizard.png)

「Local server configuration」画面が表示されます。全てデフォルトのままで良いので、そのまま「Next >」ボタンをクリックします。

![LocalServerConfiguration.png](https://umidori.github.io/gns3_setup/LocalServerConfiguration.png)

「Local server status」画面で「Next >」ボタンをクリックすると、警告が表示されますが、無視して「OK」ボタンをクリックします。

![LocalServerStatus.png](https://umidori.github.io/gns3_setup/LocalServerStatus.png)

![LocalServerStatusError.png](https://umidori.github.io/gns3_setup/LocalServerStatusError.png)

「GNS3 VM」画面では「Virtual Box」を選択し、「Next >」ボタンをクリックします。

![GNS3VM.png](https://umidori.github.io/gns3_setup/GNS3VM.png)

Virtual BoxのGNS3 VMが起動したら、Finishボタンをクリックします。これで「Setup Wizard」が完了します。

![Summary.png](https://umidori.github.io/gns3_setup/Summary.png)

GNS3のメニューから「GNS3」->「Preferences...」->「GNS3 VM」を選択して表示される画面の「Run the VM in headless mode」にチェックを入れると、GNS3 VMが起動しても、画面には表示されなくなります。メニューから「GNS3」->「Quit GNS3」を選択すると、起動したVirtual BoxのVMとともにGNS3が終了します。

# GNS3での仮想ネットワーク構築

スイッチングハブを使った簡単なネットワークを構築します。
セットアップが完了したGNS3を起動します。プロジェクト名を求められるので、適当な名前を入力して「OK」ボタンをクリックします。

![Project.png](https://umidori.github.io/gns3_setup/Project.png)

GNS3が立ち上がったら、画面の左のアイコンの「Browse Switches」をクリックします。

![BrowseSwitches.png](https://umidori.github.io/gns3_setup/BrowseSwitches.png)

表示されたアイコンの中の「Ethernet switch」を画面中央のペインにドラック＆ドロップします。

![EthernetSwitch.png](https://umidori.github.io/gns3_setup/EthernetSwitch.png)


サーバ選択画面が表示されたら「GNS3 VM」を選択して「OK」ボタンをクリックすると、中央のペイン上にスイッチアイコンが表示されます。

![ChooseServer.png](https://umidori.github.io/gns3_setup/ChooseServer.png)

![Switch1.png](https://umidori.github.io/gns3_setup/Switch1.png)

次は仮想のPCを作成します。今度は画面の左のアイコンの「Browse End Device」をクリックします。

![BrowseEndDevices.png](https://umidori.github.io/gns3_setup/BrowseEndDevices.png)

表示されたアイコンの中の「VPCS」を画面中央のペインにドラック＆ドロップします。

![VPCS.png](https://umidori.github.io/gns3_setup/VPCS.png)

「Ethernet switch」のときと同じように、サーバ選択画面が表示されるので「GNS3 VM」を選択して「OK」ボタンをクリックします。中央のペイン上にPCアイコンが表示されます。

![PC1.png](https://umidori.github.io/gns3_setup/PC1.png)

スイッチとPCをケーブルで繋ぎます。左のアイコンの中の「Add a link」をクリックしたのち、画面の「Switch1」アイコンをクリックします。結線するポートが表示されるので、その中の適当なポートを選択します。

![Switch1Ethernet0_2.png](https://umidori.github.io/gns3_setup/Switch1Ethernet0_2.png)

次に画面の「PC1」アイコンをクリックします。同じように結線のためのポートが表示される（今回は１つだけ表示されます）ので、それを選択します。

![PC1Ethernet0_1.png](https://umidori.github.io/gns3_setup/PC1Ethernet0_1.png)

スイッチとPCを繋いだら、PCを起動します。「PC1」アイコンを右クリックし、表示されたメニューの中から「Start」を選択します。

![PC1_Start.png](https://umidori.github.io/gns3_setup/PC1_Start.png)

PCアイコン近くに表示されていた赤い点が緑に変わり、PCが起動したことがわかります。

![Swich1PC1Start.png](https://umidori.github.io/gns3_setup/Swich1PC1Start.png)

PCが起動したら、PCのコンソールを開いてIPアドレスを与えます。PC1アイコンをダブルクリックするとコンソールが開きます。

![PC1Console1.png](https://umidori.github.io/gns3_setup/PC1Console1.png)

コンソールで「ip 192.168.100.1/24」を実行すると、PC1のIPアドレスが「192.168.100.1/24」になります。「save」を実行して変更したIPアドレスを保存します。「save」を実行しないとIPは保存されません。

![PC1Console2.png](https://umidori.github.io/gns3_setup/PC1Console2.png)

分かりやすいように画面上の「PC1」の文字をダブルクリックし、上で指定したIPアドレスに変更します。

![HostNameIP.png](https://umidori.github.io/gns3_setup/HostNameIP.png)

PCとケーブルを追加して、下記の画面のようなネットワークを作成します。

![Switch1PC1-4.png](https://umidori.github.io/gns3_setup/Switch1PC1-4.png)

「Swich1」アイコンを右クリックし、表示されたメニューの中から「Configure」を選択します。

![Switch1Configure.png](https://umidori.github.io/gns3_setup/Switch1Configure.png)

Settingsの中のPortとVLANを所定の値にした後、「Add」ボタンをクリックして設定を変更します。

![Switch1Port2Vlan2.png](https://umidori.github.io/gns3_setup/Switch1Port2Vlan2.png)

下記のような構成にした後、「OK」ボタンをクリックして変更を確定します。

|Port|VLAN|Type  |接続先PC     |
|----|----|------|-------------|
|0   |1   |access|192.168.100.1|
|1   |1   |access|192.168.100.2|
|2   |2   |access|192.168.110.1|
|3   |2   |access|192.168.110.2|

作成したネットワークの隣に同じような構成のネットワークをもう一つ作成します。



![Switch1-2.png](https://umidori.github.io/gns3_setup/Switch1-2.png)


新たに作成したネットワークの構成は下記の通りです。

|Port|VLAN|Type  |接続先PC     |
|----|----|------|-------------|
|0   |1   |access|192.168.100.3|
|1   |1   |access|192.168.100.4|
|2   |2   |access|192.168.110.3|
|3   |2   |access|192.168.110.4|

Swich1とSwitch2をケーブルでつなげます。

![Switch1-2PC1-8.png](https://umidori.github.io/gns3_setup/Switch1-2PC1-8.png)

スイッチ同士をトランク接続します。設定は下記の通りです。

|Swich1 Port|Swich1 Type|Swich2 Port|Swich2 Type|
|-----------|-----------|-----------|-----------|
|7          |dot1q      |7          |dot1q      |

これでスイッチを使ったVLAN構成のネットワークが完成しました。仮想PCのコンソールからお互いにpingを打ち合って接続状態を確認します。

![PC1Console3.png](https://umidori.github.io/gns3_setup/PC1Console3.png)

以上で、GNS3を使ったネットワーク構築方法の説明を終了します。

