## PART ONE  数组遍历（双指针）

### p1.有序数组找index

~~~java
package Suanfa.LeetCode.Double_zhizheng;
/*
@author pxu
@create 2019/10/31 21:55
问题ID：LeetCode
问题描述：给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。
函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。
解题思路：使用双指针，一个指针指向值较小的元素，一个指针指向值较大的元素。
指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。
如果两个指针指向元素的和 sum == target，那么得到要求的结果；
如果 sum > target，移动较大的元素，使 sum 变小一些；
如果 sum < target，移动较小的元素，使 sum 变大一些。

cYc代码
public int[] twoSum(int[] numbers, int target) {
    if (numbers == null) return null;
    int i = 0, j = numbers.length - 1;
    while (i < j) {
        int sum = numbers[i] + numbers[j];
        if (sum == target) {
            return new int[]{i + 1, j + 1};
        } else if (sum < target) {
            i++;
        } else {
            j--;
        }
    }
    return null;
}
*/
public class p1_SortedArray {
    public static void main(String[] args) {
        int[] numbers = {2,7,11,15,17,18,19};
        int[] out = twoSum(numbers,19);
        for (int i = 0; i < out.length; i++) {
            System.out.println(out[i]);
        }
    }
    public static int[] twoSum(int[] numbers, int target) {
        if (numbers == null) return null;//自己写的时候未加上
        int front = 0;
        int rear = numbers.length- 1;//数组直接xxxx.length

        while((numbers[front] + numbers[rear]) != target && front<rear){//循环可以就是while(front<rear)
            if((numbers[front] + numbers[rear]) < target){
                front++;
            }
            if((numbers[front] + numbers[rear]) > target){
                rear--;
            }
        }
        int[] answer = {front+1,rear+1};
        return answer;
        //可以return一个匿名对象，return new int[]{i + 1, j + 1};

    }
}
~~~



### p2.找平方和

```java
package Suanfa.LeetCode.Double_zhizheng;


/*
@author pxu
@create 2019/11/1 20:05
问题ID：LeetCode
问题描述：给定一个非负整数 c ，你要判断是否存在两个整数 a 和 b，使得 a2 + b2 = c。
解题思路：双指针，logn的时间复杂度。
*/
/*
总结：没有看清题目，2和0的测试用例没有过。
*/
public class P2_pingfanghe {
    public static void main(String[] args) {
        System.out.println(judgeSquareSum(2));

    }
    public static boolean judgeSquareSum(int c) {
        if(c==0){
            return false;
        }
        int front = 0;
        int rear = (int)Math.sqrt(c)+1;
        //第一次写的时候开方都不会写,后来明白了sqtr为math的静态方法，直接通过类名调用即可
        //而且还不会写强制转换。int rear = (int)Math.sqrt(c);
        while(front < rear)
            if((front*front+rear*rear) == c){
                return true;
            }
            else if((front*front+rear*rear) > c){
                rear--;
            }
            else{
                front++;//前指针后移
            }

        return false;
    }
}
```

### p3.互换元音字母

```java
package Suanfa.LeetCode.Double_zhizheng;
/*
@author pxu
@create 2019/11/1 20:38
问题ID：LeetCode
问题描述：互换原音字符
解题思路：
使用hash快速判断是否有元音字母
*/
/*
cYc答案参考：
和我代码想法一样，只是他使用的是hash表
private final static HashSet<Character> vowels = new HashSet<>(
        Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));

public String reverseVowels(String s) {
    if (s == null) return null;
    int i = 0, j = s.length() - 1;
    char[] result = new char[s.length()];
    while (i <= j) {
        char ci = s.charAt(i);
        char cj = s.charAt(j);
        if (!vowels.contains(ci)) {
            result[i++] = ci;
        } else if (!vowels.contains(cj)) {
            result[j--] = cj;
        } else {
            result[i++] = cj;
            result[j--] = ci;
        }
    }
    return new String(result);
}
*/
public class P3_reversezimu {
    public static void main(String[] args) {
        String str = "aoeiuAOEIU";
        System.out.println(reverseVowels(" "));
    }
    public static String reverseVowels(String s) {
        if(s == null || s.length()<=0)
            return null;
        int front = 0;
        int rear = s.length()-1;//数组长度的时候直接xxx.length;
        char[] ch = new char[rear+1];//建立一个数组，后用这个数组返回字符串的值

        while( front <= rear ){
            //!!!!!把次数改为<=便通过了测试用例，之前输出了/u0000是因为哦0<0不满足，导致ch数组使用了默认值！！
            //!!!!!所以双指针遍历数组的时候一定要考虑等于的情况！！！！
            char ch_front = s.charAt(front);
            char ch_rear = s.charAt(rear);

            if(!isExist(s.charAt(front))){
                //char ch_front = s.charAt(front);//ch[front++] = s.charAt(front) 没有这句话,会把你期待的后一个字母赋值
                ch[front++] = ch_front;

            }
            if(!isExist(s.charAt(rear))){
                ch[rear--] = ch_rear;
            }
            if(isExist(ch_front) && isExist(ch_rear) ){//!!!!因为上面对front的操作使得后面第三次判断时候已经改变了
                ch[front++] = ch_rear;
                ch[rear--] = ch_front;

            }
        }
        return new String(ch);
    }
    public static boolean isExist (char ch){
        String str = "aoeiuAOEIU";
        if(str.indexOf(ch)!=-1)
            return true;
        else
            return false;

    }
}
```

