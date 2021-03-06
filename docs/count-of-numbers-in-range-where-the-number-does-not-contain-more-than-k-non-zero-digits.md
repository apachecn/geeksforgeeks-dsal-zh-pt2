# 在数字不超过 K 个非零数字的范围内的数字计数

> 原文:[https://www . geesforgeks . org/范围内数字计数-其中数字不包含大于 k 的非零数字/](https://www.geeksforgeeks.org/count-of-numbers-in-range-where-the-number-does-not-contain-more-than-k-non-zero-digits/)

给定一个由两个正整数 L 和 R 以及一个正整数 K 表示的范围，求该范围内数字不超过 K 个非零数字的个数。
**例:**

```
Input : L = 1, R = 1000, K = 3
Output : 1000
Explanation : All the numbers from 1 to 1000 
are 3 digit numbers which obviously cannot 
contain more than 3 non zero digits.

Input : L = 9995, R = 10005
Output : 6
Explanation : Required numbers are 
10000, 10001, 10002, 10003, 10004 and 10005
```

先决条件:[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)
解决这类问题可以有两种方法，一种是组合解法，另一种是基于动态规划的解法。下面是使用数字动态编程方法解决这个问题的详细方法。
**动态规划解法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]范围内，我们可以通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，很容易地得出在[L，R]范围内的答案。现在，我们需要定义 DP 状态。
**差压状态** :

*   既然我们可以把我们的数字看作一个数字序列，那么一个状态就是我们当前所处的 ***位置*** 。如果我们处理的是 10 <sup>到 18</sup> 的数字，这个位置可以有 0 到 18 的值。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第二个状态是 ***计数*** ，它定义了非零数字的数量，我们已经放置在我们试图构建的数字中。
*   另一个状态是布尔变量**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数**

**在最后一次递归调用中，当我们在最后一个位置时，如果非零数字的计数小于或等于 K，则返回 1，否则返回 0。
以下是上述办法的实施情况。** 

## **C++**

```
// CPP Program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits

#include <bits/stdc++.h>
using namespace std;

const int M = 20;

// states - position, count, tight
int dp[M][M][2];

// K is the number of non zero digits
int K;

// This function returns the count of
// required numbers from 0 to num
int countInRangeUtil(int pos, int cnt, int tight,
                     vector<int> num)
{
    // Last position
    if (pos == num.size()) {
        // If count of non zero digits
        // is less than or equal to K
        if (cnt <= K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight] != -1)
        return dp[pos][cnt][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int dig = 0; dig <= limit; dig++) {
        int currCnt = cnt;

        // If the current digit is nonzero
        // increment currCnt
        if (dig != 0)
            currCnt++;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call
        ans += countInRangeUtil(pos + 1, currCnt,
                                currTight, num);
    }
    return dp[pos][cnt][tight] = ans;
}

// This function converts a number into its
// digit vector and uses above function to compute
// the answer
int countInRange(int x)
{
    vector<int> num;
    while (x) {
        num.push_back(x % 10);
        x /= 10;
    }
    reverse(num.begin(), num.end());

    // Initialize dp
    memset(dp, -1, sizeof(dp));
    return countInRangeUtil(0, 0, 0, num);
}

// Driver Code to test above functions
int main()
{
    int L = 1, R = 1000;
    K = 3;
    cout << countInRange(R) - countInRange(L - 1) << endl;

    L = 9995, R = 10005, K = 2;
    cout << countInRange(R) - countInRange(L - 1) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits
import java.util.*;
class Solution
{
static final int M = 20;

// states - position, count, tight
static int dp[][][]= new int[M][M][2];

// K is the number of non zero digits
static int K;
static Vector<Integer> num;

// This function returns the count of
// required numbers from 0 to num
static int countInRangeUtil(int pos, int cnt, int tight )
{
    // Last position
    if (pos == num.size()) {
        // If count of non zero digits
        // is less than or equal to K
        if (cnt <= K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight] != -1)
        return dp[pos][cnt][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight!=0 ? 9 : num.get(pos));

    for (int dig = 0; dig <= limit; dig++) {
        int currCnt = cnt;

        // If the current digit is nonzero
        // increment currCnt
        if (dig != 0)
            currCnt++;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num.get(pos))
            currTight = 1;

        // Next recursive call
        ans += countInRangeUtil(pos + 1, currCnt, currTight);
    }
    return dp[pos][cnt][tight] = ans;
}

// This function converts a number into its
// digit vector and uses above function to compute
// the answer
static int countInRange(int x)
{
    num= new Vector<Integer>();
    while (x!=0) {
        num.add(x % 10);
        x /= 10;
    }
    Collections.reverse(num);

    // Initialize dp
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            for(int k=0;k<2;k++)
            dp[i][j][k]=-1;
    return countInRangeUtil(0, 0, 0);
}

// Driver Code to test above functions
public static void main(String args[])
{
    int L = 1, R = 1000;
    K = 3;
    System.out.println( countInRange(R) - countInRange(L - 1) );

    L = 9995; R = 10005; K = 2;
    System.out.println(  countInRange(R) - countInRange(L - 1) );
}
}
//contributed by Arnab Kundu
```

## **蟒蛇 3**

