# qd
Vue
1. https://www.jianshu.com/p/edaf43e9384f ES6：export default 和 export 区别 - 简书
2. http://es6.ruanyifeng.com/?search=import&x=0&y=0#docs/module#export-default-%E5%91%BD%E4%BB%A4 Module 的语法 - ECMAScript 6入门
3. https://www.cnblogs.com/pengaijin/p/7646524.html es6中export、export default、import的理解
4. https://www.cnblogs.com/lemoncool/p/9645587.html解决Vuex持久化插件-在F5刷新页面后数据不见的问题
5. https://blog.csdn.net/wang1006008051/article/details/82424335 vuex刷新数据消失问题
6. https://blog.csdn.net/sinat_36539161/article/details/83791198 Vue 页面刷新，状态数据丢失问题
7. https://www.cnblogs.com/zhongchao666/p/9567527.html vuex页面刷新数据不保留，解决方法
8. https://segmentfault.com/a/1190000008589736 Vue源码详解之nextTick：MutationObserver只是浮云，microtask才是核心
9. https://www.cnblogs.com/xiaotanke/p/7448383.html export ，export default 和 import 区别
10. https://www.cnblogs.com/daiwenru/p/6694530.html vue2.0 子组件和父组件之间的传值


nlp
http://automateddeveloper.blogspot.co.uk/2016/11/using-opennlp-for-named-entity.html

```

        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()) {
            String[] nums = null;
            nums = sc.nextLine().replace("[","").replace("]","").split(",");
            int num[]=new int[nums.length];
            for(int i=0;i<num.length;i++) {
                num[i] = Integer.valueOf(nums[i]);
            }
            int h = sc.nextInt();
            minEatingSpeed(num, h);
        }

class Solution {
    public int minEatingSpeed(int[] piles, int H) {
        int lo = 1;
        int hi = 1_000_000_000;
        while (lo < hi) {
            int mi = (lo + hi) / 2;
            if (!possible(piles, H, mi))
                lo = mi + 1;
            else
                hi = mi;
        }

        return lo;
    }

    // Can Koko eat all bananas in H hours with eating speed K?
    public boolean possible(int[] piles, int H, int K) {
        int time = 0;
        for (int p: piles)
            time += (p-1) / K + 1;
        return time <= H;
    }
}
```

