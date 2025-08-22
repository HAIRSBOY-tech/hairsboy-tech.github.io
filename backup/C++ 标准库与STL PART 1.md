<h1 class="atx" id="c-标准库与stl库--------part-1">C++ 标准库与STL库&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PART 1</h1>
<h2 class="atx" id="string类"><code>string</code>类</h2>
<p>·头文件:<code>string</code>
·名称空间:<code>std</code></p>
<p>(1)特性:
1.<code>string</code>是模板具体化<code>basic_string&lt;char&gt;</code>的一个typedef.
2.<code>size_type</code>是一个依赖实现的整型，位于头文件<code>string</code>
3.<code>string::npos</code>为字符串的最大长度，通常为<code>unsigned int</code>的最大值.</p>
<p>(2)基础方法</p>
<table>
<thead>
<tr>
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td><code>size()</code>、<code>length()</code></td>
<td>返回字符串的字符个数</td>
</tr>
<tr>
<td><code>operator[]()</code></td>
<td>下标访问法</td>
</tr>
<tr>
<td><code>operator+()</code></td>
<td>拼接字符串</td>
</tr>
<tr>
<td><code>operator=()</code></td>
<td>赋值</td>
</tr>
</tbody></table>
<p>(3)构造函数</p>
<table>
<thead>
<tr>
<th>构造函数</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td><code>string(const char *s);</code></td>
<td>将string对象初始化为C风格字符串。用法：string(要初始化为的C风格字符串);</td>
</tr>
<tr>
<td><code>string(size_type n,char c);</code></td>
<td>创建一个包含n个c字符的字符串。用法string(需要的字符数，填充的字符);</td>
</tr>
<tr>
<td><code>string(const string &amp;str);</code></td>
<td>复制构造函数</td>
</tr>
<tr>
<td><code>string();</code></td>
<td>默认构造函数</td>
</tr>
<tr>
<td><code>template&lt;class Iter&gt;string(Iter begin,Iter end);</code></td>
<td>初始化为区间[begin,end)之间的字符,其包含begin不包含end.begin和end可以看做是指针(迭代器)。用法：string(开始位置，结束位置)；</td>
</tr>
<tr>
<td><code>string(const string &amp;str,size_type pos,size_type n=npos);</code></td>
<td>初始化为对象str中从位置pos开始到结尾的字符，或从位置pos开始的n个字符.用法：string(被操作string对象，开始位置，抽取字符数=到达结尾)；</td>
</tr>
<tr>
<td><code>string(string &amp;&amp;str) noexcept;</code></td>
<td>[C++11]初始化为str,并可能修改（移动构造函数）</td>
</tr>
<tr>
<td><code>string(const char*s,size_type n);</code></td>
<td>初始化为s的前n个字符，即使超过'\0'用法：string(要操作的C风格字符串,需要的长度)</td>
</tr>
<tr>
<td><code>string(initializer_list&lt;char&gt; il);</code></td>
<td>[C++11]初始化为花括号初始化列表里的字符.Initializer_list是初始化列表，如{1,2,3,4,5};</td>
</tr>
</tbody></table>
<p>(4)string版<code>getline()</code>用法:<code>getline(输入流对象，string对象)；</code>
该函数自动调整string大小
当读取的字符数达到最大值,设置failbit</p>
<p>(5)string的逻辑运算符均被重载。用于进行字典序比较</p>
<p>(6)字符搜素:<code>find()</code>方法：
&nbsp;&nbsp;&nbsp;&nbsp;(6.1)<code>size_type find(const string &amp;str,size_type pos=0) const;</code>
&nbsp;&nbsp;&nbsp;&nbsp;(6.2)<code>size_type find(const char *s,size_type pos=0) const;</code>
&nbsp;&nbsp;&nbsp;&nbsp;(6.3)<code>size_type find(const char ch,size_type pos=0) const;</code>
从字符串的pos位置查找子字符串str(或s)或字符ch的位置。
若找到，返回其首地址，否则返回 string::npos。
(6.1)(6.2)(6.3)用法:<code>find(string字符串或C风格字符串或字符，开始位置=0);</code>
&nbsp;&nbsp;&nbsp;&nbsp;(6.4)<code>size_type find(const char *s,size_type pos,size_type n) ;</code>从字符串的pos位置开始，查找s的前n个字符组成的字符串，返回方式同(1)(2).
用法:<code>find(待取的C风格字符串,查找的开始位置,取的字符数);</code></p>
<p>(7)其他搜索:与find()的重载特征都相同
&nbsp;&nbsp;&nbsp;&nbsp;(7.1)<code>rfind()</code>查找子字符(串)最后一次出现的位置.
&nbsp;&nbsp;&nbsp;&nbsp;(7.2)<code>find_first_of()</code>查找参数中任何一个字符首次出现的位置
&nbsp;&nbsp;&nbsp;&nbsp;(7.3)<code>find_last_of()</code> 与（7.2）相仿，但查找最后一个
&nbsp;&nbsp;&nbsp;&nbsp;(7.4)<code>find_first_not_of()</code>查找第一个不包含在参数中的字符
&nbsp;&nbsp;&nbsp;&nbsp;(7.5)<code>find_last_not_of()</code>与（7.4）相仿，但查找最后一个
(8)其他方法:
<code>capacity() </code>返回当前分配给字符串的内存块的大小
<code>reserve(长度)</code> 请求内存块的最小长度
<code>c_str()</code>返回对应的C风格字符串</p>
<h3 class="atx" id="注"><strong>注</strong>:</h3>
<p>模板basic_string有4个具体化，每个具体化都有一个typedef名称:</p>
<pre><code class="fenced-code-block language-cpp">typedef basic_string&lt;char&gt; string;
typedef basic_string&lt;wchar_t&gt; wstring;
typedef basic_string&lt;char16_t&gt; u16string;//C++11
typedef basic_string&lt;char32_t&gt; u32string;//C++11</code></pre>
<p>其原型如下：</p>
<pre><code class="fenced-code-block language-cpp">template&lt;class charT,class traits=char_traits&lt;charT&gt;,
class Allocator=allocator&lt;charT&gt; &gt; basic_string;</code></pre>
<p><code>charT</code>是字符类型，<code>traits</code>是其特征，<code>Allocator</code>管理内存分配(使用 new和delete)</p>
<h3 class="atx" id="stl">STL</h3>
<p>一、基本概念</p>
<p>1.&nbsp;STL包括了一组表示<strong>容器</strong>(类似数组)、<strong>迭代器</strong>(能够用来遍历容器的对象，与能够遍历数组的指针相似，<strong>是一个广义指针</strong>)、<strong>函数对象</strong>(类似于函数的对象)和<strong>算法</strong>(完成特定任务的过程)的模板。</p>
<p>2.&nbsp;<strong>分配器</strong>：各种STL容器模板都接受一个可选的模板参数，该参数指定了使用哪一个分配器对象来管理内存。(使用的是new和delete)</p>
<p>3.&nbsp;所有的STL容器提供的基本方法：</p>
<p><code>.size()</code>容器中的元素个数</p>
<p><code>.swap()</code>交换两个容器的内容</p>
<p><code>.begin()</code>返回一个指向容器第一个元素的迭代器</p>
<p><code>.end()</code>返回一个表示超过容器尾的指针</p>
<p>4.&nbsp;每一个容器都定义了一个迭代器，为一个名为<code>iterator</code>的typedef，作用域为类。声明一个迭代器：</p>
<p><code>类名::iterator 迭代器名;</code></p>
<p>其可以：解除引用<code> operator*()</code>、自增<code>operator++()</code></p>
<p>E.g. <code>vector&lt;double&gt;::iterator</code></p>
<p>5.&nbsp;<strong>超过结尾</strong>(past_the_end):指向容器最后一个元素后面的元素的迭代器</p>
<p>6.&nbsp;某些STL容器特有的方法:</p>
<p>(1)&nbsp;<code>push_back(追加的元素)</code>将元素添加到末尾，并增加长度</p>
<p>(2)&nbsp;<code>erase(开始迭代器，结束迭代器)</code>删除制定区间的元素，接受两个迭代器(包含<code>operator+()</code>方法),包括开始不包括结束。</p>
<p>(3)&nbsp;<code>insert(新元素的插入位置迭代器，被插入区间开始迭代器，被插入区间结束迭代器);</code>用于插入元素，接受3个迭代器，包括开始不包括结束。</p>
<p>e.g.<code>new_v.insert(new_v.begin(),old_v.begin(),old_v.end())；</code></p>
<p>将矢量old_v的内容插入到矢量new_v的第一个元素前面</p>
<p>二、基本算法(头文件 algorithm)</p>
<p><code>for_each(开始迭代器，结束迭代器，要应用的函数指针);</code>前两个是一个容器的区间(不包括结束)，最后是函数指针，会被应用于区间的各个元素，被指向的函数不能修改元素值。
<code>random_shuffle(开始迭代器，结束迭代器);</code>随机排列区间的元素，要求容器随机访问。
<code>sort(开始迭代器，结束迭代器)</code>
<code>sort(开始迭代器，结束迭代器,自定义排序函数)</code>
只接受区间时，使用&lt;运算符，对区间升序排序。(要有对应的<code>operator&lt;()</code>函数)
接受区间和函数指针时，函数返回值为false表示排序不正确.</p>
<p>三、<strong>迭代器</strong>:</p>
<p>1.&nbsp;C++将<code>operator++()</code>作为前缀版本，将<code>operator++(int)</code>作为后缀版本。其中的参数根本不会使用，因此无需指定名称</p>
<p>2.&nbsp;迭代器都能进行解除引用和比较</p>
<p>3.迭代器的类型：</p>
<p>(1)&nbsp;<strong>输入迭代器</strong>：来自容器的信息被称为<strong>输入</strong>，可被程序用来<strong>读取</strong>容器中的<strong>信息</strong>，但<strong>不一定</strong>让程序<strong>修改</strong>，该种算法<strong>不修改值</strong>。(只读不写)</p>
<p>基于输入迭代器的任何算法都是<strong>单通行</strong>的，可以<strong>递增</strong>，不可倒退。</p>
<p>(2)&nbsp;<strong>输出迭代器</strong>：将信息从程序传输给容器的迭代器。<strong>只能解除引用修改容器值</strong>，不能读取。(只写不读)输出迭代器是单通行的。</p>
<p>(3)&nbsp;<strong>正向迭代器</strong>：与输入迭代器和输出迭代器相似，只用<code>++</code><strong>运算符遍历容器。每次沿容器向前移动一个元素。总是按照相同的顺序遍历一系列的值。仍可以对以前的值解除引用</strong>，能够<strong>读写数据</strong>，也可只读数据。</p>
<p>(4)&nbsp;<strong>双向迭代器</strong>：包含了正向迭代器的特性，支持<code>--</code>运算符。</p>
<p>(5)&nbsp;<strong>随机访问迭代器</strong>:能够直接跳转到任意元素（随机访问），包含了双向迭代器的特性，支持随机访问。</p>
<p>随机访问迭代器操作：a、b为迭代器值，n为整数，r为随机访问迭代器的变量或引用。这些表达式只有在容器区间内（包括超尾）才合法。其操作如下：</p>
<p><code>a+n 或 n+a:指向a所指向的元素后的第n个元素;</code></p>
<p><code>a-n:指向a所指向的元素前的第n个元素;</code></p>
<p><code>r+=n、r-=n：复合运算符；</code></p>
<p><code>a[n]同*(a+n);b-a减法;a&lt;b,a&gt;b,a&lt;=b,a&gt;=b用来比较地址。</code></p>
<p>(6)每个迭代器的性能</p>
<table>
<thead>
<tr>
<th>Iterator Capability</th>
<th>Input</th>
<th>Output</th>
<th>Forward</th>
<th>Bidirectional</th>
<th>Random Access</th>
</tr>
</thead>
<tbody><tr>
<td>Fixed and repeatable order</td>
<td>N</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
</tr>
<tr>
<td>++i&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; i++</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
<td>Y</td>
</tr>
<tr>
<td>--i&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; i--</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
<td>Y</td>
</tr>
<tr>
<td>i[n]</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>i + n</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>i - n</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>i+=n</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>i-=n</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>N</td>
<td>Y</td>
</tr>
</tbody></table>
<p>4.<strong>概念</strong>、<strong>改进</strong>与<strong>模型</strong>：</p>
<p>概念是一系列的要求；改进是概念上的继承（因为其无法使用C++的类继承来描述，如将指针用作迭代器）；模型是概念的具体实现。</p>
<p>以下算法使用头文件algorithm</p>
<p>(1)&nbsp;STL <code>std::sort()</code>函数：接受指向容器（数组）的第一个元素的迭代器（指针）和指向超尾的迭代器（指针）,<strong>用于排序</strong>。</p>
<p>用法：<code>sort(首迭代器，超尾迭代器);</code></p>
<p>(2)&nbsp;STL <code>std::copy()</code>函数：从一容器<strong>复制元素</strong>到另一迭代器，前两个迭代器指出要复制的元素范围（输入迭代器），最后一个迭代器（输出迭代器）指出要将第一个元素复制到的位置（目的地）。</p>
<p>注意：目标容器要足够大。复制不同于插入，其会覆盖原有的数据。</p>
<p>用法<code>copy(开始，结束，目的地)；</code></p>
<p>四、迭代器使用 <strong>头文件：iterator</strong></p>
<p>(1)&nbsp;将信息复制到输入输出和其他迭代器</p>
<p><strong>适配器</strong>:用于将其他接口转为STL接口</p>
<p>①表示输出流的迭代器：<code>ostream_iterator</code>模板，其是一个适配器，可将其他的接口转换为STL接口用法：</p>
<p><code>ostream_iterator&lt;被发送给输出流的数据类型，输出流所使用的字符类型&gt;</code></p>
<p><code>迭代器名(输出流名称，每个数据的分隔符(字符串));</code></p>
<p>如：<code>ostream_iterator&lt;int,char&gt; cout_iter(cout,” ”);</code></p>
<p>使用<code>*cout_iterator++ =15</code>即可复制，等价于<code>cout&lt;&lt;15&lt;&lt;” ”;</code></p>
<p>可复制到输出流内使用数据，可以创建无名迭代器。</p>
<p>如：<code>copy(dict.begin(),dict.end(),ostream_iterator&lt;int,char&gt;(cout,””));</code></p>
<p><code>//ostream_iterator&lt;int,char&gt;(cout,””))也可以换为一个具体的名称。</code></p>
<p>②<code>istream_iterator</code>使<code>istream</code>输入可用作迭代器接口，拥有两个模板参数，声明方法：<code>istream_iterator&lt;读取的数据类型，输入流使用的字符类型&gt;迭代器名(输入流名)</code>，使用cin代表cin管理输入流，省略构造函数表示输入失败。可将其运用到copy()算法中，直到EOF、不匹配或其他问题为止。样例：</p>
<p><code>copy(istream_iterator&lt;int,char&gt;(cin),istream_iterator&lt;int,char&gt;(),dict.begin);</code></p>
<p>③<code>reverse_iterator</code>(反向迭代器):对反向迭代器递增操作将导致其被递减。</p>
<p>vector类有rbegin()和rend()的成员函数，rbegin()返回指向超尾元素的反向迭代器(<code>vector&lt;T&gt;::reverse_iterator</code>)，rend()返回第一个元素的反向迭代器。</p>
<p>若要反着打印容器内容，可以进行如下操作:</p>
<p><code>copy(dice.rbegin(),dice.rend(),ostream_iterator&lt;int,char&gt;(cout,””));</code></p>
<p>反向指针通过<strong>先递减再解除引用</strong>解决问题。(即<em>rp将在</em>rp的当前值之前对迭代器解除引用。)</p>
<p>④插入迭代器:添加新的元素，不会覆盖已有的数据，并会自动分配内存来容纳新的内容</p>
<p><code>back_insert_iterator</code>将容器插入到容器尾部</p>
<p><code>front_insert_iterator</code>:插入到容器的前端</p>
<p><code>insert_iterator</code>:将元素插入到其构造函数指定的位置前面</p>
<p>可以直接使用<code>copy()</code>函数。</p>
<p>限制如下：<code>back_insert_iterator</code>需要允许在尾部快速插入的容器(插入操作的时间复杂度为常数,如vector)，<code>front_insert_iterator</code>需要允许在起始位置做时间固定插入的容器类型(如queue)，<code>insert_iterator</code>没有限制。</p>
<p>这些迭代器将容器类型作为模板参数。<code>back_insert_iterator</code>的构造函数假设传递给它的类型有<code>push_back()</code>方法。声明<code>front_insert_iterator</code>大同小异。<code>insert_iterator</code>需要指出位置。他们的声明格式为：</p>
<p><code>back_insert_iterator &nbsp;&lt;容器类型&gt; 迭代器名(容器名);</code></p>
<p><code>front_insert_iterator &lt;容器类型&gt; 迭代器名(容器名);</code></p>
<p><code>insert_iterator&lt;容器类型&gt; 迭代器名(容器名,插入位置);</code></p>
