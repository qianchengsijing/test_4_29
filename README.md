# test_4_29
#include <stdio.h>
//栈在括号匹配中的应用
#define MaxSize 10
typedef struct{
	char data[MaxSize];
	int top;
}SqStack;
//初始化
void InitStack(SqStack &S)
{
	S.top = -1;
}
//判空
bool StackEmpty(SqStack S)
{
	if(S.top == -1)
		return true;
	else
		return false;
}
//遇到左括号入栈
bool Push(SqStack &S,char x)
{
	if(S.top == MaxSize-1)
		return false;
	S.data[++S.top] = x;
	return true;
}
//遇到右括号弹出栈顶元素
bool Pop(SqStack &S,char &x)
{
	if(S.top == -1)
		return false;
	x = S.data[S.top--];
	return true;
}
bool bracketCheck(char str[],int length){
	SqStack S;
	InitStack(S);
	for(int i=0;i<length;i++)
	{
		if(str[i] == '(' || str[i] == '[' || str[i] == '{')
			Push(S,str[i]);//扫描到左括号则入栈
		else
		{
			if(StackEmpty(S))//扫描到右括号且栈为空
				return false;
			char topElem;//定义栈顶元素
			Pop(S,topElem);//弹出栈顶元素后与右括号对比是否匹配
			if(str[i] == ')' && topElem != '(')
				return false;
			if(str[i] == ']' && topElem != '[')
				return false;
			if(str[i] == '}' && topElem != '{')
				return false;
		}
	}
	return StackEmpty(S);//最后扫描完所有元素后，栈空说明匹配成功
}
