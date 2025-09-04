# EchoStateNetworkAnalysis
研究に関するコード
## 研究の方向性
Echo state network(ESN)[^1][^2]はRecurrent Neural Network(RNN)と同じアーキテクチャを持つニューラルネットワークモデルである．
しかし，ESNは通常のRNNと異なる特徴を持つ．
それは内部状態の重み行列がランダム行列であり，最後の出力層の重みのみを学習する点である．
これによって大幅に学習コストを下げることができる．
また，ESNは次のようにモデル化される．
$$
\bm{x}(n+1) = \bm{F}(W_{\rm{res}}\bm{x}(n) + W_{\rm{in}}\bm{u}(n+1) + W_{\rm{back}} \bm{y}(n))
\bm{y}(n+1) = W_{\rm{out}}\bm{x}(n+1)
$$
（定義は後で書く）

一方で，ランダム行列というのがなんでも良いわけではなく，ESNが良い性能を発揮するためにはある条件が存在する．
それはecho state property(ESP)[^1]と呼ばれる条件である．
ESPを満たしているESNは入力と出力が１対１の関係になっており，同じ時系列の入力$\bm{u}(t)$に対して同じ出力を返す性質を持つ．
このようなESPの条件は以下のように表すことができる．
$$
\lim_{n\to \infty} W_{\rm{res}}^n = 0
$$
この条件は$W_{\rm{res}}$のスペクトル半径$\rho<1$とも言い換えられる．

このようにESNではネットワークを定義した時点で，そのネットワークがESPを満たすかどうかがわかるということである（多分）．
そこで，このような時間発展の行列解析によってESNがどの程度の精度と記憶容量を持つか（＝性能の定量化）を調べる．
その後それらの先行研究を参考に，Koopman解析と紐づけられないかを検討する．

（おそらく）
時間発展は行列のみでなく活性化函数$\bm{F}$にも依存する？のであればKoopman解析はその非線形性も込みで解析できるから新たな指標ができると期待．
さらに，ダイナミクスがわかっている状態でKoopman行列を推定し，そのダイナミクスに基づいたリザバーを持つネットワークがどの程度の性能を持つかということが調べられないか．
（コンシステンシーを保ちつつカオス性が強いと性能が出るらしいので、その辺りと比較がひつよう）

## 先行研究調査
[^1]: H. Jaegar, H. Haas, "Harnessing Nonlinearity: Predicting Chaotic Systems and Saving Energy in Wireless Communication",vol. 304, no. 5667, pp. 78-80, April 2004 DOI: 10.1126/science.109127
    [ref](https://www.columbia.edu/cu/biology/courses/w4070/Reading_List_Yuste/haas_04.pdf)
[^2]: H. Jaegar, "The ”echo state” approach to analysing and training recurrent neural networks",German National Research Center for Information Technology GMD Report, vol. 148, no. 34, December 2001
    [ref](http://www.faculty.jacobs-university.de/hjaeger/pubs/EchoStatesTechRep.pdf)
