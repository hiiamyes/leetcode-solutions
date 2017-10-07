# [Algorithms - Easy](https://leetcode.com/problemset/algorithms/?difficulty=Easy)

## \#104. Maximum Depth of Binary Tre
* 2017-10-08
* 第一次真的秒殺 + bug free 耶耶
* 142ms, 21.47%

```
/**
* Definition for a binary tree node.
* function TreeNode(val) {
* this.val = val;
* this.left = this.right = null;
* }
*/
/**
* @param {TreeNode} root
* @return {number}
*/
var maxDepth = function(root) {
if (root === null) return 0;
return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```

## \#9 - Palindrome Number

* 一開始不知道 palindrome number 是什麼ＸＤ
* 重點應該在怎麼 **Do this without extra space**，因為這樣就不能用 string split reverse 做了
* 結果我還是用 string split，但沒有用到 reverse
* 378ms, 40.04%
* 看了別人的解法覺得好好笑又好強ＸＤ

/\*\*

* @param {number} x
* @return {boolean}
\*/
var isPalindrome = function\(x\) {
if \(x &lt; 0\) return false;
const numberArray = `${x}`.split\(""\);
const numberArrayLength = numberArray.length;
var i = 0;
while \(i &lt;= Math.ceil\(numberArrayLength / 2\)\) {
if \(numberArray\[i\] !== numberArray\[numberArrayLength - i - 1\]\) return false;
i++;
}
return true;
};

## \#13 Roman to Integer

* 我竟然不知道 roman numeral 是啥 Orz
* 感覺又有 add 又有 subtract 的邏輯好麻煩（wiki 說的）
* 結果發現只有在 iValue &lt; nextValue 的時候才需要 subtract～ easy!! \(偷偷看別人解法才發現\)
* 212ms, 56.67%

```
/**
* @param {string} s
* @return {number}
*/
var romanToInt = function(s) {
const symbols = {
I: 1,
V: 5,
X: 10,
L: 50,
C: 100,
D: 500,
M: 1000
};

const romanArray = s.split('');
var i = 0;
var result = symbols[romanArray[0]];
while(i < romanArray.length - 1) {
const iValue = symbols[romanArray[i]];
const nextValue = symbols[romanArray[i+1]];
result += nextValue;
if(iValue < nextValue){
result -= 2 * iValue;
}
i++;
}
return result;
};
```

## \#14 Longest Common Prefix

* 什麼是 common prefix string?
```
/**
* @param {string[]} strs
* @return {string}
*/
var longestCommonPrefix = function(strs) {
switch (strs.length) {
case 0:
return "";
case 1:
return strs[0];
default:
var isCheckFinish = false;
var iChar = 0;
var commonPrefix = "";
do {
iChar++;
for (var iString = 1; iString < strs.length; iString++) {
try {
if (strs[0].charAt(iChar) !== strs[iString].charAt(iChar)) {
isCheckFinish = true;
iChar = -1;
break;
}
} catch (e) {
isCheckFinish = true;
break;
}
}
} while (!isCheckFinish);
if (iChar === -1) {
return "";
} else {
return strs[0].slice(0, iChar);
}
}
};
```
* 暴力一個一個比較法，結果 time limited exceed...
* 打了個瞌睡起來偷看別人解法，發現竟然可以用 sort... 太扯囉～
* 115ms, 60.16%
```
/**
* @param {string[]} strs
* @return {string}
*/
var longestCommonPrefix = function(strs) {
var LCP = "";
if (strs !== null && strs.length > 0) {
strs = strs.sort();
const firstStringArray = strs[0].split("");
const lastStringArray = strs[strs.length - 1].split("");
for (var i = 0; i < firstStringArray.length; i++) {
if (firstStringArray[i] === lastStringArray[i]) {
LCP += firstStringArray[i];
} else {
break;
}
}
}
return LCP;
};
```

## \#20 Valid Parentheses

