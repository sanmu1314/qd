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


http://hcysun.me/vue-design/zh/essence-of-comp.html#%E7%BB%84%E4%BB%B6%E7%9A%84%E4%BA%A7%E5%87%BA%E6%98%AF%E4%BB%80%E4%B9%88
https://v3.cn.vuejs.org/guide/introduction.html#vue-js-%E6%98%AF%E4%BB%80%E4%B9%88
https://www.nuxtjs.cn/


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
public class EnglishRule {
    private static LanguageRule languageRule = new LanguageRule("eng", new ArrayList<Rule>());

    public EnglishRule() {
        common();
        number();
        name();
        betweenPunctuation();
        list();
    }

    public LanguageRule getRule() {
        return languageRule;
    }

    private List<Rule> getRuleList() {
        return languageRule.getRuleList();
    }

    private void common() {

        languageRule.addRule(new Rule(true, "\\n", ""));
        languageRule.addRule(new Rule(true, " ", "\\n"));

        languageRule.addRule(new Rule(true, "[\\.\\?!]+\\s+", "[^\\.]"));//分句边界的关键点
//        languageRule.addRule(new Rule(true, "[\\.\\?!]+", "\\s+[^\\.]"));//分句边界的关键点

        languageRule.addRule(new Rule(true, "[\\.\\?!]+", "\\s*(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why)"));

        languageRule.addRule(new Rule(true, "[!?\\.-][\\\"\\'“”]\\s+", "[A-Z]"));
//        languageRule.addRule(new Rule(true, "[!?\\.-][\\\"\\'\\u{201d}\\u{201c}]\\s+", "[A-Z]"));

        languageRule.addRule(new Rule(true, "(?<=\\S)(!|\\?){3,}", "(?=(\\s|\\Z|$))"));

        languageRule.addRule(new Rule(false, "[\\.\\?!]+\\s*", "(?=[\\.\\?!])"));
        languageRule.addRule(new Rule(false, "([a-zA-z]°)\\.\\s*", "(?=\\d+)"));

        languageRule.addRule(new Rule(false, "\\s", "(?=[a-z])"));
//        languageRule.addRule(new Rule(false, "(?<=\\s+)", "(?=[a-z])"));
//        languageRule.addRule(new Rule(false, "(?<=\\S)@", "(?=\\S)"));
//        languageRule.addRule(new Rule(true, "(?<=\\S)(!|\\?){3,}", "(?=(\\s|\\Z|$))"));
    }

    private void number() {
        languageRule.addRule(new Rule(false, "\\d\\.", "(?=\\d)"));
//        languageRule.addRule(new Rule(false, "\\s+[\\w]\\.", "\\s+[\\w][\\s|\\.]"));
    }

    private void name() {
//        languageRule.addRule(new Rule(false, "(Mr|Mrs|tel)\\.", ""));
        languageRule.addRule(new Rule(false, "(Mr|Mrs|Ms|Dr|p.m|a.m|tel)\\.", "\\s*"));

//        languageRule.addRule(new Rule(false, "(p\\.m\\.|a\\.m\\.)\\s+", "\\w"));
        languageRule.addRule(new Rule(true, "(P\\.M\\.|A\\.M\\.)", "\\s+"));
//        languageRule.addRule(new Rule(false, "[A-Z]\\.", "(?!(Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why))"));
        languageRule.addRule(new Rule(false, "(?<=(?<=^)[A-Z]\\.\\s+|(?<=\\A)[A-Z]\\.\\s+|[A-Z]\\.\\s+|(?<=^)[A-Z][a-z]\\.\\s+|(?<=\\A)[A-Z][a-z]\\.\\s+|(?<=\\s)[A-Z][a-z]\\.\\s)",
                "(?!(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why))"));
//        languageRule.addRule(new Rule(false, "[\\.| ][A-Z]\\.\\s*", "(?=([A-Z][\\.| ]))"));
    }

