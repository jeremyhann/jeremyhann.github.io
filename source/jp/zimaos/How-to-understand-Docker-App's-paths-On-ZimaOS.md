---
title: ZimaOSにおけるDockerアプリのパスを理解する方法
description:
type: “Docs”
tip: 上部バーの固定フォーマットは削除しないでください。descriptionは記事の説明であり、未入力の場合は内容の最初の段落の文字を切り取ります。
---
# DockerとZimaOS
Dockerは、ユーザーが軽量コンテナ内でアプリケーションのデプロイ、スケーリング、管理を自動化できるプラットフォームです。これらのコンテナはアプリケーションとその依存関係をバンドルし、さまざまな環境での一貫したパフォーマンスを確保します。Dockerの効率性はアプリケーションを隔離する能力にあり、それによりよりポータブルでスケーラブルになります。

![](https://manage.icewhale.io/api/static/docs/1722494286724_image.png)
Dockerアプリについて話すとき、ZimaOSは非常に印象的で、わずか数回のクリックでプロセスを簡素化します。ZimaOSは、NAS愛好家、プロユーザー、スタジオユーザーにとっても画期的な存在です。その直感的なインターフェースは、データのバックアップと管理を簡素化します。

![](https://manage.icewhale.io/api/static/docs/1722494305565_image.png)
しかし、ZimaOSでDockerアプリを使用する際に、パスを本当に理解していますか？ZimaOSのパスとDockerアプリのパスを区別できますか？

# Dockerのパスの整理方法
Dockerコンテナを実行すると、それはホストシステムとは別のファイルシステム内で動作します。Dockerがパスをどのように整理するかの一般的な概要は次のとおりです。

- コンテナファイルシステム：Dockerコンテナ内では、ファイルシステムがホストマシンから隔離されています。コンテナ内で実行されているアプリケーションは、通常は/から始まる自分自身のルートファイルシステムを見ます。たとえば、コンテナ内の/app/dataにデータを保存するアプリケーションを持っている場合、このパスはそのコンテナのファイルシステム内にのみ存在します。

- ボリューム：コンテナのライフサイクルを超えてデータを永続化するために、Dockerはボリュームを使用します。ボリュームは、通常ホストシステム上にあるコンテナのファイルシステム外のディレクトリまたはファイルで、コンテナ間で共有できます。これらは特定のパスでコンテナにマウントされることが多いです。

![](https://manage.icewhale.io/api/static/docs/1722494354267_image.png)
他のデータ共有モードもあり、ここで学ぶことができます。

# Plexの例
![](https://manage.icewhale.io/api/static/docs/1722494383898_image.png)
人気のメディアサーバーアプリケーションであるplexを例に、ZimaOSを使用してDocker内でパスがどのように整理されているかを理解しましょう。

**Dockerアプリ**：Plexは、ZimaOSのアプリストアでDockerアプリとして配布されています。ZimaOSのアプリストアからPlexをインストールすると、ZimaOSはいくつかのディレクトリ用のパスを指定します。

- コンテナ内の/config：このディレクトリにはPlexの設定ファイルが格納されています。ZimaOS上では、そのボリュームパスは/DATA/AppData/plex/configで、これはコンテナの/configにマウントされ、設定がコンテナの再起動を超えて永続化されることを保証しています。

- コンテナ内の/media：これはPlexがメディアファイルにアクセスする場所です。また、メディアファイルのボリュームパスはZimaOS上の/DATA/Mediaであり、コンテナの/mediaにマウントされています。

ホストにファイルが保存されるようにすることを忘れないでください。これにより、たとえコンテナが停止または再作成されても、データは無傷のまま保持されます。
![](https://manage.icewhale.io/api/static/docs/1722494441184_image.png)
Plexの設定をクリックすると、詳細な設定を見つけることができます。さらに、このページでは、ボリュームパスの隣にある灰色のアイコンをクリックすることで、ボリュームパスを簡単に変更できます。

![](https://manage.icewhale.io/api/static/docs/1722494459333_image.png)
Dockerのパスと、それがPlexのようなアプリケーションとどのように統合されるかを理解することで、NAS愛好家やホムラボユーザーは、コンテナ化の柔軟性と永続ストレージの信頼性を組み合わせて、アプリケーションを効率的に管理できます。