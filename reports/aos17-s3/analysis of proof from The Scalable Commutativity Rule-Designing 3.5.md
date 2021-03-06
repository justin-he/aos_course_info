<h4>对3.5proof的分析</h4>

<p>
&nbsp;&nbsp;下面通过建立一个来自于引用实现M和历史记录H=X||Y的扩展实现m进行证明
</p>

<p>
&nbsp;&nbsp;对于任何历史记录X||P（其中P是Y的前缀），P中的实现的步骤并没有冲突。m在SIM交换区域中可以修改。
</p>

<p>
  &nbsp;&nbsp;首先假设一个来自M的m<sub>ns</sub>。m<sub>ns</sub>在重启模式中开启。当输入匹配H时，m<sub>ns</sub>在不调用M的情况下能够根据H做出响应。但是，当输入偏离H时，m<sub>ns</sub>无法做出响应，在这种情况下进入模仿模式。
  &nbsp;&nbsp;m<sub>ns</sub>的状态包含两部分。
    </p>
<p>
1、s.h： 保存了待重新执行的H的一部分或者是模拟模式的EMULATE指令。其中s.h初始化为H。
</p>

<p>
2、s.refstate：为引用的状态。
</p>

<p>

&nbsp;&nbsp;假设m<sub>ns</sub>以一种受限的方式接收CONTINUE调用。
</p>

<p>
  &nbsp;&nbsp;这种实现的响应对于任何的历史记录总是匹配那些来自引用的实现。在重复模式下，m<sub>ns</sub>中的任何两步在访问s.h时都是冲突的。这些访问情况记录了哪种调用曾经出现过，如果没有这些访问就不可能在之后初始化M的状态。当然，这也是交换规则所产生的缘由。按照这个说法，所有接下来的响应将仍然有效。m与m<sub>ns</sub>相似，在无冲突模式下扩展m被用来执行Y中的指令。其状态如下：
</p>

<p>
• s.h[t]—每个线程的历史记录. 初始化为X ||COMMUTE || (Y|t), COMMUTE模式下扩展m指令表明扩展区域开始的地方； 
</p>

<p>
• s.commute[t]—每个线程的标记，表明交换区域是否已经到达。初始化为FALSE.
</p>

<p>
• s.refstate—引用实现的状态。
</p>

<p>
&nbsp;&nbsp;在交换区域中的，m的每一步操作只访问对于调用线程特定的状态部分。意味着交换区域中的任何两步都没有访问冲突，这就是交换规则的证明部分。当通过H’ 初始化引用实现的状态时，其构造采用SIM交换规则。如果观察到的调用在交换区域之前发生了偏离，然后正如在m<sub>ns</sub>中一样H’ 将恰好与观察到的调用相等。但是，如果观察到的调用在交换区域之中或者之前就发生偏移，那就没有足够的信息恢复调用的指令。因此，H’ 可能重新编排Y中的调用。
</p>
