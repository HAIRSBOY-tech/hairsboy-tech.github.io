<h1 class="atx" id="c-stl-2">C++ STL 2</h1>
<p>五、容器</p>
<p>早期的11个容器类型：<code>deque</code>、<code>list</code>、<code>queue</code>、<code>stack</code>、<code>vector</code>、<code>map</code>、<code>multimap</code>、<code>set</code>、<code>multiset</code>和<code>bitset</code>。C++11新增容器：<code>forward_list</code>、<code>unordered_map</code>、<code>unordered_mulitmap</code>、<code>unordered_set</code>和<code>unordered_mulitset</code>。</p>
<p>1.容器的基本特征：</p>
<p><code>X</code>表示容器；<code>T</code>表示存储在容器中的对象类型;<code>a</code>、<code>b</code>表示类型为<code>X</code>的值；<code>r</code>表示类型为<code>X&amp;</code>的值；<code>u</code>表示类型为<code>X</code>的标识符。</p>
<table>
<thead>
<tr>
<th>表达式</th>
<th>返回类型</th>
<th>说明</th>
<th>（时间）复杂度</th>
</tr>
</thead>
<tbody><tr>
<td><code>X::iterator</code></td>
<td>指向<code>T</code>的迭代器</td>
<td>正向迭代器</td>
<td>编译时间</td>
</tr>
<tr>
<td><code>X::value_type</code></td>
<td><code>T</code></td>
<td><code>T</code>的类型</td>
<td>编译时间</td>
</tr>
<tr>
<td><code>X u;</code></td>
<td></td>
<td>创建容器u(空)</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>X ();</code></td>
<td></td>
<td>创建匿名空容器</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>X u(a);X u=a;</code></td>
<td></td>
<td>调用复制构造函数后<code>u==a</code>.</td>
<td>线性O(n)</td>
</tr>
<tr>
<td><code>r=a</code></td>
<td>X&amp;</td>
<td>赋值运算符</td>
<td>线性O(n)</td>
</tr>
<tr>
<td><code>a.begin()</code></td>
<td>迭代器</td>
<td>指向第一个元素的迭代器</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>(&amp;a)-&gt;~X()</code></td>
<td>void</td>
<td>析构函数</td>
<td>线性O(n)</td>
</tr>
<tr>
<td><code>a.end()</code></td>
<td>迭代器</td>
<td>返回指向超尾元素的迭代器</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>a.size()</code></td>
<td>无符号整型</td>
<td>返回元素个数</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>a.swap(b)</code></td>
<td>void</td>
<td>交换a、b的内容</td>
<td>固定O(1)</td>
</tr>
<tr>
<td><code>a==b</code>&nbsp; &nbsp; <code>a!=b</code>与<code>a==b</code>相反</td>
<td>可转为bool</td>
<td>如果a、b长度相等，相应的元素都相等，返回真。</td>
<td>线性O(n)</td>
</tr>
</tbody></table>
<p>复杂度描绘了执行操作所需要的时间。从快到慢依次为：编译时间、固定时间、线性时间。</p>
<p>2.C++11 新增的容器要求：rv表示类型为X的非常量右值</p>
<table>
<thead>
<tr>
<th><code>X u(rv);X u=rv;</code></th>
<th></th>
<th>调用移动构造函数</th>
<th>线性</th>
</tr>
</thead>
<tbody><tr>
<td><code>a=rv;</code></td>
<td><code>X&amp;</code></td>
<td>调用移动赋值运算符</td>
<td>线性</td>
</tr>
<tr>
<td><code>a.cbegin()</code></td>
<td><code>const_iterator</code></td>
<td>返回指向第一个元素的const迭代器</td>
<td>固定</td>
</tr>
<tr>
<td><code>a.cend()</code></td>
<td><code>const_iterator</code></td>
<td>返回指向超尾元素的const迭代器</td>
<td>固定</td>
</tr>
</tbody></table>
<p>移动操作可能修改源对象，还可能转让所有权，而不做任何复制。</p>
<p>1.&nbsp;<strong>序列容器</strong>：(7种STL容器：<code>deque</code>双端队列、<code>forward_list</code>链表、<code>queue</code>队列、<code>priority_queue</code>优先队列(二叉堆)、<code>stack</code>(栈)和<code>vector</code>(矢量))</p>
<p>(1)&nbsp;<code>queue</code>队列能够能够在队尾添加元素，在队首删除元素；<code>deque</code>表示双端队列允许在两端添加或删除元素（<code>array</code>也被归为序列容器）。</p>
<p>(2)&nbsp;特征：按线性顺序排列，即存在第一个元素，最后一个元素，除了该两个元素处其他的元素前后都分别有一个元素。</p>
<p>(3)序列的要求：t表示类型为T的值，n表示整数，p、q、i、j表示迭代器（T可做存储在容器中值的类型）</p>
<p>①基本操作[注：区间[x,y）的范围包括x(起始)不包括y(结束)]</p>
<table>
<thead>
<tr>
<th>表达式</th>
<th>返回类型</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td><code>X a(n,t);X(n,t);</code></td>
<td></td>
<td>声明一个由n个t值组成的序列,名称为a或匿名。格式：X(需要的数量，需要的值)</td>
</tr>
<tr>
<td><code>X a(i,j);X (i,j);</code></td>
<td></td>
<td>声明一个名为a(或匿名)的容器并初始化为区间[i,j)的内容。格式：X(开始，结束/[区间])</td>
</tr>
<tr>
<td><code>a.insert(p,t);</code></td>
<td>迭代器</td>
<td>将t插入到p的前面格式：insert(位置，待插入值)</td>
</tr>
<tr>
<td><code>a.insert(p,n,t);</code></td>
<td>void</td>
<td>将n个t插入到p的前面格式：insert(位置，需要的数量，待插入值)</td>
</tr>
<tr>
<td><code>a.insert(p,i,j);</code></td>
<td>void</td>
<td>将区间[i,j)中的元素插到p前格式：insert(要插入的位置，[区间]/开始位置，结束位置)</td>
</tr>
<tr>
<td><code>a.erase(p);</code></td>
<td>迭代器</td>
<td>删除p所指向的位置格式：erase(删除位置)</td>
</tr>
<tr>
<td><code>a.erase(p,q);</code></td>
<td>迭代器</td>
<td>删除区间[p,q)中的元素格式：erase([待删除的区间]/开始位置，结束位置)</td>
</tr>
<tr>
<td><code>a.clean()</code></td>
<td>void</td>
<td>清空容器</td>
</tr>
</tbody></table>
<p>②可选要求:在允许的情况下，时间复杂度为固定时间。</p>
<table>
<thead>
<tr>
<th>表达式</th>
<th>返回类型</th>
<th>含义</th>
<th>容器</th>
</tr>
</thead>
<tbody><tr>
<td><code>a.front()</code></td>
<td>T&amp;</td>
<td>*a.begin() 返回首元素</td>
<td>vector,list,deque</td>
</tr>
<tr>
<td><code>a.back()</code></td>
<td>T&amp;</td>
<td>*--a.end() 返回尾部元素</td>
<td>vector,list,deque</td>
</tr>
<tr>
<td><code>a,push_front(t)</code></td>
<td>void</td>
<td>a.insert(a.begin(),t) 在头部插入</td>
<td>list,deque</td>
</tr>
<tr>
<td><code>a.push_back(t)</code></td>
<td>void</td>
<td>a.insert(a.end(),t) 在尾部插入</td>
<td>vector,list,deque</td>
</tr>
<tr>
<td><code>a.pop_front(t)</code></td>
<td>void</td>
<td>a.erase(a.begin()) 删除头部</td>
<td>list,deque</td>
</tr>
<tr>
<td><code>a.pop_back(t)</code></td>
<td>void</td>
<td>a.erase(--a.end()) 删除尾部</td>
<td>vector,list,deque</td>
</tr>
<tr>
<td><code>a[n]</code>&nbsp; &nbsp; <code>a.at(n)</code></td>
<td>T&amp;</td>
<td>*(a.begin()+n)&nbsp; 访问元素</td>
<td>vector,deque</td>
</tr>
</tbody></table>
<p>注意：<code>at()</code>方法会检查边界，若越界则引发<code>out_of_range</code>异常。</p>
<p>(4)序列容器的详解</p>
<p>·矢量类 <code>std::vector</code></p>
<p>模板类<code>vector</code>即<code>std::vector</code>位于<code>vector</code>头文件中。</p>
<p>可以动态修改长度、可以随机访问元素、在尾部添加删除元素的时间固定、在头部中间删除元素复杂度为线性时间、它是可反转容器，拥有rbegin()和rend()、使用reverse_iterator可以反向遍历容器。</p>
<p>声明格式：<code>vector&lt;元素类型&gt; 对象名(元素个数);</code></p>
<p>其类似于数组，可用<code>operator[]()</code>访问元素。(提供随机访问功能)</p>
<p>·deque<strong>双向队列</strong>[Double-ended Queue]</p>
<p>模板位于头文件<code>deque</code>类似于<code>vector</code>容器，支持随机访问，从deque对象的开始位置插入和删除元素的时间是固定的。</p>
<p>·list<strong>双向链表</strong></p>
<p>模板位于<code>list</code>头文件中。</p>
<p>除了第一个和最后一个元素之外，每个元素都与前后的元素相链接，可以双向遍历。list链表中任一位置进行插入和删除的时间是固定的。list可以反转，但不支持数组表示法和随机访问。从容器插入或删除元素后，链表迭代器指向元素不变。</p>
<p>| list成员函数[Alloc模板参数有默认值] |
| --- | --- |
| 函数 | 说明 |
| <code>void merge(list&lt;T,Alloc&gt;&amp;x)merge(要合并的链表) </code>| 将链表x与调用链表合并。两个链表必须已近排序。合并后的经过排序的链表保存在调用链表中，x为空。时间复杂度为线性时间 |
| <code>void remove(const T&amp; val)remove(待删除实例列表)</code> | 从链表中删除val的所有实例，复杂度为线性时间。 |
| <code>void sort() </code>| 使用&lt;排序，n个元素时间复杂度为 |
| <code>void splice(iterator pos ,list&lt;T,Alloc&gt; X)splice(插入位置，待插入链表) </code>| 将链表X的内容插入到pos的前面，X将清空。复杂度为固定时间。 |
| <code>void unique()</code> | 将连续相同的元素压缩为单个元素，复杂度为线性时间。 |</p>
<p><code>insert()</code>和<code>splice()</code>的区别：</p>
<p>&nbsp;<code>insert()</code>将原始区间的副本插入到目标地址；<code>splice()</code>将原始区间移到目标地址，在其执行后迭代器仍然有效。</p>
<p>非成员函数<code>sort()</code>需要随机访问迭代器。</p>
<p>·[C++11]forward_list<strong>单链表</strong></p>
<p>在单链表中，每个节点只链接到下一个节点，并没有链接到前一个节点。则它只要正向迭代器，它是不可反转容器，比list更简单。</p>
<p>·queue<strong>队列</strong>[适配器类]</p>
<p><code>queue</code>模板位于头<code>queue</code>，不允许随机访问队列元素，不允许遍历队列，可以将元素添加到队尾，从队首删除元素，查看首尾的值，检查元素数目和测试是否为空。</p>
<p>| queue的操作 |
| --- | --- |
| 方法 | 说明 |
| <code>bool empty() const</code> | 队列为空返回true否则为false |
| <code>size_type size() const </code>| 返回元素数目 |
|<code> T&amp; front()</code> | 指向队首元素的引用 |
| <code>T&amp; back() </code>| 指向队尾元素的引用 |
|<code> void push(const T&amp;x)</code> | 在队尾插入x |
| <code>void pop()</code> | 删除队首元素 |</p>
<p>&nbsp;·priority_queue<strong>优先队列</strong>模板：</p>
<p>位于头<code>queue</code>中，支持操作与<code>queue</code>相同。主要区别在于其最大的元素被移到队首，内部默认底层类为<code>vector</code>，</p>
<p>可以修改确定元素的比较方法，构造函数如下：</p>
<p><code>priority_queue&lt;int&gt; pq1;//默认大根堆</code></p>
<p><code>priority_queue&lt;int&gt; pq2(greater&lt;int&gt;);//小根堆</code></p>
<p><code>priority_queue&lt;int, vector&lt;int&gt;, less&lt;int&gt;&gt; que; //定义大根堆</code>
<code>priority_queue&lt;int, vector&lt;int&gt;, greater&lt;int&gt;&gt; que; //定义小根堆，VS下需要加入头文件#include&lt;functional&gt;</code></p>
<p>·stack<strong>栈</strong>：</p>
<p>位于<code>stack</code>头文件中，其特点是先入后出。</p>
<p>不允许随机访问遍历；允许压栈出栈，查看栈顶值，检查元素数目和栈是否为空。</p>
<p>| stack操作 |
| --- | --- |
| 方法 | 说明 |
| <code>bool empty() const</code> | 栈为空返回true否则为false |
|<code> size_type size() const</code> | 返回元素数目 |
|<code> T&amp; top()</code> | 返回指向栈顶的引用 |
|<code> void push(const T&amp;x)</code> | 在栈顶压入x |
| <code>void pop()</code> | 删除栈顶元素(出栈) |</p>
<p>·array [C++11]它是非STL容器，其长度固定，拥有成员operator[]和at()，可将STL算法用于它。</p>
<p>4.<strong>关联容器</strong>：对容器概念上的另一改进。</p>
<p>关联容器将<strong>值</strong>与<strong>键</strong>关联起来，并使用键来查找值。</p>
<p>对于容器<code>X</code>，<code>X::value_type</code>指出了存储在容器中的值的类型，<code>X::key_type</code>指出了键的类型。提供了对元素的快速访问。</p>
<p>允许插入新元素，但不能指定插入的位置。使用树实现，根节点链接1到2个节点，每个节点都如此，从而形成分支结构。</p>
<p>STL提供4个关联容器：<code>set</code>、<code>multiset</code>(位于<code>set</code>头文件)、<code>map</code>、<code>multimap</code>(位于map头文件)；<code>set</code>的值与键类型相同，键是唯一的，<code>set</code>的值就是键。<code>multiset</code>与<code>set</code>相似，只是可能有多个值相同。</p>
<p>在<code>map</code>中，值与键的类型不同，键是唯一的，每个键对应一个值，</p>
<p><code>multimap</code>类似，只是一个键可以对应多个值。</p>
<p>(1)&nbsp;set<strong>集合</strong></p>
<p>①关联集合，可反转，可排序，且键是唯一的，不可以存储多个相同的值；</p>
<p>②声明:<code>set&lt;键值类型&gt; 名称;</code></p>
<p>第二个模板参数是可选的，可以用来指示对键进行排序的比较函数或对象。默认用<code>less&lt;键值类型&gt;</code>。</p>
<p>③通用函数[要先排序]</p>
<p><code>set_unior()</code>求并集(合并相同的值)，前两个参数指定第一个集合的区间，接下来两个指定第二个集合的区间，第五个指定了插入的地方，即输出迭代器.</p>
<p>用法：<code>set_unior(第一个集合的开始，第一个集合的结束/[第一个集合的区间],第二个集合的开始，第二个集合的结束/[第二个集合的区间]，输出的位置);</code></p>
<p><code>set_intersection()</code>求交集、<code>set_difference()</code>求两集合之差的用法与上面相同</p>
<p>④set的方法</p>
<p><code>lower_bound(键值)</code>将键作为参数并返回一个迭代器，指向集合中第一个不小于键参数的成员</p>
<p><code>upper_bound(键值)</code>将键作为参数并返回一个迭代器，指向集合中第一个大于键参数的成员</p>
<p>使用的都是二分法,复杂度\Theta(\log n)</p>
<p>(2)&nbsp;multimap</p>
<p>①创建：</p>
<p><code>multimap&lt;键类型，数据类型&gt; 名称;</code>第三个模板参数可选，用于指出对键进行排序的比较函数或对象，默认为<code>less&lt;&gt;</code>；</p>
<p>为了将信息结合在一起，实际的值与键将进行结合，<code>pair&lt;class T,class U&gt;</code>模板将这两种值存储到一个对象当中。</p>
<p>如果<code>keytype</code>是键类型，<code>datatype</code>是数据类型，则值类型为<code>pair&lt;const keytype,datatype&gt;</code></p>
<p>(注意<code>multimap</code>直接存值，即<code>pair</code>)数据项是按键排序的。</p>
<p>②使用：模板<code>pair</code>的构造函数:</p>
<p><code>pair&lt;键类型,数据类型&gt;(键,值);</code></p>
<p>使用<code>insert(pair值)</code>方法插入容器。对于<code>pair</code>对象可以用<code>first</code>和<code>second</code>来访问键与值。</p>
<p>③获取multimap信息</p>
<p>成员函数<code>count(键)</code>接受键作为参数，返回具有该键的数目；</p>
<p>成员函数<code>lower_bound()</code>和<code>upper_bound()</code>将键作为参数，原理与set的相同;</p>
<p>成员函数<code>equal_range()</code>用键作为参数，返回两个迭代器</p>
<p>他们表示的区间与该键匹配。该方法将两个值封装在一个pair对象中，这个pair的两个模板参数均为迭代器。</p>
<p>5.<strong>无序关联容器</strong>：对容器概念的另一种改进。底层差别在于其基于数据结构哈希表，提供了效率。</p>
<p>共4种：<code>unordered_set</code>、<code>unordered_multiset</code>、<code>unordered_map</code>、<code>unordered_multimap</code>.</p>
<p>C++11 库提供了模板 <code>hash&lt;key&gt;</code>，无序关联容器默认使用该模板。</p>
<p>见仓库中的<code>附录.pdf</code></p>
