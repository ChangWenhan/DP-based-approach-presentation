### 1) Experimental Results in the First Scenario

#### Fig. 3(a) 静态环境

现象1：在图片三的a表中，可以看到随着网络变大与恶意agent的增加，四种方法的成功率在降低，

解释：这是因为当一个网络的规模变大，一个packet需要走更多的步数到达目的地，但是为了保存sensor的能量，一个packet通常被设置了一个小的“步数限制”，也就是time-to-live (TTL),因此一部分packet在大规模的的网络中不能在有步数限制的情况下到达终点。成功率就下降了。

现象2：随着网络变大与恶意agent的增加，BC-based approach和Regular approach的成功率的差距在减小。

解释：每当一个packet走一步，发送的agent就可能向邻居寻求advice，BC-based方法需要进行大量的广播与投票，因此通信开销预算在早起就用光了，这时候无法寻求advice的BC-based也就变成了Regular方法。

现象3：随着网络变大与恶意agent的增加，DP-based approach和DP-removed approach的成功率的差距在增大。

解释：DP-removed没有使用差分隐私，所以更容易受到恶意agent的影响，agent就会被误导，把packet传送到远离目的地的地方，包被成功传送的概率也就降低了。

#### Fig. 3(b)

四种方法的成功率都随着时间步长的增加而提高，但由于缺乏agent建议，常规方法的收敛速度慢于其他三种方法。

#### Fig. 3(c)

现象1：当agent数大于100时，四种方法的平均步数保持相对稳定。

解释：由于网络规模很大，许多数据包可能必须用尽其跳限（即TTL）才能到达目的地，因此，平均跳数几乎没有增加的空间。

#### Fig. 3(d)

BC-based的方法使用最多的通信开销。相比之下，基于DP-based和DP-removed方法因为它们的建议机制,使用更少的通信开销。

<img src="C:\Users\christan\Desktop\figure3.png" alt="avatar" style="zoom: 80%;" />

#### Fig. 4(a) 动态环境

现象1：相比静态环境，成功率降低，通信开销升高。

解释：因为网络是动态的，当一个agent离开一条路线或许就被破坏了，用那个agent作为依赖点的的数据包就要去寻找其他路线，这个情况就会增加多余的步数并且消耗通信开销，由于额外的步数，数据包可能无法在其步数限制内到达目的地，因此成功率会降低。

#### Fig. 4(b)

现象：四种方法的收敛速度比静态环境慢一点

解释：这是因为，当一个agent离开时，与该离开agent有关的其他业务代表的knowledge已经过时了。 这些agent必须学习新知识。 这种情况会降低收敛速度。

<img src="C:\Users\christan\Desktop\figure4.png" alt="avatar" style="zoom:67%;" />

### 2) Experimental Results in the Second Scenario

#### Fig. 5(a) 静态环境

现象1：BC-based and DPremoved两个方法与常规方法相比，获得的合作者比例更少。

解释：合作的发展是在竞争环境中，agent的邻居是该agent的对手。 因此，受agent邻居青睐的行为可能对该代理人不利。

现象2：随着恶意agent在网络中的数量的增加，DP-based/DP-removed方法和Regular方法的差距从百分之十降低到百分之三

解释：基于上一个现象的解释，如果一个agent的邻居大多数是defector，那么他这个合作者可能就会被建议变成一个defector。然而，如果一部分邻居是恶意agents，他们可能建议合作者继续当一个合作者，因为这样defector就可以继续利用合作者，让合作者有一个非常低的回报。这样的行为意外的让合作者的数量增加了。

现象：当恶意agent的比例小于0.1，因为上面讲述的原理，DP-based方法获得的合作者的比例比Regular方法获得的更少，但是当恶意agent的比例大于0.1的时候反而优于Regular方法。

原因：因为差分隐私，Laplace噪声被加入到了回报里面，回报被agent用来判断选择adviser。

Laplace噪声会影响agent选择adviser！

例子1：

当合作者遇到了一个defector，合作者会获得回报Su=-1，defector会得到回报Te=5，当两个defector相遇，他们都会得到回报Pu=0，当两个合作者相遇，他们都会得到回报Re=4。

当一个合作者遇到了一个defector并且defector是一个恶意agent，defector或许会建议合作者继续做一个合作者，这样可以最大化defector的回报。

如果合作者使用的DP-removed方法，合作者或许就在下一次就改变了adviser，因为和作者的回报非常低，但是如果用了DP-based方法，就可能在下一次选择中继续用这个defector，因为合作者的回报Su=-1加上了Laplace噪声就会接近Pu=0，因此合作者变成defector的可能性也就低了。

例子2：

<img src="C:\Users\christan\Desktop\oho.png" alt="Image text" style="zoom:67%;" />

#### Fig. 5(b)

现象：DP-base方法下收敛速度最快。

解释：这是因为这个时候agents不像其他两种情况下defector和cooperater转变的那么快

#### Fig. 5(c)

现象：Fig. 5(c) shows the average payoff obtained by using the four approaches. Fig. 5(c) has a similar trend to Fig. 5(a).

解释：随着合作者的比例上升，平均回报也在上升，因为两个agent合作能比对立赚到更多回报，平均下来也更多。

#### Fig. 5(d)

现象1：BC-based方法用了最多的通信预算，比其他三种方法多用了大约百分之五十

解释：因为BC-based方法有广播机制。老生常谈

现象2：DP-removed and DP-based两种方法有近乎相同的通信开销，并且稍微比Regular高百分之三。

解释：两种方法有相同的寻求建议的机制，自然消耗的就差不多，Regular不许agent咨询，所以保存了通信开销。

<img src="C:\Users\christan\Desktop\figure5.png" alt="Image text" style="zoom:67%;" />

#### Fig. 6(a) 动态环境，展示四种方法在第二种场景的性能，但是图a有疑惑

现象：DP-based方法比Regular获得了更多的合作者比例，大约7%，甚至是在恶意代理比例小于0.1的情况下，DP-remove获得了和Regular方法近乎相同的合作者比例。

解释：因为网络的动态问题，Regular方法中一个agent很难取学习一个稳定的更新策略。其他三种方法agents被允许向其他寻求advice，那么agent就可以像其他的邻居咨询

#### Fig. 6(b)

现象：收敛速度变慢了

解释：因为是动态网络了

#### Fig. 6(c)

现象：这个图展示的是获得的平均回报，他和a有类似的趋势.

解释：平均回报主要且正相关受合作者的比例影响，更高的合作者比例也就会有更高的平均回报

#### Fig. 6(d)

现象：四种方法有着与在静态环境中近乎相同的通信开销。

解释：通信开销取决于网络中的agent数量，以及寻求建议的机制。这个实验中一个agent进入离开基本的数量是稳定的，咨询机制也是不会变的，所以通信开销不被动态环境影响太多。

<img src="C:\Users\christan\Desktop\figure6.png" alt="Image text" style="zoom:67%;" />

