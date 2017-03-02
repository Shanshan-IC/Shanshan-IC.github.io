---
layout: post
title: Langhong Online Test 31th Oct. 2017 
category: Interview
tag: Interview CPP
---

* content
{:toc}

Interview on 27. Oct for 朗虹, Some programming tests.

## Question 1.

假设股市每秒更新一次数据，即当前的股票价格。现在需要制作一个程序实现实时计算当前一个小时内的股票A的价格参数，即计算这一个小时内的股票价格的平均值和所有时刻的最大值最小值。例如：在11点时计算10点01秒到11点00秒的价格均值和更新全局最大最小值，在11点01秒时计算10点02秒到11点01秒的价格均值和更新全局最大最小值。

The idea is using ring buffer to update.

```cpp
class PriceParam
{
private:
	float average_f;  //一小时内的价格均值
	float maxPrice_f; //全局最大价格
	float minPrice_f; //全局最低价格
	float data[3600];
	int front;
	int rear;
	float sum_Now;//update the sum 

public:
	PriceParam() {
		average_f = 0.0;
		maxPrice_f = 0.0;
		minPrice_f = 0.0;
	}

	bool isEmpty() {
		return front == rear;
	}

	bool isFull() {
		return front == (rear + 1) % 3600;
	}

	void push(float price) {
		if (isFull()) {
			int temp = pop();
			sum_Now -= temp;
		}
		data[rear] = price;
		rear = (rear + 1) % 3600;
		sum_Now += price;
	}

	int pop() {
		int temp = data[front];
		front = (front + 1) % 3600;
		return temp;
	}

	void CalculatePriceParam(float currentPrice) {
		if (currentPrice > maxPrice_f)
			maxPrice_f = currentPrice;
		if (currentPrice < minPrice_f)
			minPrice_f = currentPrice;
		push(currentPrice);
		if (isFull())
			average_f = sum_Now / 3600;
		else
			average_f = sum_Now / ((3600-front+rear)%3600);
	}
};

int main() {
	bool systemRunning = true;
	PriceParam* param = new PriceParam();
	while (systemRunning)
	{
		float price;
		cin >> price;  //从网络获取当前的价格
	    param->CalculatePriceParam(price);//计算当前的价格参数
	}

	return 0;
}
```

## Question 2

有两个有序的数组（从小到大排列）, find the medium of two arrays
It's similiar with the [Leetcode4](https://leetcode.com/problems/median-of-two-sorted-arrays/)

```cpp
struct MyDataArray{
	int *data;
	int size;
};

int help(MyDataArray &array1, int start1, MyDataArray &array2, int start2, int k) {
	if (array1.size - start1 > array2.size - start2)
		return help(array2, start2, array1, start1, k);
	if (array1.size == start1)
		return array2.data[start2 + k - 1];
	if (k == 1)
		return min(array1.data[start1], array2.data[start2]);
	int pa = min(start1 + k / 2, array1.size);
	int pb = start2 + k - pa + start1;
	if (array1.data[pa - 1] < array2.data[pb - 1])
		return help(array1, pa, array2, start2, k - pa + start1);
	else if (array1.data[pa - 1] > array2.data[pb - 1])
		return help(array1, start1, array2, pb, k - pb + start2);
	else
		return array1.data[pa - 1];
}

// complexity is O(log(m+n))
int FindMedium(MyDataArray &array1, MyDataArray &array2) {
	int k = array1.size + array2.size;
	if (k % 2 == 1)
		return help(array1, 0, array2, 0, k / 2 + 1);
	else
		return (help(array1, 0, array2, 0, k / 2) + help(array1, 0, array2, 0, k / 2 + 1)) / 2;
}

int main() {
	MyDataArray array1, array2;
	array1.data = new int[5];
	array1.size = 5;
	for (int i = 0; i < 5; i++)
		cin >> array1.data[i];
	array2.size = 6;
	array2.data = new int[6];
	for (int i = 0; i < 6; i++)
		cin >> array2.data[i];

	int ans = FindMedium(array1, array2);
	cout << ans << endl;

	return 0;
}
```

## Question 3

定义 int64_t为8字节的数据类型

```cpp
    //要求将din的第5到第8字节赋值给result.name
    //第1个字节赋值给result.score1
    //第2个字节赋值给result.score2
    //第3个字节赋值给result.score3
    //第4个字节赋值给result.score4
struct MyDataStruct
{
    char name[4];
    unsigned char score1,score2,score3,score4;
};

MyDataStruct GetInformation(int64_t din)
{
	MyDataStruct result;
	//数值与0xFF按位与运算
	//One solution is to use the bit operation
	//result.score1 = din & 0x0FF;
	//result.score2 = (din>>8) & 0x0FF;
	//another solution is to use the pointer
	//
	result.score1 = *(char*)&din;
	result.score2 = *((char*)&din+1);
	result.score3 = *((char*)&din + 2);
	result.score4 = *((char*)&din + 3);
	for (int i = 0; i < 4; i++)
		result.name[i] = *((char*)&din + 4 + i);
	//如样例中: result.name={0xDD, 0xCC, 0xBB, 0xAA};
	//result.score1=0x44 result.score2=0x33 
	//result.score3=0x22 result.score4=0x11
	return result;
}
void main()
{
    int64_t var=0xAABBCCDD11223344;
    MyDataStruct ans;
    ans=GetInformation(var);
}
```