### p4.删除字符串成为回文字符串

```java
package Suanfa.LeetCode.Double_zhizheng;
/*
@author pxu
@create 2019/11/4 18:45
问题ID： LeetCode  
问题描述：给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串
解题思路：所谓的回文字符串，是指具有左右对称特点的字符串，例如 "abcba" 就是一个回文字符串。
使用双指针可以很容易判断一个字符串是否是回文字符串：令一个指针从左到右遍历，
一个指针从右到左遍历，这两个指针同时移动一个位置，每次都判断两个指针指向的字符是否相同，
如果都相同，字符串才是具有左右对称性质的回文字符串。


*/
public class P4_huiwenzifuchuan {
    public static void main(String[] args) {
        System.out.println(validPalindrome("abcbad"));

    }
    public  static boolean validPalindrome(String s) {
        if(s==null || s.length()<=0)
            return false;
        int front  = 0;
        int rear = s.length()-1;
        for(;front < rear;front++,rear--){//后面两个是逗号隔开
            if (s.charAt(front)!=s.charAt(rear)){
                return Ispalindrome(s,front+1,rear) || Ispalindrome(s,front,rear-1);
            }
        }
        return true;

    }
    public static boolean Ispalindrome (String s, int front, int rear){
        for(;front < rear;front++,rear--){//后面两个是逗号隔开
            if (s.charAt(front)!=s.charAt(rear)){
                return false;
            }
        }
        return true;
    }



}
```

### p5.合并有序数组

```java
package Suanfa.LeetCode.Double_zhizheng;
/*
@author pxu
@create 2019/11/4 19:28
问题ID： LeetCode  
问题描述：给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。
说明:
初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
解题思路：
*/
public class P5_Merge_Sorted_Array {
    public static void main(String[] args) {
        int[] nums1 = {0};
        int[] nums2 = {1};
        merge(nums1,0,nums2,1);
        for (int i = 0; i < nums1.length; i++) {
            System.out.println(nums1[i]);
        }


    }

    public static void merge(int[] nums1, int m, int[] nums2, int n) {//num1是长数组，m,n知道了
        int index1 = m-1;
        int index2 = n-1;
        int index3 = m+n-1;
        while (index1 >= 0 || index2 >=0 ){//一中数组中值大
            if(index1 < 0){//说明有一个已经遍历合并完了，然后直接插入另一组就可以
                nums1[index3--] = nums2[index2--];
            }
            else if(index2 < 0){//说明有一个已经遍历合并完了，然后直接插入另一组就可以
                nums1[index3--] = nums1[index1--];
            }
            else if(nums1[index1] > nums2[index2]){
                    nums1[index3--] = nums1[index1--];
                }
             else{//二中数组中值大，等于号
                    nums1[index3--] = nums2[index2--];
                }
                //在上面的情况下，就是上一句的--会导致此次判断空指针异常
                // 就会产生空指针异常，因为此时index2已经变为-1了。
//                if(nums1[index1] == nums2[index2]){//二中数组一样大
//                    nums1[index3--] = nums1[index1];
//                    nums1[index3--] = nums2[index2];
//                   index1--;
//                  index2--;
//                }

            }



        }

}
```

### p6.