# 看说序列

> 原文:[https://www.geeksforgeeks.org/look-and-say-sequence/](https://www.geeksforgeeks.org/look-and-say-sequence/)

在看说(或数说)序列中找到第 n 项。看说序列是以下整数的序列:
1，11，21，1211，111221，312211，13112221，1113213211，…

***以上序列是如何生成的？***
第 n 个术语在由 reading (n-1)生成的第 n 个术语中。

```
The first term is "1"

Second term is "11", generated by reading first term as "One 1" 
(There is one 1 in previous term)

Third term is "21", generated by reading second term as "Two 1"

Fourth term is "1211", generated by reading third term as "One 2 One 1" 

and so on
```

如何找到第 n 个术语？

**示例:**

```
Input: n = 3
Output: 21

Input: n = 5
Output: 111221
```

想法很简单，我们生成从 1 到 n 的所有术语，前两个术语初始化为“1”和“11”，其他所有术语都是使用以前的术语生成的。为了使用前一个术语生成术语，我们扫描前一个术语。扫描术语时，我们只需跟踪所有连续字符的计数。对于相同字符的序列，我们将计数附加在字符之后，以生成下一个术语。

下面是上述想法的实现。

## C++

```
// C++ program to find n'th term in look and say
// sequence
#include <bits/stdc++.h>
using namespace std;

// Returns n'th term in look-and-say sequence
string countnndSay(int n)
{
    // Base cases
    if (n == 1)      return "1";
    if (n == 2)      return "11";

    // Find n'th term by generating all terms from 3 to
    // n-1.  Every term is generated using previous term
    string str = "11"; // Initialize previous term
    for (int i = 3; i<=n; i++)
    {
        // In below for loop, previous character
        // is processed in current iteration. That
        // is why a dummy character is added to make
        // sure that loop runs one extra iteration.
        str += '{content}apos;;
        int len = str.length();

        int cnt = 1; // Initialize count of matching chars
        string  tmp = ""; // Initialize i'th term in series

        // Process previous term to find the next term
        for (int j = 1; j < len; j++)
        {
            // If current character does't match
            if (str[j] != str[j-1])
            {
                // Append count of str[j-1] to temp
                tmp += cnt + '0';

                // Append str[j-1]
                tmp += str[j-1];

                // Reset count
                cnt = 1;
            }

            //  If matches, then increment count of matching
            // characters
            else cnt++;
        }

        // Update str
        str = tmp;
    }

    return str;
}

// Driver program
int main()
{
    int N = 3;
    cout << countnndSay(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th
// term in look and say sequence

class GFG
{

    // Returns n'th term in
    // look-and-say sequence
    static String countnndSay(int n)
    {
    // Base cases
    if (n == 1)     return "1";
    if (n == 2)     return "11";

    // Find n'th term by generating
    // all terms from 3 to n-1.
    // Every term is generated
    // using previous term

    // Initialize previous term
    String str = "11";
    for (int i = 3; i <= n; i++)
    {
        // In below for loop, previous
        // character is processed in
        // current iteration. That is
        // why a dummy character is
        // added to make sure that loop
        // runs one extra iteration.
        str += '{content}apos;;
        int len = str.length();

        int cnt = 1; // Initialize count
                     // of matching chars
        String tmp = ""; // Initialize i'th
                         // term in series
        char []arr = str.toCharArray();

        // Process previous term
        // to find the next term
        for (int j = 1; j < len; j++)
        {
            // If current character
            // does't match
            if (arr[j] != arr[j - 1])
            {
                // Append count of
                // str[j-1] to temp
                tmp += cnt + 0;

                // Append str[j-1]
                tmp += arr[j - 1];

                // Reset count
                cnt = 1;
            }

            // If matches, then increment
            // count of matching characters
            else cnt++;
        }

        // Update str
        str = tmp;
    }

    return str;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;
        System.out.println(countnndSay(N));
    }
}

// This code is contributed
// by ChitraNayal
```

## C#

```
// C# program to find n'th
// term in look and say sequence
using System;

class GFG
{

    // Returns n'th term in
    // look-and-say sequence
    static string countnndSay(int n)
    {
    // Base cases
    if (n == 1)     return "1";
    if (n == 2)     return "11";

    // Find n'th term by generating
    // all terms from 3 to n-1.
    // Every term is generated using
    // previous term

    // Initialize previous term
    string str = "11";
    for (int i = 3; i <= n; i++)
    {
        // In below for loop, previous
        // character is processed in
        // current iteration. That is
        // why a dummy character is
        // added to make sure that loop
        // runs one extra iteration.
        str += '{content}apos;;
        int len = str.Length;

        int cnt = 1; // Initialize count of
                     // matching chars
        string tmp = ""; // Initialize i'th
                         // term in series
        char []arr = str.ToCharArray();

        // Process previous term
        // to find the next term
        for (int j = 1; j < len; j++)
        {
            // If current character
            // does't match
            if (arr[j] != arr[j - 1])
            {
                 // Append count of
                // str[j-1] to temp
                tmp += cnt + 0;

                // Append str[j-1]
                tmp += arr[j - 1];

                // Reset count
                cnt = 1;
            }

            // If matches, then increment
            // count of matching characters
            else cnt++;
        }

        // Update str
        str = tmp;
    }

    return str;
    }

    // Driver Code
    public static void Main()
    {
        int N = 3;
        Console.Write(countnndSay(N));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find
# n'th term in look and
# say sequence

# Returns n'th term in
# look-and-say sequence
def countnndSay(n):

    # Base cases
    if (n == 1):
        return "1"
    if (n == 2):
        return "11"

    # Find n'th term by generating
    # all terms from 3 to n-1.
    # Every term is generated using
    # previous term

    # Initialize previous term
    s = "11"
    for i in range(3, n + 1):

        # In below for loop,
        # previous character is
        # processed in current
        # iteration. That is why
        # a dummy character is
        # added to make sure that
        # loop runs one extra iteration.
        s += '{content}apos;
        l = len(s)

        cnt = 1 # Initialize count
                # of matching chars
        tmp = "" # Initialize i'th
                 # term in series

        # Process previous term to
        # find the next term
        for j in range(1 , l):

            # If current character
            # does't match
            if (s[j] != s[j - 1]):

                # Append count of
                # str[j-1] to temp
                tmp += str(cnt + 0)

                # Append str[j-1]
                tmp += s[j - 1]

                # Reset count
                cnt = 1

            # If matches, then increment
            # count of matching characters
            else:
                cnt += 1

        # Update str
        s = tmp
    return s;

# Driver Code
N = 3
print(countnndSay(N))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n'th term in look
// and say sequence

// Returns n'th term in
// look-and-say sequence
function countnndSay($n)
{
    // Base cases
    if ($n == 1)    
        return "1";
    if ($n == 2)    
        return "11";

    // Find n'th term by generating
    // all terms from 3 to n-1.
    // Every term is generated
    // using previous term

    // Initialize previous term
    $str = "11";
    for ($i = 3;
         $i <= $n; $i++)
    {
        // In below for loop,
        // previous character is
        // processed in current
        // iteration. That is why
        // a dummy character is
        // added to make sure that
        // loop runs one extra iteration.
        $str = $str.'{content}apos;;
        $len = strlen($str);

        $cnt = 1; // Initialize count of
                  // matching chars
        $tmp = ""; // Initialize i'th
                   // term in series

        // Process previous term
        // to find the next term
        for ($j = 1; $j < $len; $j++)
        {
            // If current character
            // does't match
            if ($str[$j] != $str[$j - 1])
            {
                // Append count of
                // str[j-1] to temp
                $tmp = $tmp.$cnt + 0;

                // Append str[j-1]
                $tmp = $tmp. $str[$j - 1];

                // Reset count
                $cnt = 1;
            }

            // If matches, then increment
            // count of matching characters
            else $cnt++;
        }

        // Update str
        $str = $tmp;
    }

    return $str;
}

// Driver Code
$N = 3;
echo countnndSay($N);
return 0;

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find n'th
// term in look and say sequence

// Returns n'th term in
// look-and-say sequence
function countnndSay(n)
{

    // Base cases
    if (n == 1)    
        return "1";
    if (n == 2)    
        return "11";

    // Find n'th term by generating
    // all terms from 3 to n-1.
    // Every term is generated
    // using previous term

    // Initialize previous term
    let str = "11";

    for(let i = 3; i <= n; i++)
    {

        // In below for loop, previous
        // character is processed in
        // current iteration. That is
        // why a dummy character is
        // added to make sure that loop
        // runs one extra iteration.
        str += '{content}apos;;
        let len = str.length;

        // Initialize count
        // of matching chars
        let cnt = 1;

        // Initialize i'th
        // term in series
        let tmp = "";
        let arr = str.split("");

        // Process previous term
        // to find the next term
        for(let j = 1; j < len; j++)
        {

            // If current character
            // does't match
            if (arr[j] != arr[j - 1])
            {

                // Append count of
                // str[j-1] to temp
                tmp += cnt + 0;

                // Append str[j-1]
                tmp += arr[j - 1];

                // Reset count
                cnt = 1;
            }

            // If matches, then increment
            // count of matching characters
            else cnt++;
        }

        // Update str
        str = tmp;
    }
    return str;
}

// Driver Code
let N = 3;

document.write(countnndSay(N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
21

```

**另一种方法(使用 STL):** 还有一个想法，我们可以使用 c++ stl 中的无序 _map 来跟踪位数。基本思想是使用一个生成器函数，它将从前一个字符串生成字符串。在 count and say 函数中，我们将迭代从 1 到 n-1 的整数，并不断更新结果。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// generator function returns int string from prev int
// string e.g. -> it will return '1211' for '21' ( One 2's
// and One 1)
string generator(string str)
{
    string ans = "";

    unordered_map<char, int>
        tempCount; // It is used to count integer sequence

    for (int i = 0; i < str.length() + 1; i++) {
        // when current char is different from prev one we
        // clear the map and update the ans
        if (tempCount.find(str[i]) == tempCount.end()
            && i > 0) {
            auto prev = tempCount.find(str[i - 1]);
            ans += to_string(prev->second) + prev->first;
            tempCount.clear();
        }
        // when current char is same as prev one we increase
        // it's count value
        tempCount[str[i]]++;
    }

    return ans;
}

string countnndSay(int n)
{
    string res = "1"; // res variable keep tracks of string
                      // from 1 to n-1

    // For loop iterates for n-1 time and generate strings
    // in sequence "1" -> "11" -> "21" -> "1211"
    for (int i = 1; i < n; i++) {
        res = generator(res);
    }

    return res;
}

int main()
{

    int N = 3;
    cout << countnndSay(N) << endl;
    return 0;
}
```

**Output**

```
21

```

感谢 Utkarsh 和 Neeraj 提出上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息