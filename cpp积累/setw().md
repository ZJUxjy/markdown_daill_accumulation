# std::setw()
 std::setw(n)的作用是设置输出宽度为n，默认右对齐并用空格补充。
例子
```
#include <iomanip>
#include <iostream>
#include<string.h>
using namespace std;
 
int main()
{
 
	/*默认为右对齐，此时加不加std::right都可以 */
	cout << std::setw(5) << "0" << "1" << endl;
	cout << std::setw(5) << "00" << "1" << endl;
	cout << std::setw(5) << "000" << "1" << endl;
 
	
	/*用<<left或者std::left改成左对齐*/
	cout << std::left << std::setw(5) << "0" << "1" << endl;
	cout << std::left << std::setw(5) << "00" << "1" << endl;
	cout << std::left << std::setw(5) << "000" << "1" << endl;
 
	/*当要输出的字符串宽度大于setw设置的宽度时，直接输出想要输出的字符串即可*/
	cout << std::right <<std::setw(5) << "0000000" << "1" << endl;
 
	/*用其他符号填充*/
	cout << std::right <<std::setw(5) << setfill('*') << "0" << "1" << endl;
	cout << std::left << std::setw(5) << setfill('*') << "0" << "1" << endl;
 
 
	return 0;
}
```

输出结果：
 
