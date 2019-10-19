# 21、leetcode125. 验证回文串
解法一：
--  
思路：
--
    双指针，一个指针从头遍历，一个指针从尾部遍历。依次判断两个指针的字符是否相等，同时要跳过非法字符。当两个指针相遇的时候就意味着这个字符串是回文串了。  
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/18 13:59
 * @descriptor  125. 验证回文串
 */
public class IsPalindrome_125 {
    public static boolean isPalindrome(String s) {
        s = s.toLowerCase();//转为小写
        int i = 0,j = s.length() - 1;
        while(i < j){
            while(!isPar(s.charAt(i))){//跳过非法字符
                i++;
                if(i == s.length()) //匹配 "   " 这样的空白字符串防止越界
                    return true;
            }
           while(!isPar(s.charAt(j)))
               j--;
           if(s.charAt(i) != s.charAt(j)){
               return false;
           }
           i++;
           j--;
        }
        return true;
    }
    public static boolean isPar(char c){
        if((c >= '0' && c <= '9') || (c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z'))
            return true;
        else
            return false;
    }
    public static void main(String[] args) {
       // String s = "A man, a plan, a canal: Panama";
       //amanaP :lanac a ,nalp a ,nam A
        String s = "0P";
        System.out.println(isPalindrome(s));
    }
}
</pre>
解法二：
--  
思路：
--
    把 '0' 到 '9' 映射到 1 到 10，'a' 到 'z' 映射到 11 到 36 ，'A' 到 'Z' 也映射到 11 到 36 。然后把所有数字和字母用一个 char 数组存起来，没存的字符就默认映射到 0 了。这样只需要判断字符串中每个字母映射过去的数字是否相等，如果是 0 就意味着它是非法字符。    
代码： 
--
<pre>
**
 * @author lihe
 * @date 2019/10/18 13:59
 * @descriptor  125. 验证回文串
 */
public class IsPalindrome_1251 {
    private static char[] c = new char[256];
    static{
        for (int i = 0; i < 10; i++) {// 映射 '0' 到 '9'
            c[i+48] = (char)(i+1);
        }
        for (int i = 0; i < 26;i++) { // 映射 'a' 到 'z' 和 映射 'A' 到 'Z'
            c[i+'a'] = c[i + 'A'] = (char)(i+11);
        }
    }
    public static boolean isPalindrome(String s) {
        char[] chars = s.toCharArray();
        int i = 0,j = s.length()-1;
        while(i < j){
            char c1 = c[chars[i]];
            char c2 = c[chars[j]];
            if(c1 != 0 && c2 != 0){
                if(c1 != c2){
                   return false;
                }
                i++;
                j--;
            }else{
                if(c1 == 0){
                    i++;
                }if(c2 == 0)
                    j--;
            }
        }
            return true;
    }
    public static void main(String[] args) {
       // String s = "A man, a plan, a canal: Panama";
      //amanaP :lanac a ,nalp a ,nam A
        String s = "0P";
        System.out.println(isPalindrome(s));
    }
}
</pre>
