#C++的一些基础知识
 [C++语言细节的官方参考网站](http://www.cplusplus.com/reference/cctype/)  
 [Linux函数参考](http://linux.die.net/man/3/pthread_join)
[]()
- 

1. C++标准库兼容了C语言的标准库,C语言的头文件形如name.h,C++会将文件命名为cname.去掉了.h后缀且在文件面name前加了字母c.名为cname	的头文件从属于std.而.h的头文件则不然.标准库中的名字总能在命名空间中找到.
2. 要使用vector必须使用下面头文件
    ```
        #include <vector>
        using std::vector;    //如1所述,标准库的名词大都在std命名空间
    ```
3. vector能容纳绝大多数类型的对象作为其元素,但是因为引用不是对象,所以不存      在包含引用的vector.
4. sizeof是运算符,strlen为函数.sizeof可以用类型做参数,strlen只能用char*做参数,且必须是以"\0"结尾的.一般编译器在编译时便计算过	sizeof的值.strlen在运行时计算,一般用来计
5. 算字符串的长度,而且不包含末尾的'\0'.sizeof后如果是类型必须加括号,如果是变量名可以不加括号.
	对于静态数组处理:
	```
	    char *ss = "0123456789";
	    cout<<sizeof(ss)<<endl; //-->4 ss指向字符串常量的字符指针,获得指针所占空间
	    cout<<sizeof(*ss)<<endl;//-->1 *ss是字符.获得字符串第一位'0'所占空间char类型
	    cout<<strlen(ss);      //-->10 输出数组字符串长度,不包含结尾'\0'
	```
6. vector初始化时使用圆括号和花括号意义不同.(p.g 89)圆括号时可以说提供的值来构造vector对象.花括号时可以列表初始化该vector对象,	当无法列表初始化时,会是其他方法.如:
	```
	    vector<string> v1{10};      //v1有10个默认初始化的元素
	    vector<int> v2{10};         //v2有1个元素,值为10,列表初始化
	    vector<string> v3{10, "hi"};//v3有10个元素都初始化为"hi"
	
	    vector<string> v4("hi");    //粗无,不能使用字符串字面值构建vector对象
	    vector<int>    v5(10);      //v5有10个元素,每个都是0
	```
7. 复杂数组的声明(由内向外,由右向左理解)(p.g 102)
	```
	    int *ptrs[10]           //含有10个整形指针的数组
	    int &refs[10];          //错误,不存在引用的数组
	    int (*Parray)[10] = &arr; //Parray指向一个含有10个整数的数组.*Parray,Parray为指针.[10]表示Parray是一个纸箱大小为10的数组的指针
	    int (&arrRef)[10] = arr;  //arrRef引用一个含有10个整数的数组.(&arrRef)表示arrRef是个引用,它引用的对象是一个大小为10的数组.数组中元素类型是int
	    int *(&arry)[10] = ptrs; //array是一个10个int行指针的数组的引用
	```
    int *(&arry)[10] = ptrs分析:由内向外,arry是一个引用,右侧克制,arry引用的对象时一个大小为10的数组,观察左侧知数组的元素类型是指向int的指针.
8. 数组指针理解的一题目(测试理解)
    `int (*p)[4] = ia;` p指向含有4个整数的数组
    `int *ip[4];`整型指针的数组
	```
	    int array[5] = { 1, 2, 3, 4, 5 };
	    int *pArray = (int *)(&array + 1);
	    cout << "*(array + 1)  ? " << *(array + 1) << endl;
	    cout << "*(pArray - 1) ? " << *(pArray - 1) << endl;
	
	    int (*pArray2)[5] = (&array + 1);
	    cout << "*(pArray2 - 1) ? " << **(pArray2 - 1) << endl;
	```
9.  int ia = {0,1,2,3,4,5,6,7,8,9};  
	decltype(ia) ia3 = {0,1,2,3,4,5,6,7,8,9};
	//decltype(ia) 返回的类型是由10个整数构成的数组.  
10. strlen(p),strcmp(p1,p2),strcat(p1,p2),strcpy(p1,p2),参数p1,p2必须指向以非空字符作为结束的数组.,不然会有错误.
	```
		char ca[] = {'C', '+', '+' };
		cout << strlen(ca) <<endl;    //错误,ca没有以'\0'结尾
	```
11. 要使用范围for语句处理多维数组,出了最内存的循环外,其他所有循环的控制变量都应该是引用类型.
    ```
        for(auto &row :ia)
        for(auto col : row)
    ```
12. 初始化规则.C++允许使用字面值初始化常量引用.
```
    const int &r1 = 42;
    int &r2 = 42;        //错误,不能使用字面值初始化一个非常量引用 p.g 45
```	
13. 数组形参
```
    void print(const int *);
    void print(const int[]);
    void print(const int[10]);
```
三个函数等价.p.g 193

14. 在include语句中，“<>”表示在标准路径中搜索头文件，““””表示在本目录中搜索。故在上例中，可把hello1.c的“#include<my.h>”改为“#include “my.h””，当 gcc时 就不需要加上“-I”选项了。
15. std::cout 里的解析顺序是从右向左进行的.
16. [C语言解析结构的右左法则](http://www.cnblogs.com/ficow/p/5282066.html)
17. 静态成员变量的初始化.`静态成员仍然遵循public，private，protected访问准则。`,`静态成员不能在类定义里边初始化，只能在class body外初始化`.
数据类型 类名：：静态数据成员名 = 初值


		class Singleton
		{
		private:
		static Singleton* _instance;  //私有变量也能修改
		Singleton(){}
		public:
		static Singleton *getInstance()
		{
		if (nullptr == _instance)
		{
		_instance = new Singleton();
		cout << "we have create a new singleton" << endl;
		}
	
		return _instance;
		}
		};
	
		Singleton* Singleton::_instance = nullptr;  //类的静态成员变量要初始化!,也要声明返回值
		//注意：不能用参数初始化表对静态成员初始化。一般系统缺省初始为0.

18. c++中输出百分号.

		%和转义字符\一样特殊，所以输出%是用%%，而不是\%

19. c++ [在cout中的输出控制](http://www.cnblogs.com/lucyjiayou/archive/2012/01/04/2312225.html)
		
		输出16进制
		cout << hex << 98110 << endl;

20. assert的使用
	- 头文件: `assert.h`
	- 函数原型

			void assert(int expression); //参数为0则报错

	- 报错格式 `Assertion failed: expression, file filename, line line number `
	- 忽略方法: 可以使用

			#define NDEBUG //头文件中
			-DNDEBUG	   //makefile时的选项
21. `memset` 对字符串数组的取首址操作一样 

		char name[50];
		memset(name, 0, 5);
		memset(&name, 0, 5);

			
