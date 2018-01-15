# KMP算法
## 摘要
KMP算法是一种高效的字符串匹配算法，在学数据结构的时候没有理解的特别透彻，现在重新复习，对这个算法加强了理解。
## 算法
### 复杂度
对于普通的字符串匹配，需要O(MN)的时间复杂度，但是KMP通过一个O(M)的预处理，将这个复杂度降到了O(M+N)。

### 思想
在字符串O中寻找f出现的位置，当ｉ位置不匹配时，需要将ｆ向后移动一位重新进行比较。但是我们可以发现在已经匹配的子串中的某些特点可以简化比较的次数，即通过对ｆ的预处理实现一次移动多位从而提高效率。
- **核心思想**：看ｆ中已经匹配过的长度为i的子串，如果我们找到最长的相等的前缀子串和后缀子串，我们就可以直接向后移动该前缀子串和后缀子串的长度ｋ，从而简化算法。所以需要提前得到一个next数组用来存取i长度子串的k值。
- **重点**：求next数组，i代表**子串的长度**，所以下标从１开始，next的大小是ｆ的长度加一，假设我们现在已经求得next[1]、next[2]、……next[i]，分别表示长度为1到i的字符串的前缀和后缀最大公共长度，现在要求next[i+1]，如果位置i和位置next[i]处的两个字符相同（下标从零开始），则**next[i+1]等于next[i]加1**。如果两个位置的字符不相同，我们可以将**长度为next[i]的字符串继续分割**，获得其最大公共长度next[next[i]]，然后再和位置i的字符比较。这是因为长度为next[i]前缀和后缀都可以分割成上部的构造，如果位置next[next[i]]和位置i的字符相同，则next[i+1]就等于next[next[i]]加1。如果不相等，就可以继续分割长度为next[next[i]]的字符串，**直到字符串长度为0为止**。

## JAVA代码实现
```java
public class KMP {
    public static int[] getNextArray(String P) {
        if(P == null || P.length() == 0) {
            return null;
        }
        int[] next = new int[P.length() + 1];
        next[0] = 0;
        next[1] = 0;
        for(int i = 1; i < P.length(); i++){
            int temp = next[i];
            while(next[i] > 0 && P.charAt(i) != P.charAt(temp)) {
                temp = next[temp];
            }
            if(P.charAt(i) == next[temp]) {
                temp++;
            }
            next[i+1] = temp;
        }
        return next;
    }
    public static void KMPSearch(String O, String P) {
        int[] next = getNextArray(P);
        int n = 0;
        for(int i = 0; i < O.length(); i++){
            while(n > 0 && O.charAt(i) != P.charAt(n)) {
                n = next[n];
            }
            if(O.charAt(i) == P.charAt(n)) {
                n++;
            }
            if(n == P.length()){
                System.out.println("Find the position" + (i-n));
                System.out.println(O.substring(i-n+1, i+1));
                n = next[n];
            }
        }
    }

    public static void main(String[] args) {
        String o = "gdsgadgsdhdfgasfsadfdsfgsadgdsagasdhfdsgasdfsadgs";
        String p = "fds";
        KMPSearch(o,p);
    }
}

```
## 总结
KMP是一种十分高效的字符串匹配算法，我需要继续学习。
##　参考
[KMP算法详解](http://blog.csdn.net/yutianzuijin/article/details/11954939/)


