---
title: BFS的一般写法
date: 2017-09-10 22:06:58
tags: 
	- leetcode
	- BFS
categories: 面试题
---
* 因为我自己对BFS一直不是很6，帮柳华做笔试题的时候很简单的一个bfs都没有写对，现在总结一下。
	* BFS一般用队列来实现，现在以二叉树的层次遍历为例，这是一个典型的BFS。
	* 队列的写法：	
	
	```
	class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root==NULL){
            return result;
        }
        queue<TreeNode*> que;
        que.push(root);
        while(!que.empty()){
            int len=que.size();
            vector<int> temp;
            //遍历每一层的节点
            for(int i=0;i<len;i++){
                TreeNode* node=que.front();
                que.pop();
                temp.push_back(node->val);
                if(node->left){
                    que.push(node->left);
                }
                if(node->right){
                    que.push(node->right);
                }
            }
            result.push_back(temp);
        }
        return result;
    }
};
	```
	* 在编程之美上还有没有用到stl的队列，用vector去模拟的队列，这里代码也放上。

	```
	class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(root==NULL){
            return result;
        }
        vector<TreeNode*> vec;
        vec.push_back(root);
        int cur=0,last;
        //cur表示当前遍历的节点，last表示下一层的节点
        while(cur<vec.size()){
            int last=vec.size();
            vector<int> temp;
            while(cur<last){
                temp.push_back(vec[cur]->val);
                if(vec[cur]->left){
                    vec.push_back(vec[cur]->left);
                }
                if(vec[cur]->right){
                    vec.push_back(vec[cur]->right);
                }
                cur++;
            }
            result.push_back(temp);
        }
        return result;
    }
    };
	```