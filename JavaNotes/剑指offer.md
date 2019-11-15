## P3. 一维数组判断是否有重复数字

```java
package Suanfa.jianzhiOffer;
/*
@author pxu
@create 2019/10/29 14:18
问题ID：《剑指Offer》P2
问题描述：在一个长度为 n 的数组里的所有数字都在 0 到 n-1 的范围内。数组中某些数字是重复的，
但不知道有几个数字是重复的，也不知道每个数字重复几次。请找出数组中任意一个重复的数字。
解题思路：
1.归位法
要求时间复杂度 O(N)，空间复杂度 O(1)。因此不能使用排序的方法，也不能使用额外的标记数组。
对于这种数组元素在 [0, n-1] 范围内的问题，可以将值为 i 的元素调整到第 i 个位置上进行求解。
以 (2, 3, 1, 0, 2, 5) 为例，遍历到位置 4 时，该位置上的数为 2，但是第 2 个位置上已经有一个 2 的值了，
因此可以知道 2 重复.
*/
public class P1_yiweishuzuchazhao {

    public static void main(String[] args) {

        int[] numbers = {0,3,1,0,2,5,3};
        int[] dup = {0,2,3};
        System.out.println(duplicate(numbers,numbers.length,dup));
    }

    public static boolean duplicate(int nums[],int length,int [] duplication) {
        if(nums == null || length<=0)//或的关系
            return false;
        for(int i =0;i<length;i++){
            while(nums[i]!=i){
                if(nums[i] == nums[nums[i]] )
                {
                    duplication[0] = nums[i];
                    return true;
                }

                swap(i,nums[i],nums);
            }

        }
        return false;
    }
    public static void swap(int i,int j,int[] numbers){//第一次没定义参数类型使得出现大量错误
        int temp;
        temp = numbers[i];
        numbers[i] = numbers[j];
        numbers[j] = temp;
    }
}
```

## P4. 二维数组查找问题

```java
package Suanfa.jianzhiOffer;
/*
题目描述：
给定一个二维数组，其每一行从左到右递增排序，从上到下也是递增排序。
给定一个数，判断这个数是否在该二维数组中。
解题思路
要求时间复杂度 O(M + N)，空间复杂度 O(1)。其中 M 为行数，N 为 列数。
该二维数组中的一个数，小于它的数一定在其左边，大于它的数一定在其下边。
因此，从右上角开始查找，就可以根据 target 和当前元素的大小关系来缩小查找区间，
当前元素的查找区间为左下角的所有元素。
*/
public class P3_shuzuzhongCFDSZ
{

    public static void main(String[] args)
    {
        int[][] array = new int[][]{{1, 2, 8,9}, {2,4,9,12}, {4, 7, 10,13},{6,8,11,15}};
        System.out.println(Find(5,array));

    }
    public static boolean Find(int target, int[][] array)
    {
        if (array == null || array.length == 0 || array[0].length == 0)
            return false;
        int m = array.length;
        int n = array[0].length;
        int m_index = m-1;
        int n_index = 0;
        while(array[m_index][n_index]!= target)
        {
            if (target>array[m_index][n_index])
                n_index++;
            else
                m_index--;
            if( m_index == 0 && array[m_index][n_index]>target)
                return false;
            if( n_index == n-1 && array[m_index][n_index]<target)
                return false;
//            if(m_index == 0 && n_index == 0 && array[m_index][n_index]>target )
//                return false;
//            if(m_index == m-1 && n_index==n-1 && array[m_index][n_index]<target )
//                return false;
//            if(m_index == 0 && n_index==n-1 && array[m_index][n_index]!=target)
//                return false;
        }
        return true;


    }

    }
```

P5. 替换空格

```java
package Suanfa.jianzhiOffer;
/*
@author pxu
@create 2019/10/30 22:39
问题ID：《剑指Offer》P5 
问题描述：请实现一个函数，将一个字符串中的每个空格替换成“%20”。
例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。
解题思路：
*/
public class P5_replaceKG {
    public static void main(String[] args) {
        StringBuffer str = new StringBuffer("we are happy");
        System.out.println(replaceSpace(str));


    }

    public static String replaceSpace(StringBuffer str){
        if(str == null || str.length()<=0)
            return str.toString();//为什么？之后看这里的时候请注意。
        int front = str.length()-1;//循环遍历的index
        int length = str.length();
        for (int i = 0; i < length; i++) {//此处的length不可以使用str.  会导致死循环
            if (str.charAt(i) == ' ') {//先扩充str的长度
                str.append(' ');
                str.append(' ');
            }
        }
        int rear = str.length()-1;//循环插入的index
        for (; front >= 0; front--){
            if (str.charAt(front)!=' '){
                str.setCharAt(rear--,str.charAt(front));//第一次没有rear--，没有移动指针
            }
            else{
                str.setCharAt(rear--,'0');
                str.setCharAt(rear--,'2');
                str.setCharAt(rear--,'%');
            }

        }
        return str.toString();

    }
}
```

## 类似题目

