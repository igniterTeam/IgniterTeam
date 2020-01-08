
[BDD Cucumber Features Best Practices](https://www.linkedin.com/pulse/bdd-cucumber-features-best-practices-liraz-shay)

# 写声明式 Feature

Declarative(声明式) 与 Imperative（命令式） 的区别在于：命令式会把尽可能多的细节描述出来，而声明式则仅把需要完成什么描述。

参考下例：

```gherkin
Given I open a browser
And I navigate to http://xxx.xx.xx
When I type the username field bob97
And I type in the password field F1d0
And I click on Submit button
Then I should see the message Welcome Back Bob
```

```gherkin
Given I am on the Login Page
When I sign in with correct credentials
The I should see a welcome message
```

以两例，前者为命令式，后者为声明式。
前者显得很啰嗦，而后者则更可读且把实现细节留给了具体的代码实现。

**写声明式测试**这条原则适用于所有语言或其他 test runner。测试应该关注于要完成什么而非其实现的细节
（Tests should largely focus on what needs to be accomplished, not the details of how it is done）。
它应该让非开发人员也可轻易读懂。

# 避免 UI 操作步骤

```gherkin
Given I am on the home page
When I fill in "Username" with: "jondkinney"
And I fill in "Password" with: "SuperSecret123"
And I check "Remember me"
And I press "Log in"
Then a user session should be persisted
And I should be on my dashboard
And I should see "You hav successfuly logged in."
```

```gherkin
Given I am on the home page
When I login as an admin
Then I should be on my dashboard
And I should see "You have successfully logged in."
```
例2移除大量的操作细节，更加可读。

# 避免连接步骤

如果在某个步骤中你需要连接某两个操作，那就把它写成两个步骤。
```gherkin
Then I should be on my dashboard and I should see "You have successfully logged in."

# 尽量分离，增加可读性和模块复用
Then I should be on my dashboard
And I should see "You have successfully logged in."
```

# 使用背景

如果一个场景中的特性需要反复重复一些步骤，那把它们放到 Background 里。
> Don't Repeat Yourself

# 限制每个 Feature 中场景的个数

每个 feature 文件仅留一个 Feature
限制每个 feature 场景个数
一个经验值是，每个 Feature 的场景数限制在 10 来个左右(原文 dozen) 

# 限制每个场景中的步骤个数

# 避免巨大的数据表

过大的数据表，会让用例理解难度增加，执行时间增加。当你需要写数据表时，问下自己以下问题：

- 是否每行都用表示一个同等的类的变量
- 是否每行数据表达不同的行为，如果是，考虑拆分成不同的场景
- 是否所有输入组合都是必须的，避免不必要的重复
- **feature 文件阅读者是否需要知道这个表？**：如果不需要，将之隐藏在实现中。

以上问题仅用于常规检查，但不是一个必须严格执行的规则。其主旨为：**场景应该聚集于一个行为，且仅使用必要的变量**

# Less is More

**场景应该短小精悍**(Scenarios should be short and sweet)。一般我会建议一个场景只有个位数的步骤。过长的场景不易于立场。
且通常它就意味着这是个较差的实践。如前文所述，命令式的步骤就会导致步骤过长问题。这里将再详细讨论下命令式与声明式的区别。

声明式步骤旨在指出行为应该 **(How)如何** 发生。它们通过是通过产品特性来驱动。考虑以下通过 Google 搜索的步骤：


```gherkin
When the user scrolls the mouse to the search bar
And the user clicks the search bar
And the user types the letter “p”
And the user types the letter “a”
And the user types the letter “n”
And the user types the letter “d”
And the user types the letter “a”
And the user types the ENTER key
```

上例的粒度也许过于夸张，但它模拟了命令式步骤如何实现一个功能，它们通过要通过好多步骤才能完成一个目标。
因此，它们不如声明式步骤那么能自解释。

# 选择一个发标题(scenario/feature)

(略)

#



