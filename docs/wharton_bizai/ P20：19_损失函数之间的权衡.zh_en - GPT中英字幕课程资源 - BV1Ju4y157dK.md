# 沃顿商学院《AI For Business（AI用于商业：AI基础／市场营销+财务／人力／管理）》（中英字幕） - P20：19_损失函数之间的权衡.zh_en - GPT中英字幕课程资源 - BV1Ju4y157dK

 When might we want to prioritize certain types of metrics over others when evaluating machine learning output？



![](img/dfc525e35c82a2eceff6a2eb404a61cf_1.png)

 The key question really is what are the relative costs of false negatives and false positives in the particular application or business context that we're considering？

 So， for example， when might we want a highly sensitive test？

 So consider a medical application where the algorithm is screening for a very serious disease or a type of cancer。

 For instance， when we want to make absolutely sure that we don't miss a person with the condition。

 even at the potential cost of falsely identifying some cases having the condition。

 even if they don't。 So if you want to be absolutely sure we don't miss anybody with the condition。

 then we might want a highly sensitive test。 We want to prioritize sensitivity in that case。

 Another example is， and this is part of the context with the science was actually developed during World War II。

 was when we have a radar system that's trying to detect incoming aircraft。

 So if we're worried about incoming aircraft or enemy attack of some type and we want a system that's going to detect potential incoming aircraft。

 we might want a highly sensitive test。 We don't mind a few false alarms。

 but we want to make absolutely sure that we don't miss any cases that are actually occurring。

 So that's another example where we might want a highly sensitive test。 On the other hand。

 one might be want a precise test。 One might want to say。

 be absolutely sure that something is the case before we say or predict it is the case。

 Imagine you're developing an algorithm to predict when it's okay for a car to take a left turn。

 Now we might want to be absolutely sure that it is okay to take a left before recommending the decision to take a left。

 Even if that means we'll possibly miss a few opportunities to take a left turn。

 that's okay as long as we're absolutely sure when we predict the left or recommend the left that a left is actually okay。

 So that's an example of a time you might want to prioritize precision。

 Another example of when precision might be something to prioritize is identifying some type of violation that has a very severe punishment。

 So for example， cheating that leads to expulsion。 So we might want to be extremely sure that a particular person was guilty before we actually made that decision of an algorithmic sense。



![](img/dfc525e35c82a2eceff6a2eb404a61cf_3.png)

 Even if it means that we might miss a few cases where that actual type of violation occurred。

 we might want to have a very precise test just to make sure we don't falsely accuse someone of that crime or that violation when they didn't were not actually guilty of that violation。

 [BLANK_AUDIO]。

![](img/dfc525e35c82a2eceff6a2eb404a61cf_5.png)