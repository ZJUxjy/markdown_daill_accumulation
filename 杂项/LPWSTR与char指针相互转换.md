## 1.LPWSTR转char*

直接用（char*）强制转换虽然不报错，但是数据会出错，使用以下代码可以完成LPWSTR对char*的无损转换 

```cpp
/******************************************************************************************
Function:        ConvertLPWSTRToLPSTR
Description:     LPWSTR转char*
Input:           lpwszStrIn:待转化的LPWSTR类型
Return:          转化后的char*类型
*******************************************************************************************/
char* ConvertLPWSTRToLPSTR(LPWSTR lpwszStrIn)
{
	LPSTR pszOut = NULL;
	try
	{
		if (lpwszStrIn != NULL)
		{
			int nInputStrLen = wcslen(lpwszStrIn);
 
			// Double NULL Termination  
			int nOutputStrLen = WideCharToMultiByte(CP_ACP, 0, lpwszStrIn, nInputStrLen, NULL, 0, 0, 0) + 2;
			pszOut = new char[nOutputStrLen];
 
			if (pszOut)
			{
				memset(pszOut, 0x00, nOutputStrLen);
				WideCharToMultiByte(CP_ACP, 0, lpwszStrIn, nInputStrLen, pszOut, nOutputStrLen, 0, 0);
			}
		}
	}
	catch (std::exception e)
	{
	}
	
	return pszOut;
}
```

## 2.char* 转换成 LPCTSTR

```cpp
char ch[1024] = "wo shi ni baba";
int num = MultiByteToWideChar(0,0,ch,-1,NULL,0);
wchar_t *wide = new wchar_t[num];
MultiByteToWideChar(0,0,ch,-1,wide,num);
```
num 获得长字节所需的空间

MultiByteToWideChar()表示将s中的字符传递到ps指向的内存中。-1表示传输至s中的'\0'处，num表示传递的字节个数。

3.LPWSTR转char*
```cpp
wchar_t widestr[1024] = L"wo shi ni yeye";
int num = WideCharToMultiByte(CP_OEMCP,NULL,widestr,-1,NULL,0,NULL,FALSE);
char *pchar = new char[num];
WideCharToMultiByte (CP_OEMCP,NULL,widestr,-1,pchar,num,NULL,FALSE);
```