    private void quotes() {
//        languageRule.addRule(new Rule(false, "(?<=\\s)'(?:[^']|'[a-zA-Z])*'", ""));
//        languageRule.addRule(new Rule(false, "(?<=\\s)‘(?:[^’]|’[a-zA-Z])*’", ""));
//        languageRule.addRule(new Rule(false, "(?<=\\s)\\(", "([^\\)]|\\([a-zA-Z])*\\)"));
//        languageRule.addRule(new Rule(false, "(?<=\\s)\\{", "([^\\}]|\\{[a-zA-Z])*\\}"));
    }

    private void betweenPunctuation() {

        languageRule.addRule(new Rule(false, "(?<=\\s)'(?:[^']|'[a-zA-Z])*'", ""));

        languageRule.addRule(new Rule(false, "(?<=\\s)‘(?:[^’]|’[a-zA-Z])*’", ""));

        languageRule.addRule(new Rule(false, "\"(?>[^\"\\\\]+|\\\\{2}|\\\\.)*\"", ""));
//        languageRule.addRule(new Rule(false, "\"(?=(?P<tmp>[^\\\"\\\\]+|\\\\{2}|\\\\.)*)(?P=tmp)\"", ""));

        languageRule.addRule(new Rule(false, "«(?>[^»\\\\]+|\\\\{2}|\\\\.)*»", ""));

        languageRule.addRule(new Rule(false, "“(?>[^”\\\\]+|\\\\{2}|\\\\.)*”", ""));

        languageRule.addRule(new Rule(false, "\\[(?>[^\\]\\\\]+|\\\\{2}|\\\\.)*\\]", ""));

        languageRule.addRule(new Rule(false, "\\((?>[^\\(\\)\\\\]+|\\\\{2}|\\\\.)*\\)", ""));

        //''单引号内不分句，但如果存在以单引号开头的单词目前分句会出现错误
//        languageRule.addRule(new Rule(false, "(?<=\\s)'(?:[^']|'[a-zA-Z])*'\\S", ""));

        languageRule.addRule(new Rule(false, "(?<=\\s)\\-\\-(?>[^\\-\\-])*\\-\\-", ""));
    }

