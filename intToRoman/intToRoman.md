# intToRoman


#### 题目

罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。

示例 1:

输入: 3
输出: "III"
示例 2:

输入: 4
输出: "IV"
示例 3:

输入: 9
输出: "IX"
示例 4:

输入: 58
输出: "LVIII"
解释: L = 50, V = 5, III = 3.
示例 5:

输入: 1994
输出: "MCMXCIV"
解释: M = 1000, CM = 900, XC = 90, IV = 4.



### CODE
```c++
//mycode
 class Solution {
public:
    string intToRoman(int num) {
        if(num<1||num>3999)return "";
        string str;
        int m=num/1000;
        for(int i=0;i<m;i++){
            str+="M";
        }
        num%=1000;
        if(num>=900){
            str+="CM";
            num-=900;
        }else if(num<900&&num>=500){
           int c=num/100-5;
            str+="D";
            for(int i=0;i<c;i++){
            str+="C";
            }
            num%=100;
        }else if(num>=400&&num<500){
            str+="CD";
            num-=400;
        }else{
            int c=num/100;
            for(int i=0;i<c;i++){
            str+="C";
            }
            num%=100;
        }
        if(num>=90){
            str+="XC";
            num-=90;
        }else if(num<90&&num>=50){
           int c=num/10-5;
            str+="L";
            for(int i=0;i<c;i++){
            str+="X";
            }
            num%=10;
        }else if(num>=40&&num<50){
            str+="XL";
            num-=40;
        }else{
            int c=num/10;
            for(int i=0;i<c;i++){
            str+="X";
            }
            num%=10;
        }
       if(num>=9){
            str+="IX";
        }else if(num<9&&num>=5){
           int c=num-5;
            str+="V";
            for(int i=0;i<c;i++){
            str+="I";
            }
           
        }else if(num>=4&&num<5){
            str+="IV";
          
        }else{
           
            for(int i=0;i<num;i++){
            str+="I";
            }
          
        }

        return str;
    }
};
//good code

class Solution {
public:
    string intToRoman(int num) {
        int values[]={1000,900,500,400,100,90,50,40,10,9,5,4,1};
        string reps[]={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        
        string res;
        for(int i=0; i<13; i++){
            while(num>=values[i]){
                num -= values[i];
                res += reps[i];
            }
        }
        return res;
    }
};
```