* 感覺應該稍簡單，直覺想用 regexp 解
* 但發現好像不太好用 regexp XD
* `return s.replace('()', '').replace('[]', '').replace('{}','').length === 0` 本來覺得是絕招，沒想到 \(\[\]\) 竟然是 valid = =
* 所以 \(\[\]\[\]\) 也是 valid = =
* 結果寫個超醜的 switch 還錯無敵多次
* 109ms, 62.39%
\`\`\`
/\*\*

* @param {string} s
* @return {boolean}
\*/
var isValid = function\(s\) {
const corresponds = {
"\(": "\)",
"\[": "\]",
"{": "}"
};
var stringArray = s.split\(""\);
var result = \[\];
result.push\(stringArray.shift\(\)\);
while \(stringArray.length &gt; 0\) {
const character = stringArray.shift\(\);
switch \(character\) {
case "\(":
case "\[":
case "{":

```
result.push(character);
break;
```

case "\)":
case "\]":
case "}":

```
if (corresponds[result[result.length - 1]] === character) {
result.pop();
} else {
result.push(character);
}
break;
```

}
}
return result.length === 0;
};

```
## \#21. Merge Two Sorted Lists
* 很好，sorted linked list 是什麼...，再被戳破沒修過資結
* splicing together the nodes of the first two lists 是什麼意思？
* 決定直接看 solution 學 = =+
```

/\*\*

* Definition for singly-linked list.
* function ListNode\(val\) {
* this.val = val;
* this.next = null;
* }
\*/
/\*\*
* @param {ListNode} l1
* @param {ListNode} l2
* @return {ListNode}
\*/
var mergeTwoLists = function\(l1, l2\) {
console.log\(l1, l2\)
if\(!l1\) return l2;
if\(!l2\) return l1;
if\(l1.val &lt; l2.val\) {

```
l1.next = mergeTwoLists(l1.next, l2);
return l1;
```

}else {

```
l2.next = mergeTwoLists(l2.next, l1);
return l2;
```

}
};
\`\`\`

* 其實還滿直覺的吼
* 888ms，超出 statistics graph XDD

## \#26. Remove Duplicates from Sorted Array

* in place 的定義應該要好好搞清楚一下
* In-place means that you should update the original string rather than creating a new one.
* 用 splice！拼接。
* 286ms, 13%
* 雖然很快寫出來但 performance 好差喔～
* 看了別人的 solution 發現是可以不用 splice 的！
\`\`\`
/\*\*
* @param {number\[\]} nums
* @return {number}
\*/
var removeDuplicates = function\(nums\) {
if \(nums.length === 0\) return 0;
if \(nums.length === 1\) return 1;
var num = nums\[0\];
var index = 1;
while \(index !== nums.length\) {
if \(num === nums\[index\]\) {
nums.splice\(index, 1\);
} else {
num = nums\[index\];
index++;
}
}
return nums.length;
};

```
## \#27. Remove Element
* 2017-07-12
* 嗯... 一開始不太想用 splice，想說有沒有什麼特別又快的方法
* 結果打完球太累不想花腦袋了直接用 splice 解ＸＤ
* 152ms, 8.76%
```

/\*\*

* @param {number\[\]} nums
* @param {number} val
* @return {number}
\*/
var removeElement = function\(nums, val\) {
var i = 0;
var count = 0;
while \(i &lt; nums.length\) {
if \(nums\[i\] === val\) {
nums.splice\(i, 1\);
} else {
i++;
}
}
return nums.length;
};
\`\`\`

## \#28. Implement strStr\(\)

* 2017-07-12
* RexExp 瞬殺～
* 105ms, 82.96%
```
/**
* @param {string} haystack
* @param {string} needle
* @return {number}
*/
var strStr = function(haystack, needle) {
try{
return new RegExp(needle).exec(haystack).index
}catch(e){
return -1
}
};
```

## \#35. Search Insert Position

* 2017-07-13
* 喔耶秒殺，雖然還是看起來笨笨的 while + if 解法
* 原來比較快的解法是從一半一半去比大小呀！
* 103ms, 65.33%

```
var searchInsert = function(nums, target) {
if (nums.length === 0) return 0;

var i = 0;
while (i < nums.length) {
if (target === nums[i]) {
return i;
} else if (target < nums[i]) {
return i;
} else {
i++;
}
}
return i;
};
```

## \#38. Count and Say

* 2017-07-17
* 一開始搞錯規則，沒想到 111 是要變成 31 而不是 2111 = =
* from hint1: 結果就又是 pattern 題，喔不對好像搞錯...
* from hint2: 還是要用 recursive？沒錯
* 108ms, 53.93%
/**
* @param {number} n
* @return {string}
*/
var countAndSay = function(n) {
if (n === 1) return "1";
var pre = countAndSay(n - 1).split("");
var count = 1;
var number = pre[0];
var say = "";
for (var i = 0; i < pre.length; i++) {
if (pre[i + 1] === number) {
count++;
} else {
say += `${count}${number}`;
number = pre[i + 1];
count = 1;
}
}
return say;
};

## \#53. Maximum Subarray

* 2017-07-19
* contiguous subarray 是啥咪東西 = =
* 呀～ 就只是取相鄰數字的 array 而已啦～
* 把 accumulated sum 畫成 line chart 後發現可能是要取最低點到最高點！
* 喔但 lowest point 要比 highest point 前面
* \[-2, -1\] 炸掉，好像漏考慮很多 case...，例如 lowest point 在 highest point 後面的
* 放棄自己想 Orz
* 甘～ 為什麼大家的 solution 都不用想把 sub array 吐出來...
* DP 是殺毀～～ optimization problem
* 好啦看別人的還是有突破盲點
* 132ms, 41.12%

```
/**
* @param {number[]} nums
* @return {number}
*/
var maxSubArray = function(nums) {
if (nums.length === 1) return nums[0];

var highestValue = nums[0];
var accu = nums[0];
for (var i = 1; i < nums.length; i++) {
accu = accu < 0 ? 0 : accu;
accu += nums[i];
if (accu > highestValue) {
highestValue = accu;
}
}

return highestValue;
};
```

## \#58. Length of Last Word

* 2017-07-19
* 還以為終於可以一次 bug free，殊不知沒考慮到 "a " 要先 trim。ＱＱ
* 109ms, 34.31%
```
/**
* @param {string} s
* @return {number}
*/
var lengthOfLastWord = function(s) {
const words = s.trim().split(" ");
return words[words.length - 1].replace(" ", "").length;
};
```

## \#66. Plus One

* 2017-07-19
* 就只是單純要把數字 +1 嗎＝＝？
* 大概是要考慮進位的狀況吧
* 用 Unary plus \(+\) 把 String 轉 Number 踢到鐵板？
* +'6145390195186705543' = 6145390195186705000，為什麼最後幾位數變成 0?
* Number.parseInt\('6145390195186705543'\) = 6145390195186705000，parseInt\(\) 一樣 ＝＝＋
* 看來是 overflow 的問題了呀呀呀
* 145ms, 9.05%

// 會 overflow 的 solution
const plusOne = +digits.join\(''\) + 1
return `${plusOne}`.split\(''\).map\(n =&gt; +n\)

```
/**
* @param {number[]} digits
* @return {number[]}
*/
var plusOne = function(digits) {
var i = digits.length - 1;
for (i; i >= 0; i--) {
if (digits[i] === 9) {
digits[i] = 0;
if (i === 0) digits.unshift(1);
} else {
digits[i]++;
break;
}
}
return digits;
};
```

## \#67. Add Binary

* 2017-07-21
* 怎麼感覺好簡單但一時之間不知道怎麼解...
* 先轉 number -&gt; sum 再轉回 binary string 會不會太蠢...
* 阿阿，好醜的寫法～
* 132ms, 46.12%

```
/**
* @param {string} a
* @param {string} b
* @return {string}
*/
var addBinary = function(a, b) {
if (a === "") return b;
if (b === "") return a;

var result = [];
var aa = a.split("");
var bb = b.split("");
var i = 0;
var inc = 0;
while (i < a.length || i < b.length) {
var sum =
(+aa[aa.length - 1 - i] || 0) + (+bb[bb.length - 1 - i] || 0) + inc;
result.unshift(sum % 2);
inc = ~~(sum / 2);
i++;
}
if (inc) result.unshift(1);
return result.join("");
};
```

## \#69. Sqrt\(x\)

* 2017-08-05
* 原來要用牛頓法啊... \(幾百年前的數學\)
* 結果拖了好久（兩個多禮拜吧...）才用 community 裡說的 binary search 方式完成，還是沒用牛頓（遠目）
* 135 ms, 74.70%

```
/**
* @param {number} x
* @return {number}
*/
var mySqrt = function(x) {
if (x === 0) return 0;

let min = 1;
let max = Number.MAX_SAFE_INTEGER;
let sqrt;

while (min !== max) {
let mid = Math.floor((min + max) / 2);

if (mid * mid <= x && (mid + 1) * (mid + 1) > x) {
sqrt = mid;
break;
} else if (mid * mid < x) {
min = mid;
} else if (mid * mid > x) {
max = mid;
}
}

return sqrt;
};
```



## \#70. Climbing Stairs

* 2017-08-05
* 喔耶瞬殺～ 排列組合好好玩～～
* 但名次也太差了吧... 大概是不能用排列組合算 = =
* 125 ms, 5.93%

```
/**
* @param {number} n
* @return {number}
*/
var climbStairs = function(n) {
if (n === 1) return 1;
let result = 0;
const n2 = Math.floor(n / 2);
for (let i = 0; i <= n2; i++) {
result += combination(n - i, i);
}
return result;
};

