
![[Pasted image 20230121164218.png]]

这道题确实不难，思路很容易想到但是其中的细节容易出错，最后也是看了题解才做出了（哭哭）

因为所求IP地址的位数是固定的，所以可以直接用四重循环而不用担心时间，一开始我想得复杂了，想着在每一次循环中直接判断位数超出和有效，结果逻辑混乱。按照题解中的做法在最后才整体判断和用substr函数来避免比较大小的方法确实更为简洁。

```c++
class Solution {

public:

    vector<string> restoreIpAddresses(string s) {

        vector<string> ret;

        if(s.size()>12){

            return ret;

        }

        for(int i=1;i<4;i++){

            for(int j=1;j<4;j++){

                for(int k=1;k<4;k++){

                    if((i+j+k<s.size())&&(i+j+k+3>=s.size())){

                        string a=s.substr(0,i);

                        string b=s.substr(i,j);

                        string c=s.substr(i+j,k);

                        string d=s.substr(i+j+k);

                        if ((is_valid(a))&&(is_valid(b))&&(is_valid(c))&&(is_valid(d))){

                            string tmp=a+"."+b+"."+c+"."+d;

                            ret.push_back(tmp);

                        }

                    }

                }

            }

        }

        return ret;

    }

    bool is_valid(string s){

        if((stoi(s)>255)||(stoi(s)<0)){

            return false;

        }

        if (s=="0"){

            return true;

        }

        for(int i=0;i<s.size();i++){

            if ((s[i]<'0')||(s[i]>'9')){

                return false;

            }

            if((i==0)&&(s[i]=='0')){

                return false;

            }

  

        }

        return true;

  

    }

};
```