    private void list() {
//        languageRule.addRule(new Rule(true, "\\.", "(\\s+(^)[a-z](\\.)|(\\A)[a-z](\\.)|(\\s)[a-z](\\.))\\s"));
        languageRule.addRule(new Rule(false, "((?<=^)[a-z]\\.|(?<=\\A)[a-z]\\.|(?<=\\s)[a-z]\\.)", "\\s*(?!(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why))"));

//        languageRule.addRule(new Rule(false, "(?<=\\()[a-z]+(?=\\))|(?<=^)[a-z]+(?=\\))|(?<=\\A)[a-z]+(?=\\))|(?<=\\s)[a-z]+(?=\\))", ""));

//        languageRule.addRule(new Rule(false, "(?<=^)[a-z](?=\\.)|(?<=\\A)[a-z](?=\\.)|(?<=\\s)[a-z](?=\\.)", ""));
//        languageRule.addRule(new Rule(true, "", "\\s+((?<=\\s)\\d{1,2}\\.(?=\\s)|^\\d{1,2}\\.(?=\\s)|(?<=\\s)\\d{1,2}\\.(?=\\))|^\\d{1,2}\\.(?=\\))|(?<=\\s\\-)\\d{1,2}\\.(?=\\s)|(?<=^\\-)\\d{1,2}\\.(?=\\s)|(?<=\\s\\⁃)\\d{1,2}\\.(?=\\s)|(?<=^\\⁃)\\d{1,2}\\.(?=\\s)|(?<=\\s\\-)\\d{1,2}\\.(?=\\))|(?<=^\\-)\\d{1,2}\\.(?=\\))|(?<=\\s\\⁃)\\d{1,2}\\.(?=\\))|(?<=^\\⁃)\\d{1,2}\\.(?=\\)))"));
        languageRule.addRule(new Rule(false, "(?<=\\s)\\d{1,2}\\.(\\s)|^\\d{1,2}\\.(\\s)|" +
                "(?<=\\s)\\d{1,2}\\.(\\))|^\\d{1,2}\\.(\\))|(?<=\\s\\-)\\d{1,2}\\.(\\s)|(?<=^\\-)\\d{1,2}\\.(\\s)|" +
                "(?<=\\s\\⁃)\\d{1,2}\\.(\\s)|(?<=^\\⁃)\\d{1,2}\\.(\\s)|(?<=\\s\\-)\\d{1,2}\\.(\\))|(?<=^\\-)\\d{1,2}\\.(\\))|" +
                "(?<=\\s\\⁃)\\d{1,2}\\.(\\))|(?<=^\\⁃)\\d{1,2}\\.(\\))|(\\•)\\s*\\d{1,2}\\.(\\s)|(?<=\\s)\\d{1,2}(\\))",
                "\\s*"));
//        languageRule.addRule(new Rule(false, "((\\s)\\d{1,2}\\.(?=\\s)|^\\d{1,2}\\.(?=\\s)|(\\s)\\d{1,2}\\.(?=\\))|^\\d{1,2}\\.(?=\\))|(\\s\\-)\\d{1,2}\\.(?=\\s)|(^\\-)\\d{1,2}\\.(?=\\s)|(\\s\\⁃)\\d{1,2}\\.(?=\\s)|(^\\⁃)\\d{1,2}\\.(?=\\s)|(\\s\\-)\\d{1,2}\\.(?=\\))|(^\\-)\\d{1,2}\\.(?=\\))|(\\s\\⁃)\\d{1,2}\\.(?=\\))|(^\\⁃)\\d{1,2}\\.(?=\\)))", ""));
        languageRule.addRule(new Rule(true, "", "\\s+((?<=\\s)\\d{1,2}\\.(?=\\s)|" +
                "^\\d{1,2}\\.(?=\\s)|(?<=\\s)\\d{1,2}\\.(?=\\))|^\\d{1,2}\\.(?=\\))|((?<=\\s)\\-)\\d{1,2}\\.(?=\\s)|" +
                "(^\\-)\\d{1,2}\\.(?=\\s)|((?<=\\s)\\⁃)\\d{1,2}\\.(?=\\s)|(^\\⁃)\\d{1,2}\\.(?=\\s)|((?<=\\s)\\-)\\d{1,2}\\.(?=\\))|" +
                "(^\\-)\\d{1,2}\\.(?=\\))|((?<=\\s)\\⁃)\\d{1,2}\\.(?=\\))|(^\\⁃)\\d{1,2}\\.(?=\\))|(\\•)\\s*\\d{1,2}\\.(\\s)|" +
                "(?<=\\s)\\d{1,2}(?=\\)))"));
    }

}

