---

copyright:
  years: 2014, 2018
lastupdated: "2018-02-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# ネットワーク・トラフィックをエッジ・ワーカー・ノードに制限する
{: #edge}

エッジ・ワーカー・ノードを使用すると、外部的にアクセスされるワーカー・ノードの数を減らし、ネットワーキングのワークロードを分離することができるので、クラスターのセキュリティーが改善されます。 これらのワーカー・ノードがネットワーキング専用としてマーク付けされると、他のワークロードはワーカー・ノードの CPU やメモリーを消費してネットワーキングに干渉することがなくなります。
{:shortdesc}



## ワーカー・ノードをエッジ・ノードとしてラベル付けする
{: #edge_nodes}

クラスター内の複数のノードに `dedicated=edge` ラベルを追加して、Ingress とロード・バランサーがそれらのワーカー・ノードにのみデプロイされるようにします。

開始前に、以下のことを行います。

- [標準クラスターを作成します。](cs_clusters.html#clusters_cli)
- クラスターに 1 つ以上のパブリック VLAN があることを確認してください。 エッジ・ワーカー・ノードは、プライベート VLAN だけがあるクラスターには使用できません。
- [クラスターを Kubernetes CLI のターゲットとして設定](cs_cli_install.html#cs_cli_configure)します。

手順:

1. クラスター内のすべてのワーカー・ノードをリストします。 **NAME** 列からプライベート IP アドレスを使用して、ノードを識別します。 エッジ・ワーカー・ノードとするワーカー・ノードを 2 つ以上選択します。 2 つ以上のワーカー・ノードを使用することにより、ネットワーキング・リソースの可用性が向上します。

  ```
  kubectl get nodes -L publicVLAN,privateVLAN,dedicated
  ```
  {: pre}

2. `dedicated=edge` により、ワーカー・ノードにラベルを付けます。 `dedicated=edge` によりワーカー・ノードにマークが付けられると、すべての後続の Ingress とロード・バランサーは、エッジ・ワーカー・ノードにデプロイされます。

  ```
  kubectl label nodes <node_name> <node_name2> dedicated=edge
  ```
  {: pre}

3. クラスター内にあるすべての既存のロード・バランサー・サービスを検索します。

  ```
  kubectl get services --all-namespaces -o jsonpath='{range .items[*]}kubectl get service -n {.metadata.namespace} {.metadata.name} -o yaml | kubectl apply -f - :{.spec.type},{end}' | tr "," "\n" | grep "LoadBalancer" | cut -d':' -f1
  ```
  {: pre}

  出力:

  ```
  kubectl get service -n <namespace> <name> -o yaml | kubectl apply -f
  ```
  {: screen}

4. 直前のステップからの出力を使用して、それぞれの `kubectl get service` 行をコピーして貼り付けます。 このコマンドは、ロード・バランサーをエッジ・ワーカー・ノードに再デプロイします。 再デプロイする必要があるのは、パブリック・ロード・バランサーだけです。

  出力:

  ```
  service "<name>" configured
  ```
  {: screen}

`dedicated=edge` によりワーカー・ノードにラベルを付け、すべての既存のロード・バランサーと Ingress をエッジ・ワーカー・ノードに再デプロイしました。 次に、他の[ワークロードがエッジ・ワーカー・ノードで実行されないように](#edge_workloads)、そして[ワーカー・ノード上のノード・ポートへのインバウンド・トラフィックをブロックするように](cs_network_policy.html#block_ingress)します。

<br />


## ワークロードがエッジ・ワーカー・ノード上で実行されないようにする
{: #edge_workloads}

エッジ・ワーカー・ノードの利点の 1 つは、それらがネットワーク・サービスだけを実行するように指定できることです。 `dedicated=edge` 耐障害性の使用は、すべてのロード・バランサーと Ingress サービスが、ラベルの付けられたワーカー・ノードにのみデプロイされることを意味します。 ただし、他のワークロードがエッジ・ワーカー・ノード上で実行されてワーカー・ノードのリソースを消費することがないようにするため、[Kubernetes テイント ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/) を使用する必要があります。
{:shortdesc}

1. `edge` ラベルのあるすべてのワーカー・ノードをリストします。

  ```
  kubectl get nodes -L publicVLAN,privateVLAN,dedicated -l dedicated=edge
  ```
  {: pre}

2. テイントを各ワーカー・ノードに適用します。このテイントは、ポッドがワーカー・ノード上で実行されるのを防ぎ、`edge` ラベルのないポッドをワーカー・ノードから削除します。 削除されるポッドは、容量のある他のワーカー・ノードに再デプロイされます。

  ```
  kubectl taint node <node_name> dedicated=edge:NoSchedule dedicated=edge:NoExecute
  ```

これで、`dedicated=edge` 耐障害性のあるポッドだけがエッジ・ワーカー・ノードにデプロイされます。