const combination = (a, b) => {
let result = 1;
for (let i = 0; i < b; i++) {
result *= a - i;
}
for (let i = 0; i < b; i++) {
result /= b - i;
}
return result;
};

```

## \#83. Remove Duplicates from Sorted List
* 2017-08-10
* 一開始想先做 DP 出也是 linked list 的結果再 output array result 但失敗了
* 最後用的單純的方法直接 output array result
* 138 ms, 64.31%

```
/**
* Definition for singly-linked list.
* function ListNode(val) {
* this.val = val;
* this.next = null;
* }
*/
/**
* @param {ListNode} head
* @return {ListNode}
*/
var deleteDuplicates = function(head) {
let result = [];
while (head && head.val !== null) {
head.val !== result[result.length - 1] && result.push(head.val);
head = head.next;
}
return result;
};
```

## \#88. Merge Sorted Array
* 2017-08-12
* 原本想說有沒有什麼可以不用 javascript built-in function 的方法，但最後還是用了 splice 和 shift
* 為什麼 input 會有 [0]0[1]1 這種 case = =，[0]不是算 size 1 喔...
* 不知道為什麼 nums1 = nums1.concat(nums2) 不會正確把 value assign 給 nums1...
* 這題是不是做壞了呀...
* 好聰明... 原來要從後面開始排就可以避掉需要做 splice 的動作！！
* 112 ms, 59.62%

```
/**
* @param {number[]} nums1
* @param {number} m
* @param {number[]} nums2
* @param {number} n
* @return {void} Do not return anything, modify nums1 in-place instead.
*/
var merge = function(nums1, m, nums2, n) {
while (n > 0) {
nums1[m + n - 1] =
m !== 0 && nums1[m - 1] > nums2[n - 1] ? nums1[--m] : nums2[--n];
}
};
```

## \#100. Same Tree
* 2017-08-13
* 秒殺耶耶
* 105 ms, 60.46%

```
/**
* Definition for a binary tree node.
* function TreeNode(val) {
* this.val = val;
* this.left = this.right = null;
* }
*/
/**
* @param {TreeNode} p
* @param {TreeNode} q
* @return {boolean}
*/
var isSameTree = function(p, q) {
if (p === null && q === null) return true;
if (p === null || q === null) return false;
return (
p.val === q.val &&
isSameTree(p.left, q.left) &&
isSameTree(p.right, q.right)
);
};
```

## \#101. Symmetric Tree
* 2017-09-19
* recursive 好像比較直覺，就每個 node 都確保他是 symmetric 就好，錯了這樣不對 = = [1223443] 就爆了
* [1, 2] === [1, 2] 是 false @@???
* 152 ms, 15.45%

```
/**
* Definition for a binary tree node.
* function TreeNode(val) {
* this.val = val;
* this.left = this.right = null;
* }
*/
/**
* @param {TreeNode} root
* @return {boolean}
*/
var isSymmetric = function(root) {
if (root === null || (root.left === null && root.right === null)) return true;
return sym([root.left, root.right]);
};

const sym = nodes => {
for (let i = 0; i < nodes.length / 2; i++) {
if ((nodes[i] || {}).val !== (nodes[nodes.length - 1 - i] || {}).val)
return false;
}
const next = nodes
.filter(n => n !== null)
.map(n => [n.left, n.right])
.reduce((a, b) => a.concat(b), []);
return next.length === 0 ? true : sym(next);
};
```
