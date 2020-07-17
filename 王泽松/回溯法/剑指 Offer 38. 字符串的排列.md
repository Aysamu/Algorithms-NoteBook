# 剑指 Offer 38. 字符串的排列

类似47回溯法，数组换成字符串



### 完整代码：

```c++
class Solution {
public:
    vector<string> res;
    string path;
    void backtrack(string s,string path,vector<int>&already){
        vector<int> Remains;
        if(path.size()>s.size()) return;
        if(s.size()==path.size()){
            res.push_back(path);
            return;
        }
        for(int i=0;i<s.size();i++){
            int flag=1;
            for(int j=0;j<already.size();j++){
                if(already[j]==i){
                    flag=0;
                    break;
                }
            }
            if(flag==1){
                Remains.push_back(i);        
            }
        }
        for(int i=0;i<Remains.size();i++){
            if(i>0&&s[Remains[i]]==s[Remains[i-1]])
                continue;
            path.push_back(s[Remains[i]]);
            already.push_back(Remains[i]);
            backtrack(s,path,already);
            path.pop_back();
            already.pop_back(); 
        }
    }
    vector<string> permutation(string s) {
        sort(s.begin(),s.end());
        vector<int> already;
        backtrack(s,path,already);
        return res;
    }
};
```

