# 共通鍵暗号方式の色々な実装
このレポジトリでは共通鍵暗号方式についての様々な実装のプログラムについて示す。
## RSA暗号
代表的な公開鍵暗号であるRSA暗号について暗号化と復号化のプログラムがRSA.pyとなっている。
理論は以下のようになっている。
### RSA暗号における鍵生成
① 2つの大きな素数p, qを秘密で選び、N = pqを 算する
② gcd((p-1)(q-1),e)=1となる 然数eを適当に選ぶ
③拡張ユークリッドアルゴリズムを(e, (p-1)(q-1))に対して行い、eの 元をdとする
④P=(N, e)を公 鍵として公 、dを秘密鍵として保持する
### RSA暗号における暗号化
公開鍵P=(N, e)と平文mを入力したときの暗号文Cは次式で計算できる。
𝐶=𝑚𝑒 (𝑚𝑜𝑑 𝑁)
### RSA暗号における復号化
秘密鍵dと暗号文Cを入力としたときの復号化された平文m’は次式で計算できる。 
𝑚′=𝐶𝑑 (𝑚𝑜𝑑 𝑁)
また、このプログラムと素数のランダム生成プログラムを組み合わせてRSA暗号システムのプログラムRSAsystem.pyが出来上がる。
## フェルマーテストとミラーラビンテスト
素数のランダム生成のために使用する素数判定法としてフェルマーテストとミラーラビンテストがある。それぞれ、Fermat_test.pyとMillerRabin_test.pyで実装されている。
それぞれの理論は以下のようになっている。
### フェルマーテストの理論
フェルマーテストは乱択アルゴリズムと呼ばれる概念を導入した素数判定法である。
乱択アルゴリズムとは 常の動作が決定的な手続きに従って行われ、アルゴリズム終了時に正しい判定が行われるアルゴリズムとは違い、動作が乱数によってランダムに決められ正しい判定が行われるとは限らないが、決定的なアルゴリズムと比べ高速であるというものである。フェルマーテストとMiller-Rabinテストはともに乱択アルゴリズムである。
フェルマーテストは次のフェルマーの小定理を利用する。
p>0を素数としたとき1≤𝑎≤𝑝−1とすると、 𝑎𝑝≡𝑎 (𝑚𝑜𝑑 𝑝)
が成り立つという定理である。これに して両 をaで割ると、 𝑎𝑝−1≡1 (𝑚𝑜𝑑 𝑝)
となる。この対偶をとって、 𝑎𝑝−1≢1 (𝑚𝑜𝑑 𝑝)
となるならば、pは素数ではないと結 づけられる。
アルゴリズムは次のような手 になっている。
素数判定する整数p、最大繰り し回数をSとして1≤𝑖≤𝑆の 以下を繰り す。
① aを1からp-1の中からランダムに選ぶ
② もし𝑎𝑝−1≢1 (𝑚𝑜𝑑 𝑝)ならば、「素数でない」と判定し終了
③ i=Sならば、「素数である」と判定、そうでなければiを増加させ①に戻る
### ミラーラビンテストの理論
「pが素数であるとき、 然数aが𝑎2≡1 (𝑚𝑜𝑑 𝑝)を満たすならば𝑎≡ 1 (𝑚𝑜𝑑 𝑝)が成り立つ」
この対偶をとると、𝑎2≡1 (𝑚𝑜𝑑 𝑝)かつ𝑎≢ 1 (𝑚𝑜𝑑 𝑝)となるaが存在したらpは素数でないと結論付けられる。
アルゴリズムは次のような手 になっている。
素数判定する整数p、最大繰り し回数Sを入力する。
P > 2かつ偶数ならば「素数でない」と判定し終了
𝑝−1=2𝑢𝑣となる整数𝑢≥0と奇数𝑣≥0を つける。
1≤𝑖≤𝑆の 以下を繰り す。
① aを1からp-1の中からランダムに選ぶ
② もし𝑎𝑝−1≢1 (𝑚𝑜𝑑 𝑝)ならば、「素数でない」と判定し終了
③j=1,…,uに対して 𝑎2𝑗𝑣≡1 (𝑚𝑜𝑑 𝑝)かつ𝑎2𝑗−1𝑣≢ 1 (𝑚𝑜𝑑 𝑝)となるjが存在すれば「素数でない」と判定し終了
④ i=Sならば「素数である」と判定し終了そうでなければ①へ戻る
