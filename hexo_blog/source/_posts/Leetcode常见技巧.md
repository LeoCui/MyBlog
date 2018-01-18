---
title: Leetcode常用技巧
date: 2016-11-03 18:22:42
tags:  
  - leetcode
  - stl
categories: c/c++
---
* return NULL和return 一个空的数组不是一回事
* unordered_set 和unordered_map和map,set的区别在于前者内部实现是hash，后者是红黑树
* 常见STL：
	* string: push\_back()，pop\_back()，+，length()，empty()，s.append(n,c);
	* vector: push\_back()，pop\_back()，size()，empty()，
		* vector<int> vector1;
		* vector<int> vector1(n);//包含n个默认初始化的值
		* vector<int> vector1(n,val); //包含n个数，默认值val
		* vector<int> vector1(vector2);
		* vector<int> vector1=vector2;
		* vector<int> vector1{1,2,3,4,5};
		* vector<int> vector1={1,2,3,4,5};
	* queue: pop，front，size()，empty()，
* 经常需要用到匿名对象：比如
	* vector\<vector\<bool\>\> vec(m,vector<bool>(n,false));
	* vector.push_back(Test(1,2));Test是一个类
* earse的删除操作:

```
for(iter=vector.begin();iter!=vector.end();){
	if(*iter==val){
		iter=iter.erase();
		//erase返回被删除元素后一个或者vector.end()
	}
	else{
		iter++;
	}
}
```

* erase的sort()

```
	sort(vector.begin(),vertor.end(),cmp);
	bool cmp(type a,type b){
		
	} //cmp函数的意义：如果返回true,就保持a,b这样的顺序
```
* 在处理一些边界条件不好处理时，比如处理矩阵时要看四周，这时对于边界情况就不好处理，常见的方法是在周围加一圈，但是现在有更好的办法。   
	* 在边界时不成立： （j不在边界）&&（）----在边界为0，后面不用算
	* 在边界时成立：（j在边界）||（）---在边界时直接为1
* 常用的reverse(x.begin(),x.end())在库algorithm中
* INT_MIN,INT_MAX
* 二分法的时候：常用mid=left+(right-left)/2,我之前一直以为和mid=(left+right)/2一样。今天才发现不是这样的：   

         
```
left=1;
right=INT_MAX;
while(left<=right){
	mid=(left+right)/2;  //错误，整数溢出了，mid算成负数了
	mid=left+(right-left)/2;  //正确
}
```
* 子串：必须连续 								                  
  子序列：不必连续