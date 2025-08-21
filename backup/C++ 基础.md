<h1 class="atx" id="基本内容">基本内容</h1>
<p>一、类型的范围</p>
<p>位于头文件<code>climits</code>或者<code>limits.h</code>中,都是一些宏定义</p>
<table>
<thead>
<tr>
<th>宏</th>
<th>意义</th>
</tr>
</thead>
<tbody><tr>
<td>INT_MAX</td>
<td>int的最大值2^{31}-1</td>
</tr>
<tr>
<td>INT_MIN</td>
<td>int的最小值-2^{31}</td>
</tr>
<tr>
<td>UINT_MAX</td>
<td>unsigned int 的最大值 2^{32}-1</td>
</tr>
<tr>
<td>LONG_MAX</td>
<td>long的最大值2^{31}-1</td>
</tr>
<tr>
<td>LONG_MIN</td>
<td>long的最小值-2^{31}</td>
</tr>
<tr>
<td>ULONG_MAX</td>
<td>unsigned long 的最大值 2^{32}-1</td>
</tr>
<tr>
<td>LLONG_MAX</td>
<td>long long的最大值2^{63}-1</td>
</tr>
<tr>
<td>LLONG_MIN</td>
<td>long long的最小值-2^{63}</td>
</tr>
<tr>
<td>ULLONG_MAX</td>
<td>unsigned long long最大值2^{64}-1</td>
</tr>
</tbody></table>
<p>二、C++11初始化方式：将大括号初始化器用于单值变量：类型名 变量名{表达式};
大括号中可以不包含任何信息，变量会初始化为0
类型名 变量{}; 或 类型名 变量={}; 其中变量的值为0.</p>
<p>三、整型字面量：
①C++整型的三种表示：十进制、八进制、十六进制
如果第一位为1<del>9，基数为10；如果第一位为0，第二位为1</del>7，基数为8；如果前两位为0x或0X，基数为16.（基数为R表示R进制数）
▲▲计算机中的数据都以二进制存储。
②cout的控制符hex表示输出16进制整数，oct表示输出8进制整数，dec表示输出10进制整数。默认为10进制整数。
③C++将整型常量存储为int类型
④其他类型常量的表示：
前后缀 &nbsp;&nbsp;&nbsp;&nbsp;表示的类型 &nbsp;&nbsp;&nbsp;&nbsp;前后缀 &nbsp;&nbsp;&nbsp;&nbsp;表示的类型
l或L后缀 &nbsp;&nbsp;&nbsp;&nbsp; long &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; u或U后缀 &nbsp;&nbsp;&nbsp;&nbsp;unsigned int
ul后缀 （不区分大小写与顺序） &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;unsigned long
ll\LL后缀 &nbsp;&nbsp;&nbsp;&nbsp; long long &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ull\Ull\uLL\ULL后缀 unsigned long long</p>
<p>·char 只有8位，常用于处理字符
▲cout将char类型数据打印为字符，int类型打印为整数。</p>
<p>四、指针
·概念：存储地址的变量或常量，&amp;为取地址符，用法： &amp;变量名
·声明：指向的类型* 指针名=地址; 或 指向的类型* 指针名;
·解除引用：取得指针所指向的值，用法 <em>地址 其效果相当于使用原变量。
·空指针：值为0的指针，标准库中有符号常量NULL来表示（C++11用关键字nullptr表示）
·显示地址时，cout以十六进制表示法显示。提醒：int <em>m强调</em>m为int变量，int</em> m强调m为int<em>变量。（以后用int*表示指向int的指针）int</em> p1,p2;会创建一个指针和一个变量，指针变量的长度一致。
警告：在解除引用指针前，要先初始化指针！！！</p>
<p>·▲▲动态分配内存
①．方法： 指针=new 要分配的类型;
new运算符会根据要分配的类型寻找内存，并把内存地址返回给指针。（在老的实现里，内存不足会返回空指针，新的实现可能引发异常）
释放内存： delete 指针;
注意：一定要把new和delete配对使用！！！！否者会发生内存泄露。delete释放指针指向的内存，不删除指针。不能尝试释放已经释放的内存块，这是未定义行为。
内存泄露：指因内存管理不当导致内存并未回收且无法被利用。
只能用delete来释放new分配的内存，对于空指针运用delete是安全的。
②．动态数组
（i）在编译时给数组分配内存叫静态联编（static binding）
（ii）在程序运行时选择数组的长度，叫动态联编（dynamic binding）,创建的数组叫动态数组
（iii）创建方法： 指针=new 要分配的类型[元素类型];
返回首元素的地址
释放： delete[] 指针;
注意：new[]与delete[]配对使用！！！！
可以把指针当作数组名，如*arr等价于arr[0]。依此类推。
C与C++的数组与指针基本等价，其内部使用指针访问数组</p>
<p>·指针、数组、指针算术
将指针变量加一后，增加的量相当于它指向的类型的字节数。如_Type<em>的变量加一，指向地址向后偏移sizeof(_Type)。此处的_Type表示任意类型。
C和C++将数组名解释为地址。数组名的地址为数组首元素的地址。
▲如果a是数组,N是整数，则 *(a+N)等价于a[N],所以</em>a等价于a[0]</p>
<p>▲对数组名使用sizeof得到数组的大小，而对指针使用sizeof则为指针的大小，此时数组名不被视为地址。</p>
<p>▲▲易错点：对数组名取地址时，数组名不会解释为地址，而是得到整个数组的地址，如下：
short tell[10];//tell和&amp;tell的指向地址一致。
此时tell（或说&amp;tell[0]）是两字节内存块的地址，对其加一后指针向后偏移两字节，而&amp;tell是一块20个字节的内存块，在加一后该指针向后偏移20字节。即tell是short&amp;。而&amp;tell是short(*)[10]。可以这样声明：short (<em>pas)[10]=&amp;tell;省略括号pas会先与[10]结合，导致pas是一个指针数组。（可以理解为</em>pas是一个数组，有括号先算括号）
指针算术还可以获得两个指针的差，获得一个整数，是中间间隔的元素个数。</p>
<p>·当给cout提供一个字符指针时，cout会从所给地址上的字符开始打印，直到遇到空字符。
字符数组和字符串常量都是一个地址，指向第一个字符。
·strcpy(目标,源字符串)复制字符串。
·new[]的括号中可以使用变量
·指向结构变量和对象的指针、使用new创建动态结构
箭头成员运算符：访问指针里的对象的成员，用法：
指针-&gt;成员 等价于 *(指针).成员  </p>
<p>·存储与堆栈
（i）自动存储：在函数内部定义的常规变量使用自动存储空间，被称为自动变量。他们在所属的函数被调用时自动产生，在函数结束时消失。
（ii）静态存储：在整个程序执行的期间都存在的存储方式，创建静态变量的方式：在函数外面定义它；在函数内部使用关键字static。
（iii）动态存储：new和delete管理了内存池，叫自由存储空间(FREE STORE)或堆(HEAP)，与静态变量和其他变量分开。
·类型结合：创建指针数组Type_name* ptr_arr[LENGTH]</p>
<p>五、输入输出的注意事项</p>
<ol>
<li><p>cout.setf(ios_base::fixed,ios_base_floatfield);防止程序把较大的值切换为E表示法。
通常cout会删除小数结尾的0.</p>
</li>
<li><table>
<thead>
<tr>
<th>方法</th>
<th>解释</th>
</tr>
</thead>
<tbody><tr>
<td>std::cin&gt;&gt;字符数组;</td>
<td>使用空白来确定字符串的结束位置，一次只读取一个单词。多余的在输入队列中，然后被逐一读取</td>
</tr>
<tr>
<td>cin.getline(字符数组名,字符数（字符数组长度）)</td>
<td>读取一行输入，直到到达换行符。丢弃换行符，用空值字符替代。在读取指定数目字符或遇到换行符时停止读取。如果输入字符数较多，余下的字符留在输入队列中，getline()设置失效位。</td>
</tr>
<tr>
<td>cin.get(字符数组名,字符数（字符数组长度）)</td>
<td>读取一行输入，直到到达换行符。将换行符留在输入队列中。读取空行时设置失效位(failbit)</td>
</tr>
</tbody></table>
<p>cin.get()和cin.getline()都返回cin对象的引用，便可再次调用其他方法。</p>
</li>
<li><p>混合输入面向行的数字和字符串：在输入数字后，换行符被保留，需要自行丢弃。</p>
</li>
<li><p>常规的cin输入返回cin对象的引用。</p>
</li>
</ol>
<p>六、C风格字符串·C风格字符串的操作：头文件cstring中的函数，用法如下：
strcpy(目标,源字符串)复制字符串，
strcat(目标,源字符串)附加一个字符串到另一个字符串末尾。
strncat()、strncpy()前两个参数，第三个参数还要指出最大复制多少字符，更安全</p>