<languageRules>
  <languageRule name="eng">

    <!--common-->
    <rule break="yes">
      <beforebreak>\n</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak> </beforebreak>
      <afterbreak>\n</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak>[\.\?!]+\s+</beforebreak>
      <afterbreak>[^\.]</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak>[\.\?!]+</beforebreak>
      <afterbreak>\s*(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why)</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak>[!?\.-][\"\'“”]\s+</beforebreak>
      <afterbreak>[A-Z]</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak>(?&lt;=\S)(!|\?){3,}</beforebreak>
      <afterbreak>(?=(\s|\Z|$))</afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>[\.\?!]+\s*</beforebreak>
      <afterbreak>(?=[\.\?!])</afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>([a-zA-z]°)\.\s*</beforebreak>
      <afterbreak>(?=\d+)</afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>\s</beforebreak>
      <afterbreak>(?=[a-z])</afterbreak>
    </rule>

    <!-- number -->
    <rule break="no">
      <beforebreak>\d\.</beforebreak>
      <afterbreak>(?=\d)</afterbreak>
    </rule>

    <!-- name -->
    <rule break="no">
      <beforebreak>(Mr|Mrs|Ms|Dr|p.m|a.m|tel)\.</beforebreak>
      <afterbreak>\s*</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak>(P\.M\.|A\.M\.)</beforebreak>
      <afterbreak>\s+</afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>(?&lt;=(?&lt;=^)[A-Z]\.\s+|(?&lt;=\A)[A-Z]\.\s+|[A-Z]\.\s+|(?&lt;=^)[A-Z][a-z]\.\s+|(?&lt;=\A)[A-Z][a-z]\.\s+|(?&lt;=\s)[A-Z][a-z]\.\s)</beforebreak>
      <afterbreak>(?!(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why))</afterbreak>
    </rule>

    <!-- betweenPunctuation -->
    <rule break="no">
      <beforebreak>(?&lt;=\s)'(?:[^']|'[a-zA-Z])*'</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>(?&lt;=\s)‘(?:[^’]|’[a-zA-Z])*’</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>"(?>[^"\\]+|\\{2}|\\.)*"</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>«(?>[^»\\]+|\\{2}|\\.)*»</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>“(?>[^”\\]+|\\{2}|\\.)*”</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>\[(?>[^\]\\]+|\\{2}|\\.)*\]</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>\((?>[^\(\)\\]+|\\{2}|\\.)*\)</beforebreak>
      <afterbreak></afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>(?&lt;=\s)\-\-(?>[^\-\-])*\-\-</beforebreak>
      <afterbreak></afterbreak>
    </rule>

    <!-- list -->
    <rule break="no">
      <beforebreak>((?&lt;=^)[a-z]\.|(?&lt;=\A)[a-z]\.|(?&lt;=\s)[a-z]\.)</beforebreak>
      <afterbreak>\s*(?!(A |Being|Did|For|He|How|However|I|In|It|Millions|More|She|That|The|There|They|We|What|When|Where|Who|Why))</afterbreak>
    </rule>
    <rule break="no">
      <beforebreak>(?&lt;=\s)\d{1,2}\.(\s)|^\d{1,2}\.(\s)|(?&lt;=\s)\d{1,2}\.(\))|^\d{1,2}\.(\))|(?&lt;=\s\-)\d{1,2}\.(\s)|(?&lt;=^\-)\d{1,2}\.(\s)|(?&lt;=\s\⁃)\d{1,2}\.(\s)|(?&lt;=^\⁃)\d{1,2}\.(\s)|(?&lt;=\s\-)\d{1,2}\.(\))|(?&lt;=^\-)\d{1,2}\.(\))|(?&lt;=\s\⁃)\d{1,2}\.(\))|(?&lt;=^\⁃)\d{1,2}\.(\))|(\•)\s*\d{1,2}\.(\s)|(?&lt;=\s)\d{1,2}(\))</beforebreak>
      <afterbreak>\s*</afterbreak>
    </rule>
    <rule break="yes">
      <beforebreak></beforebreak>
      <afterbreak>\s+((?&lt;=\s)\d{1,2}\.(?=\s)|^\d{1,2}\.(?=\s)|(?&lt;=\s)\d{1,2}\.(?=\))|^\d{1,2}\.(?=\))|((?&lt;=\s)\-)\d{1,2}\.(?=\s)|(^\-)\d{1,2}\.(?=\s)|((?&lt;=\s)\⁃)\d{1,2}\.(?=\s)|(^\⁃)\d{1,2}\.(?=\s)|((?&lt;=\s)\-)\d{1,2}\.(?=\))|(^\-)\d{1,2}\.(?=\))|((?&lt;=\s)\⁃)\d{1,2}\.(?=\))|(^\⁃)\d{1,2}\.(?=\))|(\•)\s*\d{1,2}\.(\s)|(?&lt;=\s)\d{1,2}(?=\)))</afterbreak>
    </rule>

  </languageRule>
</languageRules>