```
# Python Program to find the count of
# numbers in a range where the number
# does not contain more than K non
# zero digits

# This function returns the count of
# required numbers from 0 to num
def countInRangeUtil(pos, cnt, tight, num):

    # Last position
    if pos == len(num):

        # If count of non zero digits
        # is less than or equal to K
        if cnt <= K:
            return 1
        return 0

    # If this result is already computed
    # simply return it
    if dp[pos][cnt][tight] != -1:
        return dp[pos][cnt][tight]

    ans = 0

    # Maximum limit upto which we can place
    # digit. If tight is 1, means number has
    # already become smaller so we can place
    # any digit, otherwise num[pos]
    limit = 9 if tight else num[pos]

    for dig in range(limit + 1):
        currCnt = cnt

        # If the current digit is nonzero
        # increment currCnt
        if dig != 0:
            currCnt += 1

        currTight = tight

        # At this position, number becomes
        # smaller
        if dig < num[pos]:
            currTight = 1

        # Next recursive call
        ans += countInRangeUtil(pos + 1, currCnt, currTight, num)

    dp[pos][cnt][tight] = ans
    return dp[pos][cnt][tight]

# This function converts a number into its
# digit vector and uses above function to compute
# the answer
def countInRange(x):
    global dp, K, M

    num = []
    while x:
        num.append(x % 10)
        x //= 10

    num.reverse()

    # Initialize dp
    dp = [[[-1, -1] for i in range(M)] for j in range(M)]
    return countInRangeUtil(0, 0, 0, num)

# Driver Code
if __name__ == "__main__":

    # states - position, count, tight
    dp = []
    M = 20

    # K is the number of non zero digits
    K = 0

    L = 1
    R = 1000
    K = 3
    print(countInRange(R) - countInRange(L - 1))

    L = 9995
    R = 10005
    K = 2
    print(countInRange(R) - countInRange(L - 1))

# This code is contributed by
# sanjeev2552
```

## **C#**

```
// C# Program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits
using System;
using System.Collections.Generic;

class GFG
{

static int M = 20;

// states - position, count, tight
static int [,,]dp = new int[M, M, 2];

// K is the number of non zero digits
static int K;
static List<int> num;

// This function returns the count of
// required numbers from 0 to num
static int countInRangeUtil(int pos,
                int cnt, int tight )
{
    // Last position
    if (pos == num.Count)
    {
        // If count of non zero digits
        // is less than or equal to K
        if (cnt <= K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos, cnt, tight] != -1)
        return dp[pos, cnt, tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight != 0 ? 9 : num[pos]);

    for (int dig = 0; dig <= limit; dig++)
    {
        int currCnt = cnt;

        // If the current digit is nonzero
        // increment currCnt
        if (dig != 0)
            currCnt++;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call
        ans += countInRangeUtil(pos + 1, currCnt, currTight);
    }
    return dp[pos,cnt,tight] = ans;
}

// This function converts a number into its
// digit vector and uses above function to compute
// the answer
static int countInRange(int x)
{
    num = new List<int>();
    while (x != 0)
    {
        num.Add(x % 10);
        x /= 10;
    }
    num.Reverse();

    // Initialize dp
    for(int i = 0; i < M; i++)
        for(int j = 0; j < M; j++)
            for(int k = 0; k < 2; k++)
            dp[i, j, k] = -1;
    return countInRangeUtil(0, 0, 0);
}

// Driver Code
public static void Main()
{
    int L = 1, R = 1000;
    K = 3;
    Console.WriteLine( countInRange(R) - countInRange(L - 1) );

    L = 9995; R = 10005; K = 2;
    Console.WriteLine( countInRange(R) - countInRange(L - 1) );
}
}

/* This code contributed by PrinciRaj1992 */
```

## **java 描述语言**

```
<script>
// Javascript Program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits
let M = 20;

// states - position, count, tight
let dp = new Array(M);
for(let i = 0; i < M; i++)
{
    dp[i] = new Array(M);
    for(let j = 0; j < M; j++)
    {
        dp[i][j] = new Array(2);
        for(let k = 0; k < 2; k++)
            dp[i][j][k] = 0;
    }
}

// K is the number of non zero digits
let K;
let num;

// This function returns the count of
// required numbers from 0 to num
function countInRangeUtil(pos, cnt, tight )
{
    // Last position
    if (pos == num.length)
    {

        // If count of non zero digits
        // is less than or equal to K
        if (cnt <= K)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][cnt][tight] != -1)
        return dp[pos][cnt][tight];

    let ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    let limit = (tight!=0 ? 9 : num[pos]);

    for (let dig = 0; dig <= limit; dig++) {
        let currCnt = cnt;

        // If the current digit is nonzero
        // increment currCnt
        if (dig != 0)
            currCnt++;

        let currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call
        ans += countInRangeUtil(pos + 1, currCnt, currTight);
    }
    return dp[pos][cnt][tight] = ans;
}

// This function converts a number into its
// digit vector and uses above function to compute
// the answer
function countInRange(x)
{
    num= [];
    while (x!=0) {
        num.push(x % 10);
        x = Math.floor(x/10);
    }
    num.reverse();

    // Initialize dp
    for(let i=0;i<M;i++)
        for(let j=0;j<M;j++)
            for(let k=0;k<2;k++)
            dp[i][j][k]=-1;
    return countInRangeUtil(0, 0, 0);
}

// Driver Code to test above functions
let L = 1, R = 1000;
K = 3;
document.write( (countInRange(R) - countInRange(L - 1)) +"<br>");

L = 9995; R = 10005; K = 2;
document.write(  (countInRange(R) - countInRange(L - 1)) +"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

****Output:** 

```
1000
6
```** 

****时间复杂度:** O(M * M * 2 * 10)其中 M = log(MAX)，这里 MAX 是最大值。
**辅助空间:** O(M*M)**