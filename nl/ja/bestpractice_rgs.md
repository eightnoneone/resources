---

copyright:

  years: 2018
lastupdated: "2018-06-08"

---

{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:tip: .tip}


# リソースをリソース・グループに編成するためのベスト・プラクティス
{: #bp_resourcegroups}

リソース・グループとは、アクセス制御および課金の目的でアカウント・[リソース](/docs/resources/acct_resources.html#resource)を編成するための機能です。 Cloud Foundry スペースの使用に精通している場合、リソース・グループへのリソースの編成は、スペースへのリソースの編成方法と同様と考えることができます。 リソースとは、リソース・グループ内に作成、管理、および含めることができるすべてのものです。 ユーザーはリソース・グループには追加されません。 追加できるのはリソースのみです。 

現在、すべてのサービスが {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) アクセス制御の使用とリソース・グループへの割り当てをサポートしているわけではありません。 IAM で管理されているサービスは、新しいサービス・インスタンスをカタログから作成するときに、それらをリソース・グループに割り当てるよう求めるプロンプトを出します。 リソース・グループ内のリソースおよびリソース・グループ自体へのアクセスは、IAM で管理されます。 IAM の役割を使用することにより、リソース・グループ内に編成されているリソースへのアクセス権限をユーザーに提供できます。 また、IAM の役割は、リソース・グループの表示機能や編集機能、またはリソース・グループへの新しいサービス・インスタンスの追加機能やアクセス管理機能も提供できます。

また、「ID およびアクセス」UI からリソースへのアクセス権限を割り当てるときに、IAM で管理されているサービスのリストを表示することができます。 **「管理」** &gt; **「セキュリティー」** &gt; **「ID およびアクセス」**に移動してユーザーまたはサービス ID を選択し、**「アクション」**メニューから**「アクセス権限の割り当て」**を選択します。 次に、**「リソースへのアクセス権限の割り当て」**を選択し、**「サービス」**ドロップダウン・メニューで、IAM の使用をサポートするサービスを表示できます。 まだ IAM の使用をサポートしていないすべてのサービスについては、Cloud Foundry の組織、スペース、および役割を引き続き使用できます。 

Cloud Foundry の組織、スペース、および役割は、リソース・グループおよび IAM の役割とは明らかに別のものです。 したがって、Cloud Foundry の役割が、リソース・グループ内のリソースにアクセス権限を付与することはできません。 
{: tip}


## リソース・グループのセットアップ

デフォルトで、すべてのユーザーには、名前変更可能な単一のリソース・グループが与えられます。 請求可能なアカウントを持っている場合は、リソースを編成するためのリソース・グループを複数作成できます。 リソースを複数の異なるリソース・グループに編成することにより、以下のことが可能になります。

* 最小数のポリシーを使用することより、一連のリソースへのアクセス権限の割り当てが容易になる 
* 課金目的でリソース・グループの使用量情報を表示する 

新規リソース・グループを作成するには、以下の手順を実行します。

1. **「管理」**&gt;**「アカウント」**&gt;**「リソース・グループ」**に移動します。
2. **「リソース・グループの作成」**をクリックします。
3. リソース・グループの名前を入力します。
4. **「追加」**をクリックします。


## リソース・グループへのリソースの追加

IAM アクセス制御を使用して管理されているサービスは、Cloud Foundry の組織やスペースでなく、リソース・グループに属します。 カタログから、それらのいずれかのサービスについて、サービス・インスタンスを作成すると、そのインスタンスをリソース・グループに割り当てるよう求めるプロンプトが出されます。 

**重要**: インスタンス作成時のリソース・グループの選択は最終的なものであり、変更できません。

追加のサービスでリソース・グループの割り当ておよび IAM アクセス制御の使用が有効になると、マイグレーション資格を持つ既存の Cloud Foundry サービス・インスタンスがある場合、ダッシュボードで通知されます。 [サービス・インスタンスをリソース・グループにマイグレーション](/docs/resources/instance_migration.html)することにより、選択したリソース・グループ内に新しくリンクされたインスタンスが作成され、Cloud Foundry インスタンスは別名になります。 


## リソース・グループおよびリソース・グループ内のリソースへのアクセス権限の割り当て

アクセス・ポリシーを作成することにより、アクセス・グループに編成されたユーザーまたはユーザーのグループにアクセス権限を提供します。 アクセス・ポリシーは、ターゲット (通常、リソース・グループ内のサービスの 1 つのサービス・インスタンスまたはすべてのインスタンス) と、許可されるアクセスのタイプを定義する役割を設定します。 アカウント所有者として割り当てる必要があるアクセス・ポリシーには、次の 2 つのタイプがあります。これにより、アカウント内のユーザーがリソース・グループ内のリソースを処理するためにアクセスできるようになります。

* リソース・グループ内のリソースへのアクセス権限。 アクセス権限は、グループ内のすべてのリソースに対して付与するか、グループ内の選択したサービスのみに対して付与することができます。
* ユーザーがグループを管理できるようにするためのアクセス権限。つまり、ユーザーは、グループを管理するためにグループの表示、グループの名前の編集、他のユーザーのアクセス権限の管理を行うことができます。そして最も重要なこととして、グループに新しいサービス・インスタンスを作成して追加することができます。

以下の表で、2 つのタイプのアクセス権限の詳細、および割り当てられた各プラットフォーム IAM 役割によりユーザーが操作できるようになる内容を確認してください。

| アクセス・ポリシーの詳細  | リソース・グループに対するアクセス権限のアクション | リソース・グループ内のリソースに対するアクション | 
|:-----------------|:--------------|:---------------|
| アクセス権限の割り当て先 | 選択されたリソース・グループ | リソース・グループ内の選択されたサービス |
| ビューアー役割  | グループとその特性の表示。ただし、グループ内のリソースは表示できない | グループ内のリソースの表示 | 
| オペレーター役割 | 適用外 | 適用外 | 
| エディター役割 | グループの名前またはその他の特性の表示または編集。ただし、グループ内のリソースの表示または編集はできない | リソース・グループ内のリソースの作成、削除、編集、一時停止、再開、表示、バインド、およびアクセス管理 |
| 管理者役割 |  グループのアクセス権限の表示、編集、または管理。ただし、グループ内のリソースの表示、編集、または管理はできない | リソース・グループ内のリソースの作成、削除、編集、一時停止、再開、表示、バインド、およびアクセス管理 | 
{: caption="表 1. リソース・グループに対するアクセス権限" caption-side="top"}

ユーザーが新しいサービス・インスタンスを作成し、それをリソース・グループに追加できるようにするには、ユーザーにリソース・グループのビューアー以上の役割およびサービスのエディター以上の役割を割り当てる必要があります。
{: tip}


## サンプル・アクセス・ポリシー

以下のサンプル・アクセス・ポリシーを検討し、リソース・グループに属する、アカウント内のリソースへのアクセスの割り当て方法の判別に役立ててください。

1. アカウント全体で {{site.data.keyword.Bluemix_notm}} コンテナー・サービスに対するプラットフォーム役割の「管理者」を付与するポリシー。 これらの詳細を含むポリシーは、このサービスのすべてのインスタンスへのアクセスをユーザーに許可し、ユーザーが少なくともビューアー役割を持っているリソース・グループ内のサービスのインスタンスを作成することを許可します。 いずれかのリソースの管理者役割を持つユーザーは、他のユーザーにそのリソースへのアクセス権限を付与することもできます。
2. リソース・グループ (ただし、そのメンバー・リソースは除く) に対するプラットフォーム役割の「ビューアー」をユーザーに付与するポリシー。 これらの詳細を含むポリシーは、このリソース・グループにサービスのインスタンスを作成するために必要な、リソース・グループの表示可能性をユーザーに許可します。
3. リソース・グループ内のすべてのリソースに対してプラットフォーム役割の「エディター」をユーザーに付与するポリシー。 リソースに対してエディター役割を持つユーザーは、そのリソースを編集または削除できます。
4. アカウント全体 (IAM が有効になっているすべてのサービス) に対してプラットフォーム役割の「管理者」をユーザーに付与するポリシー。 これらの詳細を含むポリシーは、アカウント全体のすべてのリソースに対してユーザーがいかなるプラットフォーム・アクションを実行することも許可します。また、アカウント内のリソース・グループの管理など、アカウントに対する管理アクションも実行できます。

## ユースケース例

これらの各ユースケースでは、ユーザー・グループ全員に同一レベルのアクセス権限を付与したい場合、それらのユーザーを[アクセス・グループ](/docs/iam/groups.html#groups)に追加します。 アクセス・グループを使用することにより、アクセス・グループのすべてのメンバーはそのグループに割り当てられたアクセス権限を継承するため、最小数のアクセス・ポリシーを使用できます。
{: tip}

1. 全員が一緒に単一プロジェクトの作業を行う、ユーザー数が 10 人だけの小規模なアカウントを持っている。 一部のユーザーは、アカウントの管理および他のユーザーへのアクセス権限の割り当てを行える必要がある。 一部のユーザーは、経費が発生するサービス・インスタンスのプロビジョンを行える必要がある。 その他のユーザーはアプリケーション開発者であり、彼らに必要なことは、アプリケーション・コンポーネントのサービス・インスタンスを使用できることだけである。 これらのユーザー全員に、アカウントのさまざまな役割とデフォルト・リソース・グループを付与する必要がある。追加のリソース・グループを作成して、リソースを分離したり、一部のユーザーに一部のリソースへのアクセスを制限したりする必要はない。 ユーザーには、各自のニーズに合わせてアカウントおよびデフォルト・リソース・グループに対する役割を付与できる (アカウントを管理し、他のユーザーにアクセス権限を付与する必要があるユーザーには、アカウントの「管理者」、サービス・インスタンスをプロビジョンできる必要があるユーザーには、デフォルトのリソース・グループおよびそのメンバーに対する「エディター」、サービス・インスタンスの使用のみを必要とするユーザーには、リソース・グループ・メンバーに対する「ライター」または「リーダー」)。
2. 3 つのプロジェクトの作業を行う 3 つの異なるチームを含むアカウントを持っている。 数名のユーザーは管理者であり、新しいユーザーをアカウントに追加したり、新しいリソース・グループを作成したり、リソース・グループへのアクセス権限をユーザーに割り当てたりできる必要がある。 残りのユーザーに必要なことは、自分のプロジェクトに関連付けられたリソース・グループにアクセスすることだけである。 管理者アカウントには「管理者」役割を割り当てる。 残りのユーザーには、各自のプロジェクトに関連付けられたリソース・グループおよびリソース・グループ・メンバーに対するさまざまな役割を割り当てる (インスタンスを作成する必要があるユーザーにはリソース・グループの「エディター」、そしてインスタンスを使用できる必要があるユーザーには、リソース・グループ・メンバーの「リーダー」または「ライター」)。
3. 複数のリソース・グループを含むアカウントを持っている。 アカウント全体にわたるサービス A の管理者であり、そのサービスのすべてのインスタンスにアクセスする必要があり、さらにインスタンスを作成できる必要もあるユーザーが何人かいる。ただし、それらのユーザーは、アカウント内のその他のリソースにアクセスする必要はない。 それらのユーザーにはアカウント・レベルでサービス A に対する「管理者」役割を割り当て、さらに、それらのユーザーがインスタンスを作成できる必要があるアカウント内のすべてのリソース・グループの「ビューアー」役割を割り当てる。
4. あるサービスの特定のリソースへのアクセス権限 (例えば、IBM Cloud オブジェクト・ストレージ内のバケット A への書き込み権限) だけが必要なユーザーがアカウント内にいる。 このユーザーは、アカウント内のリソース・グループを表示したり、このクラウド・オブジェクト・ストレージのインスタンス内の他のサービスや他のバケットにアクセスできてはならない。 このユーザーには、クラウド・オブジェクト・ストレージの特定のインスタンス内のバケット A に対する「ライター」役割を付与する。 このポリシーは、サービス固有のインターフェース (この例では、Cloud オブジェクト・ストレージ UI) またはメインのアクセス権限の割り当て UI のいずれかを使用して付与できる。 サービス固有の UI ではリソース・リストから選択できるのに対し、アクセスの割り当て UI では、サービス・インスタンス・レベルより下のリソースが表示されず、それらのリソースにポリシーを割り当てるには、手動で CRN を入力する必要があるため、サービス固有の UI の使用を推奨する。